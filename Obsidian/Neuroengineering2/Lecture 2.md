
20/10/2025
***

# <span style="color:rgb(223, 109, 109)">Do these models actually exist?</span>

Now that we’ve discussed the **internal models** and how their **interactions** (feedforward, feedback, and prediction) can represent the computational logic of motor control, the next natural question is:  

**Do these models actually exist in the brain?**  

![[Pasted image 20251022183928.png]]

In other words, can we identify **neural structures and physiological mechanisms** that correspond to the **inverse model**, the **forward model**, the **responsibility estimator**, and so on?

To explore this, we now move from _theoretical modeling_ to _neurophysiology_:  we’ll look at which **brain areas** are responsible for performing these computations —  how they communicate, adapt, and coordinate to produce accurate, flexible, and predictive motor control.

# <span style="color:rgb(223, 109, 109)">Brain Areas involved in Motor Control</span>

![[Pasted image 20251022184311.png]]


There are multiple areas in the brain that contribute to motor control, and these areas are **highly interconnected**. As we have seen before, **loops** are essential — the sensory–motor loop ensures that **sensory feedback**, **motor commands**, and **actuation mechanisms** all work in tight coordination within a continuous cycle.

We can highlight the **five main functional loops** involved in motor control:

1. **The spinal loop** (arc reflex)— the most peripheral one, corresponding to the **spinal cord reflex arc**, which allows for rapid, automatic responses to sensory stimuli.
    
2. **The spinal–cortical loop** — connecting the spinal cord with the **motor cortex**, enabling voluntary control and modulation of spinal activity.
    
3. **The cortico–cerebellar loop** — linking the **cortex** with the **cerebellum** through the **thalamus**. This loop is fundamental for **motor coordination**, **error correction**, and **timing**.
    
4. **The cerebello–spinal loop** — through the **brainstem**, allowing the cerebellum to directly influence posture, balance, and fine adjustments in movement.
    
5. **The cortico–basal ganglia loop** — which plays a central role in **movement initiation**, **action selection**, and **motor learning**.
    
![[Pasted image 20251022185029.png]]
The **brainstem** and **thalamus**, although much more than simple relays, can be considered — in a first approximation — as **buffering and transmission hubs**, mediating information exchange among these loops.

# <span style="color:rgb(223, 109, 109)">Primary Motor Cortex</span>
![[Pasted image 20251022201540.png]]

Let’s now go through these brain areas to understand, based on experimental studies, the **roles they play in motor control**.

We start with the **primary motor cortex (M1)**.  
==This is the area from which it is possible to evoke muscle activity with the **lowest possible stimulus intensity**.== In other words, by applying a small stimulation in M1, one can elicit a contraction in a specific muscle — and this is precisely the physiological basis of the **motor homunculus**: a somatotopic representation where each region of the cortex corresponds to a specific part of the body.

However, it’s crucial to understand that this one-to-one mapping is a **simplified representation**. ==When we actually **move** a muscle, we are not just activating a single, isolated cortical area — **many more regions** are co-activated. Likewise, a single cortical neuron can contribute to the activation of **multiple muscles**, and conversely, the activation of one muscle can depend on the activity of **many cortical neurons**.==

Therefore, the apparent one-to-one relationship revealed by minimal stimulation only reflects the **lowest threshold activation**, not the full complexity of cortical organization. This distributed activation is essential for **motor planning**, **coordination**, and **synergistic control** — aspects that would be impossible to achieve with a purely localized representation.

Furthermore,==the primary motor cortex receives **converging inputs** not only from the spinal cord — as part of the spine–cortex loop — but also from the **cerebellum** and the **basal ganglia**==. These pathways provide information related to **error correction**, **movement sequencing**, and **learning**, allowing the cortex to integrate predictive and feedback signals.

In conclusion, while the homunculus is a valid and experimentally reproducible concept, it represents a **useful but oversimplified map** of motor function. The true organization of the motor cortex is **distributed, overlapping, and context-dependent**, reflecting the cooperative nature of cortical control in real movement.

## <span style="color:rgb(239, 179, 1)">Motor Cortex Histological Structure</span>
 
![[Pasted image 20251022202823.png]]
Another key characteristic of the **motor cortex** concerns its **microstructural organization**.  
The motor cortex, like all cortical regions, is organized into **columns of neurons** — this **columnar organization** is the basic structural and functional unit of the cortex. ==Despite the immense complexity and power of the brain’s computational architecture, this organization is **highly regular and repetitive**==, which is precisely what makes it tractable from a computational modelling point of view.

==In total, the motor cortex (1/8 inch thick) contains roughly **six billion neurons**, distributed across these vertical columns. Each column comprises **six distinct layers** , and each layer has **specific connectivity patterns** with other brain regions:==

- **Layer 1**: Contains mainly dendrites and axons that receive **inputs from the periphery** and other cortical areas.
- **Layer 2/3**: Responsible for **cortico-cortical communication**, connecting with other parts of the cortex.
- **Layer 4** (less developed in M1 but prominent in sensory cortex): Typically receives **afferent input** from the thalamus in other cortical areas.
- **Layer 5**: Sends **descending output** signals to the **spinal cord**, **brainstem**, and **pons**, thus directly contributing to motor execution.
- **Layer 6**: Establishes **reciprocal connections with the thalamus**, closing the sensory–motor feedback loop.
    

This laminar and columnar architecture means that **each cortical column functions as a mini-processing unit**, integrating sensory information, internal predictions, and motor output signals.

From a computational standpoint, this **repetition of structure across the cortex** is crucial. It allows us to model cortical function in a more unified and scalable way — the same **computational principles** can be applied across different areas (motor, sensory, associative), even though each region processes distinct types of information.

## <span style="color:rgb(239, 179, 1)">Primary Motor Cortex </span>

![[Pasted image 20251022203817.png]]
Now, let’s try to understand how **motor cortex activation** relates to what we have discussed so far about **motor control** and **the production of motor commands**.  

