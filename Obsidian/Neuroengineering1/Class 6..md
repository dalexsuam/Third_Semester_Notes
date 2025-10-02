
***

02/10/2025

Today we will see a new kind of architecture. Autoencoders.

The idea is to overcome the acquisition of the fully-connected and CNN we reduce the numbers of weights and issues related them by increasing the number of layers (check)


![[Pasted image 20251002083645.png]]

Instead of learning in a back-propagation. we are going to show to learn layer by layer. Focusing on one layer regarding what happen in the next layer and apply learning for that layer. The trade-off is that we are not able to use the traditional supervised learning.

Remember weights are task dependent (regression and clasification). here it doesn´t happen cos there is no task.

![[Pasted image 20251002083912.png]]
We see that supervised learning we have the labels. In unsupervised learning we have no labels, we need to find a counter-measure for this lack. We see we have clustering and PCA, but also autoencoders and generative models, these are progressing neural network that increase the complexity that try to avoid the weights depending on the task but exploring other considerations towards to increase as much as possible the generality of the network.

When we are taken the two CNN each with each task, if I changed them, non of them would work. (Most probably) cos the weights were computed w.r.t that certain task (different classifications).

The idea of the autoencoding is that it can be applied to any task :)


![[Pasted image 20251002084339.png]]
THe idea is to extract representative features layer-by-layer. Recap this process is called encoding, putting in place a network which is not only enconding but also decoding. What is the reference? the label? THe data itself, the layer should be able to encode the data, reaching a sort of ... and finally try to infer the same data. I have no additional label to be used by I am, compressing, decoding and bringing back the data... Considering a proper architecture. 

The output should be very close to the input. The image shows a representational example, we try to replicate the input. Actually the output decoder is able to replicate the input into the output when a proper training is put is placed. We need a proper training to let this network to work like this.

The simplest way in architecture for autoencoder, is 1 encoding and 1 decoding layer. a batch of neurons, we don´t know what it is doing but from architecture pov it is enough having the set of neurons organized in a layer.

![[Pasted image 20251002084828.png]]

I have an input, I have 1 hidden layer, in this case is the encoding layer, then we have a decoding layer that in this case is also the output layer. In terms of connectivity you might see I put in place a very general assumption, a fully connection, I am not assuming any particular constrain, convolutional, etc. Just fully connection and as always we might consider the neuron are acting throughout activation functions. In the hidder layer we´re using a linear activation, this means the encoding is performing a linear combination of the input, in the output we have a linear processing of the outputs of the hidden layer. 

We know also we can improve the ability to represent information using non-linear functions.

We have an output z, and we consider a training that let z get an output exactly equal to the input. In this case from architectural pov we have one constrain that is the dimentionality of the hidden layer, that is exactly the number of neurons we´re setting in the autoencoder unit. As we might interpret, i´m using less number of neurons w.r.t the input, this network is compressing data. Reducing the dimentionality of the hidden layer, the idea is that this dimentionality allows to extract features. As we call a feature map, in a convolutional layer, we can call it here feature detector, feature map, the difference here is that the feature map is the set of weight of the filter, here we don´t have a weight that define a filter(in CNN) cos we have a lot of weights, any neuron is up to N weights, the processing here is not local but global, weŕe not sure what this filter is doing. 

Autoencoders can be use to any kind of data. In general we might implement them using also Convolutional hidden layers. 

![[Pasted image 20251002085644.png]]

Example: I have my dataset, made up with geometrical figures, We have four kind of different shapes with a certain distribution in rotation and position. 

We see we have 30x30 = 900 pixels at the input, we have an encoder layer with 100 neurons and a decoder with 900 neurons which would get back the size of the initial input. Then what features are the encoded by signals $y_i$? What it is represented in this weights?

![[Pasted image 20251002090130.png]]
THe basic of autoencoder is to split layer by layer the training, letś consider a multilayer network and letś focus in each.

Layer 1, for instance. the principle of training is that if I have some sort of algorithm that is able to compute the weights of the hidden layers, and the output layer, I've solved the training process and from so on the decoding layer is no longer needed. Then, we go to the Layer 2, and attach the L2 to the L1, and now we need to train L2. We use the same dataset to train L2 as L1, and then we have decoder 2, perform the same training, and we get rid of D2, then L3, and so on...
Every training we are learning the weights from the last layer. Basiccally the output of L1 is becoming the input of L2, then you create the decoding layer according to L2, and then apply the training, remove the decoder, concatenate it with L3, do decoder, bla bla...

The assumption is that we´re proggresively reducing the size of the layer. The number of neurons in the first layer layer is greater than the following one $H_1>H_2$

![[Pasted image 20251002090509.png]]

