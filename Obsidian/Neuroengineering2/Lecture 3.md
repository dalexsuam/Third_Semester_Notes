
24/10/2025
***
Continuing with 
## <span style="color:rgb(239, 179, 1)">Modelling Single Neurons</span>

### <span style="color:rgb(161, 40, 226)">Adaptive Exponential Integrate-and-Fire (AdEx)</span>
We can further refine the Integrate-and-Fire concept, maintaining low computational cost while better capturing **subthreshold behaviors**. One such model is the **Adaptive Exponential Integrate-and-Fire (AdEx)** model.

![[Pasted image 20251029172935.png]]

The AdEx model includes **two state variables**:

- **Vm** – the membrane potential, and
- **w(t)** – an adaptive current, which is coupled to the membrane potential through the parameter _a_.

==An **exponential term** is added to the membrane potential equation to describe the **initiation and shape of action potentials**. While the Izhikevich model uses a quadratic term for spike initiation, AdEx replaces this with an exponential component, allowing for a smoother and more biophysically realistic spike onset.==

Depending on the parameter values, the ==AdEx model can reproduce a wide range of **electroresponsive properties**== such as adaptation and bursting. ==Additionally, it introduces a **smooth spike initiation zone**==, replacing the strict voltage threshold of the simpler LIF model.

Like the Izhikevich model, the ==AdEx model also accounts for **subthreshold resonances** and **adaptive behaviors**, providing a good compromise between **biological realism** and **computational efficiency**.==
### <span style="color:rgb(161, 40, 226)">Extended-Generalized LIF neuron model (e-GLIF)</span>

To conclude the overview of neuron models, after seeing the Hodgkin–Huxley (HH), the point Leaky Integrate-and-Fire (LIF), the Izhikevich, and the Adaptive Exponential (AdEx) models, we now consider the **Extended Generalized Leaky Integrate-and-Fire (eG-LIF)** model.

This model further develops the LIF framework by including **three ordinary differential equations**:

![[Pasted image 20251029175120.png]]
- one for the **membrane potential**,
- one for the **adaptive current**, and
- one for the **spike-triggered depolarizing current**.
    

The parameters in the model can be grouped into two types:

- **Biological parameters** (shown in blue in the equations), which are derived from experimental data and ensure biological plausibility, and
- **Artificial parameters** (shown in red), which are adjusted during model optimization to reproduce the desired **electroresponsive properties** of specific neuron types.

![[Pasted image 20251029175247.png]]
A key novelty of the eG-LIF model is the introduction of a **refractory period** and **stochastic spike generation**. Instead of using a fixed threshold for firing, the spike occurrence is now **probabilistic** — the closer the membrane potential is to the threshold, the higher the probability of generating a spike. This mechanism provides a more realistic representation of neuronal firing, as it captures the natural variability seen in biological neurons.

The **exponential term** describing spike initiation, already present in the AdEx model, is maintained here to model the **subthreshold dynamics** more accurately. 

![[Pasted image 20251029175353.png]]
After a spike occurs, the membrane potential resets to its resting value, the depolarizing current is set to one, and the adaptive current is incremented, representing the neuron’s **adaptation process**.

Overall, the eG-LIF model balances **biological realism** and **computational efficiency**, while also introducing **stochasticity** to capture the inherent variability of neuronal firing.

# <span style="color:rgb(223, 109, 109)">Model Implementation, Optimization and Validation</span>

Any computational model — whether it represents a single neuron or a more complex system — must go through a **process of development, testing, optimization, and validation**.

1. <span style="color:rgb(2, 141, 192)"><b>Model Development</b>:  </span>
![[Pasted image 20251029180821.png|300]]
    The first step is to design the model itself, defining its structure, parameters, and equations.
    
<span style="color:rgb(2, 141, 192)">2. <b>Characterization and Constraints</b>:  </span>
![[Pasted image 20251029180841.png|300]]
    Next, we must specify the **cell-specific features** that the model should reproduce (for example, autorhythm, resonance, or adaptation) and set **constraints** that the model must not violate.
    
