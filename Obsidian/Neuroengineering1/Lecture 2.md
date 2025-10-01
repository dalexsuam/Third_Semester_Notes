
***
Date: 19/09/2025

Last time we were interested to implement in modeling a traditional analytical function using a network for regression. The following is an explanation for this.

# <span style="color:rgb(223, 109, 109)">Network for Perform Regression</span>

![[Pasted image 20250922222516.png]]

This diagram depicts a **feedforward neural network** designed for a **regression** task. The goal is to predict a continuous, unbounded value.

In regression tasks, the **output can take any real value**, i.e. it is **unbounded**. For this reason, the **output neuron uses a linear activation function**. This ensures that the network can produce values in the whole range $(-\infty, +\infty)$.
    
The **hidden layer**, however, introduces **non-linearity**. In this example, it has **two neurons**, both with **tanh activation functions**.

## <span style="color:rgb(239, 179, 1)">Network Architecture</span> 

This is a **two-layer network**:
- **Input Layer:** 2 nodes ($X_1$​, $X_2$​).
- **Hidden Layer:** 2 neurons with the **tanh** activation function.
- **Output Layer:** 1 neuron with a **linear** activation function.

## <span style="color:rgb(239, 179, 1)">Role of Activation Functions</span> 

- **Hidden Layer (`tanh`):** This non-linear function allows the network to learn complex relationships. It squashes values to the range $(−1,1)$.
$$
tanh(z) = \frac {e^{z}-e^{-z}}{e^{z}+e^{-z}}
$$
- **Output Layer (`Lin` - Linear):** Used for regression to produce unbounded outputs ($-\infty, +\infty$). It performs a simple linear transformation.
    $$
    Lin(z) = z
    $$
## <span style="color:rgb(239, 179, 1)">Mathematical Formulation</span> 

The output $u$ is calculated in two steps:

<span style="font-weight:bold; color:rgb(161, 40, 226)">Step 1:</span> Calculate the outputs of the hidden neurons, $y_1$ and $y_2$

Each neuron computes a weighted sum of its inputs, adds a bias term, and passes the result through the **tanh** function.
$$
y_1=tanh⁡(w_{1,1}x_1+w_{1,2}x_2−T_1)
$$
$$
y_2=tanh⁡(w_{2,1}x_1+w_{2,2}x_2−T_2)
$$

<span style="font-weight:bold; color:rgb(161, 40, 226)">Step 2:</span> Calculate the final network output, $u$

The output neuron takes $y_1$​ and $y_2$​ as inputs, computes their weighted sum, adds a bias term $T_3$, and applies the **linear** activation.

$$
u=v_1y_1+v_2y_2-T_3
$$
**Where:**
- $w_{i,j}$: Weights from input $j$ to hidden neuron $i$.
- $T_1,T_2$​: Bias terms for the hidden neurons.
- $v_1,v_2$​: Weights from the hidden neurons to the output neuron.
- $T_3$​: Bias term for the output neuron.


# <span style="color:rgb(223, 109, 109)">Activation Functions f</span>

## <span style="color:rgb(239, 179, 1)">Sigmoidal Activation Function</span> 

![[Pasted image 20250922230316.png]]

The **sigmoid function** (in particular, the logistic sigmoid or _logsig_) is one of the most common activation functions used in neural networks. Its output is always between **0 and 1**, which makes it especially useful when we want to interpret the result as a **probability**.

The function is defined as:
$$
u=\frac{1}{1+e−^{(P−T)}}​
$$
where the net input $P$ is a weighted sum of the inputs, $T$ is the **threshold** (or bias):

$P=\sum_{i}w_{i}x_{i}$

For a single input $x$, this simplifies to $P=wx$

### <span style="color:rgb(161, 40, 226)">Key properties</span> 

| Sensitivity                                                                                                                                                                                                                                                                                             | Saturation and Vanishing gradient problem                                                                                                                                                                                                                                                                                     | Initialization                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The output reacts strongly to input changes when $P \approx T$.<br>    <br>In this central region, the function looks almost **linear**.<br>    <br>At the extremes (very large or very small $P−T$), the output is close to **0 or 1** and barely changes $\rightarrow$ this is called **saturation**. | When the neuron is saturated, the slope (derivative) of the sigmoid is very small.<br>    <br>This means weight updates during training become tiny $\rightarrow$ learning slows down or even stops.<br>    <br>This is one of the main reasons why deep networks can struggle with the sigmoid (vanishing gradient problem). | If the starting weights and bias make most inputs land in the saturated zone, the neuron won’t learn much.<br>    <br>==To avoid this, weights are usually initialized so that most inputs fall in the sensitive middle region of the sigmoid.== |
### <span style="color:rgb(161, 40, 226)">Tuning the Shape: Role of W and T</span> 
- **Weight $W$:** controls how steep the curve is.
    - Larger $W \rightarrow$ sharper transition, more like a **step function**.
    - Smaller $W \rightarrow$ smoother transition, behaves almost like a **linear function** over a wide range.
    
- **Threshold $T$:** shifts the curve left or right.
    
    - Increasing $T \rightarrow$ curve shifts right, requires larger input to “activate” (reach 0.5).    
    - Decreasing $T \rightarrow$ curve shifts left, neuron activates with smaller inputs.


## <span style="color:rgb(239, 179, 1)">Hyperbolic Tangent</span> 

The output is bounded between -1 and 1. ==It is usually preferred for hidden layers over the logistic function because its output is zero-centered, which often helps models learn faster.==
$$
u=tanh(P−T)=\frac{e^{(P−T)}+e^{−(P−T)}}{e^{(P−T)}−e^−{(P−T)}}​
$$

![[Pasted image 20250922231847.png]]
When visualized, a neuron with a sigmoidal activation function can be thought of as a smooth surface over the input space:

| Neuron                               | Surface Representation               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250922231951.png]] | ![[Pasted image 20250922232001.png]] |
- The **base plane** corresponds to the input variables ($X_1, X_2$​).
- The **vertical axis** corresponds to the neuron output ($u$). 
- The resulting surface illustrates how the output changes depending on the combination of inputs and the neuron parameters.

For a single neuron with two inputs:

$P = w_1 x_1 + w_2 x_2$

and for a **tanh neuron**, the output is:
$$
u = \tanh(w_1 x_1 + w_2 x_2 - T)
$$
- The **weights** $(w_1, w_2)$ define the slope and orientation of the sigmoidal surface in the input space.
- The **threshold** $T$ shifts the surface horizontally, changing the input values at which the neuron activates.

### <span style="font-weight:bold; color:rgb(161, 40, 226)">Comparison: LogSig vs Tanh</span>

| Feature             | Logistic Sigmoid (LogSig)                                              | Hyperbolic Tangent (Tanh)                                     |
| ------------------- | ---------------------------------------------------------------------- | ------------------------------------------------------------- |
| **Range**           | $0 \leq u \leq 1$                                                      | $-1 \leq u \leq 1$                                            |
| **Centering**       | Output centered at 0.5                                                 | Output centered at 0                                          |
| **Interpretation**  | Natural fit for probabilities (binary outputs)                         | Better for hidden layers (zero-centered accelerates learning) |
| **Gradient issues** | Saturates for very large/small inputs $\rightarrow$ vanishing gradient | Same issue, but zero-centering reduces bias shift             |
| **Typical use**     | Output layer in binary classification                                  | Hidden layers in feed-forward networks                        |

