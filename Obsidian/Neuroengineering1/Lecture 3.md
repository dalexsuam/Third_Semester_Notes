
***
Date: 22/09/2025

# <span style="color:rgb(223, 109, 109)">Notes on delta rule</span> 

## <span style="color:rgb(239, 179, 1)">Local Minima</span> 

![[Pasted image 20250928123845.png]]

The convergence of the Delta Rule is highly dependent on the initial values of the weights. If the training process starts with weights close to a local minimum, the algorithm may converge to that point rather than to the global minimum. 

>[!info] Using a range of different initial weight sets increases the probability of escaping poor local minima and of eventually converging to the global minimum.

## <span style="color:rgb(239, 179, 1)">Dependence on Activation Function</span> 

- <span style="color:rgb(161, 40, 226)"><b>Need for Differentiability</b>  </span>
    For the gradient descent algorithm to operate correctly, the activation function must be differentiable. This ensures that weight updates can be guided smoothly by the slope of the error function.
    
- <span style="color:rgb(161, 40, 226)"><b>Linear Activation</b>  </span>
    Linear activation functions are appropriate when a continuous output is required. However, they can cause the weights to grow without limit, making them impractical in many learning scenarios unless additional constraints or normalization techniques are applied.
    
- <span style="color:rgb(161, 40, 226)"><b>Logistic (Sigmoid) Activation</b>  </span>
    The logistic sigmoid function maps inputs to the range $[0,1]$, which makes it suitable for probabilistic interpretations. However, its limited range can restrict learning speed due to saturation effects in the extreme regions of the curve. Values get "stuck" near 0 or 1 (slow learning there)
    
- <span style="color:rgb(161, 40, 226)"><b>Hyperbolic Tangent (Tanh) Activation</b>  </span>
    The $\tanh$ function maps inputs to the range $[−1,1]$. This symmetric output distribution increases the representational and learning capability of the neuron, as it allows both positive and negative activations, reducing bias shifts and often resulting in faster convergence compared to the logistic sigmoid. Still suffers from saturation (slow learning for very high or low inputs)

## <span style="color:rgb(239, 179, 1)">Weight Initialization</span> 

Weights should be initialized randomly in a small range around zero. Large weights can saturate the sigmoid function, slowing learning. Keeping weights near zero avoids saturation, ensures small weight norms, and allows gradients to propagate effectively.

## <span style="color:rgb(239, 179, 1)">Weight Updating</span>

<span style="font-weight:bold; color:rgb(161, 40, 226)">On-line</span>:
 Updating means each pattern’s error sequentially contributes to the weight update (patterns can be chosen randomly). For the perceptron learning rule, every iteration updates the weights.
 $$\Delta w_{ij} = \eta \, (t_i-u_i)f'(P_i)x_j$$
 where $t_i$​ is the target, $u_i$​ the real output, $f'(P_i)$ the derivative of the activation function, $x_j$​ the input pattern, and $\eta$ the learning rate.

<span style="font-weight:bold; color:rgb(161, 40, 226)">Batch Updating:</span> Batch updating accumulates the errors from all patterns before updating the weights. For the delta rule, this means summing the contributions of all training samples to compute the final $\Delta w_{ij}$.
$$
\Delta w_{ij} = \eta \sum _{k=1}^R \left( t_i^{(k)}-u_i^{(k)}\right) f'\left( P_i^{(k)}\right) x_j^{(k)}
$$
Batch updating reduces the influence of a single sample by effectively averaging contributions across the training set.

<span style="color:rgb(161, 40, 226)"><b>Mini-Batch Updating</b></span>: Mini-batch updating is a middle approach between on-line and full batch updating. The training set $R$ is divided into subsets $S$, and weight updates are computed for each mini-batch before applying them. The process is repeated for all subsets until the full dataset is processed.

For a mini-batch $S$, the weight update is:
$$
\Delta w_{ij}^{(1)} = \eta \sum_{k=1}^{S} (t_i^{(k)} - u_i^{(k)}) f'(P_i^{(k)}) x_j^{(k)}
$$$$\Delta w_{ij}^{(2)} = \eta \sum_{k=S+1}^{2S} (t_i^{(k)} - u_i^{(k)}) f'(P_i^{(k)}) x_j^{(k)}$$​Weights are updated after each mini-batch:
$$w_{ij} = w_{ij} + \Delta w_{ij}^{(n)}$$
This continues until all subsets are processed. Mini-batch updating reduces the effect of single samples while avoiding the full computation of the entire dataset at once.

