
![[Pasted image 20250922103959.png]]
![[Pasted image 20250922104106.png]]
We requiere differentiable function to perform the gradient descent computing.

![[Pasted image 20250922104157.png]]

The idea is to let the weight vector be close to 0 on average. We would like to stay away from saturation regions (sigmodal function), so we're able to assure small weight vector modules. 

![[Pasted image 20250922104256.png]]

For perceptron learning rule we use on-line. Every iteration will contribute to the update of the weights.


![[Pasted image 20250922104433.png]]

On the other side for delta rule as we started considering a full batch updating strategy where we considered all of the elements in the training set considering their contributions where summed up to provide the final $\Delta W_{ij}$

Batch updating is muting out the effect of a single sample of a training set, it sort of compute an average contribution.

The last way is considered a middle approach between full batch and on-line

![[Pasted image 20250922104536.png]]

We then consider subset of the overall training data set. The overall dataset that has been split in some group and we're computing the update for each specific mini-batch and update the weight. This is true up to the end of the subsets S.

![[Pasted image 20250922104657.png]]

If I have 10 subsets and 100 samples in the data sets i'll have 10by10. Or 100 subsets will have 100by1.

Another interesting concept is the learning rate: Way of modulating the size of the gradient. This is the main rule of this quantity, it is an scalar value and ranges from 0 up to 1 and this can be better represented as:
![[Pasted image 20250922104845.png]]
Consider a negative gradient which scales down the module of the gradient by various learning rate. The idea is that I'm moving along the error function, if I have set properly the learning rate I'll find converge. 

What happen if learning rate is too large??
![[Pasted image 20250922104956.png]]

Here we're in risk of not converging, so we could not reach it.

On the other side if it is very small
![[Pasted image 20250922105025.png]]

It might be more conservative but will be pretty slow to achieve the converge. From analyitical pov, there is no choice to set the value but an heuristic choice. The rate might set 0.001, 0.01 so on... Common values for learning rate. 
![[Pasted image 20250922105136.png]]
We might face a problem with the error function. If we're moving in the yellow function we're reaching the minimum easily. But if we consider the other, there is a very flat spot and in this region que gradient in very small, cos the derivate in this part in close to 0. I'll move faster initially but then i'll move pretty slow.

STOPPING RATE

![[Pasted image 20250922105301.png]]

previous example was 50 iterations. But, cos classification was easy to understand. In a general problem we can't say what is the optimal condition for our training, for this there are many diff criteria to take into account.


Consider to enable a max number of iterations, very trivial way
CONSIDER A MODULUS OF THE GRADIENT TO STOP THE ITTERATIONS WHEN MODUUS IS LOWER THAN THE PREDIFINED THRESHOLD or Alternatively we might consider the error function and some sort of trade-off epsilon value we might set for the error function to be reach. 

I'll read the criteria, an hybrid criteria and the value of the error function for the sum. Taking into account the values of alpha and beta and the value of the threshold.


![[Pasted image 20250922105529.png]]

We revised the delta ruled considering the squared error. In general you might extend from an optimization to a regularization problem introducing constrains, in this case we have one constrain related to the weight. In this case is to avoid the possibility for weights to get higher values.

Initially is a function squared, the modulus, the idea is that during the training we're copying with the standard error function. The difference between the output and corresponding nominal value in the meantime we want it to be small. So, if we're using sigmoidal neurons, we would like to use the neuron to work in the active and not saturation region. Conversely, we have to consider an additional regularization rate, some hyperparameter and needs to be setup heuristically a priori.

This is an example of error function where we minimize the diff of the output and nominal value but we might have another function depending on the output and the task. In a sort of regression problem, this could be useful, in a classification problem we might use cross entropy.

![[Pasted image 20250922105913.png]]

Numerosity is depending on data. The more the better the effect in the training (it is heuristic rule, a good practice).

Select data that are targeting the task we're interested in, avoid other representations, get rid of them. 

Considering the values of the inputs, it is important to normalize or scale the inputs. There are diff approaches. It is always fundamentals to let the input data in small values, specially for non-linear we have to avoid saturation. 

![[Pasted image 20250922110210.png]]

We're dealing with data. We need to use it to train the model, and verify the model has a good regularization properties. After the training phase I can validate the training model with data no ever seen. We can divide the dataset in three groups

Training set, validation set used during training but it won't be used for learning but just to verify error function quantity, and the last test set is the extrapolation quality to verify the training...

We have to make a balance between preventing underfitting and overfitting.

Underfitting: don't cope enough complexity of the task
Overfitting: We're using too complex to represent a simpler task

From ANN pov, this means, to avoid too much layers or too much neural units (overfitting), we're dealing with the structure of the network and we have some hyperparameters (number of layers, activation functions, number of neurons). Make the network, check it and see if it is overfitting, if so, check the data, but also the model (in this case reduce the complexity).


![[Pasted image 20250922110650.png]]

First activity of developer is to tune hyperparameters of the network in the terminology of the ANN is called ablation task and this ablation task that is a GridSearch, changing a little bit the hyperparameter and... Basically we have the results of many trainings, compare diff architectures and choose the best architecture that fits your task that is called ablation.