<span style="color:rgb(2, 141, 192)">3. <b>Optimization Phase</b>:  </span>
![[Pasted image 20251029181534.png|300]]
    Once the targets and constraints are defined, we move to **optimization**, which adjusts the model parameters so that the simulated behavior matches the expected neuronal properties.
    Optimization relies on minimizing a **cost function** that combines two main components:
    A **target term**, which measures how well the model reproduces the desired features.      
    A **penalty term**, which prevents the model from violating the defined biological or computational constraints.

**Example: Testing a Neuron Model**

![[Pasted image 20251029180947.png]]
To validate the model, we apply a series of **stimulating input currents** designed to reveal the neuron’s electroresponsive properties:

- **Phase 1 – No stimulation:**  
    The input is zero. Here, the model should reproduce **autorhythm** (if present) and **subthreshold oscillations**.
    
- **Phase 2 – Increasing stimulation:**  
    The input current gradually increases. The model should exhibit:
    
    - an **initial spike frequency**,
    - a **current–frequency relationship** (higher current → higher frequency), and
    - **spike-frequency adaptation**, where the firing rate decreases over time despite constant stimulation.
        
- **Phase 3 – Negative current pulse:**  
    This inhibitory input tests for **post-inhibitory rebound burst**, where the neuron fires a burst of spikes immediately after the inhibition ends.
![[Pasted image 20251029181030.png]]
- **Phase 4 – High-frequency pulses:**  
    Large, brief input pulses are used to verify **phase reset** — how the neuron’s rhythmic firing re-synchronizes after perturbations.
    
- **Phase 5 – Periodic stimulation at different frequencies:**  
    These inputs allow the detection of **resonance**, identifying the preferred frequency at which the neuron responds most strongly.
    
By systematically testing the model under these input conditions, we can **compare its simulated output to expected biological behavior**.  
The model’s **free (artificial) parameters** are then **optimized** until the model reproduces all the required electroresponsive features — ensuring that it behaves like the neuron type it represents.

<span style="color:rgb(2, 141, 192)">4. <b>Model Validation</b>:</span>

![[Pasted image 20251029181816.png|300]]
After the **model optimization** phase, the next crucial step is **model validation**. Validation must not rely only on theoretical or literature-based features, but rather on **experimental electrophysiological data** — typically obtained from **in vitro recordings**.

![[Pasted image 20251029181936.png]]
For example, in the case of **cerebellar Golgi cells**, the model’s simulated responses are compared with real electrophysiological recordings:

- On the **left**, we have the **experimental traces** from in vitro studies.
- On the **right**, the **simulated behavior** of the modeled Golgi cell.
    
When the model is accurate, we can observe that it reproduces key properties such as:
- **Autorhythm** (spontaneous firing),
- **Depolarization-induced bursting**,
- **Post-inhibitory rebound burst**,
- **Subthreshold oscillations**, and
- **Resonance**.

This same validation process can be repeated for **each cerebellar cell type**.  
For instance:
![[Pasted image 20251029182034.png]]
- **Granule cells**,
- **Molecular layer interneurons**,
- **Deep cerebellar nuclei (DCN) cells**,  

each of which displays distinct electroresponsive features. The goal is to **start from the same general model equations** but then:

- Use **biological parameters** obtained from experiments,
- **Optimize the free parameters** through fitting and simulation,

so that each population has its own **tailored model**, faithfully reproducing the behavior of that specific neuronal type.

In this way, instead of having **one universal neuron model**, we build a **family of biologically grounded models** — one for each cell population inside the cerebellum.

## <span style="color:rgb(239, 179, 1)">From Single Neurons to the Cerebellar Microcircuit</span>

![[Pasted image 20251029182212.png]]
Now that we have biologically grounded models for each **neuron type** — granule cells, Golgi cells, Purkinje cells, basket cells, and deep cerebellar nuclei (DCN) cells — we can begin to **model the cerebellar microcircuit**.

At this stage, we can simulate **single neuronal populations**, but that is not yet a full network.  
To move from **individual neurons** to a **functional network**, we need two essential components:

1. **Connectivity data** — defining how the different neuronal populations are connected to each other.
2. **Spatial organization**, or what is called the **scaffold design** — defining _where_ neurons are located and _how_ their spatial arrangement determines their connectivity.
![[Pasted image 20251029182244.png]]