We can set the number $n$ of subsets by knowing the total size of the training set $R$ and the number of subsamples we would like $S$. (We use the function floor to approximate to the lower value. that is, $floor(5.65)=5$)
![[Pasted image 20250928160001.png]]
## <span style="color:rgb(239, 179, 1)">Learning Rate</span> 

Weight update rule:
$$\Delta w = - \eta \, \nabla f(x)$$


| Contour Plot                         | Geometrical Cost Function            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250928160523.png]] | ![[Pasted image 20250928162112.png]] |

When we update the weights with gradient descent, we always move in the opposite direction of the gradient, because that direction points downhill in the error surface. The learning rate $\eta$ controls how large each step is. 

| Contour Plot                         |
| ------------------------------------ |
| ![[Pasted image 20250928162533.png]] |

* **If the learning rate is set to a small value**, the steps are tiny. This makes the algorithm stable, but it will take many iterations before the weights reach the minimum of the error function.

| Contour Plot                         |
| ------------------------------------ |
| ![[Pasted image 20250928162414.png]] |

* **If the learning rate is chosen properly**, each step is large enough to make fast progress but still small enough to remain inside the valley of the error surface. In this case, the algorithm smoothly converges toward the minimum.

| Contour Plot                         |
| ------------------------------------ |
| ![[Pasted image 20250928162459.png]] |


* **If the learning rate is too large**, the steps become so big that instead of approaching the bottom of the valley, the algorithm overshoots and jumps to the other side. On the next iteration, it overshoots again in the opposite direction. The result is an oscillating movement around the minimum without ever settling.
* **If the learning rate is extremely large**, the steps can even carry the weights completely outside the valley, pushing them farther and farther away from the minimum. In that case, the algorithm diverges, and the error increases instead of decreasing.

## <span style="color:rgb(239, 179, 1)">Stopping Criteria</span> 

![[Pasted image 20250928163755.png]]

When applying gradient descent, the shape of the error function strongly influences how the weights evolve. If the error surface looks like a steep, smooth curve, the gradient always points clearly toward the minimum, and the updates can reach it efficiently (like the yellow one). However, if the error function has regions that are very flat, the situation changes (like the red one). In those flat areas the slope of the curve is almost zero, which means the gradient becomes very small.

At the start of training, the error function usually has a steep slope. In this region the gradient is large, so the updates to the weights are also large. This makes the algorithm move quickly toward the minimum.

But if the error function has a flat region, the slope there is almost zero. Since the gradient is proportional to the slope, the updates in this part become very small. As a result, the algorithm slows down: each iteration only slightly changes the weights, and progress toward the minimum is much slower.

This is where the idea of a **stopping rate** comes in. Because the gradient decreases as we approach flat regions or the minimum, there comes a point where the updates are so small that the algorithm has effectively stopped improving. ==At that point we can say it has converged, or we can define a stopping rule that ends training once the error reduction falls below a chosen threshold.==

<span style="color:rgb(161, 40, 226)"><b>Stop Criteria for Gradient Descent:</b></span>

1. **Maximum number of iterations**
    - Stop the algorithm once a predefined number of steps is reached.
        
2. **Gradient-based criterion**
    - Stop when the Euclidean norm of the gradient vector is smaller than a predefined threshold:
$$
\left \lVert \frac{\partial E}{\partial w} \right \rVert < \delta 
$$
    - This indicates the slope is very small and further updates would have minimal effect.

3. **Error-based criterion**
    
    - Stop when the value of the error function drops below a predefined threshold.
$$
E < \varepsilon
$$        
3. **Hybrid criterion**
    
    - Combine multiple conditions (e.g., stop if either the gradient is small, the error is low, or the maximum iterations are reached).
$$
\alpha \left \lVert \frac{\partial E}{\partial w} \right \rVert + \beta E < \gamma 
$$
## <span style="color:rgb(239, 179, 1)">Loss / Cost Function with Regularization</span> 

To improve training and avoid issues such as large weight values or saturation of sigmoidal neurons, a **regularization term** is often added to the standard error function. A common choice is the squared norm of the weights, $||w||^2$, which encourages the weights to remain small.

The total cost function then becomes a combination of the error function and the regularization term:

$$F = \frac{1}{2} \sum_{i=1}^{N} (t_i - u_i)^2 + \beta \, ||w||^2$$
where:
- $t_i$​ is the target output,
- $u_i$​ is the network output,
- $\beta$ is the regularization rate, a hyperparameter set heuristically,
- $||w||^2$ penalizes large weights.
    