This way I might reconstruct a multilayer network. From architec pov how to setup thing? How to train it?...

![[Pasted image 20251002090557.png]]
The assumption the train has to solve the match of one input and an output that has to be identical... I might use again backpropagation in unsupervised approach. it is not straight forward, cos we don´t have a label that define a task, but from the arch pov weŕe in the same condition, we have a reference in the output, and so we approach it with backpropagation under unsupervision. So, one way to consider the training is to have a input- to have an output (standard loss function that might use here that is exactly the squared error), this backpropagation is an interative process, initialize the weights properly, all the same steps we´ve been learning... But, the difference is that learning weights in an autoencoder is usually called unsupervised backpropagation, it is not completely the same. 

We have another issue, # of neurons in the hidden layer, it is defining the degree of compression. We start from a dimensionality and it needs to be encoded in a smaller one and then we need to bring it back to the initial dimensionality. 

because of this it is consider that it is an ill-posed problem cos of this we need additional constrains, how the processing is performed in the hidden layer in this case. Instead of using just the gradient, we have another one...


![[Pasted image 20251002091231.png]]

There are different possibilities constrains, here we use smt called sparsity that can be regarded as a way of let not all the neurons work concurrently. Not all the neurons are producing an output. 

Depending on the input pattern, we change the activation of certain neurons (Each pattern active the layer in a different way) Note different x(i) and y(i)

Bold X is the frist pattern into my training set, if we recall, the set of images is my training set. Each pattern is one image, and in this case I´m focusing into one neuron into the hidden layer and we´re reading the output. THen, we´re reading the neuron, and then we turn on and so on... If we have R patterns, the same neuron will produce R outputs... So, the idea is to analyze on average what happen on the output of the neuron. y(1) in the output of the neuron corresponding to pattern x1, y(2) is the output of the same neuron corresponding to pattern x(2) and so on..
![[Pasted image 20251002092102.png]]

The idea is that if we´re considering the individual output vector y(R) of all neuron, we´ll see that this neuron will select an specific feature, if I change the neuron, another activation would take place, it should be different, because one neuron is encoding one feature, and another neuron is encoding a different feature. If i´m receiving a circle image, a neuron might encode the circle, and another one no. so, we fire up the neuron which does it. This is the way of implementing sparsity in a network in order to encode the neuron.

![[Pasted image 20251002092417.png]]

Basically if the output approaches 1, it is active, if not, inactive. And then we have the computation of the input for an activation function (Action potential + bias), this case, the activation for all the input patterns and then i´m the summation across all the patterns in the training set. In this case, the $\rho$ is consider the average activation of the hidden unit over all the data in the training set. Basically, this factor may span from 0 to 1, it is an average activation which is ranging from 0 to 1, the summation is leading to a scalar factor that may be go from 0 to 1.

If the $\rho$ is equal to 1, it means that all the neurons are active, there is no sparsity, and the opposite is 0, it means that the neuron is not active at all. We might add some constrain to this $\rho$ factor, tailor it to an specific value. 25% of my neurons should be reactive or conversely or 1 neuron should react to the 25% of the data into the training set. If we´re considering the $\rho$ average activation. And I can actually set this parameter to let the network be more or less sensitive , $p^(^)$ = p, we have to compare with the sparsity parameter should be close to 0.05, 5% constrain rho being like that and this contribution to the gradient contribution and upgrade the weights, and ==this is a hyperparameter of the training that we have to set up and choose. Is your hidden layer sensitive or not that much?== The more it decreases, the more it gets sensitive, which would lead to overfitting. That is why we have limitations in this . 

![[Pasted image 20251002093214.png]]
Let´s take this example, I have one pattern k in the data set, I´m feeding the network and reading that there are two activated neuron, then i´m changing the input patter to m, and i´m reading other neurons that are active. in this way this network is acting in a sparse way, basically those two neurons are encoding features included in the pattern k, the same happen with the other two neurons with the pattern m.
![[Pasted image 20251002093340.png]]
And now we consider the pattern n and we see that the same two neurons are acting from pattern n and pattern k, these might be very alike, both could be circle. However, this is just one layer, that is extracting the features relationship from the very first time and we cannot expect that from the very first layer we´re extracting all of the features :) 

![[Pasted image 20251002093639.png]]

Assuming we were training layer-by-layer. What happened here? In this case, I have different types of activations for the same input. MOst likely we´ve used different sparsity factors in the same network, same input pattern. That is why the activation changes, let´s say 1% and 10%/ That is why it is not easy to train between the number of layer we have to consider, because it depends on the complexity of the input pattern and the number of neurons is again heuristic has to be defined and at the end, also the sparsity factor has to be defined.


