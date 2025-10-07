
06/10/2025
***
![[Pasted image 20251006123555.png]]

![[Pasted image 20251006123609.png]]
Generative process: ability of generate date and new data. Invented data, smt that is pretty close to human imagination. We´re able to guess something that is real, but also, we can guess that is not real.

For the generative process, these two conditions are not different (differentiate of imagining real and unreal stuff) they don´t differ in realistic and imagination stuff. The model considers it as the same. 

We start from a low dimensional encoding, and then we have some simplified stuff like a binary network, and starting from it generates a more complex information -> tensor, multidimensional network. This case is binary -> binary but at the output we could have a real value, floating, integer, whatever...

What is doing a generative process? Doing two basic processes: to upsample the input (interpolation, means putting some data in your signal and try to increase the size of the signal), but also another process is introduce information, a smart interpolator (lineal interpolator,etc.). So, it is basically doing some sort of interpolation, using a model in the domain of deep learning. An interpolation/upsampling will be done in the processes of deep learning domain.

In the encoding space we have neurons that can perform processing: convolution, filtering (same as autoencoder with fully connected architecture, same concept). ==Basically the generative process is implementing reconstruction filters!==

The generative process might have a model, not in the deep learning domain (a gaussian function), and we´d extracting new data extracted from the gaussian. We´ll see some processes inside of the blue-box.

In the deep learning domain we might split in many steps this transformation between input and output, many layers, in encoding we´d speaking of convolution, in decoding is deconvolution, which in deep learning would be the way of performing interpolation

![[Pasted image 20251006124311.png]]
I have a data defined in specific domain/size, and we would like to move it from small domain to larger domain. We´d take the information and let the upsampled data deal with the same information but add some more information. You know when we´re interpolating, we´re inserting data according to the model, we´d do this with a linear model/bilinear model, or bilinear plane in x, and y, we´re actually inventing new data according to the model.

In deep learning we don´t know what the model is, and we´re exploiting the power of the deconvolutional operator...
![[Pasted image 20251006124622.png]]


I might start with a small image and move towards a large one, but if I move to this transformation in the limit, iĺl insure that the input is not longer an image that is an encoder which is not longer intuitive. This is the way we upsampling the image.

Here we starting with a vector/latent space, and we´re processing this by an encoder. Then we change the encoding, taking the same decoder and we end up into a realization understandable. If I have defined a latent space I might have some attributes in this case we have 6 elements in this vector, so, we have 2^6 different realizations. I´ll 64 encoding at the input and most likely the same 64 at output.

Iḿ increasing the size of the encoding pattern, this means that my representation is becoming more and more complex, and it´d no long 64 pattern but thousands...




![[Pasted image 20251006125207.png]]
Moving in a generative process in deep learning we´re not computing the transform between input-output in just one shot but in many shots. Especially, when we´re encoding a low dimensionality w.r.t output, my upsampling is better implemented if we´re moving from one smaller size to another one not that large, bigger but not huge! It is nice to move not that much from layer to layer in upsampling size.

The concept of convolution in encoding network has a correspondence in the decoding network throughout this is the deconvolution (transprosed convolution). As we´re using neuron architecture, we have again as many neurons in the layers as needed, the wiring depends of the architecture, if CONVOLUTIONAL, we´ll have convolutional wiring. However, we could also have fully-connection, we could also speak about deconvolution but the implementation wouldn´t be transposed deconvolution but another stuff. SO, transposed convolution is only for CN.

example
![[Pasted image 20251006125623.png]]

I have a 4x4 image. And I Have a 3x3 filter.

I have a convolutional layer, 1 feature mapping that is identified by this filter. I have some parameters that define the implementation of the convolutional filter.

![[Pasted image 20251006125721.png]]

I´m just convolving, setting the filter, striding, and we have in the output the last 2x2 according to the parameters of the filter.. THe filter is then doing processing and compressing data.

![[Pasted image 20251006125827.png]]

NOw, backwards, starting from an input, exactly our previous output. We´d would like to now apply a convolutional filter which is exactly the same as the previous convolution, but now the difference is that we´re applying a larger size filter than the input, and we´d apply now de-convolution -> upsampling data with this filter.

