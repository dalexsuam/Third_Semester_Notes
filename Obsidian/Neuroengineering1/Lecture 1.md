
***
Date: 18/09/2025

# <span style="color:rgb(223, 109, 109)">Artificial Neural Networks</span> 

## <span style="color:rgb(239, 179, 1)">Introduction</span> 

The human central nervous system (CNS), composed of the brain and spinal cord, contains approximately **100 billion neurons**. These neurons display both morphological and functional diversity and can be classified into various types, such as local interneurons, projection interneurons, motor neurons, sensory neurons, and neuroendocrine cells.

![[Neuron_typologies.png| 300]]

A typical neuron consists of a **cell body** (which includes the nucleus) and two main types of extensions that serve to receive and transmit electrical impulses. Neurons can be classified as **afferent** (carrying information from the periphery to the CNS) or **efferent** (carrying information from the CNS to the periphery).

Among them, **sensory neurons** are morphologically distinct. Their input extensions connect to specialized receptor cells — such as mechanoreceptors, photoreceptors, or nociceptors — through a single input axon, enabling them to detect specific external or internal stimuli.

![[Neuron_interconnection.png|| 300]]

A neuron receives **input signals** through **synapses**, which are located on its dendrites or on the cell membrane. When the combined (summed) input is strong enough to **exceed a threshold**, the neuron becomes activated and generates an **output signal** that travels along its axon. This signal can then reach other synapses and activate additional neurons.

Each neuron can form connections with **up to several thousand other neurons**, and these connections can be either **<span style="color:rgb(2, 141, 192)">excitatory</span>** or **<span style="color:rgb(71, 215, 140)">inhibitory.</span>

- **<span style="color:rgb(2, 141, 192)">Excitatory connections**</span> increase the total summation of the input signal, making it more likely that the neuron will fire.
    
- **<span style="color:rgb(71, 215, 140)">Inhibitory connections</span>** reduce the total effect, making it less likely for the neuron to fire.
    

In a synaptic junction, we distinguish between the **presynaptic neuron**, which sends the nerve impulse, and the **postsynaptic neuron**, which receives it through the binding of neurotransmitters.

The transmission of signals between neurons is mostly mediated by **neurotransmitters**, which are organic chemical compounds. Neurotransmitters are also present at the axon endings of motor neurons, where they stimulate muscle fibers.

There are both **excitatory** and **inhibitory neurotransmitters**, as summarized below:

| **Type of Neurotransmitter** | **Examples**                                                    | **Effect**                                        |
| ---------------------------- | --------------------------------------------------------------- | ------------------------------------------------- |
| **Excitatory**               | Acetylcholine, Noradrenaline, Glutamate                         | Increase likelihood of firing (enhance summation) |
| **Inhibitory**               | Dopamine, Gamma-Aminobutyric Acid (GABA), Serotonin, Endorphins | Decrease likelihood of firing (reduce summation)  |

# <span style="color:rgb(223, 109, 109)">Synthesis of Electro-chemical physiology of the neuron</span> 

The **cell membrane** forms the boundary of the neuron and maintains a voltage difference between the inside and the outside, called the **membrane potential**. The membrane is extremely thin (about 70–150 Å Angstrom) but has a high capacitance (about 1 $μF/cm^2$). It is impermeable to proteins, yet selectively permeable to certain ions, mainly <span style="font-weight:bold; color:rgb(2, 141, 192)">potassium</span> $(K⁺)$, <span style="font-weight:bold; color:rgb(2, 141, 192)">sodium</span> $(Na⁺)$, and <span style="font-weight:bold; color:rgb(2, 141, 192)">chloride</span> $(Cl⁻)$**, through ion channels** embedded in its surface.

## <span style="color:rgb(239, 179, 1)">Resting Potential</span> 

![[Pasted image 20250919074115.png| 500]]

Imagine to take a segment of this neuron and cut it so that you can identify an INTERNAL part of the cell, separated by a MEMBRANE from the EXTERNAL part. Imagine also to take a voltage measurement with two electrodes, and to measure the difference between IN and OUT.  
What you're measuring it' the **resting potential**, of about <span style="font-weight:bold; color:rgb(71, 215, 140)">-70 to -90 mV</span>.