## <span style="color:rgb(239, 179, 1)">More in General</span> 

![[Pasted image 20250922232655.png]]

An activation function defines the output of a neuron based on its net input. It is a crucial component that introduces non-linearity, allowing neural networks to learn complex patterns. The general form for a neuron's output u is:

$$
u = f(\, \vec{w} \cdot \vec{x} - T \,)
$$
![[Pasted image 20250923084716.png]]

| Function                         | Equation                                                                           | Output Range         | Key Properties                                                                                   |
| :------------------------------- | :--------------------------------------------------------------------------------- | :------------------- | :----------------------------------------------------------------------------------------------- |
| **Linear**                       | $f(z) = z$                                                                         | $(-\infty, +\infty)$ | Used for regression. No non-linearity is introduced.                                             |
| **Step**                         | $f(z) = \begin{cases} 0 & \text{if } z < 0 \\ 1 & \text{if } z \geq 0 \end{cases}$ | $\{0, 1\}$           | The classic perceptron function. Not used in modern deep learning.                               |
| **LogSig** (Sigmoid)             | $f(z) = \dfrac{1}{1 + e^{-z}}$                                                     | $(0, 1)$             | Smooth approximation of step. Suffers from saturation and vanishing gradients.                   |
| **Tanh** (Hyperbolic Tangent)    | $f(z) = \tanh(z) = \dfrac{e^{z} - e^{-z}}{e^{z} + e^{-z}}$                         | (−1,1)(-1, 1)        | Zero-centered version of sigmoid; often performs better in hidden layers.                        |
| **ReLU** (Rectified Linear Unit) | f$(z) = \max(0, z)$                                                                | $[0, +\infty)$       | **Most popular hidden layer function.** Computationally efficient, mitigates vanishing gradient. |

# <span style="color:rgb(223, 109, 109)">Introduction to the Learning Concept in ANN</span> 

At the start, we **don’t know the optimal values** of the weights ($W$) and thresholds/biases ($T$).  
The goal of **training** is to find good values for these parameters.

## <span style="color:rgb(239, 179, 1)">What Learning <i>Does</i> and <i>Does Not</i> Do</span>

- Learning **does not change** the topology (the number of layers, neurons, or connections).
- Instead, learning **modifies the strength of the connections** by adjusting $W$ and $T$.
- **Exception:** modern methods like _dropout_ temporarily deactivate some neurons during training, but this is only a _regularization trick_, not a permanent topology change.


![[Pasted image 20250923085005.png]]

- **Positive weights (excitatory):** strengthen the signal.
- **Negative weights (inhibitory):** weaken or oppose the signal.

==Learning requires a **training dataset**.==
==- In **supervised learning**, the weights are initialized (often randomly).
-At first, the network works poorly, but through training, it **gradually tunes** $W$ and $T$ to improve performance.==

### <span style="color:rgb(161, 40, 226)">Training as Optimization</span>

Training can be seen as an **optimization problem**:
- Find parameters $(W,T)$ that minimize the error between predictions and targets.
- Achieved via iterative methods (e.g., gradient descent).
- At each **epoch**, the network evaluates how well its current parameters perform and updates them accordingly.

$(W, T) \; \longrightarrow \; (W', T') \; \longrightarrow \; (W'', T'') \; \dots$


## <span style="color:rgb(239, 179, 1)">Learning Paradigms in ANN</span>

When we train a neural network, there are two main approaches: **supervised learning** and **unsupervised learning**.

> In **supervised learning**, the training data comes with both the **inputs** and the **expected outputs**. ==These expected outputs are called **labels**==. For example, if the input is an image of a handwritten digit, the label would be the number it represents (e.g., “5”). The network produces its own prediction, and we compare it with the label. At the beginning, the predictions are usually very poor, so the **error** between the label and the prediction is large. With each training step (epoch), the network adjusts its parameters so that the error becomes smaller and smaller. From an optimization point of view, the goal is to make the difference between the true label and the predicted output as small as possible.
> 
> In **unsupervised learning**, things are different because we don’t have labels. The training data only contains **inputs**, with no reference outputs. The network has no external “teacher” telling it what the correct answer should be. Instead, it tries to **discover patterns, structures, or relationships** within the data itself. For example, it might group similar inputs together (clustering) or learn a compressed representation of the data (dimensionality reduction). Here, there is no clear “optimal” output — the learning process is guided only by the data’s internal structure.


# <span style="color:rgb(223, 109, 109)">Synthesis: Key Points about ANN </span> 

Artificial Neural Networks (ANN) can be seen as **black-box computing systems**: they take inputs, process them internally, and produce outputs. What happens inside is determined by a set of **parameters** and **functions** that shape the network’s behavior.

![[Pasted image 20250923092223.png]]

The **weights** are the free parameters of the network. They are adjusted during training, and together with the **thresholds (biases)**, they store the knowledge that the network has acquired from data. The **activation functions**, on the other hand, are usually considered **hyperparameters** — they are chosen beforehand and determine the nonlinear behavior of each neuron.

It is important to note that ANNs are **not direct models of the human brain**, but rather mathematical abstractions inspired by it. They come in many different **architectures**, such as feedforward networks, convolutional networks, or recurrent networks, depending on the task.

Training the network means **estimating the optimal values of the weights and thresholds**. For example, in the small network shown below, we have:

- 4 inputs connected to 3 hidden neurons $\rightarrow$ $4 \times 3 = 12$ weights, plus 3 thresholds = **15 parameters**.
    
- 3 hidden neurons connected to 2 output neurons  $3 \times 2 = 6$ weights, plus 2 thresholds = **8 parameters**.
    
![[Pasted image 20250923092528.png]]

In total, this simple network has:

$15 + 8 = 23 \quad \text{parameters (weights + thresholds) to learn}$

Thus, the complexity of an ANN is strongly tied to the number of free parameters it contains. The training process can be seen as finding the right configuration of these parameters so that the network performs the desired task effectively.

### <span style="color:rgb(161, 40, 226)">From Linear to Nonlinear Models</span>

Let’s consider a network with **4 inputs** $(x_1, x_2, x_3, x_4​)$ and **2 outputs** $(u_1, u_2)$.

A **linear model** for the outputs can be written as:

$u_1 = a_1 x_1 + b_1 x_2 + c_1 x_3 + d_1 x_4$
$u_2 = a_2 x_1 + b_2 x_2 + c_2 x_3 + d_2 x_4$

This model has **8 parameters** (4 weights per output).

If we extend this to a **quadratic (parabolic) model**, we include terms like $x_1^2, x_1 x_2, \dots$ which already raises the parameter count to **28**. The complexity grows quickly as we add higher-order terms.

![[Pasted image 20250923093812.png]]

Neural networks can approximate such polynomial relations, but in a more flexible and scalable way. Instead of explicitly defining higher-order terms, the **hidden layers** and **activation functions** allow the network to model nonlinear relationships automatically.

For example, in the last neural network architecture reported:
Total free parameters (weights + thresholds):

$15+8=23$