To do this, we move to **psychophysical experiments** performed on **primates**, such as the one illustrated here. In these studies, small **microelectrode arrays** are implanted into specific areas of the **primary motor cortex (M1)** to record the activity of individual neurons while the animal performs controlled motor tasks.

Now, let’s try to understand how **motor cortex activation** relates to what we have discussed so far about **motor control** and **the production of motor commands**.  
To do this, we move to **psychophysical experiments** performed on **primates**, such as the one illustrated here. In these studies, small **microelectrode arrays** are implanted into specific areas of the **primary motor cortex (M1)** to record the activity of individual neurons while the animal performs controlled motor tasks.

It is essential to clarify a key point:

> When we observe that a specific neuron is active during a given task, we can only conclude that **this neuron contributes to that task**, not that it is the **only** neuron responsible for it.  
> Motor functions are distributed — each movement is the result of **populations of neurons** acting together, not isolated activations.

In this particular experiment, an **M1 neuron** from the **wrist area** was recorded while the primate performed a **pole-rotation task**. The movement always started from **extension to flexion**, with identical kinematics across three different **load conditions**:

1. **No external load**
2. **A load opposing** the flexor muscles (resisting the movement)
3. **A load assisting** the flexor muscles (helping the movement)
    

As expected, the **EMG recordings** of the **flexor** and **extensor** muscles show modulation depending on whether the external load assists or resists the movement:

- In the **neutral condition** (no load), the **extensors** deactivate right after the **go signal** (vertical line on the right plots), and the **flexors** activate to produce the flexion.
- When the **load resists** the flexors, the extensors are no longer needed to maintain the initial posture, but the flexors must **increase their activity** to overcome the opposing force and complete the task.
- When the **load assists** the flexors, the opposite happens — the flexor activation is **reduced** because the external force contributes to the motion.
    
Despite these differences in muscle activation, the **overall movement kinematics** — the trajectory and timing — remain almost identical.

This experiment provides a clear demonstration that **motor cortex neurons are not merely encoding movement trajectories**, but rather **encode the dynamic parameters** of the movement — such as **force, load compensation, and muscle activation patterns** — depending on the context.

![[Pasted image 20251022204231.png]]
Now, let’s look more closely at what happens **in the recorded motor cortex neuron**.

First, note that the neuron’s activity begins **before** the go-signal — this **anticipatory activation** reflects **motor planning**. Since the monkey has been trained for this task, it can **predict the upcoming movement** and prepare the necessary motor commands even before execution. This shows that motor cortex activity is not purely reactive; it also contains **predictive components** related to movement preparation.

Next, we can clearly observe that the **firing pattern of this neuron** changes significantly across the **three loading conditions**, even though the **joint kinematics** — the angular change of the wrist — are **identical** in all of them.

This is an important finding:

> It means that the neuron is **not encoding the joint position or movement trajectory**, but rather the **force direction and intensity** required to perform the movement.

So, the **same movement**, performed under **different mechanical contexts**, produces **different patterns of neural activity** in M1.

In other words, **motor cortex neurons encode movement dynamics (forces, torques, and muscle activations)** rather than just kinematic variables (like angle or position).

This observation strongly supports the idea that the **motor cortex participates in the control of movement execution**, not simply in describing spatial motion — it is involved in **computing the necessary forces** according to the internal models and sensory feedback we discussed earlier.

![[Pasted image 20251022204558.png]]
In this second experiment, the primate performs **three distinct grasping tasks**:

1. a **light precision grip**,
2. a **strong (heavy) precision grip**, and
3. a **power grip** on a handle.

Electromyographic (EMG) recordings show that **the same muscle groups** are recruited in all three cases, with only **moderate differences in amplitude** — meaning that, from a purely muscular perspective, the tasks are quite similar.

However, when we record the activity of **specific neurons in the primary motor cortex (M1)**, we find something much more striking:  

some neurons are **highly active** during the **precision grip**, but become **almost completely silent** during the **power grip**, and vice versa.

This demonstrates that **motor cortex neurons do not merely encode muscle activity or joint motion**.  Instead, they encode **higher-order aspects** of the movement — such as the **goal**, the **required accuracy**, or the **type of manipulation** being performed.

So, even though the biomechanical activation (the EMG) remains broadly similar, the **cortical representation changes dramatically** depending on **the intent and context** of the action.

This shows that **the motor cortex encodes movement semantics** — the _purpose_ or _strategy_ of an action — rather than simply its mechanical execution.

In short:

> M1 neurons reflect not only _how_ we move, but _why_ we move that way.

This experiment bridges the gap between **low-level control (force, direction)** and **high-level motor planning (task goal, precision vs. power)**, highlighting that M1 is part of a **hierarchical system** where neurons are tuned to progressively more abstract features of behavior.

## <span style="color:rgb(239, 179, 1)">Spike Raster Plot</span>
![[Pasted image 20251022205343.png]]
In this experiment, several **neurons in the primary motor cortex (M1)** of a monkey were recorded using microelectrode arrays while the monkey performed a **center-out reaching task** — moving a manipulandum (a handle) from a central position toward one of several targets arranged around it (e.g., left, right, up, down, diagonal directions).

Each raster plot represents **spike times** (short vertical ticks) of individual neurons, aligned to the **go signal** (the cue to move).  On the x-axis: time (from 1 second before to 1 second after the go signal).  On the y-axis: repetitions of the same movement.

![[Pasted image 20251022205931.png]]
Looking at individual neurons:

- Some neurons fired **more strongly** for certain directions (e.g., left or forward).
- The same neurons were **less active or silent** when the movement was toward the opposite direction (e.g., right).
    
However, **no single neuron** was perfectly selective for one single direction.  Each neuron had a **preferred direction**, but also fired to some extent for nearby directions.

So, a single neuron doesn’t uniquely determine the direction of movement — it provides only a _partial contribution_.