![[Pasted image 20251002093850.png]]
We´re using the same math of backpropagation.

How many layers we have now? The hidden layer (encoding) and decoding (output layer). A backpropagation is nice with just one step back, formally three layers, the input, hidden, and output, but the very first is not an active layers, thus only two steps for the backpropagation.

![[Pasted image 20251002094004.png]]

We have the gradient contribution and the L2 norm, which prevents the overfitting, it is the function in the gradient, we compute the derivative and include in the gradient descent ... This is a contribution for adittional constrain, this is the first constrain and then..
![[Pasted image 20251002094116.png]]

Then we have contribution which is the sparsity function, depending on the sparsity parameter defined. If we want layers senstivitiy to be very sensitive or not. So, we have the average activation. We have to compute the derivative of the function w.r.t the weights, so, we compute the rho hat, depends on weights and basically if I have to compute the gradient, we have to start considering that rho hat contains the weights.

Three contributions: the gradient, and L2 norm and the third is the sparsity. For the time being we don´t define what is G, we need a sort of function that is able to minimize the difference between the sparsity function a rho hat. 

![[Pasted image 20251002094404.png]]

Is it a simple difference, nope. One possibility is the kullback leibler divergence, which is the curve we see. Basically, the sparsity function when iḿ using the kullback leibler divergence is becoming the function weŕe reading up to there, sort of dependency of log, having the weights in the denominator, it is complex from certain pov but it is exactly that one in a plot. IF we start at 0 point, the sparsity function have to move fro any point up to there. It is not symmetric.

As you approach the 0.2, there is a very small probability that according to the derivative of that function is moving away cos the derivate is pretty low. There is a less probability to have overshooting, that is moving to the other side. Weŕe just not minimizing a difference, but the effect that we´re moving from a large value or small from any of the sides, and we´re converging no matter. 

There might be other kind of functions alike.

![[Pasted image 20251002094934.png]]

Now, letś focus, considering one neuron. I´m considering the output and I have to evaluate each contribution. MY target is to compute $\Delta W$ , does have this layer (The last) any sparsity factor? NO.

We apply then a traditional delta rule. 

And in the layer 2, we do apply backpropagation + contribution of the derivative of the sparsity factor. We have there now $g$ is the derivative of the sparsity function $G$

![[Pasted image 20251002095215.png]]

Now, ofc let´s compute the derivative of the sparsity function :)

H is the number of neurons in the hidden layer.

Third row, we compute the gradient of the sparsity function w.r.t weights, by chain property we change the dependency...

And we get the result highlighted in purple-ish.

In this way we added a spatial contribution into the gradient that help us to constrain properly how the neurons are computed w.r.t train dataset. Take into account this is solving just for one layer, this means that for the next layer we apply the same approach but we change the $\rho$ factor. We can set the first layer less sensitive and the last layer very sensitive or the opposite. 


![[Pasted image 20251002095724.png]]

And this is in general the schematic of the whole training.

![[Pasted image 20251002095858.png]]

Coming back to the example.

We have a encoder part of the network, then a task specific network to classify stuff...
![[Pasted image 20251002100005.png]]

I have trained it using 0.15 of $\rho$ factor, $\beta$ is the scale, the weight of the sparsity function in the gradient, the one that modulates it. I have 900 patter input and I´ve chosen 100 neurons in the hidden layer. 

How many weights have any neuron in the hidden layer? Fully connection thus 900 weights each neuron. and we see that we obtain the image. the one of 30x30, that is the image of the filter. This image is the filter correspondence to the 900 neurons, 

![[Pasted image 20251002100235.png]]

Each neuron has its own representative filter.
![[Pasted image 20251002100256.png]]
Some neurons are encoding stars, triangles, circles.

Then with 0.15, this means that this neuron reacts at most to 15% of the overall training set. This is the same, we don´t know how but from an visual pov, we see that some filters are fine, others we don´t understand what we´re extract.

no matter the number of figures, the sparsity factor set the sensitivity to extract features of the data. so, it is not like we set 25% cos there are 4 possible figures. 

![[Pasted image 20251002100558.png]]
So, let´s see the difference between 0.05 than 0.25.

AND WHY ALL LOOK LIKE CIRCLES? The rotation of the circle is not present and basically the shape of the circle is overreprsented, the other shapes are rotated and does insert another degree of freedom. This means that the dataset is not completely representing all the possible shifting, rotations, position of triangles, stars, etc. 

The 0.05 is pretty selective, so it might show overfitting, and the 0.25 is poorly selecting.


![[Pasted image 20251002100951.png]]
Now, I have 100 neurons, then 50 neurons, and then apply the training in the softmax layer to do the selection. 