We have to properly select the three sample set: training, validation and test. Also cos in biomedical engineering field data acquisition is limited. Usually, the most part of the data is reserved to training 70-75%, 10% for validation and 15% test just giving reasonable proportions between the three sub-sets

![[Pasted image 20250922111104.png]]


For the simple ANN, we might improve the perceptron with a continuous activation function. The questionable part, we don't have exact rules how to set the weight vector at the beggining or select optimal batch size and we have to be practical in this activities.

---

Now, we're gonna go to multilayer networks.

![[Pasted image 20250922113124.png]]

Delta rule is not usable anymore in multi-layer ANN. But we need to make it evolve.

Another aspect in multi-layer network is the addressing to complex computations, like high polinomial order regression, or perform a classification task in domains not linearly separables. In this first case. a single linear decision boundary is helpful to discriminate distributions but the other three are more complex and from visual pov there is no way to use a single line to split the plane in two regions to correctly classify  class A or B. Here, we have to take apart the two distributions by circular decision boundary or curvilinear and so on.

We're starting from a linear decision boundary and to curve it to adapt to the distributions we're dealing with. And if we want to make the linear decision boundary a curvilinear decision boundary we have to enable in our network a non-linear neurons.

We've seen we have one mayor class of activation that is sigmoid activation function, and logistic function and tanh function, to perform non-linear processing but we can't implement them easily in a single layer network as depicted here. We need to enable an intermediate layer in between the input and output and the idea is that I can't really address non-linear task by just adding neurons in the output. I have two decision boundaries, U1 and U2, but they still remain linear and that's why no matter how I'm combining linear boundaries. 

![[Pasted image 20250922113436.png]]

Enable a inner layer between output and input and I'm getting a multi-layer network, enabling additional inner layers which are sequantially concadenated. Input layer is becoming the input of the inner layer and the output of the inner layer is the input of the subsequent and so on and so forth. 

The more layers I'm inserting and non-linear functions, the very complex problems we're handle 


![[Pasted image 20250922113633.png]]

This is some kind of concentric distribution. The inner region where dots are more gathered and the external region where we see the other class which shows another pattern.

No matter how the threshold and the weights, there is no chance we perform a correct classification.

Another way is considering two decision boundaries x1,x2 (obtained by two inner neurons (sigmoid)) Basically I'm obtaining two and will make two divisions. The idea is to using this two neurons combined in just the new output neuron, in this case a sigmoidal function is taking this linear boundaries and performs a non-linear transformation, a bending in the decision boundaries. WE can move forward and more complexity

![[Pasted image 20250922114016.png]]

I might put an additional inner layer, and will get in the output this decision boundary shape. It is the role on the training deform the decision boundary to create the proper separation in between the two classes. As soon as i'm increasing the complexity of the non-linearities that we're adding into the network, we're moving to the linear to a non-linear function (cubic-ish) and then a very complex function. 

![[Pasted image 20250922114201.png]]

In this case we deal with multilabel classification. Class1: yellow, Class2: red, Class3: blue, Class 4: green. If I'm using two output neurons, I'm ranging in both of them 1 or 0 for the logsig. 2 bits, we can set 4 classes 00, 01, 10, 11. And this help us to solve multilabel classification, more than one neuron at the output but to define properly a non-linear transformation in the inner layer to try to define curvilinear decision boundaries.

![[Pasted image 20250922114412.png]]

It is the same example as the previous slide but here we report the computations. and we have the four possible combinations

![[Pasted image 20250922114534.png]]

We could also implement regression but I have to change the output activation function with the same architecture. Not anymore a logsig. The behavior is to span from -inf to inf by mapping with x1, and x2. We might do the process more complex for example. 

A multidimensional problem at input and we have just one output dimension. 

In the first network, we have the developing time, S1 and S2. and for specific time point we take x1, and x2, and perform processing of those values. And they go in the first network to perform the mapping. In the second network, I'm sample a different number of element from the frist and second signal bulding a vector which are batch together a becoming the input of the network and this is usually the wave to perform signal processing in artificial neural network domain.

![[Pasted image 20250922114920.png]]


Or also here, we're going from one domain to another domain. The output U which is a linear function as a function of three non-linear equal functions. The analytical formulation is the same. 

![[Pasted image 20250922115117.png]]

In this case I would like to model an inverse kinematic problem, to we have two stick-arm, a kind of an arm with two degrees of freedom, q1 and q2 angles. The idea is that in a very complex structure model, we can obtain still angle q1 and q2 having as input xe and ye

COST/LOSS FUNCTIONS

![[Pasted image 20250922115653.png]]

There are different ones, according to the type of task but for example we've seen the squared error... In general MAE, RMSE, RMSEL are useful for regression for classification Binary cross-entropy is the optimal one, in categorical cross-entropy we use multiclass classification

The main difference is that if we're changing the loss function we have to recompute the formulation of the gradient and so on, the update of the weights. 

![[Pasted image 20250922115743.png]]