Georgopoulos (the author of the experiment) realized that **the brain does not encode movement direction using single neurons**, but through the **combined activity (population vector)** of many neurons.

![[Pasted image 20251023174647.png]]
Each neuron can be represented as a **vector**:

- Its **direction** corresponds to the neuron’s preferred movement direction.
- Its **amplitude (length)** corresponds to how strongly that neuron fires in the current trial (its firing rate).

By summing all these vectors across the recorded neurons, you get a **population vector** — the **weighted average** of all neural activities.

When Georgopoulos computed this **population vector**, he found that:

- The resulting vector pointed **very accurately** in the direction of the actual arm movement.
- Even though each neuron was “noisy” or broadly tuned, their collective activity encoded the precise movement direction.
    
This means that **the motor cortex represents movement direction as an emergent property** of the entire neural population — not as the output of a single neuron.

### <span style="color:rgb(161, 40, 226)">Why is the zero-degree vector slightly misaligned?</span>

Excellent question — and you already gave the right intuition.

There are several plausible reasons:

- **Experimental noise**: only a limited number of neurons were recorded; a larger sample would average out the variability.
- **Neuronal sampling bias**: the recorded neurons might not have been evenly distributed in their preferred directions.
- **Nonlinearities** or **drift** in the monkey’s behavior or electrode recording.
- **Biological variability**: cortical coding is never perfectly symmetric — and that’s normal.
    

So small misalignments like at 0° don’t invalidate the finding — they actually make it more realistic.

## <span style="color:rgb(239, 179, 1)">Summary</span>

From these few highlights on the motor cortex, we can say that it works on two levels. 

* The first level is the **one-to-one association**, represented by the **motor homunculus**, where specific cortical areas correspond to specific body parts. 
* The second level involves **high-level control**, where groups of muscles are coordinated depending on factors such as direction, force, target, precision, or type of grip.

This means that the motor cortex has a **dual role** — it handles both detailed, low-level muscle control and broader, high-level movement organization. Moreover, **training and practice** can modify both levels. For example, in a pianist, the cortical areas controlling the hands can change significantly, showing that learning reshapes how movements are represented in the brain.


# <span style="color:rgb(223, 109, 109)">Spinal Cord</span>

![[Pasted image 20251023180026.png]]
The **spinal cord** is another crucial structure. You may already know that it is organized by levels — for example, the **cervical** region controls the arms, the **thoracic** region affects the trunk, and around **L1–T1** we find control of the lower limbs. This organization explains why **spinal cord injuries** at different levels lead to different types of impairments, such as paraplegia or tetraplegia.

In addition to this vertical organization, there are also **functional spatial patterns** within the spinal cord. **Motor neurons** that activate **flexor muscles** are located posteriorly to those controlling **extensors**, and neurons for **distal muscles** are found more **laterally** than those for **proximal muscles**.

==There are two major descending pathways: the **pyramidal (corticospinal) tract** and the **extrapyramidal tract**. The **pyramidal tract**, located laterally, directly connects to motor neurons and mainly controls **fine movements** of distal muscles — essential for walking and voluntary limb actions. The **extrapyramidal tract**, which runs medially, passes through various nuclei and is primarily involved in **postural control** and **axial muscle coordination**.==

![[Pasted image 20251023180508.png]]

So here you can see the same special organization of the spinal cord. 


![[Pasted image 20251023180654.png]]
The **spinal cord** has been shown to be essential for several ==**cyclic motor tasks** — movements that repeat rhythmically and are fundamental for life. These include not only **walking**, but also **chewing**, **breathing**, and **eye saccades**, which are crucial for vision.==

==These **rhythmic tasks** combine **voluntary triggers** with **reflex-based patterns**. Typically, the **initiation** of the movement is voluntary, while the **continuation** — the repetitive or cyclic part — is controlled by **spinal interneurons**. This control mechanism is often attributed to **central pattern generators (CPGs)**, which are not specific anatomical structures but rather **functional neural circuits**.==

Experimental evidence suggests that **brainstem neurons** play a key role in generating and modulating the oscillations that underlie these rhythmic activities.

# <span style="color:rgb(223, 109, 109)">Supplementary Motor Areas</span>
![[Pasted image 20251023181344.png]]

The **supplementary motor area (SMA)** is part of the cortex, located more **frontal** compared to the **primary motor cortex (M1)** and the **primary somatosensory cortex (S1)**.

Much of what we know about M1 and the spinal cord comes from **animal experiments** and **patients with spinal cord injuries**, but the information about the SMA mainly comes from **functional magnetic resonance imaging (fMRI)** studies.

Do you know what **fMRI** is? It allows us to measure the **oxygenation levels** in different brain areas while a person performs a task. This is based on the **BOLD signal** — the _Blood Oxygenation Level Dependent_ signal — which provides an **indirect measure of brain activity**. The assumption is that when a brain region is active, it consumes more oxygen, so detecting changes in oxygen levels lets us infer which areas are working.

Because this is an **indirect and statistical measurement**, fMRI is much **slower** than recordings from electrodes that capture fast neuronal activity. However, its main advantage is that it can be performed **non-invasively in humans**.

Now, let’s look at a classic experiment.  When a subject performs a **simple finger movement**, we see activation mainly in **M1** and **S1**, while the **SMA** remains almost inactive. But when the subject performs a **finger-tapping sequence** — a coordinated and rhythmic movement involving several fingers — the activation of M1 and S1 remains, and a **strong activation appears in the SMA**. This suggests that the **SMA is crucial for timing, coordination, and sequencing** of complex movements.

Even more interestingly, when a person **imagines** performing the finger-tapping sequence — without moving at all — the **SMA still becomes active**, much like during real execution. This shows that the SMA is also involved in **movement planning and mental rehearsal**.

This mechanism is related to **mirror neurons** — neurons that activate both when we perform an action and when we observe someone else doing it. It helps explain why **learning by observation** is so powerful.