Please note that this ==resting potential is negative==.

At rest, sodium ions are concentrated outside the membrane, while potassium ions are concentrated inside. The **Na⁺ channels** are almost completely closed, whereas the **K⁺ channels** are more numerous and partially open, making the membrane about 50–100 times more permeable to potassium than to sodium.

This imbalance produces a resting membrane potential of about **–70 mV**, close to the **potassium Nernst potential** (≈ –90 mV). To maintain this state, the **sodium–potassium pump** actively exchanges ions, moving Na⁺ out and K⁺ in, using energy from ATP. At this stage, the membrane is said to be **polarized**.

![[Pasted image 20250919074402.png| 500]]

At rest, sodium ions are concentrated outside the membrane, while potassium ions are concentrated inside. The **Na⁺ channels** are almost completely closed, whereas the **K⁺ channels** are more numerous and partially open, making the membrane about 50–100 times more permeable to potassium than to sodium. <span style="font-weight:bold; color:rgb(2, 141, 192)">Think of it as potassium channels having more conductivity in terms of electrical equivalent, or sodium channels having more resistance to the flow of each ions (flow of current)</span>

This imbalance produces a resting membrane potential of about **–70 mV**, close to the **potassium Nernst potential** (≈ –90 mV). 


> [!tip]  Remember that the Nernst potential comes from the Nernst equation in which we compute the semi-element/semi-cell potential (basically, the voltage difference of individual ions) produced between inside and outside of the cell by having into account the concentration of each ions. 
> 
$$
E_{K^{+}} = \dfrac{RT}{zF}\,\ln\!\left(\dfrac{[K^+_{o}]}{[K^+_{i}]}\right)
$$
Where $R$ is the ideal gas constant, $T$ is temperature (So, there is a dependence on temperature), $Z$ is valence number (for potassium $z \rightarrow 1$) and $F$ is Faraday's constant. Then, the semi-element potential for potassium ions is given by this formula and it goes around **-90mV**. 

**Coming back to the rodeo!**

To maintain this resting potential state, the **sodium–potassium pump** actively exchanges ions, moving Na⁺ out and K⁺ in, using energy from ATP. At this stage, the membrane is said to be **polarized**.

## <span style="color:rgb(239, 179, 1)">Action Potential Generation</span> 

When a stimulus depolarizes the membrane beyond a certain **threshold**, the process becomes self-sustaining. 

Before moving on, let's be more explicit. The neuron has a resting potential of ~-70mV and depolarizing it means, making that voltage across the membrane more positive. Let's pretend to apply a negative voltage outside of the cell of -10mV. 

$$
\Delta V= V{i}-V_o
$$
Then, the voltage difference is the voltage inside of the cell minus the voltage outside of the cell. Look that every voltage outside of the cell reduces the voltage difference $-V{o}$ and if this is negative from the very beginning, we would be making this voltage difference more positive.

$$
\Delta V= -70mV - (-10mV) = -60mV
$$
Pretending that now our resting potential is affected by this voltage outside of the cell, we would have depolarized the cell. Making the voltage across it more positive. And if we depolarize it until a certain **threshold** (this threshold can be -60mV or -55mV), the cell keeps depolarizing itself  automatically for a certain time. 

Now, let's look at the different stages

![[Pasted image 20250919082344.png|500]]

1. Depolarization: $Na^{+}$  channels open, and sodium ions rush into the cell, driving the membrane potential toward the sodium Nernst potential (≈ +55 mV). The inside becomes positive relative to the outside. This make sense because if the sodium ions diffuse inside of the cell, the inside of the cell becomes more positive (positives ions is entering the region), and the outside more negative (positive ions are exiting the region). No matter where you see it, the voltage across the cell becomes way more positive
    
2. **Repolarization:** Shortly after, $Na^{+}$ channels close and $K^{+}$ channels open. Potassium ions flow out of the cell (positive ions exiting the inside of the cell, the region becomes negative) restoring negative potential inside.
    
3. **Hyperpolarization:** Because $K^{+}$ efflux temporarily overshoots, the membrane potential becomes even more negative than at rest.


## <span style="color:rgb(239, 179, 1)">Propagation Along The Axon</span> 

