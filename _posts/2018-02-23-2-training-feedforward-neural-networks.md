---
layout: page
title: "2. Training Feed-Forward Neural Networks"
category: fodl
date: 2018-02-23 18:42:22
order: 3
---

# Chapter 2: Training Feed-Forward Neural Networks
---

This chapter discusses
1. [The Fast-Food Problem](#training)
2. [Gradient Descent](#gradient-descent)
3. The Delta Rule and Learning Rates
4. Gradient Descent and Sigmoidal Neurons
5. The Backpropagation Algorithm
6. Stochastic and Minibatch Gradient Descent
7. Test Sets, Validation Sets, and Overfitting
8. Preventing Overfitting in Deep Neural Networks

and teaches the basics involved in training a feed-forward neural network, such as [minimizing the squared error](#squared-error-and-the-error-function).

---

## Training

<span style="color:#DE5F31">*<u>Def.</u> Parameter Vectors:*</span> the weights for all the connections in the neural network

<span style="color:#DE5F31">*<u>Def.</u> Training:*</span> finding the parameter vectors.

During training, we show the neural net a large number of training examples and iteratively modify the weights to minimize the errors we make on the training examples.

After enough examples, we expect that the neural network will be quite effective at solving the task it's been trained to do.

### Training a Linear Neuron

Theoretically, the intelligent selection training set is the best method. However, even though research says this renders best results, its practical applicability is questionable: it does not work well for image recognition.

Practically, minimizing squared error of a model is a better and more generally applicable approach.

---

## Squared Error and the Error Function
The following approach works in general for any type of problem when training a neural net: minimizing the error function.

#### Approach

| Step |Description |
|---|---|
|Given| large training set|
| Unknowns | weights |
|Calculate| output of neural net on \\( i^{th} \\) training example|
|Goal|<mark>minimize **square error** of training set (\\( E \\)) to pick optimal weights while training neuron and minimize error</mark>|
|Reaching Goal|<mark> select parameter vector \\( )\theta \\) s.t. \\( E \\) is as close to 0 as possible.</mark>

<u>Note:</u> not possible to use a system of equations to solve this problem, because nonlinear systems (where we can no longer set up a system of equations) work much better.

#### Error Function

The square error can be minimized by minimizing the value of the error function \\( E \\):

$$E = \frac{1}{2}\sum_i(t^{(i)}-y^{(i)})^2$$, where
- \\( t^{(i)} \\): true answer for \\( i^{th} \\) training example
- \\( y^{(i)} \\): value computed by neural network

Intuition:
- The squared error is 0 when the model makes perfectly correct predictions on every training example.
- As \\( E \\) approaches 0, the better the model.

---

## Minimizing Squared Error
As noted in the section on [the squared error and error function](#squared-error-and-the-error-function), minimizing the squared error is a common approach to optimize weights and minimize error of our models. The following section will look at following methods:
1. Gradient descent (Single Neurons)
2. Backpropagation Algorithm (Multilayer Neural Network)

### Gradient Descent Algorithm
<mark>Gradient descent minimizes the error function to help tackle the problem of training neural networks.</mark>

Given a function defined by a set of parameters, the gradient descent algorithm starts with an initial set of parameter values and iteratively moves towards a set of parameter values that minimize the error function. The iterative minimization is achieved using calculus, taking steps in the negative direction of the function gradient, or *gradient vector*. (Read more [here]("https://spin.atomicobject.com/2014/06/24/gradient-descent-linear-regression/").)

#### Gradient Descent with Sigmoidal neurons

Assumption: Neurons do not use bias term, i.e. bias = 1

Output value
\\( y = \frac{1}{1+e^{-z}} \\), where \\( z = \sum_k w_k x_k \\)

The neuron computes the weighted sum of its inputs (\\( z \\)), and feeds it into the input function to compute the final output, \\( y \\).

1. Compute gradient of error function w.r.t. weights: take derivative of logit w.r.t. input and weights: \\( \frac{\delta z}{\delta w_k} = x_k \\) and \\( \frac{\delta y}{\delta z} = \frac{e^{-z}{(1+e^{-z})^2} \\).
Expressed in terms of output:
$$ \frac{\delta y}{\delta z} = \frac{e^{-z}}{(1+e^{-z})^2} = ... = y(1-y) $$

2. Use chain rule to get derivative of output w.r.t. each weight.
3. Combine (1) and (2) and compute derivative of error function w.r.t. each weight.
4. Final rule for modifying weights:
$$ \frac{\delta E}{\delta w_k} = \sum_i \epsilon x_k^{(i)} y^{(i)} (1-y^{(i)})(t^{(i)}-y^{(i)} $$

**The new modification rule is like the delta rule, except with extra multiplicative terms included to account for the logistic component of the sigmoidal neuron.**

### Backpropagation Algorithm

- To train multilayer neural networks
- Pioneered by David E. Rumelhart, Goeffrey E. Hinton, Ronald J. Williams in 1986 (read paper [here](https://www.iro.umontreal.ca/~vincentp/ift3395/lectures/backprop_old.pdf)).

**General idea of <span style="color:#DE5F31">back propagation</span>:**
In order to find the path of steepest decent, we (i) compute how fast error changes as we change hidden activity and (ii) figure out how fast error changes when weight of individual connection is changed.

##### General dynamic programming algorithm:
1. **Calculate error derivatives w.r.t. single training examples** (i.e. compute error function derivatives at the output layer):
$$ E = \frac{1}{2}\sum_{j\in output}(t_j - y_j)^2 \rightarrow \frac{\delta E}{\delta y_j} = - (t_j - y_j) $$
where z: logit, y: activity of neuron, j: layer
2. **Inducive Step: given error derivatives of layer j, compute error derivatives for activities of the layer below in layer i:**
  - Accumulate information about how output of neuron in layer i affects logits of every neuron in layer j.
  - Partial derivative of logit w.r.t. incoming output from layer beneath = weight of connection w_{ij}
  - Error derivatives of layer i in terms of error derivatives of layer j:
  $$ \frac{\delta E}{\delta y_i} = \sum_j w_{ij}y_j(1-y_j)\frac{\delta E}{\delta y_j} $$
3. **Given the error derivatives for the activities  of the hidden units, get error derivatives for weights leading into a hidden unit.**
  - Requires all partial derivatives of error functions w.r.t. hidden unit activities
  - Sum up all partial derivatives over all training examples in dataset
  - Modification formula, which uses *batch gradient descent*:
  $$ \Delta w_{ij} = - \sum_{k \in dataset} \in y_i^k y_j^k (1-y_j^k)\frac{\delta E^k}{\delta y_j^k} $$


#### Stochastic and Minibatch Gradient Descent

*<span style="color:#DE5F31"><u>Def.</u> Batch gradient descent:</span>* uses entire dataset to compute the error surface, and then follows gradient to take the path of steepest descent. Risk: we might easily get stuck on a saddle point.

<span style="color:#DE5F31">*<u>Def.</u> Stochastic gradient descent* (SGD):</span> each iteration, error sruface is estimated only w.r.t. a single example. This allows for a dynamic error surface. As a result, descending on this stochastic surface significantly improves the ability to navigate flat regions (saddle points). This process, however, might be time consuming.

<span style="color:#DE5F31">*<u>Def.</u> Mini-batch gradient descent:</span>* at every iteration, we compute error surface w.r.t. some subset of the total dataset. <mark>Minibatch is considered another hyperparameter,</mark> and strikes a balance between efficiency of batch gradient descent and local-minima avoidance afforded by SGC.

This results in following backpropagation:
$$ \Delta w_{ij} = - \sum_{k \in minibatch} \in y_i^k y_j^k (1-y_j^k)\frac{\delta E^k}{\delta y_j^k} $$

---

## Builing and Training Deep Learning Models

### General Workflow
1. Define problem rigorously
  - Determine inputs
  - Determine potential outputs (binary, categorical, ...)
  - Get vectorized representation of inputs and outputs
2. Build neural network architecture
  - Define shape/size of input and output and raw data
  - Define internal architecture of network (number of hidden layers, connectivities, etc.)
3. Collect significant amount of data for training and modeling
  - e.g. in the form of uniformly sized pathological images that have been labeled
4. Split data into training, validation, and test sets
5. Begin gradient descent:
  - Train model on training set for an epoch at a time
  - Ensure that error on training set and validation set is decreasing at the end of each epoch
  - Once error on training or validation set stops improving, terminate training
6. Evaluate results
  - If unsatisfied:
    - Rethink architecture
    - Reconsider whether the data collected has the information required to make the prediction we're interested in
  - If training set error stopped improving, we probably need to do a better job of capturing the important features in the data.
  - If validation set error stopped improving, take measures to prevent overfitting
  - If satisfied:
    - Measure performance of model on test dataset:
      - If unsatisfactory: get more data in dataset because test set seems to consist of example types that were not well represented in training set
      - If satisfactory: done!

### Hyperparameters and Hyperparameter Optimization
In addition to weight parameters defined in the neural network, learning algorithms also require a couple of additional parameters to carry out the training process.

#### Hyperparameters

##### Learning Rate
The <span style="color:#DE5F31">*learning rate*</span> is a variable, \\( \epsilon \\), by which the gradient is multiplied. It represents a decreasing function of time, so that minimizing the squared error can be approached asymptotically.

##### Delta Rule
The <span style="color:#DE5F31">*delta rule*</span> trains a linear neuron. In order to calculate how to change each weight, evaluate the gradient (i.e. the partial derivative of the error function w.r.t. each of the weights).

Mathematically:
$$ \Delta w_k = - \epsilon \frac{\delta E}{\delta w_k} = - \epsilon \frac{\delta}{\delta w_k}(\frac{1}{2}\sum_i(t^{(i)}-y^{(i)})^2) = \sum_i \epsilon (t^{(i)}-y^{(i)})\frac{\delta y_i}{\delta w_k} = \sum_i \epsilon x_k^{(i)}(t^{(i)}-y^{(i)}) $$

##### Further/Other
- *Mini-batch gradient descent*
- The *validation set* is a helpful proxy measure for accuracy during the hyperparameter optimization process.
- *Regularization strength* (or L2 regularization)
- Probability *p* (for dropout)

#### Hyperparameter Optimization

##### [Grid Search](https://pdfs.semanticscholar.org/da24/280dfcd767524fb1a1702f50f388ca0d4082.pdf)
- Pick a value for each hyperparameter from a finite set of options, and train the model with every possible permutation of hyperparameter choices.
- Elect the combination of hyperparameters with the best performance on the validation set
- Report the accuracy of the model trained with the best combination on the test set

### Overfitting
*<span style="color:#DE5F31"><u>Def.</u> Overfitting:</span>* when a model is given too many degrees of freedom, and it does not *generalize* well.

*<span style="color:#DE5F31"><u>Def.</u> Epochs:</span>* single iteration over the entire training set.

Generally, <mark>as the number of connections in, or depth of a neural network increase, so does the propensity to overfit to the data.</mark>

#### Observations
1. ML engineer is always working with a direct trade-off between overfitting and model complexity. Therefore, there are many additional countermeasures to prevent overfitting (as will be explained in later chapters).
2. Very misleading to evaluate a model using the data that was used to train it with. Therefore, data is split up into <span style="color:#DE5F31">*training set*</span> and <span style="color:#DE5F31">*test set*</span>. (If the test set is not well constructed, we cannot draw any meaningful conclusions about the model.)
3. It is likely that while data is being trained, that there is a point in time where instead of learning useful features, we start overfitting to the training set. To avoid that that, the training process is divided into *epochs*.


#### General Process
- Given a training set of size d, and doing mini-batch gradient descent with batch size b, then the epoch is equivalent to \( \frac{d}{b} \) model updates
- At the end of an epoch:
  - Measure how well the model is generalizing by using an additional *<span style="color:#DE5F31">validation set</span>*.
  - The validation set tells us how the model does on data it has yet not seen
- If the accuracy on the training set continues to increase while the accuracy on the validation set remains constant or decreases, it should be taken as a sign to stop training because we are overfitting

The validation set is a helpful proxy measure for accuracy during the process of *hyperparameter optimization*

#### Prevent Overfitting in Deep Neural Networks

##### Regularization
*Regularization* modifies the objective function that we minimize by adding additional terms that penalize large weights.
i.e. \( Error + \lambda f(\theta) \), where \( f(\theta) \) increases as \( \theta \) increases, and \( \lambda \) represents the regularization strength (another hyperparameter).

The value chosen for \( \lambda \) determines how much we want to protect against overfitting:
- \( \lambda = 0 \): no measure against possibility of overfitting
- \( \lambda \) too large: model will prioritize keeping \( \theta \) as small as possibel over trying to find the parameter values that perform well on training set

###### L2 Regularization
- Can be implemented by augmenting error function with squared magnitude of all weights in the neural network
- Add \( \frac{1}{2}\lambda w^2 \) to error function
- Interpretation:
  - Heavily penalizes peaky weight vectors
  - Prefers diffuse weight vectors
  - Encourages networks to use all of its inputs a little rather than using only some of its inputs a lot
- When implemented during gradient descent update: using L2 regularization means that every weight is decayed linearly to 0. Therefore, it is often referred to as *weight decay*.
- Empirically performs better than L1 regularization


###### L1 regularization
- Add \( \lambda |w| \) for every weight in the neural network
- Leads the weight vectors to become sparse during optimization (i.e. very close to exactly zero)
- Neurons with L1 regularization end up using only small subset of their most important inputs, making them resistant to noise in inputs
- Very useful when you want to understand exactly which features are contributing to a decision (otherwise use L2)

##### Max Norm Constraints
- Similar goal of attempting to restrict \( \theta \) from becoming too large (but more directly than L1 or L2)
- Enforces an absolute upper bound on magnitude of incoming weight vector for every neuron
- Uses projected gradient descent to enforce the constraint
- i.e. any time gradient descent stemp moves the incoming weight vector s.t. \( ||w||2 > c \) (we project vector back onto ball with radius c)
  - typical values of c are 3, 4
- Parameter vector cannot grow out of control (even if the learning rates go too high) because the updates to the weights are always bounded

##### Dropout
- One of the most favored methods
- While training, it is only implemented by keeping one neuron active with some probability p (a hyperparameter), or setting it to zero otherwise.
- This forces network to be accurate even in the absence of certain information
- Prevents network from becoming too depentend on any one (or any small combination of) neuron.
- Prevents overfitting by providing a way to approximate combining exponentially many different neural network architectures efficiently
- Intricacies to consider:
  - Goal: outputs of neurons during test time should be equivalent to their expected outputs at training time
  - If we would fix it naively by scaling output at test time (e.g. p = 0.5), neurons must halve their outputs at test time in order to have the same (expected) output they would have during training
    - Because: neuron's output is set to 0 with probability 1-p
    - i.e. Neuron's output prior to dropout was x, after dropout it is \( E[output] = px + (1-p) * 0 = px \)
  - Undesireable naive approach (requires scaling of neuron outputs at test time, and is time consuming)

##### Inverted Dropout
- Scaling occurs at trianing time instead of at test time
- Any neuron whose activation hasn't been slices has its output divided by p before the value is propagated to the next layer
- i.e. \( E[output] = p * \frac{x}{p} + (1-p) * 0 = x \), so we can avoid arbitrarily scaling neuronal output at test time
- Much more time performant