In **rehabilitation**, especially for **stroke patients**, this principle has been used to improve recovery. During the early stages, when movement is difficult or unsafe, patients can be shown **videos of specific tasks**. This **observation-based training** stimulates the SMA and related motor areas, potentially **enhancing neural recovery** before physical therapy even begins.

# <span style="color:rgb(239, 179, 1)">Basal Ganglia</span>

![[Pasted image 20251023183257.png]]

The **Basal Ganglia** form a very **complex subcortical network** made up of several nuclei — including the **caudate nucleus**, **putamen**, **subthalamic nucleus**, and **substantia nigra**, among others. Even though we often refer to them as a single structure, they are actually a **highly interconnected circuit** located deep within the brain.

Functionally, the Basal Ganglia are involved in ==**reward processing, motivation, learning, and task selection**. They play a crucial role in **reinforcement learning**, where **reward and frustration** guide the acquisition of new motor skills.==

This aspect is especially important in **rehabilitation**. For example, when a patient repeatedly fails a movement due to an impairment, it’s not just a matter of losing motivation — the **reward-related circuits** in the Basal Ganglia are not being properly engaged, which limits relearning.

This is one reason why **robot-assisted rehabilitation** can be so effective: the robot helps the patient successfully complete a movement, **triggering the sense of reward** that activates these neural circuits and reinforces learning.

In addition, ==the Basal Ganglia act as a kind of **filter or selector**, deciding **which actions should be initiated or inhibited**.==

Clinically, this region is also significant because it’s the **target of deep brain stimulation (DBS)** used to treat **Parkinson’s disease**, typically involving the **globus pallidus** or the **subthalamic nucleus**, depending on the patient’s condition.


![[Pasted image 20251023184334.png]]


When we look at the **mechanisms of learning in the brain**, we can distinguish different types of learning processes depending on the involved structures.

The **cerebral cortex** mainly operates through **unsupervised learning**, meaning it learns by **detecting patterns and grouping activities** based on experience and repeated exposure, without explicit feedback.

In contrast, the **Basal Ganglia** are strongly associated with **reinforcement learning**, where **rewards and punishments** guide behavior. This mechanism allows the brain to strengthen the actions that lead to positive outcomes and suppress those that do not.

Next, we will see the role of the **Cerebellum**, which is primarily involved in **supervised learning** — a process where learning occurs through **explicit feedback about errors**, allowing fine-tuning and correction of movements.

![[Pasted image 20251023184524.png]]

We start from the body — the musculoskeletal system.  There is sensory feedback that goes through the sensory systems to the spinal cord via sensory fibers. Within the spinal cord, there are reflexes that send signals directly back to the muscles.

From there, sensory feedback also travels to the thalamus, which sends information to the cortex. Some of this feedback also goes directly to the inferior olive, which is strongly connected with the cerebellum (we’ll see this part later).

Going higher, sensory feedback reaches the parietal cortex, the posterior parietal cortex, and the somatosensory cortex. All of these areas are connected with the motor cortex.

The premotor cortex receives sensory feedback and sends information to the motor cortex.  
Then, the motor cortex sends signals through different nuclei — for example, the red nucleus — and from there, directly to the spinal cord and then to the muscles.

Additionally, the motor cortex also communicates with the cerebellum, which itself sends outputs to the spinal cord and muscles.

Finally, there is also a feedback loop between the cerebellum and the cortex, making the system quite complex overall.

# <span style="color:rgb(223, 109, 109)">Cerebellum</span>

Now we focus on the cerebellum, as we move toward the modeling part of computational neuroscience.

So, why the cerebellum?  
==The cerebellum contains about half of all the neurons in the brain. It receives around **40 times more inputs than the outputs it produces**, which means it performs a kind of **irreversible processing** — receiving a huge amount of information and filtering it into a much smaller, refined output.==

The cerebellum receives information about:

- The **objectives** of motor actions (the targets),
- The **motor commands**, and
- The **sensory feedback** coming from the spinal cord.

==As for its **output**, it projects to the **premotor and motor areas** of the cerebral cortex, and also from the **brainstem** to the **spinal interneurons** and **motor neurons**.

One of the most important features of the cerebellum is its **high level of plasticity**. The connections between cerebellar neurons are strongly modulated over time, meaning that the cerebellum plays a key role in **learning processes**.

Even though it represents only about **10% of the brain’s total mass**, the cerebellum contains **more than half of its neurons**. Interestingly, if its surface were unfolded, it would make up about **80% of the brain’s total protein content**.

![[Pasted image 20251023211048.png]]
 
The **cerebellum** is a small structure located at the back of the brain.
 
| ![[Pasted image 20251023211507.png]] | ![[Pasted image 20251023211327.png]] |
| ------------------------------------ | ------------------------------------ |
It is organized into **two hemispheres** and a **central part** called the **vermis**. In addition, it includes three main lobes:

- The **anterior lobe**,
- The **posterior lobe**, and
- The **flocculonodular lobe**, which is located more internally.

In the images, you can see the cerebellum and its **cortex**. If you imagine the cerebellar cortex unfolded and flattened, it would look like the diagram shown here. The actual cerebellum, however, is folded in three dimensions — what we see is a **transversal section**.

There are two main fissures:

- The **primary fissure**,
- The **horizontal fissure**.
    
These fissures can be seen in different orientations depending on the view, but they correspond to the same anatomical structures.

![[Pasted image 20251023212150.png]]
 
Now, let’s look at the central part of the cerebellum.  
The **medial region** is called the **spinocerebellum**. It includes a central structure known as the **vermis**, which connects with the **medial descending systems**. The **intermediate zones** connect with the **lateral descending systems**. Both regions play an important role in **motor execution**.

The **lateral hemispheres** are part of the **cerebrocerebellum**. They connect through the **dentate nucleus** to the **motor planning areas** of the cerebral cortex, particularly the **motor cortex**.