For example, in the cerebellum, the **Purkinje cells** are arranged **transversally** to the **parallel fibers**.  Each Purkinje cell receives inputs from thousands of parallel fibers, but each climbing fiber connects only to a few Purkinje cells (typically 2–4). This spatial geometry is not random; it is **functionally meaningful** and defines how information flows through the microcircuit.

Therefore, the **scaffold** specifies the **rules of connectivity** that depend on spatial relations — for instance, how close two elements must be for a synapse to exist.  
This transforms a set of isolated neurons into a **spatially organized microcircuit** that mirrors the real cerebellar architecture.

Finally, since one of the key roles of the cerebellum is **learning**, our model must also incorporate **synaptic models** and **plasticity rules**.  
In particular, we include **spike-timing–dependent plasticity (STDP)** mechanisms, such as those observed between **parallel fibers and Purkinje cells**, which are **supervised by the activity of climbing fibers**.

Only by combining:

- single-neuron models,
- scaffold-based connectivity, and
- biologically inspired plasticity rules,

can we obtain a **complete computational model of the cerebellar microcircuit** capable of reproducing its functional learning behavior.

## <span style="color:rgb(239, 179, 1)">Spiking Neural Networks and Building the Cerebellar Microcircuit</span>

We model the cerebellar microcircuit as a **spiking neural network** because the units (neurons) emit discrete spikes and the models are grounded on biological data. When building such a network we must decide:

![[Pasted image 20251029225922.png]]
**1. Scale and proportions**  
We downscale real neuron numbers for computational tractability, but we must **preserve the relative proportions** between populations. For example, if mossy fibers are 100 in the model, granule cells should be scaled proportionally (e.g., ≈2,000) because granule cells are numerically dominant. A small number of Purkinje cells (e.g., 24) implements the strong funneling effect: many inputs → few outputs. Each Purkinje cell is associated with one climbing fiber.

**2. Connectivity and scaffold design**  
A network is more than isolated neuron models: we must define **who connects to whom** and **how spatial arrangement shapes connectivity**. In the cerebellum this is critical — parallel fibers run transverse to the Purkinje layer, climbing fibers connect a small group of Purkinje cells, and mossy→granule→parallel-fiber projections preserve somatotopic organization.  
Connectivity therefore has two components:

- **Ordered (topographic)** connections that respect spatial locality, and
- **Sparse (random)** components that increase integration and mixing.  
    Both are needed to reproduce biological information flow.
    
**3. Plasticity rules**  
To model learning, we add **synaptic plasticity**. For the cerebellum this means implementing the **parallel-fiber → Purkinje-cell STDP** supervised by **climbing-fiber** activity (error signal). Plasticity lets the network modify synaptic weights over time and perform predictive, error-driven learning.

**4. Practical note and limitations**  
A given model is an **approximation**: you choose which properties to include (e.g., cortical plasticity only) and which to leave out. Adding features increases realism but also complexity and computational cost. Design choices must balance biological fidelity with available resources and the scientific question at hand.

![[Pasted image 20251029230025.png]]

Now we reach the **final step**: reconnecting our neural models to the full **sensory–motor loop**. 

Our ultimate goal has always been the _brain_ — but the brain never works in isolation. It is part of a closed loop that includes **sensors**, **the controller (the brain)**, and **actuators**.

- **Sensors** gather information from the environment.
- **The brain**, acting as the controller, interprets and transforms this information through a **data-driven, biologically inspired computational model**.
- **Actuators** execute actions back onto the environment, closing the feedback loop.

So far, we have successfully built the **biological controller** — our cerebellar network model. The **inputs** (coming from sensory systems) enter through the _mossy fibers_ and _climbing fibers_, while the **outputs** — the _deep cerebellar nuclei (DCN)_ activity — must be **decoded** to drive actuators. This decoding transforms neural activity into meaningful commands for movement, forming a **functional sensory–motor loop**.

However, at this stage, our model still **lacks a body** — it has no sensors, no actuators, and no interaction with a physical or simulated environment. Without that, we cannot truly test the loop. Therefore, our next essential step is to define **testing protocols**.

### <span style="color:rgb(161, 40, 226)">Why Testing Protocols Are Essential</span>