This means that with just **23 parameters**, the ANN can represent relationships that would otherwise require a much larger polynomial expansion.

>[!info] <span style="font-weight:bold; color:rgb(161, 40, 226)">Features to Explore Next:</span> Now that we understand the basics of neural networks and supervised/unsupervised learning, the next topics to explore are the **main learning techniques** and **network architectures**. These define _how_ neural networks actually learn and _how_ they are structured.


<span style="font-weight:bold; color:rgb(71, 215, 140)">LET'S GO BACK AGAIN TO OUR BASIC NETWORK TO STUDY THIS LEARNING TECHNIQUES </span>

---

***The following is a recap of the neural network architecture and analysis of techniques for learning. Starting from the most basic architecture.***

## <span style="color:rgb(223, 109, 109)">Basic Network: Perceptron</span> 

## <span style="color:rgb(239, 179, 1)">2-Layer Neural Network</span>

The simplest form of an artificial neural network is a **2-layer structure**, composed of:
- An **input layer** with $N \geq 1$ signals.
- An **output layer** with $M \geq 1$ signals.
-
The vector of inputs $[x1​,x2​,x3​,…]$ is called the **input pattern**. In biological terms, this can be thought of as a **stimulus**.

![[Pasted image 20250923094805.png]]

## <span style="color:rgb(239, 179, 1)">Pattern Classification</span>

The simplest way to use this model is for **classification tasks**.

- Example: an input pattern with 4 elements $(x1​,x2​,x3​,x4​).$
- The task is to decide whether this pattern belongs to **class A** or **class B**.

In many applications — for example, **medical decision making** — problems are naturally formulated as classification tasks.

## <span style="color:rgb(239, 179, 1)">The Perceptron Model</span>

The simplest perceptron has:
- **One single output unit** in the output layer.
- A **binary step activation function**, defined as:

$u = f(P - T) = \begin{cases} 1 & \text{if the input belongs to the category} \\ 0 & \text{otherwise} \end{cases}$

Where:
- $P = \sum_{i=1}^{N} w_i x_i$​ is the weighted sum of inputs.
- $T$ is the **threshold** of the neuron.
## <span style="color:rgb(239, 179, 1)">Decision Model</span>

For the example with 4 inputs:

$P = w_1 x_1 + w_2 x_2 + w_3 x_3 + w_4 x_4$
$u=f(P−T)$

Here:
- $x_1, x_2, x_3, x_4$= input pattern.
- $w_1, w_2, w_3, w_4$ = weights (connection strengths).
- $T$ = threshold of the neuron.
- $u$ = output (decision: 0 or 1).
    
This forms a **binary classifier**:
- $u=1$ → input belongs to the desired class.
- $u=0$ → input does not belong to the class.


# <span style="color:rgb(223, 109, 109)">Action Potential and Neural Threshold</span> 

In a perceptron, the **threshold** $T$ can be reinterpreted as an additional weight. Instead of treating it separately, we consider a **virtual input** equal to $−1$, connected with weight $T$.

![[Pasted image 20250923100414.png]]
## <span style="color:rgb(239, 179, 1)">Weighted Sum with Threshold</span>

For a neuron with two inputs:
$P = w_1 x_1 + w_2 x_2 - T$

This can be rewritten as:
$P = w_1 x_1 + w_2 x_2 + w_T \cdot x_T$

Where:
- $x_T = -1$ (the virtual constant input)
- $w_T = T$ (the threshold treated as a weight)

## <span style="color:rgb(239, 179, 1)">General Case</span>

For a neuron with inputs $(x_1, x_2, ..., x_j)$:
$P = \sum_{j=1}^M w_j x_j - T$

Or equivalently:

$P = \sum_{j=1}^{M+1} w_j x_j$

with the convention that the last input is always $x_{M+1} = -1$, and its corresponding weight is $w_{M+1} = T$

## <span style="color:rgb(239, 179, 1)">Action Potential</span>

From now on:
- The **quantity P-T is considered as just P and it is called the action potential** of the neuron.
- It already includes the effect of the threshold.

This interpretation simplifies the model: instead of handling thresholds separately, they are absorbed into the general weight–input structure.


# <span style="color:rgb(223, 109, 109)">Perceptron With Step Function in Action</span> 

![[Pasted image 20250923161333.png]]

Let us consider a simple perceptron with **two input units** and **one output unit**. The activation is defined by a **step function**:

| ![[Pasted image 20250923161406.png]]                                                                                    |
| ----------------------------------------------------------------------------------------------------------------------- |
| $u = \begin{cases} 1 & \text{if } w_1 x_1 + w_2 x_2 - T > 0 \\ 0 & \text{if } w_1 x_1 + w_2 x_2 - T \leq 0 \end{cases}$ |

Since $x_1$ and $x_2$ are binary, there are at most **4 input patterns**:
- (0,0)
- (0,1)
- (1,0)
- (1,1)
### <span style="color:rgb(161, 40, 226)">Decision Boundary</span>

The **decision boundary** is defined by:

$w_1 x_1 + w_2 x_2 - T = 0$

This boundary splits the input space into two regions:
- On one side $\rightarrow$ u=1
- On the other side $\rightarrow$ u=0

![[Pasted image 20250923162405.png]]

In the $(x_1, x_2)$ plane, the line has the form:
$$
x_2 = m x_1 + b
$$
where:
$$
m = -\frac{w_1}{w_2} (slope\space of\space the\space line)
$$
$$
b = \frac{T}{w_2} (intercept)
$$

### <span style="color:rgb(161, 40, 226)">Role of the Weight Vector</span>

The **weight vector**:
$\vec{w} = (w_1, w_2)$

- Is **orthogonal (perpendicular)** to the decision boundary.
- Indicates the **direction of sensitivity** of the perceptron.
- Larger weight $\rightarrow$ stronger influence of that input.
---

## <span style="color:rgb(239, 179, 1)">Case 1: OR port</span> 

Now, if we set some values such as 
* $w_1=1$
* $w_2 = 1$
* $T =0.5$

We obtain that our decision boundary
$$
x_2 = m x_1 + b
$$
where:
$$
m = -\frac{w_1}{w_2} (slope\space of\space the\space line)
$$
$$
b = \frac{T}{w_2} (intercept)
$$
Is going to be

$$
x_2 = -x_1 + 1/2
$$
![[Pasted image 20250923163932.png]]

| ![[Pasted image 20250923163722.png]] | Case 1: OR Gate<br><br>$P = w_1 x_1 + w_2 x_2 - T$ <br>$P = x_1 + x_2 - 0.5$<br><br>- $P>0$, output $u=1$<br>- $P \leq 0$, output $u=0$<br>    <br>**Classification:**<br>- $(0,0) \rightarrow u = 0$<br>- $(0,1) \rightarrow u = 1$<br>- $(1,0) \rightarrow u = 1$<br>- $(1,1) \rightarrow u = 1$ |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## <span style="color:rgb(239, 179, 1)">Case 2: AND port</span> 

Now, if we set some values such as 
* $w_1=1$
* $w_2 = 1$
* $T =1.5$

We obtain that our decision boundary
$$
x_2 = m x_1 + b
$$
where:
$$
m = -\frac{w_1}{w_2} (slope\space of\space the\space line)
$$
$$
b = \frac{T}{w_2} (intercept)
$$
Is going to be