Finally, the **vestibulocerebellum**, which corresponds to the **flocculonodular lobe** located in the innermost part of the cerebellum, is responsible for **balance** and **eye movement control**, contributing to **vestibular regulation**.


![[Pasted image 20251023212517.png]]
 The **cerebellum–cerebral cortex loop** is a very important pathway. It performs a kind of **filtering** and **irreversible processing** of information.

From the **cerebral cortex**, around **40 million fibers** (called _cortico-pontine fibers_) project toward the cerebellum through the **mossy fibers**.

Inside the cerebellum, this massive input is processed by the **granule cells**, which are the most numerous neurons in the brain. These granule cells expand and distribute the input signal widely within the cerebellar cortex.

From the granule cells, the information is then funneled down to about **15 million Purkinje cells**. These Purkinje cells integrate the processed input and send inhibitory signals to the **deep cerebellar nuclei (DCN)** — which represent the **main output** of the cerebellum.

Finally, the output from the DCN travels through the **thalamus** and back to the **cerebral cortex**, completing the **cerebellum–cerebral cortex loop**.
 

![[Pasted image 20251023213041.png]]

**fMRI studies** have shown that the **cerebellum** is activated during a wide variety of tasks and functions.

About **20 years ago**, the cerebellum was mainly associated with **motor control** and **motor learning**. However, over time, research has revealed that it also plays a major role in **cognitive** and **social** functions.

These include:

- **Attention regulation**,
- **Mathematical reasoning**,
- **Language processing**,
- **Verbal fluency**,
- **Word comprehension**, and
- **Memory recall**.

Overall, the cerebellum is a very interesting and crucial part of the brain, involved in many different aspects of both movement and higher-level mental functions.
 
![[Pasted image 20251023213252.png]]
If the **cerebellum** is removed, we can observe very different patterns of activity in several motor pathways — such as the **reticulospinal**, **vestibulospinal**, and **rubrospinal** pathways — especially while a person is walking.

Interestingly, even **after the removal of the cerebellum**, a patient can still **walk**, although the activity within these pathways changes significantly.

There is also a known case of a **child born without a cerebellum**, who reached the age of 14. The child was somewhat **clumsy** and **not very athletic**, but was still able to **live a normal life**.

This shows how much we still **don’t fully understand** about the cerebellum. The picture we have is **far from complete**, and it’s important to keep that in mind as research continues.

![[Pasted image 20251023213807.png]]
The **cerebellum**, just like the cerebral cortex, has a layered organization, but its internal structure is much simpler and very repetitive. This means that the same basic circuit is repeated throughout the entire cerebellum. Because of this clear and consistent organization, the cerebellum has become one of the most studied structures in the brain and one of the best understood in computational modeling.

Inside the cerebellum, the **microcircuit** is built from only a few types of neurons that are connected in a precise and repetitive pattern. The main cell types involved are **granule cells**, **Golgi cells**, **Purkinje cells**, **deep cerebellar nuclei (DCN)** neurons, and some interneurons such as **basket cells** and **stellate cells**.

The cerebellum receives **two main sources of input**: the **mossy fibers** and the **climbing fibers**. Each of them carries different kinds of information and follows a different path through the microcircuit.

#### The Mossy Fiber Pathway

The **mossy fibers** bring sensory and motor information into the cerebellum. These fibers make **excitatory synapses** with the **granule cells**, which are extremely numerous — in fact, they are the most common type of neuron in the brain.

Each granule cell then sends out a thin axon that travels upward and splits into two branches running in opposite directions across the cerebellar cortex. These long horizontal fibers are called **parallel fibers**.

The **parallel fibers** spread out and pass through the **dendritic trees** of the **Purkinje cells**, forming thousands of small synaptic contacts along the way. This structure means that the cerebellum is not only organized in layers but also has a **spatial organization**, where the inputs and outputs are arranged in a very regular pattern.

Many **Purkinje cells** can receive signals from the same set of parallel fibers, so there is a kind of **transversal organization** — parallel fibers run in one direction, and the dendrites of Purkinje cells extend perpendicularly to them.

After integrating all these inputs, the **Purkinje cells** send their signals to the **deep cerebellar nuclei (DCN)**. These nuclei are the **main output centers** of the cerebellum, and from here the processed information is sent out to other brain areas.
#### The Climbing Fiber Pathway

The **second input** to the cerebellum comes from the **climbing fibers**, which originate in the **inferior olive (IO)**.

Each climbing fiber forms a very strong connection with only a small number of Purkinje cells. They are called “climbing” fibers because they literally **wrap around the dendritic branches** of the Purkinje cells, making many contact points as they climb up. This gives each Purkinje cell a very powerful and specific input signal from the inferior olive.

So, while the mossy fibers provide **broad, distributed input**, the climbing fibers provide a **focused, precise input**, allowing the cerebellum to combine both detailed and widespread information.
#### Interneurons and Regulation

To keep the network balanced, the cerebellum also includes several types of **inhibitory interneurons**: **Golgi cells**, **basket cells**, and **stellate cells**.

These interneurons don’t produce the main output themselves but instead **modulate** the activity of the granule cells and Purkinje cells. They act like local regulators that **fine-tune** and **stabilize** the flow of activity through the microcircuit, preventing it from becoming too excited or unstable.

In summary, the cerebellar microcircuit works as a finely tuned processing system:

- **Mossy fibers** bring in massive amounts of input to the **granule cells**.
- The **parallel fibers** distribute this information widely to **Purkinje cells**.
- The **climbing fibers** deliver strong, precise signals from the **inferior olive** directly to the same Purkinje cells.
- The **Purkinje cells** integrate all of this information and send the processed signal to the **deep cerebellar nuclei**, which then form the **output of the cerebellum**.
- Meanwhile, **interneurons** constantly adjust and balance the activity inside the network.

