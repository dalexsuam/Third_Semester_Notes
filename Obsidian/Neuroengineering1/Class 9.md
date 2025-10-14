13/10/2025

![[Pasted image 20251013103035.png]]

This is a very trivial example in which we're dealing with data composed of a matrix of 2by2 elements to give high level semantic correspondence, we would like to represent pencils, some are bended w.r.t the vertical. A high dark value is proper encoding and white is less relevant encoding. You might see in the pixels all diagonal representation, and w.r.t we are going to a quantitative representation.

![[Pasted image 20251013103436.png]]

Conversely, if our info is not properly spread over the diagonal, we might consider it not useful data. that is, noise, this kind of realization of data is noise, and from the graphical pov we have no longer information spread across the diagonal.

![[Pasted image 20251013103530.png]]
From quantitative pov, I'm encoding my scale into numbers, it ranges from 0 to 1, 0 white, 1 black, but it is assumption. For encoding properly pencils, we have more darker values in the diagonals, that is, bottom right, top left. In this case I have a simplified quantification, enabling decimal values, not only 0 and 1.

![[Pasted image 20251013103658.png]]


We would like to build our discriminator which would be able to say we have true data on left, and right as false data/ noise, and I expect the discrimination would label both.

In this case we know what to expect in terms of true and false data. So, I just compute the action potential, we have the inputs and weights. And for the left one we get an output of 2, and for right it is -0.5.

The idea is that the realistic/true data has a positive output and negative one is for false output.

![[Pasted image 20251013103938.png]]
And this is the graphical representation of the discriminator. We have forward neurons processing one input into the pattern. 

In this case we also have a bias for the output neuron, and we have a sigmoidal, a logistic activation for the neuron and the result is 0.73. 


![[Pasted image 20251013104046.png]]
Then we change for the noise as input pattern, the same architecture, the neuron of the discriminator is now putting 0.37. 

If you recall I might use a logistic function having 0.5 as separation threshold to provide the binary classification. All output greater than 0.5 will be 1, and lower than 0.5 will be attribute is as class 0.

This is a binary classificator.

If the discriminator at the beginning is properly setup we'd be able to do this, and get something that is representing the real data if there is real data pattern and the opposite if there is any noise appearance. 

I both cases I have a generator producing this data.


![[Pasted image 20251013104406.png]]
How to build the generator? We have to span a latent space, we have a variable that might range in this case between 0 and 1. And here we use a continuous encoding, a binary encoding, using a vector or a continuous representation. Our z is going from 0 up to 1.

The assumption is that i'm picking randomly one element from the z latent space.

The generator, you might see is a sort of front-line layer that is composed of just 1 neuron, and this neuron is some sort of virtual neuron gain that represents in this case the span between 0 and 1, and its output is becoming the input of four output neurons, and each neuron in the output layer will correspond to an element into the data pattern. 

According to this weight setup, we're assuming that probably we've already trained it. We just need to consider properly the weights. Recall we need to increase the contributions of the diagonal and compress the contribution of the opposite diagonal to get the real data...

And according to the logistic we get this four values that should be classified as a true data

![[Pasted image 20251013104817.png]]
We'll see that depending on the label and prediction also taking the log-loss error function we might face a large or small error. 

![[Pasted image 20251013105040.png]]

What if my expected label is 0? We have a different condition given by this error function. which depends now of the -ln(1-prediction) and we'll be dealing with the same but opposite case. 
![[Pasted image 20251013105224.png]]
Why is it useful to consider that the expectation is 1, consider -ln(x). If i'm approaching the prediction towards 0, the corresponding error will be large. When prediction is coming close to 1, we're getting a lower error. 

In my training system i'll use this loss function to deal with the error of the prediction that will correspond to label 1. 
![[Pasted image 20251013105349.png]]
If I wanna deal with label 0, I have to move to -ln(1-prediction). The closer it is from 0, the smaller the error. In contrast, if the prediction moves to 1, the error is larger.

That is why we need two error losses functions, to deal two different conditions

So.

![[Pasted image 20251013105506.png]]
Mixing up the generator and discriminator. I sample my data space, and the generator will produce an output, and this will approach either a true or false data, this might happen at the initialization of the weights, during the training, having into account the two loss functions, we might constrain the generator step by step to map all the range of the z data space to produce only true data. 

We call this the tranining set and we wanna learn the statistics of the training set which is learn in the generator. 

![[Pasted image 20251013105751.png]]

In this case I pick one z value, idk how the weights are, they're randomly generated.
After that

![[Pasted image 20251013105856.png]]

we take the random generated data and ask the discriminator to classify it. 

As we move to the training we expect to the generated data given to the discriminator be more realistic and biased far away from 0, in case of generating data. In the meantime we're just extracting data from the dataset. 

![[Pasted image 20251013110051.png]]

This is a fake 0, the discriminator should produce 0. But it is actually producing a value larger than 0.5 due to the logistic function. In this case, the discriminator is classifying a wrong data as true data, this means that also the discriminator is not properly trained. The generator and discriminator are two networks which need to be initialized and be trained at the beginning. Since the expected output is 0, thus it is comitting large error, and we have to use as loss function the -ln(1-...)

But, what is doing the generator? It is trying to improve, and it is expecting to produce a realistic data, so, it is expecting to a true data, thus an error loss of -ln(..)

We have then in the same training one error function which aims label 0 and the other which aims label 1. then, they're in contrast, and recall there is a general criterum that will allow us to stop in the middle cos one is push the weights on one direction and the other is going to do the opposite, and that is why we have this training called adversarial training, cos two loss functions.