$$
x_2 = -x_1 + 3/2
$$
![[Pasted image 20250923163915.png]]

| ![[Pasted image 20250923163955.png]] | Case 2: AND Gate<br><br>$P = w_1 x_1 + w_2 x_2 - T$ <br>$P = x_1 + x_2 - 1.5$<br><br>- $P>0$, output $u=1$<br>- $P \leq 0$, output $u=0$<br>    <br>**Classification:**<br>- $(0,0) \rightarrow u = 0$<br>- $(0,1) \rightarrow u = 0$<br>- $(1,0) \rightarrow u = 0$<br>- $(1,1) \rightarrow u = 1$ |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

In this example, we see that the **behavior of the perceptron can change completely just by adjusting one parameter — the threshold**.

- With $T=0.5$, the perceptron behaves as an **OR gate**.
- With $T=1.5$, the perceptron behaves as an **AND gate**.
    
This shows that by tuning the **weights and threshold**, a single perceptron can implement different decision rules.

This is the key idea behind **training a perceptron**

# <span style="color:rgb(223, 109, 109)">Training the perceptron</span> 

Now, the idea is that **training performs the tuning of the parameters** (weights and threshold) so that the perceptron learns to reproduce the desired task.

![[Pasted image 20250923164729.png]]

Here, we have:
- One neuron
- Inputs $x_1, x_2, \dots, x_n$
- A virtual input $−1$ connected to the threshold $T$

During training, we apply **supervision**:

- A **training dataset** is provided, consisting of:
    - A set of **input examples** (training patterns)
    - A set of **corresponding expected outputs** (labels)
    
For each input pattern, the perceptron compares its output with the expected label, and the difference is used to update the parameters.
### <span style="color:rgb(161, 40, 226)">Key Points</span>

- **ANN topology** is defined by:
    - The **structure** (number of inputs, hidden units, outputs)
    - The **activation function** (in this case, a step function)
        
- **Training process**: estimation of the neural weights $\mathbf{w}$
    $\mathbf{w} = [w_1, w_2, \dots, w_n, T]$ 
    
    where the last element corresponds to the threshold, modeled as a weight with input −1.
    
- **Supervised learning**: expected outputs are known for each input pattern.
    
- **Training dataset size**:
    - Larger datasets usually improve generalization.
    - Too few training examples lead to poor results.
    - However, in practice, the optimal amount of data is never known in advance.

## <span style="color:rgb(239, 179, 1)">Training Dataset and Error Signal</span> 

For each **input pattern** we have a corresponding **reference output (label)**.
- One pattern has n elements (or n+1 if we include the virtual input −1).
- The training dataset contains **R patterns**, where R is the dataset size.

### <span style="color:rgb(161, 40, 226)">Computation of the Output</span>

The output of the perceptron is:
$$
u = f\left( \sum_{j=1}^{n+1} w_j x_j \right)
$$

where:
$f$= activation function (step)
$w_j$​ = weights (with $w_{n+1} = T$, the threshold)
$x_{n+1} = -1$, the virtual input

### <span style="color:rgb(161, 40, 226)">Error Signal</span> 

To update the parameters, we compare the output of the network with the expected reference:
$$
e = t−u 
$$
- t= target value (reference output)
- u = actual output of the perceptron
- e = error signal

![[Pasted image 20250923165250.png]]
# <span style="color:rgb(223, 109, 109)">Perceptron Learning Rule, Rosenblatt (1962)</span> 

The **Perceptron learning rule** was introduced by Rosenblatt (1962).

- **Activation**: step function
- **Training set size**: R patterns
- **Procedure**: incremental (on-line) update

## <span style="color:rgb(239, 179, 1)">Online Learning Strategy</span>

- Training is done **one pattern at a time**.
- For each input pattern $k$:
    1. Compute the perceptron output $u^{(k)}$.
    2. Compare with the target $t^{(k)}$.
    3. Compute the **error signal**.
    $$
        e^{(k)} = t^{(k)} - u^{(k)}
        $$
    4. Update the weights using the error:$$
        w_{\text{new}} = w_{\text{old}} + \Delta w^{(k)}
        $$with
        $$\Delta w^{(k)} = \eta \, e^{(k)} \, x^{(k)}$$
    where:
- $\eta \leq 1$ is the **learning rate** (hyperparameter).
- $x^{(k)}$ is the input vector of the training pattern (including the virtual input −1).
- $w = [w_1, w_2, w_3, \dots, T]$ is the weight vector (last element corresponds to threshold).

## <span style="color:rgb(239, 179, 1)">Expected Error Values</span>

Since both $u$ and $t$ are binary (0 or 1):

$e = t - u   \in \{-1, 0, +1\}$ 

- $e = 0$ → no update (correct classification).
- $e=+1$→ perceptron fired too low, increase weights.
- $e=−1$ → perceptron fired too high, decrease weights.

The perceptron only adjusts the weights when a misclassification occurs $\mathbf{e}(k) \neq 0$

Each weight update modifies the slope and position of the decision boundary, adapting the model to correctly classify the input samples over time.


# <span style="color:rgb(223, 109, 109)">Geometric Validation of the Perceptron</span> 

The perceptron can be interpreted geometrically as a way to orient the decision boundary such that:

![[Pasted image 20250923180233.png]]

$\mathbf{w} \cdot \mathbf{x} > 0 \quad \text{for all patterns in class 1 (Black dots),}$
$\mathbf{w} \cdot \mathbf{x} < 0 \quad \text{for all patterns in class 2 (White dots). }$

Here, $\mathbf{w} = [w_1, w_2]$ is the weight vector and $\mathbf{x} = [x_1, x_2]$ is the input vector.

<span style="font-weight:bold; color:rgb(161, 40, 226)">Correct Classification:</span>The decision boundary separates the classes, e.g., white dots (class 0) on one side and black dots (class 1) on the other. In this case, the line may appear nearly vertical. 

<span style="font-weight:bold; color:rgb(161, 40, 226)">Misclassification:</span> If the decision boundary is poorly oriented, some points (e.g., an upper blank dot) fall on the wrong side, resulting in a classification failure.

<span style="font-weight:bold; color:rgb(161, 40, 226)">Takeaway:</span> The perceptron rule updates the weights to rotate and shift the decision boundary, aiming to correctly separate all training patterns. Geometrically, each weight update adjusts the orientation of the line (or hyperplane in higher dimensions) to reduce misclassifications.

## <span style="color:rgb(239, 179, 1)">Perceptron Example: Weight Initialization and Decision Boundary</span>

**Setup:**
- Inputs and bias (represented as $T=−1$):

![[Pasted image 20250923181111.png|300]]

Your input vectors are 3-dimensional because of the **bias term**:

$\mathbf{x}^{(i)} = \begin{bmatrix} x_1 \\ x_2 \\ T \end{bmatrix}, \quad T=-1$

The labels (predefined values for the supervised learning).
- $t_1​=1$→ the perceptron should **output 1** for $\mathbf{x}^{(1)}$.
- $t_2 = 0$→ the perceptron should **output 0** for $\mathbf{x}^{(2)}$.
- $t_3 = 0$→ the perceptron should **output 0** for $\mathbf{x}^{(3)}$

