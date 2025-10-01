
Networks which operate convolutional operations are now Convolutional Neural Networks

<span style="color:rgb(223, 109, 109)">Convolutional Neural Networks (CNN)</span> 

Local receptive field is some sort of information processing that is restricted to an area. It is not expanding to get all the input pattern but it is in charge of the processing of a subset of the input pattern, which is implemented in CNN.

We see that this setup would lead to a new concept which is the shared-weights, before every neuron has its own set of weights and they were different from other neurons. Here, the CNN is no longer having this setup but basically neurons belonging to a convolutional layer are sharing all the same weights...

Another aspect is an especial activation function. Initially we had the rectifier linear unit to process the data linearly from positive action potentials and avoiding the negative action potential. In principle we can perform processing and compression at the same time, and enable an additional layer called pooling layer which is in charge of perform compression, reduce the size of the input.

Stepping at the convolution. For a finite number of parameters we're performing the convolution, in principle in the first layer of the complex deep network (a network with many layers), which is performing convolution, processing and compression.

![[Pasted image 20250926113336.png]]

Here, we have an output of a convolution operation. One neuron per output, and it corresponds to the amplitude of the pixel... In grayscale, ranging from 0 to 255 or whatever.

Each output has a discrete representation of the general output.

Each convolutional layer have its own functionality for this we might infer it is some sort of edge detector. We don't have information of any but the boundaries, regions where we can easily detect the transition in brightness from low contrast to the rest of ...

The processing did convolution and down-sampling (compression).

![[Pasted image 20250926113747.png]]

Here a layered network, where the processing is going from bottom to top.

From architectural pov. in m-1, it is a fully connected layer?, convolutional layer? We don't know :). But in the Layer m, we know for sure it is not a fully connected cos the neurons at the extremes, left and right are connected to just one neuron in neuron m, and there are no other connections, if there were all the connections between one neuron of layer m-1, to layer m, it would be a fully connected but it is not the case...

There is a *suspicious* connection. 

Every neuron in layer m are connected to 3 neurons from layer m-1.

We have a signal, let's pretend is a biological signal sampled with $I=[S_1,  S_2, S_3, ... S_n]$

And we are going to apply a filter with three weights, $F = [W_1, W_2, W_3]$
And we perform the convolution...

$S_1W_1+S_2W_2+S_3W_3=O_1$
This for just one neuron.

Then we perform another convolution with another neuron. 

$S_2W_1+S_3W_2+S_4W_3=O_2$ 

And the next neuron...

$S_3W_1+S_4W_2+S_5W_3=O_3$

We have that then each neuron has an activation function, we apply it to the output of each neuron.

Thus, if for instance we take the $O_2$ , $Activationfunction(O_2)= O_{2_FINAL}$

In this case, this layer m has a local receptive field of 3, cos it has three weights, the smaller the receptive field, we perform more specific computation with more resolution. The increase of local receptive field we are decreasing the resolution of the processing cos we're processing a large part of the *signal*

(Local receptive field ~ number of weights for the convolution of the next neuron)


Layer m then is a convolutional layer with the fact that every neuron is sharing the same weights, exactly the same ones. No matter, the size of the convolutional layer, no matter the number of neurons in layer m, we would always have three parameters. AND THIS IS HOW WE DIFFERENTIATE BETWEEN FULLY CONNECTION AND CONVOLUTIONAL CONNECTION :)

here we didn't add the threshold/bias. In general we consider -T (reducing the action potential by this factor) or we might consider +b. However, this doesn't change anything in the final result if $b=-T$ .

We cannot train now the "size" of the weights of the convolutional layer because they become a hyperparameter which defines the architecture of the network.
![[Pasted image 20250926115444.png]]

Here we just see the 2D representation of the convolution. Now, how to perform convolutional processing without compressing? Depending on the size of the filter, if initially it has the same size of the input, we have the same size at the output, but if the size decreases in neurons in the convolutional layer, the output is lower. Traditional convolutional has a stride 1, sample by sample but a neuronal convolution we can set a widen stride.

![[Pasted image 20250926115745.png]]

This is a graphical representation of the convolutional neuron. They all sharing the same weights. This layer is going to identify the feature map. $W_1, W_2, W_3$. The output of the layer is going to be compressed to three outputs, and the go to the activation map.

To identify the feature map (the filter) we don't need input, to identify the activation map we need the inputs to know the outputs :)

![[Pasted image 20250926120128.png]]


So, representation:

1 input is a pixel value, and this pixel value might span a continuous value, or whatever, one dot has a spatial reference in the matrix. We need to define the number of x and y (rows and columns) to know the coordinates. We've located one and it would be 1 element of the matrix.

Considering I wanna apply a convolutional operator, we need to know the size of the input. Why? to the operator it has to scan the image, but it also has to set the feature map, a simple weight vector line, but if we want to scan a region, we need the 2D representation of the filter. 

![[Pasted image 20250926120549.png]]

We see that the filter is 5by5, the circle represent the neuron in the convolutional layer, it has an specific receptive field which is determined by the size of the filter, (5by5)25+1(bias). If I implement a convolutional layer, every neuron will have the same parameters, and again this configuration would correspond to one feature map, which is a bidimensional in this case.

This is the mathematics for computing the convolution spanning x and y, we have the bias, the resulting value is the overall action potential we process in the neuron, in this case the neuron is an hiperbolic tangent, ujk, ujk has two indexes which are index in the convolutional layer, thus the convolutional layer is arranged as matrix. This matrix that is composed by a number of neurons, the output ujk, we're getting the activation map...

![[Pasted image 20250926120930.png]]

This is the result. I have a input layer, a convolutional layer and the output of the first hidden layer can be drawn like that. remember 25+1 , 26 parameters. Every neuron has exactly the same weights.

If by chance I connect those two layers with a fully-connection architecture it would be catastrophic from the pov of too many parameters. If input is MxN, each neuron in the first hidden layer would have that same number of weights,

And the total number would be MxNxHxJ (HxJ for the first hidden layer)

![[Pasted image 20250926121437.png]]
**WHAT IS DETERMINING THE VALUE OF THE WEIGHT VECTOR OR MATRIX?**

We undergo this model to a training and the result is to compute the weights. At the beginning we don't know exactly what the filter is doing. The task/target of our model is the one that will compute optimally the values of the weights in order to perform as expected during the training.

Another aspect is the stride, in general it means a convolution in which we go to one pixel to the other and, repeat it... We might scan the overall image, and here we have a stride of 1 pixel by pixel.

![[Pasted image 20250926121448.png]]

Then we have another property called topology correspondence. Neurons in a specific region are correspondent to ... The output of the local region would depend on a specific region on the input...

![[Pasted image 20250926121627.png]]

From a technical pov, we might using zero-padding, just to increase the size of the input by just inserting zeroes simetrically. IN THIS CASE IS 2X2 zero-padding, 2 in the columns and 2 in the rows. What is the meaning of using it? In order to obtain an activation map in size identical to the input. 

Properly using zero-padding i might make my convolutional layer to perform only processing and not compression

![[Pasted image 20250926122019.png]]

This is a very simple relation depend on the size of the activation map w.r.t to the convolutional layer.

fx and fy are the number of filter elements in x and y direction $L$ stands for the stride and we might have different in different directions, z is... read the slide.

We set the parameters of the filter and in this sense we've defined the size of our convolutional layer

Example:

![[Pasted image 20250926122416.png]]
In this sense we're just performing processing and not compressing.

![[Pasted image 20250926122432.png]]
Mathematical conclusion: We've action potential it is the same as we did for a single neuron... All the outputs together of the convolutional layer are called activation map and they require an input. 

![[Pasted image 20250926124555.png]]

In terms of implementation, it is always 1D, no matter the size of the input.
*SIZE DOESN'T MATTER*

![[Pasted image 20250926124749.png]]

We might pack many features maps into one layer, meaning the input is entering to the first set of neurons, one feature map correspond to a set of neuron, another feature map, another activation map, and so on... We're expecting to increase the number of feature map to perform specific computation. One feature map might be performing low-pass, another high-pass, another high-pass at diff cut-off freq... etc, every feature map will extract from the input an specific set of characteristics according to its weights.

Convolutional layers, are called encoders networks, process an input, throughout different layers, each layer performs a convolution and each layer has its own feature map.

![[Pasted image 20250926125448.png]]

Another way to deal. My input is not a simple matrix but we might have different solutions depending on the RGB contribution. Each convolutional patter for the red, the green, the blue. By increasing the depth I'm extracting features relevant in each R, G, or B. We see in blue, we have 4 layers, each might impact different features map, we're compressing the size of the input, 

![[Pasted image 20250926125646.png]]

Ok, here, we have a convolutional layer in which we're processing in bundle the three layers, the RGB together, unlike before. One neuron is spanning the same regions of the diff 3 layers, for one neuron we'll have 25+25+25+1 = 76 parameters.