Testing protocols bridge the gap between **biological models** and **real behavior**. They allow us to evaluate whether our model can reproduce the dynamics observed in living systems under specific tasks or perturbations.

In computational neuroscience, one of the main challenges is the **limited versatility** of our current brain models. To make progress, we focus on **specific behavioral paradigms** — well-defined experimental conditions — and test whether the model reproduces the expected behavior.

For example:

- Start with a **physiological model**, representing normal cerebellar function.
- Compare it to **clinical data** from patients with cerebellar impairments.
- Adjust or “injure” the model (e.g., modifying connectivity between mossy and granule cells) to replicate the observed misbehavior.

This approach provides unique insight: **models offer full access to internal variables** (membrane potentials, synaptic weights, firing rates, connectivity patterns) that are impossible to directly measure in living patients. Hence, they become powerful tools to understand _how_ structural or functional changes may lead to pathological behavior.

### <span style="color:rgb(161, 40, 226)">Connecting to Clinical Testing</span>

To make this link meaningful, **testing protocols** should be inspired by **clinical procedures** used by neurologists to identify cerebellar dysfunctions. These **behavioral tests** (e.g., balance, coordination, or timing tasks) are tightly linked to cerebellar activity and can therefore be translated into simulation protocols.

By applying these same paradigms to our model, we can ask:

- Does the model reproduce normal performance under physiological conditions?
- Does it show impaired performance when cerebellar connectivity or plasticity is altered?

In this way, testing protocols form the **functional bridge** between theoretical models and real-world clinical behavior — transforming our cerebellar network from a purely computational construct into a **tool for understanding and predicting human motor control and pathology**.
 

# <span style="color:rgb(223, 109, 109)">Clinical Testing Protocol I: Eye-Blink Classical Conditioning (EBCC)<br></span>
![[Pasted image 20251029231934.png]]
Let’s begin with the first of the three **clinical protocols** commonly used by neurologists to test cerebellar function: the **Eye-Blink Classical Conditioning (EBCC)** paradigm.

EBCC is a form of **unconscious associative learning**. During this task, the subject is repeatedly exposed to two stimuli presented in close temporal sequence:

- A **conditioned stimulus (CS)** — typically a short auditory tone or _beep_.
- An **unconditioned stimulus (US)** — a mild _air puff_ directed toward the eye.
    
After several paired presentations (beep → air puff), the subject begins to **anticipate** the air puff by closing the eyelid just before it occurs — even when the air puff is omitted. This anticipatory eyelid closure is the **conditioned response (CR)**.

In healthy individuals, the cerebellum learns the precise **timing** between the CS and the US, allowing this predictive behavior to emerge **without conscious effort**. In contrast, **cerebellar patients** fail to acquire this conditioned response: they still blink only _after_ the air puff, reacting reflexively rather than predictively. This absence of anticipatory blinking is a hallmark of **cerebellar dysfunction**.

### <span style="color:rgb(161, 40, 226)">Neural Basis and Cerebellar Circuit Involvement</span>

Neurophysiological studies have mapped the EBCC behavior directly onto the **cerebellar microcircuit**:

- The **conditioned stimulus (CS)** — the auditory tone — reaches the cerebellum via the **mossy fibers**.
- The **unconditioned stimulus (US)** — the air puff — arrives through the **climbing fibers**.
- The **conditioned response (CR)** — the motor command that closes the eyelid — emerges from the **deep cerebellar nuclei (DCN)** as the output of the cerebellar network.
    
This mapping gives us a clear computational correspondence:

- **Input 1:** Beep → mossy fibers
- **Input 2:** Air puff → climbing fibers
- **Output:** Eyelid closure command → DCN activity
    
Thus, EBCC provides an excellent experimental and computational **framework to “give a body” to the cerebellar model** — allowing sensory inputs and motor outputs to interact dynamically through the network.

### <span style="color:rgb(161, 40, 226)">Learning, Extinction, and Reacquisition Phases</span>

A key feature of EBCC is that **learning requires repetition**. The conditioned response does not appear immediately; it is **acquired** through repeated associations of the two stimuli.

This process has two complementary phases:

- **Acquisition:** The learning phase in which the cerebellum gradually establishes the temporal association between the beep and the air puff, producing anticipatory blinking.
- **Extinction:** When the stimuli are no longer paired, the conditioned response fades over time — the subject “forgets” the association.
- **Reacquisition:** Upon re-exposure, the subject relearns the association faster than the first time, indicating memory retention.

In computational terms, these phases depend on the **plasticity rules** embedded in the cerebellar model — specifically the **spike-timing dependent plasticity (STDP)** mechanisms between **parallel fibers** and **Purkinje cells**, modulated by **climbing fiber activity**.

### <span style="color:rgb(161, 40, 226)">Broader Relevance</span>
 
Interestingly, the concepts of **acquisition**, **extinction**, and **reacquisition** in EBCC directly parallel modern challenges in **artificial neural networks** — such as _catastrophic forgetting_. Just like deep networks tend to overwrite previously learned information when exposed to new data, biological systems must balance learning new associations while retaining past ones.

Hence, the EBCC paradigm is not only a **powerful cerebellar diagnostic tool**, but also an **ideal benchmark** for testing computational models of learning and memory — bridging **neuroscience**, **clinical practice**, and **machine learning theory**.

![[Pasted image 20251029233453.png]]

Before proceeding, let’s take a look at this figure. It illustrates how **data-driven spiking neural networks** can bridge the gap between **neurophysiology** and **human behavior**.

At the bottom, we see the **multi-scale approach**, where data flows from detailed recordings of neural activity (on the left) to observed human behaviors (on the right).  
From these data, we build **computational models** that reproduce the neurophysiological mechanisms of brain microcircuits.

These models are then given a “body” — meaning that they are tested through **in silico simulations** and, in some cases, **real robotic implementations**.  
The goal is to generate a **reproduced behavior** and compare it with the **target behavior** observed in biological systems.

This process — starting from biological circuits and moving toward the reproduction of behavior — is called the **bottom-up approach** (as shown by the red arrow).  
We start from what we know about real neurons, build realistic spiking models, and test whether the resulting emergent behavior matches what is observed in humans or animals.

Conversely, the **top-down approach** works in the opposite direction.  
Here, researchers start from a specific behavior, design a neural network (which could even be an artificial neural network) that reproduces it, and then compare its structure and dynamics with biological data.

## <span style="color:rgb(223, 109, 109)">Clinical Testing Protocol II: Vestibulo-Ocular Reflex (VOR)<br></span>
![[Pasted image 20251029233653.png]]
One of the clinical and experimental protocols used to test cerebellar function is the **Vestibulo-Ocular Reflex (VOR)**, which allows us to maintain a stable gaze when rotating the head.

In this case:

- **Mossy fibers** carry the **vestibular input**, related to head movement.
- **Climbing fibers** provide feedback about **retinal slip** — the motion of the visual scene on the retina.
    

Through **learning**, the cerebellum adjusts eye movements so that gaze remains stable despite head rotation.  
This coupling between head motion and eye movement emerges from the **plasticity rules** within the cerebellar microcircuit.

A useful analogy is that of a child playing with a small duck in moving water. At first, the duck is displaced by the water current. After several attempts, the child learns to compensate and guide the duck straight across the flow.  If the current suddenly changes direction, the learned correction initially produces the opposite effect, but after a few more trials, the child adapts again — this illustrates **acquisition** and **extinction** phases of learning.

Similarly, in the cerebellum, the VOR adaptation arises naturally from the activation of synaptic plasticity mechanisms, enabling the system to learn, unlearn, and relearn coordinated motion.

# <span style="color:rgb(223, 109, 109)">Clinical Testing Protocol III: Movements Perturbed by Force-field (FF)</span>

![[Pasted image 20251029233929.png]]

The **third clinical and experimental protocol** used to study cerebellar learning is **force-field motor adaptation**.  
This test examines how the cerebellum enables humans (and other animals) to adapt their movements when the physical environment suddenly changes — for example, when an external force disturbs a voluntary motion.

In this protocol, subjects are asked to perform a simple, well-controlled movement such as reaching with the arm from point A to point B.  
During the first trials, the movement is normal and straight. Then, an **external force field** is introduced (for instance, through a robotic device that pushes the hand sideways).

