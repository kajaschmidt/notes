---
layout: page
title: "1. The Neural Network"
category: fodl
date: 2018-02-04 14:57:34
order: 2
---

This chapter discusses
1. [Building Intelligent Machines](#Machine-Learning)
2. [The limits of Traditional Computer Programs](#Traditional-Computer-Programs)
3. [Mechanics of ML](#Mechanics-of-an-ML-Problem)
4. [The neuron](#The-Artificial-Neuron)
5. [Expressing Linear Perceptrons as Neurons](#The-Neuronal-Model)
6. [Feed-forward Neural Networks](#Feed-Forward-Neural-Networks)
7. [Linear Neurons and their Limitations](#Linear-Neurons-and-their-Limitations)
8. [Sigmoid, Tanh, and ReLU Neurons](#Non-linear-neurons)
9. [Softmax Output Layers](#Softmax-Output-Layers)

and builds a basic intuition for machine learning and neural networks.

---

## Traditional Computer Programs
1. perform arithmetic computations really fast
2. explicitly follow a list of instructions

---

## Machine Learning
*<u>Def.</u> Machine Learning (ML):* subset of AI; predicated on the idea of learning from example. Instead of teaching a computer a massive list of rules to solve the problem, we give it a model with which it can evaluate examples, and a small set of instructions to modify the model when it makes sense.

Expectation: over time, a well-suited model would be able to solve the problem extremely accurately.

#### Mechanics of an ML Problem
Define model to be function \\( h(\mathbf{x},\theta) \\):
- \\( \mathbf{x} \\): Input in vector form (e.g. if \\( \mathbf{x} \\) where a grayscale image, the vector's components would be pixel intensities at each point)
- \\( \theta \\): vector of parameters model uses (optimized by model as it is exposed to more and more examples). Usually, there are various \\( \theta \\) that optimize the model. Most of the time, the differences are neglectable. If they are not, more data must be collected.

<u>Figure:</u> Process of vectorizing an image for an ML algorithm ![Process of Vectorizing an image for ML algorithm](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0103.png)

*<u>Def.</u> Optimization:* Finding an optimal value for parameter vector \\( \theta \\). Optimizer aims to <i>maximize</i> performance of ML model by iteratively tweaking its parameters until error is minimized.

Examples of how a simple ML problem is to be found in [a mathematical example](#A-Mathematical-Example).

---

## Deep Learning

*<u>Def.</u> Deep Learning:* subset of ML for complex problems with  high dimensionality and non-linear relationships, where models resemble structures utilized by brains, tackling problems such as
- object recognition
- natural language processing (NLP)
  - Automated Translation
  - Speech Comprehension

### The Artificial Neuron
The approach to think about neurons as a series of vector manipulations was first introduced by [Warren S. McCulloch and Walter H. Pitts](http://www.cs.cmu.edu/~./epxing/Class/10715/reading/McCulloch.and.Pitts.pdf) in 1943.
1. Dot Product of input and weight vectors: Take input vector \\( \mathbf{x} = \begin{bmatrix}x_1 & x_2 & ... & x_n\end{bmatrix} \\), which is multiplied by a specific weight \\( \mathbf{w} = \begin{bmatrix}w_1 & w_2 & ... & w_n\end{bmatrix} \\) s.t. \\( z = \mathbf{x} \cdotp \mathbf{w} \\).
2. Apply transformation function to weighted inputs and add bias term s.t. \\( y = f(\mathbf{x} \cdotp \mathbf{w} + b) \\), where \\( b \\) is the bias term (not shown in diagram).

<u>Figure:</u> schematic for neuron in artificial neural net
![Schematic for neuron in artificial neural net](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0107.png)

Single neurons are more powerful than linear perceptrons, but not expressive enough to solve complicated learning problems.

### Feed-Forward Neural Networks
*<u>Def.</u> Artificial Neural Network:* constructed from multiple neurons hooked up with each other via the input data and output nodes (corresponding to network's answer to a learning problems).

*<u>Def.</u> Feed-Forward Neural Network:* an artificial neural network *without* connections between neurons in the same layer; without connections transmitting data from higher layer to lower layer (only from lower to higher layer).

The following diagram shows a simple example of a feed-forward neural network with three layers (input, one hidden, output) and three neurons per layer:
- Bottom layer: pulls in input data
- Middle layer, or *Hidden layer*: where most of the "magic" happens
  - where \\( \mathbf{w}^{(k)}_{i,j} \\) is the connection between the \\( i^{th} \\) neuron in the \\( k^{th} \\) layer with the \\( j^{th} \\) neuron in the \\( (k+1)^{st} \\) layer.
  - The weights constitute parameter vector \\( \theta \\)
  - Activities of hidden layers tell a lot about features in network
- Top layer (output nodes): computes final answer

The aim is to optimize \\( \theta \\).

<u>Figure:</u> a simple example of a feed-forward neural network with three layers and three neurons per layer
![A simple example of a feed-forward neural network with three layers (input, one hidden, output) and three neurons per layer](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0109.png)

##### Keep in mind:
- Not necessary/recommended that every layer has the same number of neurons. Usually, hidden layers have fewer neurons than the input layer (to force network to learn compressed representations of original input)
- Not every neuron has its output connected to the inputs of all neurons in the next layer.
- Inputs and outputs are *vectorized* representations.

#### Mathematical Representation of a Feed-Forward Neural Net
- Input of \\( i^{th} \\) layer: \\( \mathbf{x} = \begin{bmatrix}x_1 & x_2 & ... & x_n\end{bmatrix} \\) of size \\( n \\)
- Aim: find \\( \mathbf{y} = \begin{bmatrix}y_1 & y_2 & ... & y_m\end{bmatrix} \\) of size \\( m \\)
- \\( \mathbf{y} \\) is produced by propagating input through neurons, i.e. \\( \mathbf{y} = f(\mathbf{W}^T\mathbf{x} + \mathbf{b}) \\)
  - Transformation function \\( f \\)
  - Weight matrix \\( \mathbf{W} \\) of size \\( n \times m \\)
    - Each column corresponds to a neuron
    - \\( j^{th} \\): weight of connection pulling \\( j^{th} \\) element of input
  - Bias vector \\( \mathbf{b} \\) of size \\( m \\)

### Linear Neurons and Their Limitations
*<u>Def.</u> Linear Neurons:* neurons using linear function in form of \\( f(z)=axz+b \\)

| Pro | Con |
|---|---|
|Easy to compute with| Any feed-forward neural network consisting of only linear neurons can be expressed as network without hidden layers.<br> **Problem because:** hidden layer is what enables us to learn important features from input data|

<span style="color:red">To learn complex relationships, we need to use neurons that employ some sort of nonlinearity.</span>

### Non-Linear Neurons
There are three major types of neurons used to introduce nonlinearities in computations.
#### Sigmoid Neuron
- Function: \\( f(z)=\frac{1}{1+e^{-z}} \\)
- S-shaped nonlinearity
- Range: \\( z \in (0,1) \\)
- Intuition:
  - When logit is very small, output of logistic neuron is very close to 0
  - When logit is very large, output of logistic neuron is close to 1

<u>Figure:</u> Output of Sigmoid Neuron as \\( z \\) varies ![sigmoid neuron](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0111.png)

#### Tanh Neuron
Usually preferred over sigmoid neuron, because it is zero-centered.
- Function: \\( f(z)=tanh(z)= \frac{sinh(z)}{cosh(z)} \\)
- S-shaped nonlinearity
- Range: \\( z \in (-1,1) \\)
- Intuition:
  - When logit is very small, output of logistic neuron is very close to -1
  - When logit is very large, output of logistic neuron is close to 1

<u>Figure:</u> Output of Tanh Neuron as \\( z \\) varies ![](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0112.png)

#### Restricted Linear Unit Neuron (ReLU)
Recently become neuron of choice (especially in computer vision) [for a number of reasons](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.6419&rep=rep1&type=pdf) (see Ch 5).
- Function: \\( f(z)=max(0,z) \\)
- Hockey-stick shaped response
- Range: \\( z \in {0,z} \\)

<u>Figure:</u> Output of ReLU Neuron as \\( z \\) varies ![](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0113.png)

### Softmax Output Layers

*<u>Def.</u> Softmax Output Layer:* output vector representing probability distribution over a set of mutually exclusive labels, which gives an idea of how confident we are in our predictions. The output is represented by \\( )\mathbf{p} = \begin{bmatrix}p_0 & p_1 & ... & p_n\end{bmatrix}$, where $\sum^n_{i=0}p_i=1 \\), meaning that the sum of all outputs must equal to 1.

- Output of softmax layer depends on outputs of all other neurons in its layer.
- Let \\( z_i \\) be the logit of the \\( i^{th} \\) softmax neuron, and normalize it by setting the output to \\( y_i = \frac{e^{z_i}}{\sum_je^{z_j}} \\)
- Interpretation:
  - Strong prediction if a single entry is close to 1, while others are close to 0.
  - Weak prediction when multiple possible labels that are more or less equally likely.

---

## A Mathematical Example

### The [Linear *Perceptron*](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.588.3775)

Predict exam performance based on number of hours of sleeping (\\( x_1 \\)) and number of hours studying (\\( x_2 \\)), where data collected is \\( \mathbf{x}=[x_1 x_2]^T \\)
Learn model \\( h(\mathbf{x}, \theta) \\) with parameter vector \\( \theta = [\theta_1 \theta_2 \theta_3]^T \\) s.t.

$$h(\mathbf{x},\theta) = \begin{cases} -1 \text{ if } \mathbf{x}^T \cdotp \begin{bmatrix} \theta_1 \\ \theta_2 \end{bmatrix} + \theta_0 < 0\\ 1 \text{ if } \mathbf{x}^T \cdotp \begin{bmatrix} \theta_1 \\ \theta_2 \end{bmatrix} + \theta_0 \geq 0 \end{cases}$$
which describes the blueprint of the model (in this case a linear classifier dividing the coordinate plane into two halves). We have to learn parameter \\( \theta \\) s.t. the model makes the right predictions (-1 when performing below average, or 1 otherwise) given input \\( \mathbf{x} \\).

![Sample Data for exam predictor algorithm and potential classifier](https://www.safaribooksonline.com/library/view/fundamentals-of-deep/9781491925607/assets/fodl_0104.png)

The model will predict an output (in this case \\( \theta = \begin{bmatrix}-24 \\3 \\4\end{bmatrix} \\)), making a correct prediction where \\( h(\mathbf{x},\theta) = \begin{cases} -1 \text{ if } 3x_1 + 4x_2 - 24 < 0\\ 1 \text{ if } 3x_1 + 4x_2 - 24 \geq 0  \end{cases} \\) makes as many correct predictions as possible.

### The Neuronal Model
Similarly, we can use the neuronal model, which is equivalent to the linear perceptron. Note that $z$ represents the *logit*, which represents the dot product without the bias vector (i.e. $z=\sum^n_{i=0}w_i x_i)$)

$$h(\mathbf{x}, \theta) = \begin{cases} -1 \text{ if } z < 0\\ 1 \text{ if } z \geq 0 \end{cases}$$

Singular neurons are strictly more expressive than linear perceptrons. <span style="color:red">Every linear perceptron can be expressed as a single neuron, but single neurons can also express models that cannot be expressed by any linear perceptron.</span>