![[Pasted image 20250926125811.png]]

Second neuron convolution. I'm striding the filter, change the receptive field. Shared weights, same number of parameters and the same parameters, 75+1.

![[Pasted image 20250926125858.png]]

Look at this example :). We take the input, we simulate RGB, we perform zero-padding, and I have two feature maps, filter W0, filter W1. I'm in the first convolutional layer and it has embedded this two feature maps which are spanning all the three components RGB, their weights are the same. We see one matrix is for Red, another for green, and another for blue plane. 

In this example the activation is linear, no additional transform and applying the first feature map the output is 9. The result of the first convolution that is spanning these regions, the output is 9. Then, we need to move to another neuron

![[Pasted image 20250926130138.png]]

In this case we've set a stride of two, we see the difference from previously, and the output is 1. 

![[Pasted image 20250926130208.png]]

Then we get as output 3, 
and so on...
![[Pasted image 20250926130225.png]]

![[Pasted image 20250926130238.png]]
The result would be one activation map for first feature map and another activation map for the second feature map. Each feature map is corresponding activation maps (W1, W2), in this case according to the setting, I have a 5x5 planes and we end up with an image with a 3x3. We've performed processing and compression.

![[Pasted image 20250926130500.png]]

In general we might have other activation, a simple layer of RELU activation. The value of the pixel must be consistent, thus we avoid negative values of the pixel. The idea is to move layer by layer an image. Thus in this case all negative values would be set to 0.

After that we might pool the size of the output (compress) the image

![[Pasted image 20250926130744.png]]

Two main pooling processors, integrator and maximum. Considering the recepting field we're taking max or average value. 

The pooling layer has 4 neurons. Each receptive field of each neuron are 2by2.

We don't have to train this layer. 

![[Pasted image 20250926131052.png]]


I'm performing a certain task. a classification, we wanna do it with three dif labels corresponding to emotions. In general, the idea is to use a layer that should be able to provide probabilities/classification, and I would like it to the all of three sum-up 1. 

![[Pasted image 20250926131305.png]]

How to implement the output?
A probability that sum-ups 1. that is, with three neurons, we'll have an output that will compute the output potential.

In this case the neurons in the softmax are sharing information and exchanging them by computing some of the exp of the action potential and from the mathematical pov this allow to have the probability of each neuron that should sumup 1.

All of them must be positive. We can apply the delta rule by the traditional standard, we have the activation function and we might compute the error between output and label. This is a nice way to obtain straight forwards in the output a probability.



---
Here an example we don't have :)
***

The last layer bef processing is called bottom layer. it is softmax. In the training backpropagation...

Just to our info

![[Pasted image 20250926132829.png]]
How to apply backpropagation to complex CNN

also this
![[Pasted image 20250926132849.png]]


![[Pasted image 20250926132900.png]]

We see that we're putting layer by layer the sizes. and also we can reconstruct the number of overall weights which are going to be trained.

This is the final syntentic representation.

==REVISE THIS MODEL, TRY TO UNDERSTAND THE SPECIFIC SIZES LAYER BY LAYER== 


![[Pasted image 20250926133026.png]]

In this case we have a set of slices instead of a single image, and we have an input with image and number of slices. The filter is no longer 2D but 3D.

Now the receptive field is a small parallelepipedal region.

![[Pasted image 20250926133240.png]]

I can compute the size of the feature map and according to the setup of the filter i would conclude that our feature map would correspond to 31, 31, 4. 
That is the spatial structure of this feature.

![[Pasted image 20250926133326.png]]

I'll handling n different feature maps. 31 x 31 x4  are 3844 neurons, x n cos we have n feature maps.

31x31x4xn

and we have that 51xn is the number of weights. Every feature map has 51 weights, so, 5x5x2+ 1...

![[Pasted image 20250926133449.png]]

What's the difference now? We've considering the first feature map in the second layer, I'm considering one neuron and that neuron is spanning all of the feature maps! In this case I'm setting a filter 3x3x2 and that is the result. 
![[Pasted image 20250926133546.png]]

The structure of the neuron of the first feature map of the second layer has 450 neurons. 

In the second we'll have more feature maps, we've showed just one but we can have many, and each neuron in one feature map is taken random has the same topologically receptive field. 


Now,
![[Pasted image 20250926133624.png]]
Moving from fully connection to convolutional connection based on a receptive field. We're reducing a lot the number of parameters, and we're gaining some sort of explainability of how the layer is working, we call it filtering, layer is doing processing but we don't know what exactly is doing. 