| $\mathbf{x}^{(1)} = \begin{bmatrix} 1 \\ 2 \\ -1 \end{bmatrix}, \quad t_1 = 1$<br><br>$\mathbf{x}^{(2)} = \begin{bmatrix} -1 \\ 2 \\ -1 \end{bmatrix}, \quad t_2 = 0$<br><br>$\mathbf{x}^{(3)} = \begin{bmatrix} 0 \\ 0 \\ -1 \end{bmatrix}, \quad t_3 = 0$<br> | ![[Pasted image 20250923181056.png\|300]] |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
Here, the third component of each vector represents the bias term T=−1.

<span style="color:rgb(161, 40, 226)"><b>Weight Initialization:</b></span>
$\mathbf{w}_{\text{start}} = [1.0, -0.8, 0.5]$

- This initial weight vector defines the **starting decision boundary** in the $x_1, x_2$​ plane.
- The direction of the weight vector is perpendicular to the decision boundary. Points on one side of the boundary are classified as u=1, and points on the other side as u=0.

<span style="color:rgb(161, 40, 226)"><b>Geometric Interpretation:</b></span>

- The decision boundary splits the plane into two regions.    
- The weight vector points toward the region classified as 1.
- Misclassified points will trigger an update to rotate and shift the decision boundary so that the weight vector better separates the classes.

<span style="color:rgb(161, 40, 226)"><b>Example Visualization:</b></span>

- $x^{(1)}$(black dot) is on the correct side initially.
- $x^{(2)}$ and $x^{(3)}$ (white dots) may be misclassified depending on $\mathbf{w}_0$​, which would require weight updates.

## <span style="color:rgb(239, 179, 1)">Step 1: First Input</span>

We are going to assume that the Learning rate: $\eta = 1$
And the output along with the activation function is given by:

Step function: $u = \text{step}(\mathbf{w}^T \mathbf{x})$, which outputs 1 if input ≥ 0, else 0.

### <span style="color:rgb(161, 40, 226)">a. Compute u1</span>:

First Input ($\mathbf{x}^{(1)}, t_1$​)
1. Compute perceptron output:
$$
u_1 = \text{step}(\mathbf{w}_0 \cdot \mathbf{x}^{(1)})
$$
2. Compute the dot product:
$$
\mathbf{w}_0 \cdot \mathbf{x}^{(1)} = 1.0 \cdot 1 + (-0.8) \cdot 2 + 0.5 \cdot (-1) = 1 - 1.6 - 0.5 = -1.1
$$
3. Apply step function:
$$
u_1 = \text{step}(-1.1) = 0
$$

### <span style="color:rgb(161, 40, 226)">b. Computer the error</span>

$$
e_1​=t_1​−u_1​
$$
$$
e_1=1-0=1
$$
The output is **incorrect**, so we need to update the weights. $t_1 \neq u_1$

### <span style="color:rgb(161, 40, 226)">c. Update weights</span> 
$$
w_1​=w_0​+\eta⋅e_1\cdot x^{(1)}​
$$

$$
w_1 =[1.0,−0.8,0.5] +1⋅1⋅[1,2,−1]= [2.0,1.2,−0.5]
$$

- The weight vector **changes direction and magnitude**, which also moves and rotates the decision boundary.
    
- Visually, the decision boundary now better separates the points, but it might **still not classify all points correctly**.


| Before                               | After                                |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250923184506.png]] | ![[Pasted image 20250923184523.png]] |

## <span style="color:rgb(239, 179, 1)">Step 2: Second Input</span>

We are going to still have the Learning rate: $\eta = 1$
And also that the output along with the activation function is given by:

Step function: $u = \text{step}(\mathbf{w}^T \mathbf{x})$, which outputs 1 if input ≥ 0, else 0.

### <span style="color:rgb(161, 40, 226)">a. Compute u2</span>:

Second Input ($\mathbf{x}^{(2)}, t_2$​)
1. Compute perceptron output:
$$
u_2 = \text{step}(\mathbf{w}_1 \cdot \mathbf{x}^{(2)})
$$
2. Compute the dot product:
$$
\mathbf{w}_1 \cdot \mathbf{x}^{(2)} = 2.0 \cdot (-1) + 1.2 \cdot 2 + (-0.5) \cdot (-1) = -2 + 2.4 + 0.5 = 0.9
$$
3. Apply step function:
$$
u_2 = \text{step}(0.9) = 1
$$

### <span style="color:rgb(161, 40, 226)">b. Computer the error</span>

$$
e_2​=t_2​−u_2​
$$
$$
e_2=0-1=-1
$$
The output is **incorrect**, so we need to update the weights. $t_1 \neq u_1$

### <span style="color:rgb(161, 40, 226)">c. Update weights</span> 
$$
w_2=w_1​+\eta⋅e_2\cdot x^{(2)}​
$$

$$
w_1 =[2.0, 1.2, -0.5] +1⋅(-1)⋅[-1,2,−1]= [3.0,-0.8,0.5]
$$

| Before                               | After                                |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250923184523.png]] | ![[Pasted image 20250923185230.png]] |

## <span style="color:rgb(239, 179, 1)">Step 3: Third Input</span>

We are going to still have the Learning rate: $\eta = 1$
And also that the output along with the activation function is given by:

Step function: $u = \text{step}(\mathbf{w}^T \mathbf{x})$, which outputs 1 if input ≥ 0, else 0.

### <span style="color:rgb(161, 40, 226)">a. Compute u3</span>:

Third Input ($\mathbf{x}^{(3)}, t_3$​)
1. Compute perceptron output:
$$
u_3 = \text{step}(\mathbf{w}_2 \cdot \mathbf{x}^{(3)})
$$
2. Compute the dot product:
$$
\mathbf{w}_2 \cdot \mathbf{x}^{(3)} = 3.0 \cdot 0 + 0.8 \cdot (-1) + 0.5 \cdot (-1) = 0 +0.8 - 0.5 = 0.3
$$
3. Apply step function:
$$
u_3 = \text{step}(0.3) = 1
$$

### <span style="color:rgb(161, 40, 226)">b. Computer the error</span>

$$
e_3​=t_3​−u_3​
$$
$$
e_3=0-1=-1
$$
The output is **incorrect**, so we need to update the weights. $t_1 \neq u_1$

### <span style="color:rgb(161, 40, 226)">c. Update weights</span> 
$$
w_3=w_2​+\eta⋅e_3\cdot x^{(3)}​
$$

$$
w_3 =[3.0,-0.8,0.5] +1⋅(-1)⋅[0,-1,-1]= [3.0,0.2,1.5]
$$

| Before                               | After                                |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250923185230.png]] | ![[Pasted image 20250923191907.png]] |

We see that the procedure is very straight forward and it is just a matter of following the steps until we get the final decision boundary. The perceptron rule goes one by one and updates the decision boundary every step considering the error signal.

Now, as a conclusion, we are going to see if the classification performs well with the final decision boundary.