The entry of  $Na^{+}$ ions during depolarization spreads to neighboring regions of the membrane, slightly changing their polarity. This triggers adjacent Na⁺ channels to open, repeating the cycle and allowing the **action potential to propagate** along the axon.

If you look at the plot of the triggering of the action potential, you see that there are actually two important time periods (both are not properly reported in it).

* **Absolute Refractory Period:*** It is the time in which the neuron cannot be triggered again by any means to produce any other action potential no matter how strong the external stimulus is. This lasts approximately $2 ms$ and it is the time in which the <span style="font-weight:bold; color:rgb(71, 215, 140)">depolarization and repolarization</span> is taking place
* **Relative Refractory Period:** Here we could make it happen, -make what happen?- Triggering another action potential in the neuron but only if the external stimulus is pretty strong.  This lasts approximately $1 ms$ and it is the time in which the cell is coming back to its resting state during <span style="font-weight:bold; color:rgb(2, 141, 192)">hyperpolarization</span>, with this said, we could conclude the bandwidth of the neuron is of $1 kHz$ (if we take into account the relative refractory period $\dfrac{1}{1 ms}$)

The propagation of the action potential is unidirectional, because it happens at the beginning of the neuron and goes to the end of it through the axon. It doesn't trigger in both directions because the previous segment was already triggered and would be insensitive due to the absolute refractory period.

## <span style="color:rgb(239, 179, 1)">Restoration</span>

Finally, the **sodium–potassium pump** restores the original ion distributions, re-establishing the resting potential so the neuron is ready for the next signal.

In this way, the action potential travels from the **cell body** down the **axon** to the terminals, delivering the neural signal.
## <span style="color:rgb(239, 179, 1)">Measurement timing </span>

![[Neuron-with-myelin-sheath 2.webp|500]]

Here we show a myelinated neuron. Measurements of the properties of a single action potential in an unmyelinated neuron (no presence of myelin sheaths) indicate a duration of only a few milliseconds and a conduction speed of about 25 m/s. 

However, this velocity strongly depends on axon diameter and on the presence of myelin. In myelinated fibers, the propagation speed is typically an order of magnitude higher than in unmyelinated ones. Because of the absolute refractory period, the firing frequency cannot exceed a few hundred hertz, with a minimum frequency of only a few hertz. On average, the action potential duration is approximately 5 ms.

> [!note] 
> <span style="color:rgb(161, 40, 226)"><b>Speed of Signal Transmission</b></span>
>  **Myelinated:** Conducts impulses **much faster** due to **saltatory conduction** — the action potential “jumps” from one **Node of Ranvier** to the next.
>   **Unmyelinated:** Conducts impulses **slowly** because the action potential must propagate continuously along the axon.

It has been observed that face recognition tasks in humans are usually completed within a few hundred milliseconds (less than half a second). This implies that, from sensory input to recognition (a typical perceptual task), neural processing cannot involve more than about 100 serial steps. This principle has been referred to as the _hundred-step rule_. A key consequence is that neural computation must be highly parallel, since each single neural transmission carries the equivalent of only a few bits of information. As a result, knowledge in the brain is distributed across large networks of neural connections.

> [!info] Hundred-step rule  
> Neural processing in the brain cannot exceed ~100 serial steps within the time required for rapid tasks  
> (e.g., face recognition < 0.5 s).  
> → This highlights the need for **parallel computation** and **distributed knowledge representation** in the brain.


# <span style="color:rgb(223, 109, 109)">Computational Model of the Neuron</span> 

## <span style="color:rgb(239, 179, 1)">Basic Concept: Neuron as a Computational Unit</span> 

![[Pasted image 20250918085209.png]]
> [!warning] Neurons don’t vary the amplitude of the action potential to convey information; they do it by varying **how often** they happen and **the precise pattern of their timing**. That’s how they “encode” information.

A **biological neuron** can be seen as a **system that receives input signals** and produces an **output signal**.


Computationally speaking:
 * Inputs in a neuron can be seen as a vector $x=[x_{1},x_{2},x_{3}...]$ called input pattern.
 * Each input has a weight $w_{i}$ that represents its importance:
	 + $w_{i} > 0$: we have an **excitatory contribution**
	 + $w_{i} < 0$: we have and **inhibitory contribution** 
	 + $w_{i} = 0$: Input has no effect.