The idea is that during training, we minimize the difference between the outputs and the nominal values (standard squared error) while keeping the weight magnitudes small. This ensures that sigmoidal neurons remain in their **active region** rather than saturating.

Depending on the task, other forms of error functions may be used:
- **Regression:** squared error with regularization, as above.
- **Classification:** cross-entropy loss is often more appropriate.

Regularization turns the optimization problem into a constrained problem: the network tries to fit the data while respecting the constraint on the weight magnitude.

## <span style="color:rgb(239, 179, 1)">Training Data - Heuristic Rule</span> 

The quality and preparation of training data strongly affect the learning process. Some key guidelines are:

1. <span style="color:rgb(161, 40, 226)"><b>Representativeness:</b></span> Training data should reflect the target task. Avoid including many examples of one type at the expense of others, as this can bias learning.
    
2. <span style="color:rgb(161, 40, 226)"><b>Balanced classes:</b></span> If one class is easy to learn, having an excessive number of examples from that class may slow down overall learning.
    
3. <span style="color:rgb(161, 40, 226)"><b>Data quantity (numerosity):</b> </span>In general, having more data improves training results, but this is heuristic; there is no strict rule.

4. <span style="color:rgb(161, 40, 226)"> <b>Input normalization:</b> </span>Rescale input values, for example by centering them to zero mean and applying standard deviation normalization. This is especially important for non-linear activation functions, like sigmoids, to prevent saturation and ensure the network operates in its active region.
    
In practice, carefully select data relevant to the task and remove irrelevant or redundant representations. Normalizing or scaling inputs is fundamental for stable and efficient learning.

# <span style="color:rgb(223, 109, 109)">Fitting and Extrapolation Error in ANN</span>

When training a neural network, it is crucial to ensure the model learns the task properly without overfitting or underfitting. To achieve this, the dataset is typically divided into three groups:


![[Pasted image 20250928165844.png]]


1. **Training set:** used to compute the weights and directly train the model.
    
2. **Validation set:** not used for learning, but to monitor the error during training. It helps tune hyperparameters and detect overfitting.
    
3. **Test set:** used after training to assess the extrapolation quality — how well the model generalizes to unseen data.

## <span style="color:rgb(239, 179, 1)">Balancing Underfitting and Overfitting</span>

![[Pasted image 20250928165930.png]]