![[Pasted image 20251013111242.png]]

From math pov. 
We see the nash equiibrium, which  $+E_{z~p_z}ln(1-D...)$ which is continuing to classify the data as label 0. 

Take into account we have a data set, if i'm picking 1000 elements, for balacing data during the training about 1000 in z. Because when the discriminator is getting x for true data is getting label 1, that is why you're mixing up both error functions and in order to avoid unbalance.

I'm picking 1000 elements randomly in z, and if I continue picking z, i might pick already considered data, so i'm oversampling z w.r.t training set. 

![[Pasted image 20251013111700.png]]


![[Pasted image 20251013112411.png]]

If I pick one data from training set it is take from the discriminator and it'll evaluate and this evaluation is always 1. On the other side i'm picking one element in the latent space, z, i'm aplying to z the generator and the generator is producing an output and it is going as input to the discriminator and you might see there are two opposite attemps, one is trying to put the result to 0 and the disriminator is trying to modify its weights to provide the opposite, so the discriminator is fulled and produce more or less towards 1 data in a syntethic way.

![[Pasted image 20251013112553.png]]

Here you might see, the overal loss function split in the two step, in terms of implementation again we might apply a gradient base optimization cos we have outputs, we've learnt how to represent gradients w.r.t weights and have no issue and we can easily map this representative function into two mathematic functions, cos we know exactly how many layers are and neurons for each and thus the activaiton functions...


and we might consider that two cost functions are evaluating and considering one epoch in our training, we might evaluated the ascent update the weights, evaluate the gradient descent and update weights, next epoch, the same procedure, this is how the training develops, and you recall in the beginning we say we have 0, and 1, and the discrminator might try to separa true data and syntehthic data, but if we setup properly, we might move to 0,5 and this is the overall probability of the discriminator. A good property of the generator is that the discriminator will have a true data at 0,5. in that moment we gotta stop the training, 

![[Pasted image 20251013112949.png]]

This is the final architecture of the training...
This structure enables all the generative models to learn including chatgpt. all language models start with an architecture like this. 

![[Pasted image 20251013113035.png]]

This a representation implemented in the beginning to move in the optimization of the gradient ascent moved to a minimization. 

If I consider this loss function, we have a very small gradient, and this is a consequence the learning is delayed a lot, we need a lot of epochs to travel and to make the gradient increase and that is why we might...
![[Pasted image 20251013113642.png]]

Instead of maximizing this function, we minimize the other function but this is just a trick related to computational level. In this way at the beginning we are more close to the 0 in x and the gradient would allows to move to the min region quicker, and if we consider the blue maximize is sloow.

![[Pasted image 20251013113804.png]]

In terms of implementation, one epoch covers one step in discriminator and generator. 

There were many attempts to optimize this trade-off implementation. 

Basically, we led the discriminator go faster w.r.t the generator, so the discriminator start to create the right classification condition, it is learning quicker than the generator. But after a while, as soon as the generator starts learning, the separation that at the beginning is ok in the discrminator cos allows to understand what is true or false, that goes ~0.5, it starts decreasing in the opposite direction.

We are just improving or learning the weights of the discriminator without touching the parameters of the generator. 

100- discriminator -1 generator - 100 discriminator - 1 generator. It is sort of technicality otherwise the discriminator is not able to learn the diff between true or false. 

![[Pasted image 20251013114249.png]]

![[Pasted image 20251013114338.png]]


![[Pasted image 20251013114632.png]]

I'm encoding the left one, getting the latent space and using it for the generator. So, the generator is encoding-decoding network in this case. 

![[Pasted image 20251013114718.png]]

I have a generator that is mapping a CBCT-> CT (top-mid), in the realm of generative adversarial network, we implement a training that is making a discriminator that learns the diff between the synthethic from a original. 

So, if we put this archiqtecture into a cycle, we have the original ct and i'm training a generator moving from a real CT to a syntehthic CBCT and goes to another discriminator and this nework is all in bundle. The left has he same math for training as right. then, we take a syntehthic CT, and i'm feedin it to the generator F and producing a cyclic CBCT and it should be similar to the original CBCT, so, we have an additional loss function which is some kind of square error, and we have the same cycle on the other side, we have two traditional loss functions which minimize traditional square errors which are inside of the training of these adversarial couple of discriminator-generators. 

If everything goes well and converge is achieved, we have now to mix togethter the ~0.5 in both discriminators, in both adversarial trainings. two values to monitor, but also in the mean time the square error, and also need to set some sort of threshold to set a nice similarity. 

![[Pasted image 20251013115305.png]]

We might apply same architecture to another approach, and we can denoise a photopletystogram signal taking on the chest taking the reference of the photopletystogram read from the finder (There should be some signals in the blank squared) At the end of this training we''re just having generator G, retaining it, the rest we can just get rid of them. The idea is that we're taking in this case a very noisy chest signal and clean it up by means of the information that the generator has learnt looking from a clean signal from the finger. 

![[Pasted image 20251013115449.png]]

The original idea of generative adversarial network was to capture the underlined statistics considering a bunch of data. In the data there are numbers using statistics algorithms, when data is becoming complex traditional statistics are no longer useful that is why neural networks are a good approach to learn those complex statistics, we don't know what statistics but that statistics is drawn into the weights. 

But, the training is not very easy to control, if we're dealing with just one simple generative networks, we might get the ~0.5 between real and syntethic for the discriminative, but more complex architectures are a mess...