* Neuron computes a weighted sum of the inputs: $P= \sum_{i=1}^{n} w_{i}x_{i}$
* This is compared to a threshold $T$
* Output ($u$) is computed through an activation function $F$:   $u = F(P-T)$ 

<span style="font-weight:bold; color:rgb(2, 141, 192)">Biologically, this corresponds to:</span> Signal integration in the soma (**weighted sum;** dendrites receive multiple incoming signals) | Threshold comparison (**activation threshold;** the soma *decides* if the integrated signal is strong enough to trigger an action potential) | Generating an action potential along the axon (**activation function;** if threshold is exceeded, an all-or-none electrical signal travels down the axon and communicate with other neurons).

## <span style="color:rgb(239, 179, 1)">First Model: Perceptron</span>

![[Pasted image 20250918085805.png]]

It is the first simple mathematical model of a neuron (Rosenblatt, 1950s-60s).

Within its characteristics are:
* Processes **multiple inputs** and produces **one output**.
* Binary output: activated (1) or not (0) depending on the threshold.
	* Key concepts:
        - **Weighted sum** of inputs
        - **Activation function** to determine output
- Already reflects how a neuron can **classify or map patterns**

==The output of one neuron is:: one number==, many inputs and just one output.

## <span style="color:rgb(239, 179, 1)">Expansion to Neural Networks</span> 

- A **neural network** is formed by connecting many neurons:
    - Output of some neurons becomes input for others.
    - This allows **complex behaviors** not possible with isolated neurons.
        
- **Learning:** the weights $w_{i}$ are adjusted according to a **task**:
    - Classification
    - Regression
    - Mapping from one domain to another

## <span style="color:rgb(239, 179, 1)">Learning Algorithms</span> 

- **Backpropagation:** algorithm to adjust weights to minimize output error.
- 
- Allows training **deep networks** with many layers of neurons:
    - Each layer processes information sequentially
    - Output of one layer → input for the next
    - Feedback and backpropagation improve accuracy

## <span style="color:rgb(239, 179, 1)">Advanced Models</span> 
- **Convolutional Neural Networks (CNNs):** for spatial data like images
- **Recurrent Networks (RNN / LSTM):** handle sequential data, with memory
- **Transformers and LLMs (like ChatGPT):** process complex information, generate outputs, understand language
- Historical evolution: ~80 years from MCP neurons to current LLMs

## <span style="color:rgb(239, 179, 1)">Biological Correspondence</span> 

- <span style="font-weight:bold; color:rgb(161, 40, 226)">Microscopically:</span>
    - Information is encoded not in the amplitude of spikes, but in **frequency and spike patterns**
        
    - Neurons can receive **many inputs and produce one output**
        
    - Output depends on:
        1. **Weighted sum of signals**
        2. **Threshold comparison**
        3. **Activation function** (models refractory period and modulation)
            
- **Interpretation:** computational models **mimic how neurons process information**.

Now just as a way to summarize. We report the step by step.

1. **Input:** vector $x=[x1,x2,...,xn]$
2. **Weighting:** multiply each input by its weight $w_i$ 
3. **Summation:** compute $P= \sum w_{i}x_{i}$​
4. **Threshold comparison:** $P \geq T$  
5. **Activation:** function $F(P-T) \rightarrow u$
6. **Connection to other neurons:** output becomes input for next neurons
7. **Learning:** adjust weights to achieve a specific task
8. **Complex architectures:** deep networks, recurrent, convolutional, transformers

# <span style="color:rgb(223, 109, 109)">MCP Neuron Model (McCulloch & Pitts, 1943)</span> 

**Inputs:** Each input is denoted by $x_i$. Depending on its value, an input can **excite** or **inhibit** the action potential (AP).
        
**Weights:** Each input has an associated weight $w_i$​, which represents the **importance or type** of the connection:
	$w_{i} > 0$: we have an **excitatory contribution**
	$w_{i} < 0$: we have and **inhibitory contribution** 
	$w_{i} = 0$: Input has no effect.
    
**Action potential P:** The neuron sums the weighted inputs.
$P= \sum w_{i}x_{i}$

**Threshold T:** The action potential is compared to an **activation threshold**.
    