This simple yet elegant organization — repeated throughout the entire cerebellum — allows it to perform extremely complex functions with a relatively uniform internal design.


![[Pasted image 20251023214953.png]]
Looking again at the cerebellar **microcircuit**, we can see how the different neuron types are arranged within the layers of the cerebellar cortex.

The **mossy fibers** enter the cerebellum and make connections with the **granule cells**. These granule cells are **extremely numerous** — there are millions of them — and they are very small. They are located in the **granular layer**, which is the **deepest layer** of the cerebellar cortex.

Each granule cell sends an axon upward from the granular layer into the **molecular layer**, where it branches into long **parallel fibers**. These fibers run horizontally across the cerebellar cortex within the molecular layer.

In this same molecular layer, we find the **Purkinje cells**, whose **cell bodies (soma)** lie in a distinct middle layer called the **Purkinje cell layer**. Their large **dendritic trees** extend upward into the molecular layer, where they intersect with the parallel fibers.

The **climbing fibers**, coming from the **inferior olive**, also reach the Purkinje cells, wrapping around their dendritic branches. This means that Purkinje cells receive two kinds of input:

- From the **parallel fibers** of the granule cells, and
- From the **climbing fibers** of the inferior olive.
    
Within the molecular layer, there are also **molecular interneurons** — the **basket cells** and **stellate cells** — which help regulate the activity of the Purkinje cells.

In the **granular layer**, we also find another type of interneuron, the **Golgi cell**, which interacts with the granule cells and helps control their level of activity.

Altogether, this layered and highly ordered structure allows the cerebellum to process large amounts of information in a very organized and efficient way.

![[Pasted image 20251023215306.png]]
In this schematic representation, we can summarize how the main elements of the cerebellar microcircuit interact.

The **mossy fibers** provide **excitatory input** to the **granule cells**. Then, the granule cells send their axons upward, forming the **parallel fibers**, which in turn **excite the Purkinje cells**.

Along this pathway, we also find several **inhibitory interneurons** — the **basket cells**, **stellate cells**, and **Golgi cells**. Their role is to **control and balance** the overall activity of the network. Without them, the continuous excitation could make the system “explode,” meaning it would become overactive and unstable. The inhibitory cells therefore keep the signals regulated and prevent excessive activity.

The **Purkinje cells**, after integrating all their inputs, send **inhibitory outputs** to the **neurons of the deep cerebellar nuclei (DCN)**, which represent the **main output** of the cerebellum.

In parallel, the **climbing fibers** connect **directly** to the **Purkinje cells**, wrapping around their dendrites and providing powerful, specific excitatory inputs.

The **mossy fibers** themselves originate from **nuclei in the spinal cord and brainstem**. They carry both **sensory information** from the body and **motor command signals** from the cerebral cortex.

In simple terms, the cerebellar microcircuit receives **feedback from sensory systems** and **commands from motor areas**, combining these inputs to refine and coordinate movement — this is part of what’s known as the **efferent pathway** of the cerebellum.


![[Pasted image 20251024100104.png]]

The **climbing fibers** originate from the **inferior olive**. They carry a mix of **somatosensory**, **visual**, and **cerebral cortical** information to the cerebellum.

These fibers form **excitatory synapses** directly on the **Purkinje cells**, but the type of signal they produce is very different from the one generated by the **parallel fibers**.

If we zoom in on a single **Purkinje cell**, we can see that it receives two main kinds of input:

1. From the **parallel fibers**, which come from **granule cells** (these granule cells, in turn, receive input from **mossy fibers**).    
2. From a **single climbing fiber**, which wraps around the dendritic tree of that Purkinje cell.

It’s important to remember that **each Purkinje cell is connected to only one climbing fiber**, while it can receive signals from **thousands of parallel fibers**. This combination allows the Purkinje cell to integrate both broad, distributed information (from parallel fibers) and very specific, powerful signals (from the climbing fiber).


![[Pasted image 20251024100214.png]]
Here we can see recordings of **Purkinje cell activity**. The electrical signals recorded from these cells show two distinct patterns, depending on which input is active.

| Simple Spikes                        | Complex Spikes                       |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251024101030.png]] | ![[Pasted image 20251024101016.png]] |

When the **parallel fibers** are active, the Purkinje cell produces signals called **simple spikes**.

- These are **high-frequency** signals that occur **very often**, forming a continuous stream of activity.
- They represent the regular flow of information coming from the mossy fiber–granule cell–parallel fiber pathway.
    

On the other hand, when the **climbing fiber** becomes active, the Purkinje cell generates a completely different type of signal known as a **complex spike**.

- Complex spikes appear **less frequently** and at a **much lower rate** than simple spikes.
- Each complex spike is directly linked to the activation of a climbing fiber.
    
To visualize the difference, imagine you are at a show before it starts. People are chatting, walking around, placing their bags — there’s a constant background of small noises and movements. That’s like the **simple spikes**: many small, frequent signals carrying ongoing information.

Then, when the show is about to begin and someone says “Let’s start,” there’s a noticeable change — a distinct event that stands out from the background. That’s like a **complex spike**: a strong, clear signal that marks a specific moment.

So, **simple spikes** carry the continuous, ongoing information, while **complex spikes** act like a **signal or trigger**, indicating that something important has happened.

Complex spikes may **encode the timing** of particular external events or act as **starting signals** for new processes — for example, when the brain detects an **error** or something unexpected. In that sense, they may carry **error information**, helping the cerebellum adjust and learn from mistakes.

## <span style="color:rgb(239, 179, 1)">Hebbian Synapses – Spike Timing Dependent Plasticity - STDP</span>

![[Pasted image 20251024102211.png]]

Now let’s take another step forward. We will soon come back to the fibers and Purkinje cells, but first, we need to understand a key concept called **spike-timing-dependent plasticity**, or **STDP**.