The process is now a pixel-wise multiplication. We might compute an output image and the size of the output image is defined by the filter. The output is 4by4, we take the first number 8, and compute the pixel wise multiplication. (8x-1)= - 8, (8x1)= 8...

Then we do the same with the next element of the input and do the pixel-wise multiplication...And for each input i´ll have a realization. I´m applying deconvolution, and I´m having padding, striding =1, an zero-padding, it would corresponds to set some zero around the input, in this case we don´t need any and to finish:

![[Pasted image 20251006130324.png]]

The output is the sum of the four realizations. This is exactly how a 2D convolution works and we´re gonna see how this performs as a some sort of transposed convolution. Try to make a relation between math standard convolution we´re familiar with and this one, in which we start with an smaller size input with a deconvolutional filter and get as output something with larger size than input. it is indeed an up-sampling process, and if our filter is smart enough we might even invented this data with criteria. 

Who sets up the filter? ...

What is the receptive field of the first neuron, that having -8 as an output. each neuron has 1 pixel as receptive field.

Is it a convolutional wiring? I have a local receptive field and I understood that in each case each neuron shares the same weights (the same filter), then it is!

![[Pasted image 20251006130909.png]]
Taking this representation. I´m in a standard convolutional process. INput, filter, etc. 

We have some sort of matrix representation of the filter that is computed according to the input and then doing matrix computation to do flattening and then obtaining the output, in all just one matrix computation we´ve perform all of the convolutional processes, this is how algorithms implements convolutional processes. They arrange the matrix and do the multiplication. it is not one by one process, they optimize it :)

![[Pasted image 20251006131111.png]]

ANd for deconvolution, we take the matrix, compute the transpose, take the filter and do the matrix computation, obtaining the output. 

So, there is a matrix computation and we´re implementing an optimized convolution, computing that matrix, making the transposed, and we´ve implemented a deconvolution or transposed deconvolution cos we´re taking the transposed of the convolutional matrix. 

Tensorflow and pytorch implement this

Who is computing the weights of the deconvolutional filter? for the convolutional is the training, we might used a supervised training if we´re dealing with labelled task like classification or using autoencoders again we know that filters learn during training and now for sure that the same, when we´re dealing with an encoder , and attach at the bottom net we train the overall model to optimize the filter data, so the weights of the filters layer according to the task.

If we´re dealing with a convolutional network, I have to train the overall network:
Encode and decode in the same time, in bundle, in standard convolutional model.


![[Pasted image 20251006131252.png]]

The two operations and completly different, convolution and deconvolution. 

![[Pasted image 20251006114828.png]]

So, we have the standard deconvolution and fractional strided convolution. There are not substantial differences in terms of performance. The idea is to put zero padding in between pixels.
![[Pasted image 20251006114932.png]]

Deconvolution network is structured like this.

We start from a encoding. If we´re moving to a final dimension we do it by doubling the size layer by layer. From implementation pov 2 is a nice and happy number :). 

![[Pasted image 20251006115103.png]]

Recall we were using more than 1 feature map. So, that´s what we´re seeing here. We have the same layers, the same amount of feature maps, we have the same weights, etc...

You have an input, an encoding-decoding, and decoding is defined a decoding path, bottleneck is the final stage of encoding and then we start decoding. The output will depend on the task, if we´re gonna solve some sort of binary problem, a regression but binary problem we´ll have neurons with step function. But if the output is some floating number, we have linear neurons (image), or if a segmentation problem, which means to deal with an input and identify regions that belongs to one or other class, we might use in this case as a classification with softmax. 

![[Pasted image 20251006115546.png]]
In this example we´ve introduced the connection between the encoder and decoder. Look at the arrow, and see how the output of the yellow layer is glued to the blue layer on the right and then these two layers belong to the same receptive field. So, if we have a neuron in the purple, itĺl span both layers and the encoding and the decoder layer would be concatenated. It is a many standard operation for 1D,2D,3D, signals. Since the structure is symmetric we can easily concadenated each layer on one side (in yellow) with the others in blue. 

In this way the decoding layers have a receptive field including the encoding layers. Should we make all connections? Principally the first one, because it is the one that brings with it the most amount of information. 

![[Pasted image 20251006121057.png]]