**Activation function $F$:**
* In the original MCP model, $F$ is a **binary step function**:
$$
u = F(P - T) =
\begin{cases}
1, & \text{if } P \geq T \\
0, & \text{if } P < T
\end{cases}
$$
This means the output is **1 (fires)** or **0 (no firing)**.
Changing $F$ (e.g., sigmoid, ReLU) drastically changes the neuron’s behavior.
        
**Output:** $u$ (sometimes denoted as $O$ or $U$ for _uscita_, “output” in Italian).
## <span style="color:rgb(239, 179, 1)">Definition</span>

The **McCulloch & Pitts (MCP) neuron** is the first mathematical model of a biological neuron.  It is based on **binary threshold logic units** and was introduced in 1943.

## <span style="color:rgb(239, 179, 1)">Structure</span>

![[Pasted image 20250921213912.png]]

- **Inputs**:
    $x_i$ (state of input neurons)
    
- **Weights**:
    
    $w_i \quad \begin{cases} > 0 & \text{Excitation} \\ < 0 & \text{Inhibition} \end{cases}$
    
- **Summation**:
    
    $P = \sum_{j=1}^{M} w_j x_j$
    
- **Threshold**:
    $T \quad \text{(bias or activation threshold)}$
    
- **Activation function**:  
    Traditionally **binary step function**

	$u = F(P - T), \quad u \in \{0,1\}$

## <span style="color:rgb(239, 179, 1)">Biological Analogy</span>

- **Dendrites** → inputs $x_i$
- **Soma** → summation $P$ and thresholding
- **Axon** → output $u$
## <span style="color:rgb(239, 179, 1)">Properties</span>

- Output is **binary (0 or 1)**
- Can represent **Boolean functions** (AND, OR, NOT, etc.)
- Networks of MCP neurons are equivalent to **finite state machines
## <span style="color:rgb(239, 179, 1)">Limitations</span>

- Cannot solve **linearly non-separable problems** (e.g., XOR) 
- No learning mechanism (weights are fixed, not adapted)

## <span style="color:rgb(239, 179, 1)">Historical Impact</span>

- First **computational model of a neuron** (1943)
- Laid the foundation for **Artificial Neural Networks (ANNs)**
- Modern models extend MCP with:
    - Non-linear activation functions (sigmoid, tanh, ReLU, etc.)
    - Learning algorithms (e.g., backpropagation)

# <span style="color:rgb(223, 109, 109)">Neuron Activation - MCP Model</span> 

## <span style="color:rgb(239, 179, 1)">Effect of Parameters</span>

Changing the **threshold (T)**, the **activation function (f)**, or the **weights ($w_i$)** modifies the behavior of the neuron and, consequently, the entire network.

## <span style="color:rgb(239, 179, 1)">Threshold Binary Unit (MCP)</span>

- **Threshold (T):** real number named threshold of the unit
- **Action potential (P):**

    $P = \sum_{j=1}^{M} w_j x_j = w_1x_1 + w_2x_2 + \dots + w_M x_M​$

- **Activation function (f):** binary
- **Output (u):**
    $u=f(P−T)$

## <span style="color:rgb(239, 179, 1)">Binary Activation Functions</span> 

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Heaviside (Step) Function</span>: 
![[Pasted image 20250921220200.png]]
 **Definition:**
	$f(x) = \begin{cases} 1 & x > 0 \\ 0 & x \leq 0 \end{cases}​$
	  
**Output:**
	$u = f(P - T), \quad u \in \{0,1\}$
	
2. . <span style="font-weight:bold; color:rgb(161, 40, 226)">Signum Function</span>
![[Pasted image 20250921220220.png]]

 **Definition:**
	$\operatorname{sgn}(x) = \begin{cases} 1 & x > 0 \\ -1 & x \leq 0 \end{cases}$
    
**Output:**
	    $\operatorname{sgn}(P - T), \quad u \in \{-1,1\}$


## <span style="color:rgb(239, 179, 1)">Interpretation</span>

- With **Heaviside activation**: neuron output is $0$ (FALSE / inhibitory) or $1$ (TRUE / excitatory).
- With **Signum activation**: neuron output is $-1$ (inhibition) or $+1$ (excitation).
- In both cases, the MCP neuron acts as a **Boolean operator**.
## <span style="color:rgb(239, 179, 1)">Beyond Binary Activation</span>