At first, the subject’s movement becomes curved or distorted because the perturbation is unexpected.  
However, after several repetitions, the cerebellum **learns to predict and compensate** for the external force, and the subject can once again move straight from A to B — even though the disturbance is still present.  
This process is called **adaptation** or **acquisition**.

If the force field is suddenly removed, the learned compensation now produces the opposite effect — the movement overshoots or curves in the other direction.  
With further trials, the subject’s movement returns to normal.  
This second phase is called **extinction**, and if the same perturbation is reintroduced later, **reacquisition** happens faster than the first time.

### <span style="color:rgb(161, 40, 226)">Neural Interpretation</span>

In the cerebellar network model:

- The **mossy fibers** encode information about the **intended motion** and **motor commands**.
- The **climbing fibers** signal **motor errors** — the difference between the intended and the actual movement caused by the perturbation.
- The **deep cerebellar nuclei (DCN)** produce the **corrected output commands**, gradually improving movement accuracy through repeated trials.
    
The **plasticity rules** implemented between parallel fibers and Purkinje cells, under the supervision of the climbing fiber activity, enable the network to **learn these compensations** automatically — just as the brain does.

This task, together with the **Eye Blink Classical Conditioning (EBCC)** and the **Vestibulo-Ocular Reflex (VOR)**, provides a set of **testing protocols** that can be used to validate our **data-driven spiking neural network model of the cerebellum**.  
Each protocol targets a different but complementary function — associative learning, sensorimotor coordination, and motor adaptation — all of which are known to depend critically on cerebellar processing.


***
# <span style="color:rgb(223, 109, 109)">Rehabilitation Robotics</span>

## <span style="color:rgb(239, 179, 1)">Context</span>

Now we are moving to the **second block** of the course. I know it might feel like a complete shift in topic, but be patient — by the end of the course, you will see how everything connects into a coherent picture.

We are now focusing on **rehabilitation robotics**. Previously, we discussed robotics from a **neural perspective**, exploring how robots can model or replicate brain mechanisms.  

Now, we move to how **robots and related technologies** can be _used directly_ in **rehabilitation** — that is, in helping people recover or compensate for lost functions.

![[Pasted image 20251030171756.png]]

Before diving into the technical aspects, let’s look at the **context**.  
We are living in an **ageing society**, something you probably hear about frequently. This demographic shift means that the **working-age population** is decreasing, while the **elderly population** — living longer, often with pensions — is steadily increasing.

Economically, this creates challenges for sustainability.  From a **healthcare** perspective, it means more people are living longer but often **with disabilities**. Many age-related diseases and conditions (such as stroke, heart attack, or trauma) have become more manageable — thanks to major progress in **acute medicine**.

![[Pasted image 20251030171903.png]]

However, surviving an acute event does not always mean full recovery.  
Many people survive but are left with **permanent impairments or disabilities**. Therefore, **rehabilitation** has become an essential component of modern healthcare — not only to improve patients’ quality of life but also to **reduce the societal and economic burden** associated with long-term disability.

![[Pasted image 20251030172535.png]]

The **World Health Organization (WHO)** has launched a major global initiative for rehabilitation, targeting **2030** — which is, essentially, _tomorrow_. This call to action was officially published a couple of years ago, but the planning started around five years earlier.  

The goal was to reassess the **current demand for rehabilitation** and the **organization of rehabilitation services**, which in many countries still operate in almost the same way they did **20 years ago**.  
Clearly, these systems now need deep **restructuring and adaptation** to meet the new social and healthcare conditions.

The **COVID-19 pandemic** further emphasized this need. It revealed the fragility of existing healthcare structures, as all resources were redirected toward managing the pandemic. This left many patients — for example, those recovering from **heart attacks** or **strokes** — without access to proper follow-up care. So, the problem was not limited to COVID-19 itself but extended to the **entire healthcare system**, which struggled to maintain essential services.
![[Pasted image 20251030172649.png]]

In this context, one of the key aspects of the WHO’s rehabilitation reorganization is the concept of **multi-level care**, especially emphasizing **rehabilitation at the point of care** and **rehabilitation at home**.