Have you ever heard of it?  
If not, here’s the basic idea: **STDP** is a form of **Hebbian plasticity** — the main concept behind associative learning in the brain.
#### What is Hebbian Plasticity?

The principle is often summarized as:

> “Neurons that fire together, wire together.”

This means that when two neurons — a **presynaptic** and a **postsynaptic** one — are repeatedly active close together in time, the connection (or **synaptic weight**) between them becomes stronger. If they are active independently, the connection weakens.

#### How STDP Works

![[Pasted image 20251024102252.png]]
Imagine we have two neurons:

- The **presynaptic neuron** (pre-neuron), which sends a signal through its **axon**.
- The **postsynaptic neuron** (post-neuron), which receives that signal through its **dendrite**.

We observe their spikes — their electrical discharges — over time.

1. **Causal (positive timing):**
    
    - The **pre-neuron fires first**, and shortly after, the **post-neuron fires**.
    - The brain interprets this as: _“The pre-neuron helped cause the post-neuron to fire.”_
    - Result: the **synaptic connection strengthens** — the weight increases.
        
2. **Anti-causal (negative timing):**
    
    - The **post-neuron fires before** the **pre-neuron**.
    - The brain interprets this as: _“The post-neuron fired for another reason, not because of this input.”_
    - Result: the **synaptic connection weakens** — the weight decreases.

#### Why It Matters

This timing-dependent strengthening or weakening of connections forms the basis of **learning and memory** in neural networks — both biological and artificial.  
It’s how neurons **associate events** in time, allowing the brain to **predict**, **adapt**, and **correct** errors.

In short:

- **If two neurons fire together consistently → connection strengthens.**
- **If they fire independently → connection weakens.**
    
This is why STDP is considered the **main rule of plasticity in the brain** and a cornerstone of learning mechanisms, not only in the cerebral cortex but also in the **cerebellum**, where precise timing is crucial for motor coordination and error correction.

![[Pasted image 20251024102722.png]]
If the two neurons fire **at completely different times**, far apart from each other, there’s **no meaningful relationship** between their activity.  
In that situation, the brain doesn’t modify their connection — it stays about the same.

So, to summarize it in words:

- When the **presynaptic neuron fires a little before** the postsynaptic one → the connection **gets stronger**.
- When the **postsynaptic neuron fires before** the presynaptic one → the connection **gets weaker**.
- When they fire **too far apart in time** → the connection **doesn’t change**.

The idea was first proposed by **Donald Hebb in 1949**, but it wasn’t experimentally confirmed until the **1990s**, when neuroscientists observed in real neurons that the **precise timing of spikes** could change how strong the connection became — either enhancing it or weakening it.

## <span style="color:rgb(239, 179, 1)">Supervised Spike Timing Dependent Plasticity in the Cerebellum Microcircuits. <br></span>
![[Pasted image 20251024103415.png]]
**How the Climbing Fibers Supervise Learning**

Now that we understand spike-timing-dependent plasticity (STDP), let’s see how it works **inside the cerebellum**, especially at the connections between **parallel fibers** and **Purkinje cells**, under the **supervision of the climbing fibers**.

In the cerebellum, learning happens through a special kind of **Hebbian-like plasticity**, but it’s not just about two neurons firing together. Here, there’s a **third element** — the **climbing fiber** — that acts like a **teacher or supervisor** for the learning process.

So, imagine three players:

1. **Parallel fibers** – carrying sensory and motor information from the mossy fibers and granule cells.
2. **Purkinje cells** – the main output neurons of the cerebellar cortex.
3. **Climbing fibers** – special inputs coming from the **inferior olive**, which send powerful, instructive signals.

When the **parallel fibers** activate a **Purkinje cell**, they create the usual **simple spikes**.  
This is normal, ongoing communication — just transmitting sensory and motor information.

But when, at a certain moment, a **climbing fiber** also fires, it produces a **complex spike** in the Purkinje cell — a strong, distinctive signal that acts like an **error message** or **teaching signal**.

Now, here’s where plasticity comes into play:

- The **timing** between the activity of the **parallel fibers** and the **climbing fiber discharge** determines what kind of change will occur in the strength of the connection between the **parallel fibers** and the **Purkinje cell**.

If a **parallel fiber** is active **just before** the **climbing fiber** fires, the cerebellum interprets this as:

> “This input contributed to an error.”

As a result, the connection between that parallel fiber and the Purkinje cell is **weakened** — this is **long-term depression (LTD)**.

On the other hand, if a **parallel fiber** fires **outside this window**, meaning far before or after the climbing fiber discharge, its connection is **not changed**, or in some specific cases, it can even become **slightly strengthened** (**LTP**).

So the **climbing fiber** sets a kind of **temporal window** of supervision:

- When it fires, it “tells” the Purkinje cell that something unexpected has happened — a motor error, for example.
- Any **parallel fibers** that were active just **before** this error are considered responsible for it, and their connections are **depressed**.
- Those that weren’t active at that time are left unchanged.
    
In other words:

> “Only the inputs that were active right before the error get punished.”

This mechanism makes the cerebellum an **error-correction machine**. It continuously adjusts the strength of connections based on timing — learning which signals predict success and which predict mistakes.

![[Pasted image 20251024103457.png]]

In the cerebellum, the **change in synaptic weight** — that is, how much a **parallel fiber** influences a **Purkinje cell** — depends on **when** that parallel fiber fired **relative to** the **climbing fiber’s signal**.

We can think of this as a **timing window** centered around the moment when the **climbing fiber** fires (the **inferior olive spike**).

Only the **parallel fibers** that were active **shortly before** that moment will have their connection strength **modified**. Specifically, they will undergo **long-term depression (LTD)** — their influence on the Purkinje cell becomes weaker.

This means that in the cerebellum we do have a form of **spike-timing-dependent plasticity (STDP)**, but it’s **one-sided**:

- Instead of having both potentiation (LTP) and depression (LTD),
- we have **only LTD**,
- and it applies **only** to the parallel fiber–Purkinje cell synapses that were **active just before** a **climbing fiber** spike.
    

#### What Does This Mean Functionally?

The **climbing fiber** acts as a **teaching signal** or **error messenger**.  When it fires, it indicates that **something went wrong** — for example, the expected movement or sensory feedback did not match reality.

The cerebellum then “looks back” in time to see which **parallel fibers** were active right before the error occurred.  Those active inputs are assumed to have **contributed to the mistake**, so their connections are **depressed**.

In other words, the cerebellum learns by **reducing the weight** of signals that were **predictive of an error**.

#### Predictive Learning Mechanism

This form of plasticity makes the cerebellum a **predictive learning machine**.  
It continuously adjusts the strength of its internal connections based on the **temporal correlation** between incoming signals and errors.

If a parallel fiber consistently becomes active **right before** a climbing fiber (error) discharge, the system assumes:

> “This signal often precedes an error — it might be part of the cause.”

Therefore, that connection is weakened.  
Next time, the cerebellum will be less influenced by that same input, helping to **avoid repeating the same error**.

#### The Role of Timing

The **timing** is crucial because it creates a kind of **causal link**.  If two signals occur very close in time, the brain assumes a **relationship** — that one might have caused the other.

So, if the **parallel fiber** fires just before the **error signal (climbing fiber)**, the cerebellum interprets that as:

> “This input led to a wrong outcome — let’s reduce its effect.”

Through this continuous process, the cerebellum refines its responses and gradually **improves the prediction** of motor and sensory events.


#### Simplified Interpretation

You can think of it like this:

- The **parallel fibers** tell the cerebellum what it _expected_ to happen (the “plan”).
- The **climbing fiber** tells it what _actually happened_ (the “error”).
- When there’s a mismatch, the cerebellum corrects its internal model by weakening the connections that produced the wrong expectation.
    

Over time, this makes the cerebellum **more accurate**, **predictive**, and **adaptive** — learning from timing errors to fine-tune movement and coordination.



![[Pasted image 20251024104101.png]]



We'll see also afterwards by Okay Let's have a look on this, which is super nice. I take for granted that you are all familiar with this skin. We showed it last lesson. Now, this skin can be populated by the cerebellar microcircuit. Cerebellar microcircuit is receiving by mossy-fibers the ACtUAL trajectory and the efference copy. Then Purkinje cells are, granule cells are elaborating those inputs and sending through parallel fibers to Purkinje cells. Then we have the feedback controller which converts the error between the ACtUAL trajectory and the DESIRE trajectory into a feedback motor command error. And this feedback motor command error is used to modulate the connections between the parallel fibers and the porting designs. And so we have, and it's carried by the climbing fibers. And that way, this cerebeellumn can be assumed to work as an inverse model capable to be continuously updated.


1.44.06
Modeling and simulations. So, at a certain point we will model cerebellum, but now I need to introduce the Brits to make the models. Okay? So, Eduardo Accapici. We have most of you who have taken the laureate in biomedical engineering. You are a physiologist. What is your background? Okay. So, okay. I would like you to I'm taking for granted as let's say a preliminary knowledge the Hodgkin-Aftley neuron models which are done by in our journal by the Mandato Records of Biodetro Magnetismo but of course we might have somebody who comes from different backgrounds and I would be happy to give you some additional material to catch up so neurons communicate through action potentials action potentials associated to the change in membrane voltage depending on subcellular trans-channel modulation mechanism. So this is a typical spike action potential change of the voltage across the neuron membrane and it is caused by an abrupt change, fast change of sodium channels and then a slower change of potassium channels and this results in a very sharp change of the membrane potential going back to an hyperpolarized condition and finally back to the resting state. the resting potential, the occurrence of the action potential is associated with the by surpassing a threshold. The threshold is a specific parameters of each different neurons. Let's say that One of the main concepts that I would like you to, let's say, transfer from what you know, taking inputs from what we have seen in this lecture, this is a model of one neuron, but granule cells, purkinje cells, Golgi cells are all neurons. So let's say that neurons can be very different. but they are all associated to build production of action event. The structure and organization of the brain can suggest some computational analysis. The information storage is associated with the chemical and physical structures of neurons and synapses. The information transmission is associated to electrical and electrochemical signaling. The primary computing element is the neuron, the computational basis with the neuron. Now, what is important is to try to capture and describe the... Okay, now we want from, let's say, a general model of the neurons, which is the 8-inch model, we want to try to understand how to model different neurons and make them into circles, which is the computational basis of a microsyme, so an area of the brain, a computational network of the brain. To do this, we need to describe the different striking patterns of the different neurons. So we need to describe different populations of neurons work. For example, we have some, we call them electro-responsive properties or features which distinguish one population of neurons from others. Okay? For example, algorithms. Some neurons have an autorhythm at different hertz, so at different frequencies. Autorhythm is defined as spontaneous firing which occurs without any external input. There are neurons which have no otorism. So if they do not receive any input, they are silent. Other neurons have baseline frequency, which is called sub-threshold oscillations. Many neurons, even if they do not have an otorism, they do have sub-threshold oscillations. Which means they would tend to spike at a certain frequency because with the small inputs at this frequency they are much closer to the threshold. So there is a higher probability for them to spike here, here, here with respect to spike here. So this is another important property of neurons, electro-responsive properties of the neurons, again associated with no inputs from the outside. Then we have electro-responsive properties that are associated to inputs. So external inputs at increasing levels. And if we keep an input per over time, so it's not just a single injection of current, but it's a stable injection of current, we can see that neurons are spiking at different frequencies. The higher is the input current, the higher is the frequency. And this is described as the linear current-frequency relationship. So, the higher the frequency, the higher the current, the higher the frequency. This linear current frequency relationship has different slopes and different fluctuations. These different parameters describe multiple populations of neurons. Then, looking again at this train of spikes,