Relaxing the binary condition, MCP neurons can use other activation functions:

- **Linear activation** → output can assume any real value (**unbounded**)
- **Non-linear activations**:
    - Log-sigmoid (logsig)
    - Hyperbolic tangent (tanh)

These extensions lead to modern artificial neurons in ANN models.

# <span style="color:rgb(223, 109, 109)">Boolean Units</span> 

![[Pasted image 20250921220408.png]]

>[!info] By changing the values of the weights and the threshold we could aim to have different behaviors in the MCP neuron and in the case of the two inputs switching from and OR gate behavior to AND or viceversa.


# <span style="color:rgb(223, 109, 109)">Example: Decision Model (Classifier) Binary Input/Binary Output</span> 

There are the results of a patient of the following tests:
* $x_1$: Level of blood red cells
* $x_2$: Patient temperature
* $x_3$: Breath flow

Now, in order to assign either $drug A \rightarrow u=1$ or $drug B \rightarrow u=0$ 

![[Pasted image 20250922102056.png]]

We must assign a score/weight to each possibility. An in order to obtain the output we must implement as well the step activation function.
![[Pasted image 20250922102126.png]]
The neuron implements:
$$
u = \begin{cases} 1 & \text{if } \sum_j w_j x_j > T \\ 0 & \text{if } \sum_j w_j x_j \leq T \end{cases}
$$

>[!warning] Remember input and output are binary 


# <span style="color:rgb(239, 179, 1)">Decision network: Input 1, Setup 1</span> 

![[Pasted image 20250922102316.png]]

Then, we have here that $x_{1}= Y$ (Logic 1), $x_{2} = Y$ (Logic 1), $x_{3} = Y$ (Logic 1)

And the weights $w_{i}$ and threshold $T$ are assigned as following: $w_{1}= -1.288$,  $w_{2}= 2.729$, $w_{3} = 1.855$, $T=0.633$

$P = \sum_{j=1}^{M} w_j x_j$
$u = F(P - T), \quad u \in \{0,1\}$

$P = x_{1}w_{1} + x_{2}w_{2}+ x_{3}w_{3}$
$P= (1\cdot -1.288) + (1 \cdot 2.729) + (1 \cdot 1.855)$
$P=2.6265$

$u = F(2.6265 - 0.633)$
$u = F(1.9935) \rightarrow u=1$ 
Because the activation function is the Heaviside function, if it is greater than the threshold $T$, we have as output 1.

# <span style="color:rgb(239, 179, 1)">Decision network: Input 2, Setup 1</span> 

![[Pasted image 20250922112831.png]]

Then, we have here that $x_{1}= Y$ (Logic 1), $x_{2} = N$ (Logic 0), $x_{3} = Y$ (Logic 1)

And the weights $w_{i}$ and threshold $T$ are assigned as following: $w_{1}= -1.288$,  $w_{2}= 2.729$, $w_{3} = 1.855$, $T=0.633$

$P = \sum_{j=1}^{M} w_j x_j$
$u = F(P - T), \quad u \in \{0,1\}$

$P = x_{1}w_{1} + x_{2}w_{2}+ x_{3}w_{3}$
$P= (1\cdot -1.288) + (0 \cdot 2.729) + (1 \cdot 1.855)$
$P=0.567$

$u = F(0.567 - 0.633)$
$u = F(-0.066) \rightarrow u=0$

## <span style="color:rgb(239, 179, 1)">Decision network: Input 2, Setup 2</span>

![[Pasted image 20250922174039.png]]

Then, we have here that $x_{1}= Y$ (Logic 1), $x_{2} = N$ (Logic 0), $x_{3} = Y$ (Logic 1)

And the weights $w_{i}$ and threshold $T$ are assigned as following: $w_{1}= -1.288$,  $w_{2}= 2.729$, $w_{3} = 1.855$, <span style="font-weight:bold; color:rgb(161, 40, 226)">T=-0.545</span> 

$P = x_{1}w_{1} + x_{2}w_{2}+ x_{3}w_{3}$
$P= (1\cdot -1.288) + (0 \cdot 2.729) + (1 \cdot 1.855)$
$P=0.567$