- **Underfitting:** occurs when the model is too simple to capture the task complexity. From an ANN perspective, this may mean too few hidden units or insufficient network capacity. Increasing the number of hidden units or adjusting the convergence threshold can help (# of epochs).
    
- **Overfitting:** occurs when the model is too complex for the task, capturing noise instead of the underlying pattern. From an ANN perspective, this can result from too many layers or neurons. To prevent overfitting, one can:
    
    - Reduce the network complexity (fewer layers or neurons)
    - Add noise to training patterns
    - Apply regularization techniques

Train the network using the training set, monitor the error on the validation set, and adjust hyperparameters (like number of layers, activation functions, or neurons) to maintain a balance between underfitting and overfitting. After training, evaluate the model on the test set to verify its extrapolation quality.

This approach ensures the model learns effectively while maintaining good generalization to new data.

## <span style="color:rgb(239, 179, 1)">Learning and Generalization</span> 

To ensure a neural network generalizes well, it must perform accurately on patterns **not included in the training set**. A network has good generalization if its performance on the test set is similar to that on the training set. Note that a small residual error on the training set **does not guarantee good generalization**.

During training, the dataset is partitioned into **training and validation sets** (typically 10–20% of the data for validation). The network is trained only on the training set, but its performance is monitored on both the training and validation sets. Training can be stopped when the error on the validation set exceeds a predefined threshold, helping prevent overfitting.

A key activity in network development is **hyperparameter tuning**, often referred to as an **ablation task**. ==This is essentially a **grid search**: hyperparameters (like number of layers, neurons, learning rate, activation functions) are varied slightly across multiple trainings. The resulting performances are compared to select the architecture that best fits the task.==

Proper selection of the three datasets — training, validation, and test — is critical. In fields like biomedical engineering, where data acquisition is limited, a common split is:

- **Training:** 70–75%
- **Validation:** 10%
- **Test:** 15%
    
This provides a reasonable balance between sufficient training data and reliable evaluation of generalization.

# <span style="color:rgb(223, 109, 109)">Final Remarks on ANN Training</span> 

- **Training data:** should be representative of the task. Avoid having too many examples of one type at the expense of others. If a class is easy to learn, an excessive number of patterns from that class may slow overall learning. For continuous input data, it is important to **rescale inputs** (zero mean and standard deviation normalization).
    
- **Weight initialization:** weights should be initialized randomly within a small range around zero. Large initial weights can cause **sigmoidal activations to saturate**, slowing learning.
    
- **Training modes:**
    
    - **Batch mode:** small pattern errors are smoothed out, leading to more stable updates.
    - **On-line mode:** more sensitive to individual pattern errors, but shuffling the training data each epoch makes the search in weight space more stochastic, reducing the probability of being trapped in local minima.
        
- **Practical considerations:** For simple ANNs, using continuous activation functions can improve the perceptron. However, there are no exact rules for setting the initial weight vector or choosing the optimal batch size. These decisions must be guided by experience and practical experimentation.

---
> What an achievement it is to have arrived here! I’m so proud of you! 🎉
>
> Now, I must tell you—the journey ahead still has many thrilling steps to conquer. But don’t be discouraged! You’ve faced challenges before and triumphed, and you will do it again. Adventure awaits—keep pushing forward and embrace the path ahead!

![[4700.webp|400]]

---
We're going to go now to multilayer networks and we would like to introduce this topic by identifying the main issues for single layer networks.

# <span style="color:rgb(223, 109, 109)">Issues for single layer networks</span>

![[Pasted image 20250928172252.png]]

The delta rule that we used in single-layer networks is **not directly usable** in multilayer networks. Multilayer architectures are necessary to handle more complex tasks, such as high-order polynomial regression or classification problems where the data is **not linearly separable**.

![[Pasted image 20250928172312.png]]
In a linearly separable problem, a single linear decision boundary is sufficient to discriminate between classes. However, for more complex distributions, no straight line can separate the classes correctly. To classify these cases, the network must create **curvilinear or circular decision boundaries**.

==To transform a linear decision boundary into a curvilinear one, the network must include **non-linear neurons**. This is where activation functions such as **logistic sigmoid (logsig)** or **tanh** are introduced. These functions allow the network to perform non-linear processing.==

However, simply adding non-linear neurons at the output layer is **not sufficient**. Even if we have multiple output neurons forming different linear boundaries (U1, U2, etc.), their combination cannot create a truly non-linear boundary. Therefore, an **intermediate (hidden) layer** is required between input and output to enable the network to represent non-linear decision surfaces.

**Key limitations of single-layer networks:**

- Delta rule does not converge on non-linearly separable problems.
- Delta rule minimizes output error but cannot reduce classification mistakes for non-linear tasks.
- Logsig/tanh activations provide only one predefined non-linearity; for small inputs, they are almost linear.
- Adding more output neurons alone does **not** help in creating non-linear decision boundaries.

**Conclusion:** To solve non-linear tasks, we need **multilayer networks with hidden layers and non-linear activations**, as single-layer networks are restricted to linear transformations.

# <span style="color:rgb(223, 109, 109)">Multilayer network</span>

A **multilayer network** is created by adding one or more **hidden layers** between the input and output layers. Each hidden layer receives inputs from the previous layer, applies a **non-linear activation function**, and passes its output to the next layer.

The structure can be described as:

![[Pasted image 20250928172822.png]]

By sequentially composing these **non-linear transformations**, the network can implement complex input-output mappings that are impossible with a single-layer network.

The more hidden layers and non-linear functions we add, the more **complex problems** the network can handle. Each additional layer allows the network to represent increasingly intricate decision boundaries and functional relationships.


![[Pasted image 20250928172950.png]]

| ![[Pasted image 20250928173035.png]] | ![[Pasted image 20250928173043.png]] | ![[Pasted image 20250928173059.png]] |
| ------------------------------------ | ------------------------------------ | ------------------------------------ |

Consider a classification problem with a **concentric distribution**: one class occupies the inner region and the other class forms an outer ring. In this case, no matter how we set the threshold or the weights in a single-layer network, correct classification is impossible because a single linear decision boundary cannot separate the classes.

![[Pasted image 20250928173203.png]]

A solution is to use **hidden neurons** to create multiple decision boundaries. For example, two hidden neurons with sigmoid activations can each define a **linear boundary** in the input space. The outputs of these neurons are then combined in a subsequent output neuron with another sigmoid activation.


| Before                               | After                                |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250928173318.png]] | ![[Pasted image 20250928173337.png]] |


This composition allows the network to **bend the decision boundaries**, effectively creating a **non-linear separation** between the classes. By adding more hidden neurons and layers, the network can represent increasingly complex patterns and decision surfaces, handling tasks that are impossible for single-layer networks.

![[Pasted image 20250928173501.png]]

