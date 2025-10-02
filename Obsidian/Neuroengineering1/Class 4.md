25/09/2025

Exercise:

![[Pasted image 20250925083406.png]]

![[Pasted image 20250925083438.png]]

The devoted application is Regression...

![[Pasted image 20250925084235.png]]

![[Pasted image 20250925084254.png]]

Remember, negative weights are inhibitory effect and positive weights are excitatory effect

b11 is negative, the rest of them are not in the output, thus a11 and a22 wouldn't apply to produce inhibitory effects.

![[Pasted image 20250925084604.png]]

Let's consider as inputs
$P_1 = [0.8, 0.4]$ $P_2 = [0.8, -0.4]$ $P_3 = [ 5, -5]$

and the weights

$a_{11} = -0.0111$, $a_{12}= 0.1107$ $a_{21} = 0.1109$, $a_{22}=-0.0118$
$b_{11} = 8.7810$, $b_{12}= 8.7236$ $a_{21} = 5.3216$, $a_{22}=-5.2725$

Now the output of the network 
Of the first layer with the hyperbolic tangent
$$
P_{1}^{H}= a_{11}x_{1}+a_{12}x_{2}+(-1)\cdot0
$$
$$
P_{2}^{H}= a_{21}x_{2}+a_{22}x_{2}+(-1)\cdot0
$$
thus
$$
y_1=tanh(P_1^H), y_2=tanh(P_2^H)
$$
$$
y_1 = 0.0354, y_2 = 0.0840
$$
Now, the outputs for $P_1 = [0.8, 0.4]$, (input 1)

$$
u_1 = f(b_{11}y_1+b_{12}y_2) = 0.42085
$$
$$
u_2 = f(b_{21}y_1+b_{22}y_2) = 0.63016
$$
Now, the other two combination for $P_2 = [0.8, -0.4]$ (for input 2)

$$
u_1 = -0.42085
$$
$$
u_2 = -0.63016
$$
And for the last/third pattern for input pattern 3 $P_3 = [ 5, -5]$

$$
u_1 = 9.5433
$$
$$
u_2 = -0.0010003
$$

We see that the network is computing the differences and the averages at the output of the inputs 

![[Pasted image 20250925090100.png]]

![[Pasted image 20250925090248.png]]

Bef the network was calibrated between $[5,-5]$ for both inputs, now we would like to widens the range of input patterns and see what happens

$$
E_{FS}= \frac {|U_{expected} - U_{measured}|}{FS}$$
==We see that the network is computing the differences and the averages at the output of the inputs==
Thus,
$$U_{expected_1} = X_1-X_2$$
$$U_{expected_2} = \frac{X_1+X_2}{2}$$
For pattern 1. $P_1 = [0.8, 0.4]$,
$$
E_{FS}= \frac {|U_{expected} - U_{measured}|}{20}$$

$$
E_{FS}= \frac {|U_{expected} - U_{measured}|}{20} \cdot 100$$
We obtain 
$$
E_1 = 0.10\%, E_2=0.15\%
$$

For pattern 2. $P_2 = [0.8, -0.4]$

We obtain 
$$
E_1 = 0.40\%, E_2=0.41\%
$$

For pattern 3.  $P_3 = [ 5, -5]$

$$
E_1 = 2.28\%, E_2=0.05\%
$$
The more we go outside on the range, the more increases the error difference 


![[Pasted image 20250925091147.png]]

Now, we consider 

For the first case $P_1= [-5.5,5.5]$ the output of the full scale error is $3.6 \%, 0.05\%$
We move to a larger range cos the error is below 5%, and now we take, and realize that we achieve greater than 5. If the idea is to scan 5% this would be the way to get an error lower and greater than 5, thus we can infer after this we shouldn't move on
For the second case $P_2 = [-6, 6]$ the output of the full scale error is $5.26\%, 0.06\%$

We consider the difference a more critical behavior in the training cos it's easier for it to go out of the range, unlike the average (u2)

![[Pasted image 20250925091845.png]]


Now, we use the delta rule. 

$$
\Delta W = |U_{expected} - U_{measured}|\cdot f'(P)\cdot x_j
$$
$$
\Delta b_{12}= |U_{expected_1} - U_{measured_1}|\cdot 1\cdot y_2
$$
We have the expected values (labels) cos we stablished the ideal behavior
$$
\Delta b_{12}= |U_{expected_1} - U_{measured_1}|\cdot 1\cdot y_2=0.25 
$$
We don't know the reference for the output of the hidden layer. However, by using back propagation we get.



![[Pasted image 20250925093017.png]]
$$
(y_{expected}-y_j)=\sum_{i=1}^N((t_i-u_i)f'(P_i^o)w_{ij})
$$
Then
$$
\Delta a_{12}=\sum_{i=1}^2((u_{expected_1}-u_1)\cdot 1\cdot b_{i1})\cdot C^1(P_1^H)\cdot x_2
$$
output is going to be 13.94

Doing $\Delta a12$, means we're focusing in the neuron H1 and the input $x_2$

# <span style="color:rgb(223, 109, 109)">Deep Learning</span> 

Strategies that put in place diff architectures to address complexity, stability of the training using an autoencoder process to train. :)

![[Pasted image 20250925094309.png]]

Ability to extract relevant characteristics of an input. This case the main char is the face/emotion. Network is processing the image and in the end of its processing it'll provide somehow an encoding of emotions.

![[Pasted image 20250925094451.png]]
Set of visual characteristics to interpret the emotion. We're able to identify the emotion by these characteristics (From physiological pov, our brain performs the processing of the image). 

*Raw data $\rightarrow$ features* is called encoding. Extracting/Compressing to just relevant data to the aim of our task. 

![[Pasted image 20250925094747.png]]

It is only necessary to extract some specific features of the image to identify or encode the image to the aim of our task, to a very few number of pixels by means of some sort of space mapping. 

![[Pasted image 20250925094940.png]]

In order to do this extraction of principal features we have to perform some processing. Extract lines, identify geometries, set of curvilinear lines which batch together... There are many processing steps that goes from the raw data to more complex representations understandable for the model. In this case the task is to attribute a semantics to what I've seen. 

![[Pasted image 20250925095150.png]]

Primary visual cortex is composed by neurons they're structured in specific ways, in general the information is stored there where ready underwent some processing. We have the lateral geniculate nucleus to perform some processing, each area perform specific task.

For example 

Area V1 is detector mapper, images we scan out are represented by lines, in each pixel i'm detecting lines.

progressive aggregations are added in the path...

Each neuron has its own receptive field. They're not acting in the overall input but they're each selected. 

![[Pasted image 20250925095829.png]]


How complex is the encoding between the retina and the visual cortex.

![[Pasted image 20250925095931.png]]

LGN is some sort of edge detector. It is complementing two regions in the same point of the retina if at any point there is a change on the contrast. There are specific local fields in the LGN that are able to detect. This configuration is then mapped...
![[Pasted image 20250925100110.png]]

Convolution is the mathematical operation. Depending on the values of the filter we obtain different results. 