$u = F(0.567 - (-0.545))$
$u = F(1.112) \rightarrow u=1$


# <span style="color:rgb(223, 109, 109)">Artificial Neural Network</span> 


An Artificial Neural Network (ANN) can be described as a **2-component system**:

![[Pasted image 20250922174848.png]]
- <span style="font-weight:bold; color:rgb(161, 40, 226)"><b>Primary units</b></span> (neurons, nodes, units):
    - Each one has **input** and **output** lines.
    - The **output** is triggered by an **activation function**.
        
- <span style="font-weight:bold; color:rgb(161, 40, 226)">Interconnection lines</span> (channels):
    - These connect the units.
    - Each line is characterized by a number (weight, connection coefficient, or synaptic effectiveness).
    - The weight quantifies the **relevance and influence** of signals.

## <span style="color:rgb(239, 179, 1)">Interconnections</span> 

![[Pasted image 20250922175335.png]]

The output of one neuron becomes the **input** of another neuron. This forms a **forward network**: signals flow from input neurons to the final output neuron, with each neuron adding processing.
    
- Neurons are considered **units**:
    
    $N_1, N_2, N_3, \dots$

- **Interconnections** are represented by **weights**:

    - Example: the output of $n_1$ enters $n_4$ with weight $w_{41}$.   
    - If $w_{ij} = 0$, then no connection exists between neuron $i$ and $j$.

# <span style="color:rgb(223, 109, 109)">Meaning of Neural Weights</span>
## <span style="color:rgb(239, 179, 1)">Meaning of Neural Weights: Knowledge Representation</span>

![[Pasted image 20250922175335.png]]

In ANNs, **knowledge is represented by weights**. The set of weights can be organized into the **interconnection matrix**:

  $\{ w_{ij} \}$

Symmetry conditions:

$w_{ji} \quad \text{(symmetric network)}$
$w_{ij} = -w_{ji} \quad \text{(anti-symmetric network)}$

## <span style="color:rgb(239, 179, 1)">Meaning of Neural Weights: Distance-Dependent Weights</span>

Assuming that the neurons are arranged into the network according to a spatial criterion (metric domain), it can be assumed that the connection strength (both excitation and inhibition) between two neurons decreases as their inter-distance increases. This kind of neuron interconnection usually leads to an ANN featuring **spatial localization**. ==The connection strength decreases with inter-neuron distance $d_{ij}$.==
    
- A common model:
    $w_{ij} = w_{ij}^0 f(d_{ij})$
- Example with exponential decay:
    $f(d_{ij}) = e^{-\frac{d_{ij}}{\lambda}}, \quad \lambda > 0$ 
- Where:
    - $w_{ij}^0$: baseline connection strength
    - $d_{ij}$: Euclidean distance between neurons $i$ and $j$
    - $\lambda$: decay parameter
![[Pasted image 20250922175850.png]]
# <span style="color:rgb(223, 109, 109)">ANN Architectures</span> 


| ![[Pasted image 20250918093458.png]] | ![[Pasted image 20250918093616.png]] |
| ------------------------------------ | ------------------------------------ |

An alternative way of looking at the architecture of an artificial neural network (ANN) is to imagine neurons arranged in **layers**. In this view, each layer processes the outputs of the neurons in the previous layer. 

Networks organized in this way are traditionally called **feed-forward neural networks (FFNNs)**, because information flows strictly in one direction: from the input layer to the output layer, possibly through intermediate processing steps.

In a feed-forward neural network, the **input layer** is just a set of “slots” where we put the values coming from outside. These input neurons don’t really do calculations—they just pass the numbers into the network. How many input neurons we have decides how many features (or dimensions) the network can take in.

At the other end, the **output layer** gives the final answer of the network. The number of output neurons tells us the size of that answer—for example, one output neuron for a yes/no decision, or several neurons if the network needs to choose among different classes.
![[Pasted image 20250922180812.png]]
Between the input and output, the network may include one or more **hidden layers**. These layers perform intermediate computations on the signals, but their outputs are not directly observable: there is no predefined “correct” output for hidden neurons. (When we talk about supervised learning where we have labels for the inputs) When such hidden layers are present, the network is known as a **multilayer feed-forward neural network**. Each layer $k$ is associated with its own **interconnection matrix** ${w_{ij}}^k$, which specifies the weights linking neurons from the previous layer ($k-1$) to those in the current one.