| Inputs                                                                                                                                                                                                                                                          | Outputs                                                                                                                                                                                                                 | Geometrical Representation           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| $\mathbf{x}^{(1)} = \begin{bmatrix} 1 \\ 2 \\ -1 \end{bmatrix}, \quad t_1 = 1$<br><br>$\mathbf{x}^{(2)} = \begin{bmatrix} -1 \\ 2 \\ -1 \end{bmatrix}, \quad t_2 = 0$<br><br>$\mathbf{x}^{(3)} = \begin{bmatrix} 0 \\ 0 \\ -1 \end{bmatrix}, \quad t_3 = 0$<br> | $w_3 = [3.0,0.2,1.5]$<br><br>$u_1=step(w_3*x^{(1)})$<br>$u_1=step(1.9) \rightarrow 1$<br><br>$u_2=step(w_3*x^{(2)})$<br>$u_2=step(-4.1) \rightarrow 0$<br><br>$u_3=step(w_3*x^{(3)})$<br>$u_3=step(-1.5) \rightarrow 0$ | ![[Pasted image 20250923193623.png]] |

Wee see that all the outputs are matching the labels $t$ . And that in the geometrical representation there is a right classification of the two classes. 


# <span style="color:rgb(223, 109, 109)">Perceptron Learning Rule</span> 

![[Pasted image 20250923195706.png]]

The perceptron learning rule defines a linear classifier whose **decision boundary is always orthogonal to the weight vector**. The boundary can be shifted by adjusting the bias. The perceptron updates its weights whenever it misclassifies a sample, and this learning rule is **guaranteed to converge to a solution in a finite number of steps**, as long as a solution exists.

However, this guarantee holds **only for linearly separable problems**. In cases where the data is not linearly separable, a single perceptron cannot perform the classification correctly. Its decision boundary is just a line (or hyperplane) and cannot capture complex patterns.

To handle more complex distributions, the perceptron needs to be **extended**.

# <span style="color:rgb(223, 109, 109)">Extending the Perceptron</span> 

![[Pasted image 20250923200331.png]]

The **classic perceptron** has been extended in several important ways to create more powerful and flexible neural networks capable of solving complex tasks.

First, the **activation function** was generalized. While the original perceptron used a step function producing binary outputs, modern neurons use **continuous, non-linear activation functions** such as the logistic sigmoid (LogSig) or hyperbolic tangent (Tanh). These functions allow the network to model complex relationships and provide smooth gradients necessary for learning.

| ![[Pasted image 20250923200255.png]]<br> | ![[Pasted image 20250923200309.png]] |
| ---------------------------------------- | ------------------------------------ |

Second, the perceptron was generalized to handle **multi-dimensional inputs and outputs**. For the i-th neuron, the net input is calculated as a weighted sum of all inputs minus a threshold (bias):
$$P_i​=∑_{j=1}^{M​}w_{ij}​x_j​−T_i​$$

Third, the introduction of **hidden layers** between the input and output layers allows the network to learn hierarchical feature representations. This dramatically increases its computational power, transforming a simple linear classifier into a **universal function approximator**.

A neuron with a sigmoidal activation function operates in three regions:

- **Linear region** near $P_i \approx 0$, where outputs change proportionally with inputs.
- **Non-linear (transition) region**, where the neuron is highly sensitive and the input-output relationship is strongly non-linear.
- **Saturation region**, where large $|P_i|$ values cause the output to flatten, potentially slowing learning due to vanishing gradients.

In summary, the key extensions from the simple perceptron are: replacing the step function with continuous functions, supporting multiple output neurons, and introducing hidden layers. Together, these changes enable neural networks to address **highly complex, non-linear problems**.

![[Pasted image 20250924153414.png]]


==The **sigmoid function** replaces the step function by giving a smooth continuous output, but we still need a **manual threshold** to turn it into a binary classifier.==

While simple, using a single neuron with a manual threshold has a key limitation: it directly models a binary outcome. A more general and powerful solution for classification (especially with more than two classes) is the **Softmax network**.

![[0_25KoNMyn2HyjjDGM.png]]

Sigmoidal neuron provides a smooth, probabilistic output suitable for binary classification. A **manual threshold** (like 0.5) is applied to this probability to make a final class decision. For more robust and generalizable classification, especially with multiple classes, the **Softmax function** is the standard approach.

# <span style="color:rgb(223, 109, 109)">Delta Rule</span>

Learning in artificial neural networks is a **supervised process**.  We use a **training set** with R input patterns, each having a corresponding known output (*label*).

**Key Prerequisite:** The activation functions (like `LogSig`, `Tanh`, `Linear`) must be **continuously differentiable** ($C^1$). This smoothness ensures we can compute derivatives during training.

## <span style="color:rgb(239, 179, 1)">The Error (cost) Function</span>

The learning goal is to **minimize the difference between the actual output and the target output**.

**Error for a single pattern ($k$):**
$$
E^{(k)} = \sum_{i=1}^{N} \frac{1}{2} \left( t_i^{(k)} - u_i^{(k)} \right)^2
$$
- $t_i^{(k)}$​: target output of neuron $i$ for pattern $k$
- $u_i^{(k)}$​: actual output of neuron $i$ for pattern $k$
- The factor $\tfrac{1}{2}$​ simplifies derivatives
    
**Total error over the dataset:**
$$
E = \sum_{k=1}^{R} E^{(k)} = \sum_{k=1}^{R} \sum_{i=1}^{N} \frac{1}{2} \left( t_i^{(k)} - u_i^{(k)} \right)^2
$$
## <span style="color:rgb(239, 179, 1)">Learning Rule: Gradient Descent</span>

The error depends on all **weights** $E=E(\vec{w},\vec{T})$
To minimize $E$, we apply gradient descent

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Compute the gradient</span>: 
$$
\frac{\partial E}{\partial w_{ij}}, \frac{\partial E}{\partial T_i}
$$
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Update parameters</span>
$$
w_{ij}^{new}​=w_{ij}^{old}​-\eta \frac{\partial E} {\partial w_{ij}}​
$$
$$
T_{i}^{new}​=T_{i}^{old}​-\eta \frac{\partial E} {\partial T_{i}}​
$$

By repeating this process across the dataset: We progressively reduce the error $E$, the network parameters adapt, performance improves until convergence.
$$
E = \sum_{k=1}^{R} E^{(k)} = \sum_{k=1}^{R} \sum_{i=1}^{N} \frac{1}{2} \left( t_i^{(k)} - u_i^{(k)} \right)^2
$$

>[!warning] The **Delta Rule** (also called LMS – Least Mean Squares) is based on minimizing the **error function** $E$ using **gradient descent**.

**Why squared error?**
- It ensures the error is always **positive**.
- It **penalizes large errors** more heavily than small ones (due to the quadratic term).
- It is a **differentiable** function, which is essential for the gradient-based method.

The core idea is to adjust each weight $w_{ij}$​ in a direction that **reduces** the error $E$.

- **If** an increase in $w_{ij}$​ leads to an **increase** in $E$, then the weight variation $E$  should be **negative** (i.e., decrease the weight).
    
- **If** a decrease in $w_{ij}$​ leads to an **increase** in $E$, then the variation $E$ should be **positive** (i.e., increase the weight).

This intuitive principle is formalized by the **gradient descent** method.

## <span style="color:rgb(239, 179, 1)">Summary: The Iterative Training process </span> 