Let’s go step by step:

- The **point of care** refers to healthcare services provided **closer to where people live** — such as local clinics, pharmacies, or community centers.  
    These centers aim to smooth the transition between **hospital admission** and **discharge**, providing continuity of care across the territory.
    
- At the same time, hospitals should focus increasingly on **specialized, high-level units** dealing with the most complex cases.
    

Ultimately, the goal is to make **rehabilitation accessible even at home**. To understand why this is so important, let’s look at what happens in traditional inpatient rehabilitation. Typically, patients admitted for rehabilitation receive about **one hour of physical therapy in the morning**, perhaps **half an hour of speech or occupational therapy**, and then another **hour or so in the afternoon**.  
So in total, they engage in **two to three hours of therapy per day**.

However, rehabilitation is a **relearning process** — a process that should ideally mimic how **children learn motor control**. Think of a child learning to walk: from the moment they wake up, they continuously explore, move, and learn until they fall asleep. It has been estimated that a 12-month-old child performs around **1,000 sit-to-stand attempts per day**, while in a rehabilitation program, a patient might perform **only 20 repetitions**.

This shows how crucial **intensity** and **continuity** are for effective rehabilitation. That’s why developing **technologies and robotic systems** that can support **rehabilitation at home** — or during the long periods of the day when intensive therapy is not available — can become a powerful **amplifier** of treatment effectiveness, even during hospitalization.


![[Pasted image 20251030173053.png]]

Within the framework of the WHO rehabilitation initiative, a significant publication appeared in _The Lancet_, presenting results from the **Global Burden of Disease Study** aimed at **estimating the worldwide need for rehabilitation**.

![[Pasted image 20251030173119.png]]
One of the main outcomes of this study is shown in this figure.  
Here, you can see data separated by **age groups** — from _under 5 years_ to _over 95 years_ — and by **sex**, with reddish tones representing women and bluish tones representing men.

On the **vertical axis**, we have the _prevalence of disability_, that is, the proportion of the population living with disabling conditions.  
On the **horizontal axis**, we see the _years lived with disability (YLD)_ — meaning the cumulative time individuals spend living with a disability.  
For instance, if a person experiences a stroke at age 70 and passes away at 80, that corresponds to **10 years lived with disability**.

By comparing the two time points — **1990** (left block) and **2019** (right block) — the trend is clear:  there is a **marked shift toward older age groups** and a **significant overall increase** in both the prevalence and the duration of disability.  

In other words, people are living **longer**, but also **spending more years** with conditions that limit their functioning.

Interestingly, this trend appears **very similar between men and women**, highlighting a **universal demographic shift** that reinforces the urgent global need for **rehabilitation services**.

## <span style="color:rgb(239, 179, 1)">Service Robotics</span>

So, how can robots contribute to this picture and help address these growing rehabilitation needs? In fact, we can distinguish **two main targets**.

On one side, ==we have **rehabilitation robotics**== — systems designed to assist clinicians in delivering rehabilitation treatments. The goal here is to **help the patient regain functional independence**, meaning the ability to interact with the environment **without assistance**. In other words, _rehab robots_ support recovery — they are therapeutic tools used to **restore motor function**.

==On the other side, robots can also play a role in the field of **orthotics**==, which aims to **improve function** in people who have permanent motor impairments due to neurological disorders and who cannot properly control their movements when interacting with the environment.  
These technologies are often referred to as **assistive technologies**.

>[!info] The most widespread assistive technology is, in fact, the **wheelchair**. Unlike rehabilitation robotics, **assistive technologies do not aim to recover function**, but rather to **compensate for lost abilities** — for instance, to support mobility or daily activities.

Orthoses are devices designed to work **in cooperation with the intact parts of the body**, either to **control** or **assist** movement.  
This is what distinguishes **orthoses** from **prostheses**, since prostheses _replace_ a missing body part, while orthoses _support_ an existing one.

One of the first major applications of robotics in the orthotic domain came with the development of **exoskeletons**. Originally, exoskeletons were conceived to **enhance the user’s strength**, providing _superhuman_ capabilities.  

![[Pasted image 20251030173750.png]]