>[!info] In certain situations, the network may be provided with a **virtual supervisor**—an external reference that specifies what the output should be for a given input pattern. This condition makes it possible to train the network using **supervised learning**, where the ANN adjusts its internal weights to minimize the difference between its actual output and the expected output.

The layered model can also be extended to more general architectures. A **generic interconnected ANN** is not restricted to simple feed-forward links but can include:

1. **Intra-layer connections**, where neurons within the same layer exchange signals.
    ![[Pasted image 20250922181156.png]]
2. **Inter-layer connections with jumps**, where neurons in one layer $k$ project directly to neurons in a layer $k+m$ with $m>1$, bypassing intermediate layers.

![[Pasted image 20250922181221.png]]

3. **Backward connections**, where information flows from a layer $k$ back to a previous layer $k-m$. This introduces feedback and breaks the strictly unidirectional flow of FFNNs.
![[Pasted image 20250922181401.png]]

In summary, the feed-forward network is the simplest form of ANN, with a clear and ordered flow of information. When hidden layers are added, it becomes a multilayer FFNN, capable of more powerful representations. Finally, allowing intra-layer, skip-layer, or backward connections results in a **generic ANN**, capable of modeling much richer and more complex dynamics.

![[Pasted image 20250922181344.png]]

# <span style="color:rgb(223, 109, 109)">Parameters and Hyperparameters of a Neural Structure</span> 

Neural networks are described using two kinds of elements:

### <span style="color:rgb(161, 40, 226)">Parameters</span>
- These are the values the network **learns during training**.
- They include:
    - **Weights**: the strength of the connections between neurons.
    - **Thresholds (or biases)**: values that help shift the activation of a neuron.
### <span style="color:rgb(161, 40, 226)">Hyper-parameters</span>
- These are the settings that **define the architecture of the network**.
- They are chosen **before training** and stay fixed while the network learns.
- Examples:
    
    - The type of network (FFNN, RNN, CNN, …).
    - The number and type of input features.
    - The number and type of outputs.
    - How many layers the network has.
    - The choice of activation functions.

| Parameters of the network | Hyper-parameters of the network          |
| ------------------------- | ---------------------------------------- |
| Weights and thresholds    | Network architecture (FFNN, RNN, CNN, …) |
|                           | Number and typology of inputs            |
|                           | Number and typology of outputs           |
|                           | Number of layers                         |
|                           | Activation functions                     |
![[Pasted image 20250918095109.png]]
- **Parameters** are learned automatically by the network during training.
- **Hyper-parameters** are chosen by us beforehand to define the shape and structure of the network.


# <span style="color:rgb(223, 109, 109)">Typical Applications of ANN</span>

**Pattern classification and recognition**

Goal: assign an input $\mathbf{x}$ to a label $l$.
$l=f(x)$     $\mathbf{x} \in X \subset \mathbb{R}^h$, $l \in C \subset \mathbb{N}$
Example: recognizing handwritten digits, detecting tumors in medical images.
    
 **Function approximation / regression**
 
Goal: approximate a function that maps inputs to outputs.
$\mathbf{y} = f(\mathbf{x})$, $\mathbf{x} \in X \subset \mathbb{R}^h$, $\mathbf{y} \in Y \subset \mathbb{R}^k$
Example: predicting house prices, estimating physiological parameters.

**Data synthesis and compression**

Goal: represent high-dimensional input $\mathbf{x}$ with a lower-dimensional hidden code $\mathbf{h}$.
        
$\mathbf{h} = f(\mathbf{x})$, $\mathbf{x} \in X \subset \mathbb{R}^h$, $\mathbf{h} \in H \subset \mathbb{R}^k$, with $k \ll h$.
Example: autoencoders for image compression, generating synthetic data.

**Time-series forecasting**

Goal: predict the next value of a sequence from its past values.
        
$\mathbf{x}_t = f(\mathbf{x}_{t-1}, \mathbf{x}_{t-2}, \mathbf{x}_{t-3}, \dots)$, with $f$ unknown.
Example: stock price prediction, forecasting patient vital signs.