By adding an additional hidden layer, the network can **further deform the decision boundary** at the output. During training, the weights of the neurons are adjusted so that the decision boundary adapts to properly separate the classes.

![[Pasted image 20250928174123.png]]

As more hidden layers and non-linear activation functions are added, the network can represent increasingly complex transformations:

- Starting from a simple **linear boundary**,
- Moving to a **non-linear (e.g., cubic-like) boundary**,
- Eventually representing **very complex, highly non-linear decision surfaces**.

The key idea is that the network’s complexity grows with the number of layers and non-linearities, enabling it to solve tasks that are impossible with single-layer networks.

![[Pasted image 20250928174222.png]]
In a multilabel classification problem, we can assign multiple classes using **more than one output neuron**. For example, consider four classes:

- Class 1: yellow    
- Class 2: red
- Class 3: blue
- Class 4: green
![[Pasted image 20250928174252.png]]

Using **two output neurons** with a sigmoid activation, each neuron can take a value of 0 or 1. This allows encoding the four classes as binary combinations:
$$00, \ 01, \ 10, \ 11$$
The **inner (hidden) layers** perform a non-linear transformation of the inputs, creating **curvilinear decision boundaries** that allow the network to separate these multiple classes in a complex input space.

By combining multiple hidden neurons with multiple output neurons, the network can solve **multilabel problems**, handling complex class distributions that are impossible with a single-layer or single-output setup.

Here I report the computations:
![[Pasted image 20250928174506.png]]

>[!Note] This architecture is not limited to classification; the same principles can be extended to **regression** or other function approximation tasks.

## <span style="color:rgb(239, 179, 1)">Regression with Multilayer Networks</span>

The same multilayer network architecture used for classification can be adapted for **regression** by changing the **output activation function**. Instead of using a sigmoid/logsig activation, which maps outputs to a limited range, we use a **linear activation** to allow outputs to span $(−\infty, +\infty)$.

This setup is useful when:

- The network maps multiple input dimensions to a **single continuous output**.
- Inputs ($x_1, x_2, \dots$) represent features at a specific time point or sample.
- Outputs ($u$) represent the predicted continuous value.

**Example in signal processing:**

![[Pasted image 20250928175105.png]]

1. **Single-sample processing:**

![[Pasted image 20250928175120.png]]
* Two signals, $S_1$​ and $S_2$​, are sampled at a specific time point.
* Compute products and sums of the two signals ($x_1, x_2$​) and feed them as inputs to the network.
* The network performs a mapping, producing outputs with linear activation for regression.
        
2. **Batch processing / multi-sample vectors:**

![[Pasted image 20250928175519.png|300]]
 - Different numbers of elements from $S_1$ and $S_2$​ are sampled.
 - These elements are batched into input vectors ($x_{11}, x_{12}, x_{13}, \dots x_{21}, x_{22}, x_{23}, \dots$).
 - Feed these vectors to the network for processing.
 - The network applies **hidden layer transformations** and produces linear outputs, performing complex signal processing tasks.

**Architecture example:**

- Hidden layers: logsig / tanh
- Output layer: linear
- Inputs: $x_1, x_2, \dots$
- Output: $u$ (continuous value)

This approach allows ANN to perform **time-sample or batch-based signal processing**, computing mappings such as:

- Sample-by-sample products and sums
- Period-by-period norms or differences
- General non-linear transformations on input signals

## <span style="color:rgb(239, 179, 1)"> Function Modeling with Multilayer Networks</span> 

![[Pasted image 20250928180219.png]]

Artificial neural networks can be used to model **functions**, mapping any input $x$ from the function domain to an output $y$ equivalent to $u$  in the co-domain.

**Example architecture:**
- **Inputs:** $x$
- **Hidden layer:** multiple neurons with **logsig activations** ($v_1, v_2, v_3$​)
- **Output:** linear combination of the hidden neurons’ outputs to produce $u$
    

Mathematically, the output can be expressed as:

$$u = v_1 \cdot \text{logsig}(w_1 x_1 + T_1(-1)) + v_2 \cdot \text{logsig}(w_2 x_2 + T_2(-1)) + v_3 \cdot \text{logsig}(w_3 x_3 + T_3(-1)) + T_4(-1)$$

- Each hidden neuron applies a **non-linear transformation** to the input.
- The output layer computes a **linear combination** of these non-linear transformations.
- This allows the network to approximate complex functions by combining multiple non-linear components in a linear summation at the output.

![[Pasted image 20250928180237.png]]


> Key insight: The network maps one domain to another by using **linear combinations of non-linear transformations**, giving it the ability to model complex functions analytically.