The following shows how we apply the delta rule by means of the gradient descent calculation in order to minimize the error. We can as well set some stop criterion in order to finish the process under a certain condition.

1. **Initialization:** The weights $w_{ij}$​ are initialized with **small random values** at the first step. This breaks symmetry and provides a starting point for optimization.
    
2. **Iteration:**
    - **Forward Pass:** For a given input pattern (or the whole batch), compute the network output $u_i^{(k)}$
    - **Compute Error:** Calculate the total error $E$.
    - **Backward Pass (Gradient Calculation):** Compute the gradient $\frac{∂E}{∂w_{ij}}$​ for all weights.
    - **Update Weights:** Apply the Delta Rule to update all weights.  
        This cycle repeats for many iterations (epochs).

3. **Stop Criterion:** The process stops when one of the following conditions is met:    
    - The error $E$ falls **below a predefined threshold**.
    - The weights **converge** (i.e., the changes $Δw_{ij}$​ become negligibly small).
    - A **maximum number of iterations** (epochs) is reached.

# <span style="color:rgb(223, 109, 109)">Gradient Descent</span> 

Gradient descent is an optimization algorithm used to find a **local minimum** of a function. It works by iteratively moving in the direction of the steepest descent, which is defined by the **negative of the gradient** of the function at the current point.

![[Pasted image 20250924203134.png|500]]

**Core Idea:** To minimize the error function $E$, calculate its gradient with respect to the weights. Then, update each weight by taking a small step in the opposite direction of this gradient.

## <span style="color:rgb(239, 179, 1)">The Weight Update Rule</span>

The update rule for a weight $w$ is derived from the gradient. The step size is controlled by a parameter $\eta$, the **learning rate**.

$$
\Delta w =-\eta \frac{\partial E}{\partial w}
$$

Where we still have the learning rate but now the partial derivate is the gradient of the error w.r.t weight. 

## <span style="color:rgb(239, 179, 1)">Derivation of the gradient for a single Weight </span> 

![[Gradient Descend.pdf]]

Then, we end up having:

$$
\Delta w_{ij} = \eta \cdot \sum _{k=1}^{R}(t_{i}^{(k)}-u_{i}^{(k)}) \cdot f'(P_i)x_{j}^{(k)}
$$

## <span style="color:rgb(239, 179, 1)">Delta Rule vs. Perceptron Learning Rule</span>

### <span style="color:rgb(161, 40, 226)">1. Perceptron Learning Rule</span>

- Activation: **step function** (non-differentiable).
- Update rule:
    
$$
w_{ij}^{\text{new}} = w_{ij}^{\text{old}} + \eta (t - u) ​
$$
- Works only for **linearly separable problems**.
- No gradient involved (just the error $t−u$).

### <span style="color:rgb(161, 40, 226)">2. Delta Rule (Widrow–Hoff, 1960)</span>

- Activation: **differentiable ($C^1$)** functions (e.g., sigmoid, tanh).
- Uses **gradient descent** on the squared error.
- Update rule (derived earlier):
$$
w_{ij}^{\text{new}} = w_{ij}^{\text{old}} + \eta \, \delta_i \, x_j​
$$

with

$\delta_i = (t_i - u_i) \, f'(P_i)$


# <span style="color:rgb(223, 109, 109)">Delta Rule, Analytical Formulation and Example</span> 

Let's recall now the delta rule and apply it to updating the weights of the following architecture. So, we have:
![[Pasted image 20250928095757.png]]

We have said that the delta rule corresponds to:
$$
\Delta w_{ij} \approx \left( \frac{\partial E}{\partial w_{ij}} \right)
$$
$$
\Delta w_{ij} = \eta \sum _{k=1}^R \left( t_i^{(k)}-u_i^{(k)}\right) f'\left( P_i^{(k)}\right) x_j^{(k)}
$$
Where $t$ is the label, $u$ the output of the model, $f'$ is the derivative of the activation function (If it is linear, it is 1, if it is not, it would depend on the action potential), $x$ is the vector pattern. $R$ is the number of patterns in the training set.

Let's now condition every weight to the delta rule. This for the first output and its corresponding label, also for all input patterns.

$$\Delta w_{11} = \eta \sum _{k=1}^R \left( t_1^{(k)}-u_1^{(k)}\right) f'\left( P_1^{(k)}\right) x_1^{(k)} $$
$$\Delta w_{12} = \eta \sum _{k=1}^R \left( t_1^{(k)} - u_1^{(k)}\right) f'\left( P_1^{(k)}\right) x_2^{(k)} $$
$$\Delta w_{13} = \eta \sum _{k=1}^R \left( t_1^{(k)} - u_1^{(k)}\right) f'\left( P_1^{(k)}\right) x_3^{(k)} $$
$$\Delta w_{14} =\Delta T_1 =  \eta \sum _{k=1}^R \left( t_1^{(k)} - u_1^{(k)}\right) f'\left( P_1^{(k)}\right) (-1) $$
And now for the second output and its corresponding label, also for all input patterns.

$$\Delta w_{21} = \eta \sum _{k=1}^R \left( t_2^{(k)}-u_2^{(k)}\right) f'\left( P_2^{(k)}\right) x_1^{(k)} $$
$$\Delta w_{22} = \eta \sum _{k=1}^R \left( t_2^{(k)} -u_2^{(k)}\right) f'\left( P_2^{(k)}\right) x_2^{(k)} $$
$$\Delta w_{23} = \eta \sum _{k=1}^R \left( t_2^{(k)} -u_2^{(k)}\right) f'\left( P_2^{(k)}\right) x_3^{(k)} $$
$$\Delta w_{24} =\Delta T_2 =  \eta \sum _{k=1}^R \left( t_2^{(k)} -u_2^{(k)}\right) f'\left( P_2^{(k)}\right) (-1) $$
Let's proceed with the example.

## <span style="color:rgb(239, 179, 1)">Example: Learning AND logic gate with logsig activation using delta rule</span> 

This example demonstrates the training of a single neuron to learn the **logical AND function** using the **Delta Rule** with a **log-sigmoid activation function**.

![[Pasted image 20250928105544.png]]

| Problem Setup                                                                                                                                                                                                                                                             | Training Configuration                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Inputs:** Three binary inputs $(x_1, x_2, x_3)$ .<br>    <br>**Bias term:** Represented as $x_4 = -1$.<br>    <br>**Patterns:** 8 possible combinations of inputs.<br>    <br>**Target output (t):** 1 only when all three inputs are 1, otherwise 0 (AND truth table). | **Weight initialization:** Random Gaussian distribution.<br>    <br>**Update rule:** On-line (weights updated after each pattern).<br>    <br>**Learning rate:** $\eta = 0.95$.<br>    <br>**Activation function:** Log-sigmoid (logsig). |
| ![[Pasted image 20250928105904.png]]                                                                                                                                                                                                                                      | ![[Pasted image 20250928105851.png]]                                                                                                                                                                                                      |
### Initial Parameters

The starting weight vector was:

$w_{start} = [-0.35, \; 0.63, \; 1.45, \; 0.95]$

The neuron output for each input pattern was computed, for all 8 combinations and we obtained as outputs, the following

![[Pasted image 20250928110305.png]]