This is the case of the **first exoskeleton developed by General Electric in the 1960s**, which weighed nearly **700 kilograms** and was completely inefficient — more of a conceptual prototype than a functional device.

Interestingly — and this may sound a bit surprising — many of the **most advanced exoskeletons** now used in rehabilitation, for both upper and lower limbs, actually **originated from large military research projects**.  
The initial goal was to empower soldiers, but over time, the technology found a far more beneficial application in **rehabilitation medicine**, where it is now used to assist patients in regaining movement and independence.

## <span style="color:rgb(239, 179, 1)">Target Pathology: Stroke</span> 

Let’s now introduce our **target pathology**, and explain why **stroke** is often chosen as the reference condition in rehabilitation and robotic research.

A **stroke** is a **sudden loss of brain function** caused by an **interruption of blood flow** to part of the brain — what we call a **cerebrovascular accident**. This interruption may be due either to a **clot** (ischemic stroke) or a **hemorrhage**, and it deprives brain tissue of oxygen and nutrients, leading to rapid neuronal death.

We focus on stroke because it is **the most common neurological disorder leading to disability**. The vascularization of the brain runs **in parallel between the left and right hemispheres**, so when a vascular interruption occurs in one hemisphere, the resulting deficits are typically **lateralized** — they affect the **opposite side of the body**.

From an engineering perspective, we might refer to a _healthy_ and an _affected_ side, but clinically this is not entirely accurate. Physicians instead describe a _more affected_ and _less affected_ side, since the two hemispheres remain connected and both contribute to movement control through **ipsilateral and contralateral projections**. So, no side is truly “healthy”; one is simply _less impaired_.

### <span style="color:rgb(161, 40, 226)">Stroke Recovery Phases</span>

![[Pasted image 20251030175653.png]]

If we look at the graph, we can see that after the **stroke onset**, there is a **sudden drop in function**. This corresponds to the **acute phase**, when the event occurs and the situation is critical.  
Afterward, during the **post-acute phase** (Stage 2), which lasts roughly **one week to ten days**, the patient stabilizes and the condition is no longer life-threatening.

From there, the patient transitions into **rehabilitation**, which may occur:

- **In hospital** (inpatient rehabilitation),
- **At home** (Stage 3), or
- **Through outpatient services** (Stage 4).
    

The **chronic phase** follows, characterized by slower and more gradual recovery. Even at this stage, **residual disability** often remains, but some improvement may continue thanks to **neuroplastic reorganization**.

This evolution makes stroke a particularly interesting and promising target: it is both **highly prevalent** and **highly recoverable**, especially in the first months after the event. Moreover, many of the **motor deficits following stroke** — such as weakness, loss of coordination, or impaired proprioception — are **shared with other neurological conditions** (e.g., ALS or neurodegenerative diseases). Therefore, technologies designed for stroke rehabilitation can often be adapted for these other populations, increasing their overall impact.


### <span style="color:rgb(161, 40, 226)">Clinical Overview<br></span>
- **Definition:** Sudden loss of brain function caused by interruption of blood flow or hemorrhage. 
- **Incidence:** Immediately after the stroke, about **80% of patients experience hemiparesis** (partial paralysis), and around **35% maintain partial disability** even after rehabilitation.
- **Laterality:** Deficits are **contralateral** to the lesion (opposite body side).
- **Recovery trend:** Typically **exponential** in the first weeks; rapid improvement at the beginning, then slower progress over time.
- **Early recovery mechanisms:** Resolution of **local ischemia, anoxia, diaschisis, and edema reabsorption**.
- **Later recovery mechanisms:** **Cortical and subcortical reorganization**, lasting up to **six months post-stroke**.
- **Chronic phase:** Gradual, low-rate recovery with persistent functional limitations.
    

### <span style="color:rgb(161, 40, 226)">Key Ingredients of Motor Relearning</span>

Effective stroke rehabilitation relies on the following core principles:

![[Pasted image 20251030175849.png]]

- Functional and goal-oriented training
- Biofeedback
- Early intervention
- High amount of practice
- Augmented proprioception
- Exploitation of neuroplasticity
- Rewarding, interactive, and engaging task
- Repetitive training
- Volitional (active) patient contribution
- Individualized therapy
- Continuity of care