At the beginning I´ve stablish this architecture, and afterwards this receptive field have being clarified and properly defined. I have a receptive field spanning many layers, if I´m in 3D I might have a tensor relations in terms of weights. 

![[Pasted image 20251006121214.png]]

Just to clarify the rol of the skip connection. To help the up-sampling, it has the role of helping and supporting properly the up-sampling.

![[Pasted image 20251006121310.png]]

THis is called the U-NET, If we concatenate all layers in encode and decoder.

THe purple shaping the output is just the last layer of the network that is depending on the specific task we have. 

![[Pasted image 20251006121419.png]]

This is a CT that identifies a segmentation problem. femur and tibia, we use as input 1000 scans and I have in this dataset the corresponding segmented images provided by surgeons or radiological experts.

I might apply supervised learning in a regression task, in this case segmentation is a regression. I´d use a U-NET, a 3D. 

![[Pasted image 20251006121603.png]]

This is the architecture

The front end provides an output that is equal to the image to the spatial image, i commpresses by 2, and to the next, and up to the bottleneck is 64 feature maps into the convolutional layer, that is how to read the architecture, then as you might say, the blue is the deconvolution, it upsamples, after the deconvolution we might further apply convolution blocks (the green ones), three times, 32 first is deconvolution, then the output is the convolved into 32 feature maps and then the output is convolved into 32 feature maps.

NExt layer, deconvolution-upsampling, and then two convolutions. As I approach the bottle neck I scale down the spatial dimention but I inrcease the number of features, the opposite when I´m decoding the information, it increases the size of the data and decreasing the number of features..

![[Pasted image 20251006121941.png]]

In this case, how many volumes I´m classifying? three, femur, tibia, background, and these three neurons would belong to a single softmax, a 3D structure that represents the 2D scan of the CT.

We have no longer a pixel but a voxel, this point in space is represented as 3 neurons that belongs to a softmax

![[Pasted image 20251006122254.png]]

The three are linked together into a single soft-max. 100x100x100 voxel, then iĺl have 100x100x100 softmax in the output.


![[Pasted image 20251006122338.png]]
And example. 

![[Pasted image 20251006122759.png]]

We see in the first layer of encoding we have the first feature map, and we have the activation of one slice and iḿ computing the activation map of the first feature map and of the second feature map, and see theyŕe different. left layer1 feature map might be a bit better than right one in terms of contrast.  

THen we move to second layer and we also have these activation maps and we see it is identifying connected structures, or shapes.
![[Pasted image 20251006123001.png]]

In the third layer, the info is difficult to interpret, it is pretty small, we could expect to do some shape clustering, we´re not sure tho

![[Pasted image 20251006123038.png]]

Decoder performs some kind of semantics separation, tibia, fibula, in the semantics interpretation it is called on/off semantics

![[Pasted image 20251006123232.png]]

BAckground neutralization. Sparing the tibia, it is cancelling all the information but the femur. 
![[Pasted image 20251006123259.png]]

ANother semantic approach is called adversarial mapping, you have in this case layer 3 of the decoding feature map 7, you have the image that has cancelled out all the info but the femur. In this case, same feature map, another slide that has removed everything. Probably this feature map is really encoding something just related to the femur, it is truly semantic feature map in the decoding layer, it is recognizing he femur and all other regions are removed, and it also goes for the other feature map, 1/8, it is recognizing all the tibia and removing all the rest.

![[Pasted image 20251006123442.png]]

Some sort of conclusion.
We have a powerful tool to solve complex problems in some sort of automatic process. Segmentation was pretty difficult to solve, nowadays this is the simplest one, the U-NET is pretty trivial, there are now more complex systems that perform for sure better than this one but this is the core :)

COre: encoder that extract relevant features and a decoder that reconstruct that information.

If youŕe training an encoder-decoder network for one especific task. You´re training the network for extracting some stuff, but also you´ll be doing it not only for the encoder but the decoder, it has optimized the weights. That´s why we´ve trained the overall network, meaning that if I´ve changed the task, for sure the decoding part will be different, but also the encoding part. 

If I wanna have an decoder non dependent on the task, I shouldn´t use the train of the overall structure, but just train the encoder, freeze the weights and then just train the decoder. SO, i get a encoder good to extract features and a decoder tailored for a task.

![[Pasted image 20251006123853.png]]