What we would expect is having an  $u^{(k)} < 0.5$ for $k=1,2,3,4,5,6,7$ and $u^{(k)} \geq 0.5$  for $k=8$, that after passing for the logsig activation function would be 0's and 1 correspondingly and would match with the label $t$. Then we see there are some misclassifications.

**The Delta Rule is applied to update the synaptic weights of the neuron in order to minimize the error between the target output and the actual output.**

$$
\Delta w_{ij}^{(k)} =\eta \left( t_i^{(k)} -u_i^{(k)}\right) f'\left( P_i^{(k)}\right) x_j^{(k)} ​
$$
Where:
- $\eta$ = learning rate
- $t_i^{(k)}$​ = target output for pattern k.
- $u_i^{(k)}$​ = actual output for pattern k
- $P_i^{(k)}$​ = net input to the neuron
- $x_j^{(k)}$​ = input value of the j-th feature for pattern k

$k$ goes from 1 to $R$ where $R$ corresponds to the total size of the training set. $i$ corresponds to the number of the output neuron (if there are two output neurons, $i$ = 1, and $i$=2), and $j$ corresponds to the input neurons.

* The neuron’s net input is:
$$
P = w_1x_1 + w_2x_2 + w_3x_3 + w_4(-1)
$$
* The activation function is the **log-sigmoid (logsig)**:
$$
f(P) = \frac{1}{1+e^{-P}}
$$
* Its derivative, required for the update rule, is:
$$
f'(P) = f(P)\,(1 - f(P))$$
1. <span style="font-weight:bold; color:rgb(161, 40, 226)">STEP 1: 1st pattern</span>: For the first pattern $(x_1=0, x_2=0, x_3=0, x_4=-1, t=0)$:
* **Initial weights:**
    $w = [-0.35, \; 0.63, \; 1.45, \; 0.95]$
    
* ***Net input:**$$P = (0)(-0.35) + (0)(0.63) + (0)(1.45) + (0.95)(-1) = -0.95$$
1. **Neuron output (logsig):**
$$u = f(P) = \frac{1}{1+e^{0.95}} \approx 0.27$$
2. **Error:**
$$
e = t - u = 0 - 0.27 = -0.27$$

**Weight updates**:

- Since $x_1 = 0, x_2 = 0, x_3 = 0$, only the bias weight ($w_4$​) is updated.
$$\Delta w_4​=\eta \cdot e\cdot f'(P) \cdot x_4​
$$
$$=0.95⋅(−0.27)⋅(0.27)(1−0.27)⋅(−1)≈0.05$$
$\Delta w_1 = \Delta w_2 = \Delta w_3 = 0$

Note that only  $w_4$ is updated cos the $\Delta w$ depends on the input, and it is 0 for the rest.

- **New weights**:
    $w_{new} = w_{old} + \Delta w_{new}$
    
    Therefore, the updated weights are:
    $$w = [-0.35,\; 0.63,\; 1.45,\; 1.00]$$
    
1. <span style="font-weight:bold; color:rgb(161, 40, 226)">STEP 2: 2nd pattern</span>:

We can see here the transition between the initial parameters and last ones.
![[Pasted image 20250928120027.png]]
$(x_1​,x_2​,x_3​,x_4​)=(0,0,1,−1),\space t=0$

The Delta Rule is:

$$\Delta w_j = \eta \, (t - u)\, f'(P) \, x_j​$$
***Net input:**$$P = (0)(-0.35) + (0)(0.63) + (1)(1.45) + (1)(-1) = 0.45$$**Neuron output (logsig):**
$$u = f(P) = \frac{1}{1+e^{-0.45}} \approx 0.611 $$
**Error:**
$$e = t - u = 0 - 0.611 = -0.611$$

| $\Delta w_3$                                                                                       | $\Delta w_4$                                                                                         |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| <br>$\Delta w_3​=\eta \cdot e\cdot f'(P) \cdot x_3​$<br>$=0.95⋅(-0.611)⋅(0.611)(10.611)⋅(1)≈-0.14$ | <br>$\Delta w_4​=\eta \cdot e\cdot f'(P) \cdot x_4$<br>$=0.95⋅(−0.611)⋅(-0.611)(1+0.611)⋅(-1)≈ 0.14$ |

$$w_{new} = w_{old} + \Delta w_{new}$$
$$w_3=1.45-0.14=1.31$$
$$w_4 = 1+ 0.14 = 1.14$$
So only **weights connected to non-zero inputs** are updated. That’s why:
- $w_1$,$w_2$​ stay the same,
- $w_3$​ decreases,
- $w_4$​ increases.

2. <span style="font-weight:bold; color:rgb(161, 40, 226)">STEP 3: 3rd pattern</span>:

![[Pasted image 20250928121903.png]]
We continue with the procedure, this time the only the weights that change are $w_2$ and $w_4$ because the input pattern is $x_1=0, x_2=1, x_3=0, x_4=-1$

2. <span style="font-weight:bold; color:rgb(161, 40, 226)">STEP 8: 8th pattern</span>:

![[Pasted image 20250928122128.png]]
And we finish with the vector weights in the 8th input patter for which we have

$$W=[-0.13,-0.35,-0.50,1.24,1.36]
$$
Correspondingly with $w_1, w_2, w_3, w_4$

The thing is that after evaluating the neural network with this final vector of weights we obtain two miss-classifications w.r.t to the labels, two errors which are in red. We expected these output to be: 0, 0, 0, 0, 0, 0, 0, 1, after having the output passed for the logsig with threshold 0.5.

## <span style="color:rgb(239, 179, 1)">Reinforcement by Multiple Epochs</span> 

To reinforce learning, the training set (the 8 input patterns) was presented repeatedly to the network over several epochs. As an example, the network was trained for **10 iterations** (10 full passes over the training set). After these iterations the final weight vector obtained was:
$$
w_{end}​=[0.28,0.61,0.97,2.28].
$$
![[Pasted image 20250928122753.png]]
The presented values indicate progressive convergence but not yet a perfect separation according to the 0.5 threshold.

To further strengthen the learning process, the network was trained with the complete set of 8 patterns over **25 iterations**. After this extended training, the final weight vector obtained was:
$$w_{end}​=[1.00,1.04,1.23,3.06]$$
![[Pasted image 20250928122928.png]]

Compared to the 10-iteration case, the outputs of the non-target patterns remain close to zero, indicating that the network continues to suppress false positives effectively. The response for the target pattern (p8) has increased, from $u(8)=0.27$  at 10 iterations to $u(8)=0.42$ at 25 iterations. Although this shows a trend towards the desired classification, the value is still below the decision threshold of 0.5.

This behavior suggests that the learning process is progressing but has not yet fully converged.

---
The training process was further extended to **50 iterations**, using the same set of 8 training patterns. After this number of epochs, the final weight vector was:

$$w_{end}=[ 1.57,  1.50,  1.66,  4.15 ]$$
![[Pasted image 20250928123237.png]]

At this stage, the network has **finally converged**: the output for the target pattern $p_8$​ (the only TRUE case in the AND problem) has surpassed the decision threshold of 0.5, while all other patterns remain below it. This means the neuron is now correctly classifying the dataset according to the AND function
![[Pasted image 20250928123326.png]]