We're in the domain of supervised learning. Are we still able to use delta rule?
The delta rule is able to update the weights of all the neurons of the network! But in the delta rule, we have the reference value in U, and compute the error to update the weights of the previous layer, however, we have no reference to update weights in the previous layers... In this case the delta rule can't be applicable. No explicit supervision from the output of the hidden neurons.

The solution? Back propagation!!

![[Pasted image 20250922120008.png]]
Example: We have an input set of four elements, one front-end layer with three neurons, then three neurons provide input to a two-neurons layer and then we have an output layer composed of two neurons.

According with what we've said so far, these two layers (I and m) are hidden layers. The idea of backpropagation is to use the error we're computing in the output layer and move back layer by layer, backpropagating the error, this is the principle.

![[Pasted image 20250922120204.png]]

In order to backpropagating, we have to compute the activation of the output. Initialize the weights. Computing layer by layer the outputs
![[Pasted image 20250922120250.png]]


![[Pasted image 20250922120304.png]]
![[Pasted image 20250922120313.png]]

![[Pasted image 20250922120322.png]]

This step of computation is the forward step, where we compute the delta rule.

We apply the delta rule of the two output neurons.
![[Pasted image 20250922120350.png]]

And we update the weights of the output layer. Gradient descendent. y is the sender from m1 and m2. In this case we're dealing with the same approach as delta rule.

![[Pasted image 20250922120552.png]]

We try to apply the same delta-rule. but now weights are called $\Delta C$ , Sr is the sender which spans, Sr1 Sr2 and Sr3 from I1, I2, I3. This is again the derivate of the action potential of m1 and m2. But what is the reference??? yj? from mathematical point of view we have it in the formula but we don't have it! So, we have to use the backpropagation algorithm.

**In way to compute such reference**, we apply then, the approach layer by layer.
![[Pasted image 20250922120814.png]]
To continue up to the first hidden layer (backward step)

![[Pasted image 20250922120842.png]]

Let's solve it with this simpler network

![[Pasted image 20250922120915.png]]

![[Pasted image 20250922120936.png]]

we compute the output and apply the delta rule

![[Pasted image 20250922120953.png]]

and compute $w_{ij}$ with the delta rule. Six values of weights. And these are the formulations.
![[Pasted image 20250922121042.png]]

How to compute delta rule of previous layer?

![[Pasted image 20250922121121.png]]

We have 4 inputs for each of the three neurons. Then 12 values of $\Delta C_{ij}$ 

![[Pasted image 20250922121229.png]]

Compute the error function. The output of the formulation of the gradient w.r.t to C. with the chain rule. 

The sum is the effect of how o1 and o2 affect the weights yj. Basically,

![[Pasted image 20250922121819.png]]

If we consider all contributions from the training set R.

![[Pasted image 20250922122006.png]]

$l$ stands for index of the layer. So that we might use the same term for weights $w$ for every layer just changing the index of the layer. We have $\eta$  learning rate. We have $\delta$ contribution and y contribution. The output of one neuron y in layer l-1 and this output is corresponding to the k, corresponding of the contributions of the training set.

if we consider the last layer, we have the exactly delta rule, multiplied by the derivative of the activation function. If we move back into hidden layers. we have that $\delta$ has a summation of the contribution of the next delta multiplied by the corresponding weights. Sort of recursive procedure

![[Pasted image 20250922122509.png]]

Considering this three layers, we might apply the delta rule.

![[Pasted image 20250922122541.png]]

![[Pasted image 20250922122646.png]]


![[Pasted image 20250922122853.png]]

---
We've seen backpropagation is successful and it works.

![[Pasted image 20250922124306.png]]

When we do NN with python backpropagation is implemented. But, it is not fully the one solving the training problem of complex networks. It has

VANISHING GRADIENT PROBLEM.

It is losing information to be use for training the weight from...

You're starting from the output, and start experiencing some error. And we implement the delta rule, and propagate the error to previous layer to compute the weights, but we're not dealing with the original error, cos the original error was used to compute the weights previously... Ok, i didn't actually understood.

You're using noise from the beginning of the start of the network to update the weights, you're comitting error in updating the weights, the weights that have been computed are wrong and this impact on the next forward 

![[Pasted image 20250922124748.png]]

I have an output neuron and three hidden layer. Each hidden layer is one simple neuron. For every layer I can compute the output.

Try to compute the gradient associated to the first neuron. 
![[Pasted image 20250922124851.png]]
According to backpropagation, we have compute the gradient w.r.t output z, and multiply by derivatives, weights, derivates weights...

And if we're considering the $\Phi$  is a sigmoidal function, it is bounded between 0 and 1.

![[Pasted image 20250922125013.png]]

This means that in the best condition this value is 0.25.

The original gradient has been reduced four times, cos we have 4 updated of 0.25
![[Pasted image 20250922125224.png]]

When we apply backpropagation, this contribution might get confusing with the noise. With multi-layer network the vanishing problem might be an issue.


SUMMARIZATION

![[Pasted image 20250922125327.png]]



![[Pasted image 20250922125754.png]]


![[Pasted image 20250922125810.png]]

![[Pasted image 20250922125825.png]]

In general a developer of NN we have to solve this problems