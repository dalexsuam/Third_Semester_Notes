
17/10/2025
***
**Computational Neuroscience 1.**

**Part 1 - Introduction to motor control and learning**

# <span style="color:rgb(223, 109, 109)">Motor Control</span>
![[Pasted image 20251019162826.png]]

Motor control refers to the **processes occurring in our brain and nervous system that allow us to control movement and perform motor tasks**.

It’s important to understand that **almost every task we perform**, if it has an **observable or communicable outcome**, must pass through the **motor system**.

This includes not only physical actions such as:

- Talking
- Carrying objects
- Walking, dancing, or skiing

but also actions that might seem **more cognitive in nature**, like **writing**, **typing**, or **drawing**, since these tasks still require the **motor system to express our intention externally**.

In essence, **motion is a complex process** that involves the **integration of sensory input, neural processing, and muscular activation**, allowing us to translate our internal goals or thoughts into coordinated physical actions.

# <span style="color:rgb(223, 109, 109)">Why Movement is a Complex Task?</span>

Actually, **motion is a complex task** for many different reasons.

Let’s imagine two perspectives. On one side, we can open a _control systems_ window — 
we’re controlling a system, our own body.  

On the other side, we can open a _physiology_ window — we’re observing how the human body actually moves.  

And from both points of view, movement presents several challenges.
## <span style="color:rgb(239,179,1)">1. Delays</span>

![[Pasted image 20251019171319.png]]
There are **delays** in the system — why?  Because it takes time for **neural signals** to travel from the brain to the muscles, and for **sensory feedback** to go back to the brain.  Each of these loops takes time, meaning our brain must **predict and plan** ahead in order to execute fast movements correctly.

If we think in control-system terms, **controlling a system with delay** is difficult. So, our brain constantly compensates for these internal delays to achieve smooth and coordinated motion.

* **Fast movements:** When we perform **fast, voluntary movements** — like reaching for an object, typing a key, or throwing a ball —  the _entire movement_ often lasts around **300 milliseconds** (0.3 seconds or 300ms).

* **Visuomotor feedback:** refers to the time it takes for visual information (e.g., seeing where your hand is) to be processed and influence muscle activity.*
## <span style="color:rgb(239,179,1)">2. Noise</span>

![[Pasted image 20251019171550.png]]
Then we have **noise**.  Every neural signal — whether it’s a motor command or sensory feedback — contains **intrinsic noise**.  

==This means that even if the same input is given twice, the neural response will never be exactly identical.==

So there’s:

- **Sensory noise**, which limits how precisely we can perceive the world.
- **Motor noise**, which limits how accurately we can execute commands.

From a control-engineering point of view, a system with **delays and noise** is very challenging to control — yet our brain manages it continuously.

>[!important] PREDICTION and a PLANNING are NECESSARY $\rightarrow$ feedforward controller
## <span style="color:rgb(239,179,1)">3. Non-Stationarity</span>

Another assumption in control theory is that systems are **time-invariant** — meaning they don’t change with time.  

Our body is definitely **not stationary**.

We can think of this in two time scales:

- **Long-term (ontogenetic) scale** – our body changes over life: we grow, age, and our muscles and neural systems evolve.
    
- **Short-term scale** – the system changes depending on context, for example, when carrying objects of different weights.  

    Think of when you lift a suitcase you expect to be heavy but it’s empty — your motor control immediately overshoots, and then you adapt.


So, **adaptation, prediction, and learning** are fundamental to motor control.

>[!important] FLEXIBILITY AND LEARNING ARE NECESSARY

## <span style="color:rgb(239,179,1)">4. Non-Linearity</span>

![[Pasted image 20251019171848.png]]
Another key challenge: our system is **non-linear**.  
In linear systems, effects can simply add up — but in our body, **the sum of two movements is not the same as the movement resulting from the sum of their commands**.

What are the sources of non-linearity?

- **Saturation** – our muscles and joints have physical limits (range of motion).
- **Gravity** – the same movement requires different inputs depending on body orientation.
    

So, the brain must constantly adapt to these non-linear relationships.

## <span style="color:rgb(239,179,1)">5. Multidimensionality and Synergies</span>

![[Pasted image 20251019172025.png]]
Finally, motion is **multidimensional**.  We have **millions of sensory inputs** and around **600 muscles** to control.

Even if we simplify and assume each muscle can only be _on_ or _off_ (which is false), that would still mean about $2^{600}$ possible muscle activation combinations — roughly $10^{20}$ possibilities.

Clearly, the brain cannot control each muscle independently.  Instead, it uses **synergies** and **motor programs** — coordinated groups of muscles working together to achieve specific movements efficiently.

>[!important] SYNERGIES AND MOTOR PROGRAMS ARE NECESSARY

# <span style="color:rgb(223, 109, 109)">Sensory-motor integration</span>



![[Pasted image 20251019172207.png]]

At its core, **motor control** is about how the brain transforms **intentions** into **coordinated movement**, using continuous loops of sensory and motor information.

It relies on a **strong bidirectional interaction** called **sensory–motor integration**, which includes:

- **Sensors** → detect information from the environment (e.g., vision, touch) and from the body itself (**proprioception** — sense of body position and movement).
- **Actuators** → muscles, which execute the brain’s motor commands and act on the environment.
- **Controller** → the central nervous system, which integrates sensory input, predicts outcomes, and issues motor commands.
    
> Example: Even without looking, you know where your elbow is — thanks to **proprioceptive feedback**, an _internal sensor_ that informs the brain of limb positions without external input.

To study how this works, scientists have decomposed motor control into a series of **transformations** that occur between _intention_ and _action_:

### <span style="color:rgb(161, 40, 226)">1. Kinematic Transformation</span>

![[Pasted image 20251019173137.png]]

This concerns **movement geometry** — how positions and trajectories are defined in space, independent of force.

Steps include:

- Locating the **hand** and **target** (through visual and proprioceptive cues).
- Computing their **relative position** (the vector between current and desired positions).
- Planning an **endpoint trajectory** — the desired path of the hand in space.
- Transforming that trajectory into **joint coordinates** (angles of the shoulder, elbow, etc.).
- Activating the appropriate **muscles** to realize that movement.

So:

> Intention → Trajectory → Joint Angles → Muscle Activation

### <span style="color:rgb(161, 40, 226)">2. Dynamic Transformation</span>

![[Pasted image 20251019173150.png]]


Once the kinematic plan is ready, the brain must translate it into **forces and torques** that actually move the body.

But — and this is crucial — **dynamics has multiple possible solutions**:

- There are many combinations of muscle forces that can produce the _same movement_.
    
- For instance, pushing a light or a heavy door can have the **same kinematics** (same trajectory), but require **very different dynamics** (different forces and activations).

### 3. <span style="color:rgb(161, 40, 226)">Kinematics + Dynamic Transformations</span>

>From Intention to Action — Step by Step

![[Pasted image 20251019175623.png]]

This sequence describes how the brain transforms an _intention_ (e.g., “reach the cup”) into a _movement_ executed by muscles.

Let’s go through it stage by stage:

#### A → B: Locating and Planning
1. **Locate the hand and the cup**  
    The brain first determines the position of the hand and the target in **egocentric coordinates** — i.e., with respect to the body (not external space).
    
    > “My hand is 30 cm to the right of my midline, the cup is 40 cm forward.”
    
2. **Plan the movement (point B)**  
    The brain plans an **endpoint trajectory** from the current hand position to the target — the path the hand should follow in space.
    
#### B → C: Inverse Kinematics

3. **Determine the intrinsic plan**  
    Once the spatial trajectory is planned, it must be translated into **joint coordinates** (angles of the shoulder, elbow, wrist…).  
    This transformation is known as **inverse kinematics** — converting a desired position in space into the joint configurations that achieve it.
    
    > Cartesian coordinates → Joint angles
    
#### C → D: Inverse Dynamics

4. **Compute the joint torques (and then muscle activity)**  
    The next step is to determine **how much torque** each joint must produce to follow that trajectory.  
    This process is called **inverse dynamics** — computing the forces/torques from known motions, masses, and inertias.
    
    > Joint angles + accelerations + segment masses → Required torques
    
    These **joint torques** are _net torques_: the total rotational effect resulting from all muscle and external forces acting at a joint.  
    They can be computed through **mechanics**.
    
#### ⚙️ From Torques to Muscle Activations

However, **joint torques are not the same as muscle activations**:

- The same net torque can be produced by **different combinations of muscle forces** — for example, one muscle contracting strongly while another opposes it slightly.
- This means the mapping from **torques → muscle activity** is not unique.
- The nervous system must choose one of many possible solutions, often based on **efficiency, stability, or learning**.

> Example: If someone resists your hand movement, you can still move it the same way — but the muscle activations (and thus internal torques) will be totally different, even if the _external motion_ looks identical.



# <span style="color:rgb(223, 109, 109)">Perception in Motor Control — From Passive Sensing to Active Perception</span>
So far, we have mostly focused on the _motor_ side — how our brain generates movement.  
But movement doesn’t exist without perception. To move properly, we constantly need to **perceive** our body and the environment.

Let’s reflect on what perception actually means.

### <span style="color:rgb(161, 40, 226)">The Mona Lisa Example</span>

![[Pasted image 20251019192511.png]]
Imagine I show you a blurred, cropped image like this one.  
Even without seeing it clearly, you immediately recognize it: _“That’s the Mona Lisa, in the Louvre, painted by Leonardo da Vinci.”_

Now, if I take the same image and rotate it 180°, suddenly your brain says, _“No, that’s not the Mona Lisa.”_  

Nothing has changed in the pixels — it’s exactly the same visual input, only rotated.

So why does your brain react so differently?

Because **perception is not a passive process**.  
Your brain doesn’t “scan” every pixel like a camera would. Instead, it interprets sensory inputs through **experience, prediction, and stored knowledge** — through _hypotheses_ based on what it already knows about the world.

### <span style="color:rgb(161, 40, 226)">What Is <i>Active Perception</i>?</span>

This leads us to the concept of **active perception**.

Active perception means that:

- Our sensory systems don’t treat all incoming signals equally.
- The brain **selects, predicts, and interprets** sensory information based on prior experience, context, and goals.
- In other words, **what we expect influences what we perceive.**

If you’re looking at a familiar object, your brain “guesses” what it should be seeing — and only checks the details that confirm or contradict that guess.  That’s why recognition is immediate for familiar stimuli, but slow and exploratory for new ones.
### <span style="color:rgb(161, 40, 226)">Why This Matters for Motor Control</span>

Active perception is fundamental to motor control because **action and perception are deeply intertwined (entrelazados)**:

- The brain doesn’t just react to sensory input — it **predicts** it.    
- Motor commands are generated not only to move but also to **test and refine these predictions**.

This constant loop between _what we sense_ and _what we expect to sense_ is known as **sensorimotor integration**, and it’s the foundation of coordinated, adaptive movement.

| ![[Pasted image 20251019193034.png]] | ![[Pasted image 20251019193041.png]] |
| ------------------------------------ | ------------------------------------ |
Let’s continue our exploration of how the brain controls movement.  Have you ever seen this picture? (Those who have, raise your hand!)

When you look at it for the first time, it may seem confusing — just a mix of black and white spots. But once you recognize the **dog** under the **tree**, your perception suddenly changes. From that moment on, you can’t _unsee_ it.

This little exercise shows again how **our perception depends on experience** and how our brain interprets information in an active way.

Now, let’s connect this to **motor control**.

# <span style="color:rgb(223, 109, 109)">Reflexes vs. Voluntary Actions</span>

When we move, not all movements are the same.  Broadly, we can distinguish two main categories:

1. **Reflex movements**
    
    - These are _automatic_ responses — quick, hardwired transformations between stimulus and reaction.
    - They don’t require conscious control or planning.
    - Example: touching a hot surface — your hand pulls back instantly, even before you consciously feel the heat.
    - The same input will _always_ produce the same output.
        
2. **Voluntary movements**
    
    - These are **goal-directed** and **flexible**.
    - They require **planning**, **decision-making**, and often **learning**.
    - The same task (for example, reaching for a cup) can be executed in many different ways — with different muscles, trajectories, or speeds.
    - Their **execution speed** is inversely related to **accuracy** — the faster you try to move, the harder it becomes to be precise (a principle known as **Fitts’ law**).
    - They can also adapt to changes in context or environment.

## <span style="color:rgb(239, 179, 1)">Voluntary Movements</span>


Now we will focus on **voluntary movements**. When we look at how people perform voluntary tasks — such as **reaching and pointing** — we find something very interesting: **despite the infinite possible ways to move**, everyone tends to perform the movement in almost the same way.

For instance, imagine that each of you comes here and performs this simple **pointing task** — moving your hand from one position to another to touch a bottle. Even if the bottle changes slightly in **height** or **distance**, you will all move your arm along **very similar trajectories**.

Why? Because our brains, out of the _infinite possible movements_, **consistently select specific solutions**.

### <span style="color:rgb(161, 40, 226)">Levels of Indeterminacy in Movement</span>

When performing a voluntary task, the brain faces several levels of **indeterminacy** — that is, multiple valid options to achieve the same goal:

1. **End-point trajectory**
    - First, the brain decides _how the hand will move in space_ — from the start point to the target (for example, the path from your hand to the bottle).
    - This trajectory is smooth and efficient, and most people choose almost the same one.
        
2. **Joint configuration**
    
    - For the _same hand path_, there are **infinitely many ways** to position your joints — shoulder, elbow, and wrist — to reach the target.
    - Yet, our brain tends to choose one particular coordination pattern that feels natural and stable.
        
3. **Muscle activation (co-contraction)**
    
    - Finally, even for the same joint motion, the **level of muscle activation** can vary.
    - You could move softly (low co-contraction) or stiffly (high co-contraction), both producing the same net torque at the joint.        
    - Still, our brain tends to select a consistent and efficient balance between effort and stability.
    
### <span style="color:rgb(161, 40, 226)">Why This Matters</span>

Even though no two movements are ever _exactly_ the same — not even when the same person repeats the action — they always remain **similar** in their overall organization.  
This consistency is what makes **motor control** a meaningful field of study: our brain systematically chooses particular solutions among countless possibilities.

If every movement were completely random, we could never define _general principles_ of human motor control — each individual (or machine) would need its own unique control strategy.   But since our brains share common rules for movement planning and execution, we can study and model them scientifically.

### <span style="color:rgb(161, 40, 226)">Evidence from Pointing Tasks</span>
![[Pasted image 20251019193658.png]]

Studies have analyzed these principles using **center-out tasks** — simple reaching movements performed on a horizontal plane (like moving a hand from the center of a table toward different targets).
![[Pasted image 20251019194101.png]]
When participants move their hand from one point to another — for instance, from **B1 to B4**, **B1 to B5**, or **B2 to B5** — they display:

- Completely **different joint trajectories** and **joint velocities**,  
    yet...
    
- Almost **identical hand trajectories** in space.

![[Pasted image 20251019194236.png]]

The **velocity of the hand** follows a **bell-shaped curve** — smooth acceleration and deceleration — regardless of the target direction or distance.

This shows that our brain plans the **end-point movement of the hand** in a consistent, optimized way, and then adjusts the underlying joint and muscle activity to make it happen.

![[Pasted image 20251019194336.png]]
This is the hand acceleration over time and the hand velocity over time in the direction of the target, but for very different distances. So now we are looking at experiments that aim to gather information about the features of motor control.

When going from a very close target (2.5 cm away) to a farther one (30 cm away), we can see that the hand acceleration and velocity scale almost linearly.

This means that the **motor plan** — the sequence of tasks needed to accomplish the target — includes the **amplitude**, **kinematics**, and **dynamics** of the movement. Velocity and acceleration change according to the distance to the target.

This shows that the **extent of the movement is planned before it is initiated**, because the start of the movement is already different within the first few milliseconds, depending on how far the target is.

This means we are **not working in a feedback loop**, like saying:

> “Oh, the target is far, let’s go farther… oh, I reached it.”

Instead, we start the movement differently if the target is 30 cm away or 3 cm away. It might sound obvious, but when studying movement, it’s important to **measure and prove** these behaviors scientifically.

# <span style="color:rgb(223, 109, 109)">Laws of Voluntary movements</span>

## <span style="color:rgb(239, 179, 1)">1. Invariant features of voluntary movements</span>

We already mentioned this, but one example I really like is the one in this picture.  
When you were a child, you learned how to write. You trained your **dominant hand** for years until writing became accurate, smooth, and fast.

![[Pasted image 20251019213541.png]]

Now imagine trying to write the word _“ciao”_ using your **foot** in the sand. You can do it — it will be much bigger, less accurate, and slower, but still recognizable.

This shows that there is a **high-level control pattern** that is **independent of the effector** (the part of the body performing the action). Your brain can transfer the same movement concept to a different limb, even if it has never been trained for that.

Of course, the **quality of the result depends on training**, but the underlying motor plan is shared.

## <span style="color:rgb(239, 179, 1)">2. Reaction time increases with the amount of information processed<br></span>
![[Pasted image 20251019213746.png]]
This has been experimentally demonstrated: when we are given **more options or choices**, our **reaction time increases**.

The more information the brain has to process before selecting a response, the longer it takes to initiate the movement.

## <span style="color:rgb(239, 179, 1)">3. The speed–accuracy trade-off (Fitts’s Law)</span>

![[Pasted image 20251019213804.png]]
According to **Fitts’s Law**, the **faster** we move, the **less accurate** we become.

In a target-pointing task, if you move slowly, you can reach the target with high accuracy. But if you move quickly, accuracy decreases.

Think about **threading a needle** — you do it slowly because precision is crucial.

This trade-off has **two main causes**:

- **Reduced feedback processing:** when we move fast, there isn’t enough time for feedback to be received and used for correction.
    
- **Signal-dependent noise:** faster movements require stronger muscle forces, which means **more muscle fibers** are recruited. Since each fiber adds a bit of noise, the total noise increases with force, reducing accuracy.
    
## <span style="color:rgb(239, 179, 1)">4. Movement efficiency improves with experience and learning<br></span>
![[Pasted image 20251019214034.png]]

This is intuitive but fundamental. With **practice**, movements become:

- More **accurate**    
- More **fluid**
- **Faster**
- And overall, more **efficient**

It’s the same principle behind how writing with your hand is smoother than with your foot — **training refines motor control**.


# <span style="color:rgb(223, 109, 109)">Motor Learning</span>

![[Pasted image 20251019214906.png]]
Motor learning is the process through which we improve our performance by interacting with the environment. In simple terms, our brain behaves like a **neural network**: we act, observe the outcome, receive feedback, and adjust our movements to perform better next time.

For example, think of how a child learns to move. At first, a baby crawls using four limbs — a movement that doesn’t allow carrying objects. The motivation to **walk** often comes from the desire to **carry or reach a toy**. Early walking is clumsy and inefficient, but with time, walking and running become **smooth and energy-efficient**.

This same principle applies in **rehabilitation**: patients must refine their movements to regain **efficiency** with limited physical resources.
![[Pasted image 20251019214939.png]]
Motor learning represents a **balance** between:

- **Innate behaviors** – hardwired, fast, robust, and reflex-based
- **Learned behaviors** – flexible, adaptable, but slower to develop
    
Reflexes are examples of innate behaviors. They are **automatic and permanent**, and that’s why neurological exams check reflexes even in adults — their absence may indicate a neurological problem.

Interestingly, we are born with some innate reflexes that we later **lose** as we learn.  
For example, if you touch a newborn’s palm, they will instinctively **grasp your finger**. Six months later, the same child won’t react automatically — they will grab your hand **only if they choose to**. This shows how reflexes evolve into **voluntary, learned actions** as the brain matures.


![[Pasted image 20251019220122.png]]

The degree of motor learning varies across species and helps distinguish them.  
Simpler species have **more innate, less flexible** behaviors — for example, a spider can walk on its web immediately after birth.

In contrast, humans require significant **motor learning** because our environment, anatomy, and goals constantly change. This learning process continues throughout life — not just in childhood.

Whenever you:

- Recover from an injury,
- Learn a new sport, or
- Find alternative ways to move due to pain or weakness,

you are **activating motor learning** in your brain.

![[Pasted image 20251019220306.png]]

***Does it start from a tabula rasa?*** Humans do not start from a _tabula rasa_ (a blank slate). Newborns already have a set of **reflexes** that doctors test immediately after birth — for instance, the **grasp reflex** or the **sucking reflex**.

If some of these reflexes are missing, it can be an early warning of possible **neurological developmental issues**, which is why these tests are done routinely in every newborn.

![[Pasted image 20251019221041.png]]

Motor learning also involves the **co-adaptation between neural organization and anatomical structures**. In other words, as we learn new movements, both our brain and our body adapt together.

A clear example comes from **manipulation tasks** — activities that involve handling objects with our hands. One of the most distinctive features of human motor ability is the **opposability of the thumb**.

Thanks to the opposable thumb, humans can grasp and manipulate tools with great precision — something that sets us apart from other primates. Monkeys, for instance, move their thumb **in the same direction as the other fingers**, which allows them to grab objects but not to **oppose** the thumb for fine control.

This small anatomical difference has profoundly changed how humans interact with tools, demonstrating how **motor learning and anatomy evolve together** to expand our movement capabilities.


# <span style="color:rgb(223, 109, 109)">Human Motor Learning</span>
![[Pasted image 20251019221347.png]]

And then, is humankind a unique species with respect to these features? There are several indications that suggest yes.

One of the main differences between humans and other animals lies in **our ability to adapt and move across the planet**. Most animals have **localized habitats**, constrained by environmental and climatic conditions. For example, a polar bear with thick fur cannot easily survive near the equator.

Another distinctive feature is our **use of tools**. Think about the example of Tarzan — learning to use tools by imitating other animals. Tool use represents a form of what we can call **exo-Darwinism**: an evolution that happens outside of biological evolution.

While **Darwinian evolution** takes place over millions of years through genetic changes, **exo-Darwinian evolution** happens within a single lifetime, through **learning and adaptation**. From childhood to adulthood, and throughout our lives, we continuously acquire new skills and adapt to new tools and environments.

This ability to **create, use, and discard tools** is what allows humans to live almost anywhere — from the equator to the North Pole — and to adapt within **months**, not millennia. It’s this **speed and flexibility of adaptation** that truly sets humans apart from other species.


![[Pasted image 20251019221901.png]]

While certain properties of the brain **scale linearly** with body size — such as total brain weight, cortical area, or number of neurons — other properties **do not**. These nonlinear features are what make the human brain extraordinarily powerful in comparison to those of other species.

- **Dendritic complexity:**  
    Dendrites are the branching extensions of neurons that receive incoming signals. In humans, dendrites are not just more numerous but also **much more complex and branched**, allowing a single neuron to integrate input from a vastly larger network of other neurons.
    
- **Number of synapses:**  
    Even if the total number of neurons scales linearly, the **number of synaptic connections per neuron** grows exponentially in humans. This means the connectivity network — and therefore the potential for parallel processing and information integration — is much richer.
    
- **Synaptic efficiency and information rate:**  
    Each synapse can transmit more information per second (“bits per synapse”), so the **computational throughput** of the human cortex increases nonlinearly compared to other species.
    
- **Action potential dynamics:**  
    The time needed to generate an action potential — the electrical pulse that neurons use to communicate — becomes optimized, allowing faster and more energy-efficient processing.

So even though a human head is not drastically larger than that of a chimpanzee, the **“wiring” inside is far more complex**. This nonlinear scaling — especially in dendritic architecture and synaptic density — gives rise to emergent cognitive and motor abilities that are **orders of magnitude** more sophisticated.

In short, it’s not just about brain size — it’s about **how the brain’s architecture and signal processing capacity evolve nonlinearly**, enabling abstract reasoning, language, tool use, and advanced motor learning.

![[Pasted image 20251019223534.png]]

This is another very interesting piece of evidence from recent studies. Here, we can see the electrical signals from **cortical neurons** recorded in three cases:

- a **young mouse** (blue trace),
- an **adult mouse** (black trace), and
- a **human** (red trace).
    
The human cortical neurons are obtained from **brain tissue samples resected during surgeries** for epilepsy or tumors — ethically, this is one of the few ways to study living human neurons.

Each trace represents a sequence of **eight or nine input spikes** delivered to the neuron. The important thing is that the neuron needs to recognize the **order and timing** of those spikes — to know that the eighth is the continuation of a sequence, not just a new first spike. And after the sequence ends, the neuron must quickly **recover** to be ready for the next input.

![[Pasted image 20251019223626.png]]
If you look at the plots, the **human neurons** show a much more **modulated** and **stable** response over time — similar to, but more refined than, the adult mouse neurons. In particular, in **plot E**, we see that the human neuron’s response to the last spike in the train remains **about 80–90% of the amplitude** of the first one. This means that the neuron is already **fully ready** for new incoming information, maintaining almost the same efficiency across bursts.

In **plot D**, we can see the so-called **synaptic depression** — how the neuron’s response decreases slightly with repeated inputs. Humans and adult mice show a similar modulation, but humans have a **much faster recovery** time.

In fact, the **time needed for human cortical neurons to recover** and be ready for a new input is **about three times faster** than in rodents.

So this finding shows that we can’t simply extrapolate animal data to humans by scaling time. The **speed, adaptability, and information processing** of human cortical neurons are fundamentally different — not just faster, but more **efficiently organized** to handle rapid, continuous streams of information.

# <span style="color:rgb(223, 109, 109)">Feedback Control / FeedForward Control</span>


| Feedback                                                                 | Feedforward                                                                                                                               |
| ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| - Anticipatory control <br>- Sensorial information + previous experience | - Actual control<br>- Dependent on the actual sensory information  <br>- Comparison with a reference signal <br>- Characterized by a gain |

We can mostly distinguish between **feedforward** and **feedback** control.

**Feedforward control** works as an _anticipatory mechanism_, based on sensory information and previous experiences. In contrast, **feedback control** is the _actual online correction_, which depends on real-time sensory inputs and operates with a certain gain.
![[Pasted image 20251019233815.png]]
For example, imagine watching a ball fall and needing to intercept it. If we record the EMG activity of the arm muscles, we observe that as soon as the subject sees the ball descending, there is an early activation of both the biceps and triceps muscles. This stiffens the elbow joint to prepare for the impact.

This **preparatory muscular activation** is not feedback-based, because nothing has happened yet — it is an _anticipatory_ action planned before the ball’s arrival.

Then, depending on the **actual weight of the ball**, the subsequent muscle activations at impact will differ. If the ball looks like a tennis ball, we all have a **prior expectation** of its weight, and this expectation drives the anticipatory (feedforward) part.

However, if the ball turns out to be heavier or lighter than expected, the feedback response will differ — the system will correct based on the real sensory input.

A familiar example is when you lift an empty suitcase: because you anticipated it being heavy, your brain planned for a stronger lift, and as a result, you _overlift_ it when it’s actually light.


# <span style="color:rgb(223, 109, 109)">Modelling Brain Functions in Motor Control: Internal Models</span>

To study how motor control processes occur inside the brain, one of the main approaches that has been proposed is through **internal models**.

We’ll look at this in two steps:

1. How we can model these brain functions, and
2. Where in the brain these functions are accomplished.
    
**Internal models** are widely used to represent the _sensorimotor_ and _motor-sensory_ transformations that occur within the brain. In other words, they are internal simulations of the system being controlled.

For instance, to control my arm, my brain needs an **internal model** of my arm — including the possible sensory feedback it can collect. These models allow the brain to predict how the body will respond to motor commands and how sensory information will be perceived as a result.

## <span style="color:rgb(239, 179, 1)">1. Inverse Model</span>



The **first type** of internal model proposed is the **inverse model**.

This model allows the brain to transform a _desired trajectory_ into a _sequence of motor commands_. It’s called _inverse_ because it performs the opposite operation of the body.

- In the body, **motor commands → movement trajectory**.    
- In the brain, the **inverse model** does the reverse: **desired trajectory → motor commands**.
![[Pasted image 20251019234504.png]]

To perform a task, the brain must convert the intended movement (the _desired trajectory_) into the muscle activations required to achieve it. The **inverse model** handles this conversion.

Importantly, the _desired trajectory_ corresponds to the **desired sensory feedback** — what we want to perceive next. For example, when I want my hand to reach a specific spot, that goal represents my desired sensory state.

The **inverse model** therefore converts this desired sensory outcome into **feedforward motor commands**. It works very quickly, compensates for delays, and generates anticipatory control. However, since it doesn’t rely on real-time feedback, it cannot correct the movement if something unexpected occurs during execution. Once the command is issued, it simply runs its course — much like a feedforward controller.

![[Pasted image 20251019234749.png]]
In this scheme, the **inverse model** takes the desired state and generates a **feedforward motor command**, which activates the muscles. The resulting **sensory feedback** returns to the brain, where it can be compared with the desired outcome.

If a difference is detected (a _motor error_), this information can be used in two ways:

- To **update the inverse model** (learning and adaptation), or
- To **produce a feedback correction** during the movement.
    
For example, if I realize my hand is slightly off-target, I can make an adjustment — adding a feedback correction on top of my feedforward control.






Now, second model. Sorry, I have to do it right because I don't like that figure. So we have the desired trajectory, inverse model, feedforward motor commands, body, sensory feedback, which informs about the actual trajectory. The actual trajectory is compared to the desired one and the error process by a feedback controller which gives an extra input. to the motor commands the error can be used to train the inverse model because there is always a learning process, motor commands need to be actuated by the body, muscle and sensory feedback so body.


## <span style="color:rgb(239, 179, 1)">2. Forward Model</span>

![[Pasted image 20251019235707.png]]
Now let's add another piece. the Forward model gives us the state estimation. So the forward model produces estimate of the feedback of our sensory feedback, so of our state, before the sensory feedback is made available. According to the motor commands, we are sending. I think most of you can see this bag. Move our head. Rotate your head around so to see the bag and to rotate your gaze and your head. Has the bag moved? No. Has the bag moved? But On your retina, the image of the bag has moved a lot. But your brain is not accounting that information from the sensory feedback a real movement. And actually, the bag starts moving by itself. Everybody, would be like what's going on? So it's not that your brain is not accounting for the bag being able to move. But If the movement is the consequence of the activation of your own muscles, this change in the feedback is filtered, is processed in a different way with respect to the same change in the feedback due to the bag floating around. Can our brain do this? In order to do this, it needs to have a prediction of the consequences of its own, of the motor commands that it's sending, as a prediction of the sensory feedback that it will be produced. 

So, The forward model is a state estimation. It's done by a copy if the efference, the reference, the motor commands, and a forward model. and it allows us to distinguish between action, the consequences of our own actions, and external events. The goal is to detect the consequences of our own actions, to have a perceptual stability. So it's not that because I'm moving, everything is flowing around. I have a perceptual stability. and modulate attention. It's way more important to see if If this bag starts moving by itself, we need to... something is occurring. Do these experiments and you can understand this. If you push gently the side of your eye you will see a little shift in the image. But this shift in the image is a shift in the image. Your brain is telling you that there is a shift in the image. It's not a perceptual stability. Why? Because this action is not directly produced by the muscles of your eyeballs. It still is produced by your own body. So if a person does this instead of you yourself, you will perceive even more. have you understood the reason why it's super important for our brain to have this and we cannot count it exists so our point is it exists let's give it a name and then we will see and where is it.

![[Pasted image 20251020000312.png]]

desired behavior inverse model motor commands desired behavior then there is the inverse model which transform the desired behavior into a motor command. Of the motor command, so a copy of the motor command, so a copy efference is sent forward model. Why forward? Because it's doing the same as the body, receiving motor command and producing behavior. So forward model produce a predicted behavior. So what we expect as a consequence of this motor command. So the forward model maps the motor commands into the sensory space, while the inverse model estimates motor commands to obtain a desired sensory field. 



1.29.48
Why this is important? Because if I have the afferent copied, so this experiment is very nice, it's very daily living. You need to tap it in order for the ketchup to go down and then to squeeze it properly and have your ketchup. When you take the ketchup bottle, if you are doing it yourself, so left hand and right hand or the other way, what we can measure is that the grip, so when you tap it, you need to have a stiffened grip to assure that it doesn't slip. So if you are doing with your hands you can align perfectly the increase of the grip with the tapping. That's are the two green and red lines in the first panel, in the upper panel. This green and red superimposed. While somebody else tap it, your brain does not an internal representation and needs to what is your brain doing increase so to be ready to everything because you don't know exactly the pressure applied be increased according to the feedback received for the load so this the grip is higher by a bias and then when the load is increased the grip followed. To split apart these two conditions we need this sense copy which allows us to have a prediction of the next sensory feedback. So starting a movement which is exactly of a level of force so that gripping can exactly. While if another body someone else is doing the tapping of course I predict that the tapping is arriving so I start squeezing a little bit so having a harder grip but then depending on I will adapt the soap and this is another very interesting examples which I want to go through in details, you find it in the compendium, it's totally explained. And it's again, what is nice is that it accounts twice for a night. So observation, the empirical observation that physical conflicts tend to escalate. And they proved by a very nice experimental protocol, and I invite you to study it, the fact that since when you attenuating the perception of that pushing, because it's your own action, to mimic the same level of pressures, you increase it. So if she pressed, finger and then I have to reproduce the same pressing on my finger. Since there is this attenuation of the consequences of my own actions, a sensor in between the two fingers will measure a higher pressure for me to get the same perception. So this mechanism which is super important to guide attention because usually what is consequence of what I am doing is something that is very predictable why if something comes from an external input needs immediate attention okay so saving the reasons in our brain makes it the effort and the attention on the let's say dangerous external inputs much than the consequence of my own actions and this experiment is nice because it is a super but very well measured experiment so one sensors two fingers and people having a very pure demonstration of that that's a nice "Acquaintance to Experimental Design," which might be very interesting toward your thesis. So I invite you to read it. By the way, it's published on Science, so usually. And the same kind of confirmation was done by the, why can't you tickle yourself? Tickling is a very specific perception But, and as soon as you do it, since you have the image of what you are doing, the tickling perception is kind of cancelled out. You can't tickle yourself. And actually this was proved by using a robot tickling and moving. And what is nice is that you can see that if the robot is producing the tickling with a delay, with respect to their own inputs or with the rotation with respect to the direction input by the subjects the more this delay is larger and the more it is rotated so the less is similar to the motor commands the more the tickling experience is reappearing so This is self-produced, this is externally produced. The more the robot is delaying self-produced tickling, and the more the robot is rotating the self-produced tickling, the more it becomes similar to an external input, even if it is the consequence of the subject itself moving the joystick. And then there is another way to study motor control, which is about studying impairments in motor control. And so pathological conditions which impaired motor control. For example, schizophrenia patients can experience the self-tickling because if they have the... The passivity of experience is symptoms. Passivity of experience means somebody is moving my hands. So they move their hands, but they are experiencing them to be passive and somebody else doing inside their arm the movements. If they have these symptoms active, which is very, schizophrenia is a very large spectrum so it depends on the symptoms they can have external self tickling and external tickling absolutely the same so no differences then if they do not have symptoms they symptoms of external passivity they are similar to normal subjects question how to train the inverse model So we have already sketched this. It's the same sketch. So we have the desired trajectory which goes to the inverse model which produces the motor feedforward motor commands. The motor commands go to the body, the controlled object. Sensory feedback produces information about the actual trajectory. actual trajectories compared to the desired one and we have a trajectory error. To move, to transform a trajectory error into a change of motor commands, we still need another model because trajectory error is again this realm. Why corrective motor commands is in the muscle language. And this is the feedback controller. Inverse model can be trained by the feedback controller. Why? Neural network. Machine learning needs the error on the output. You train machine learning. Supervised learning needs the label, desired output versus actual output, error, bad propagation with whatever complex algorithm. The error on the output. And it's the same here. But now, and then we can even increase the complexity about motor control, which is not just a fixed range between the feedforward and the feedback. But feedforward and feedback can play differently according to the environment. So the famous example on this is if you are playing tennis in a foggy day, your preparation and gesture will mostly based on your prediction. So you know where the other player is, you have seen the gesture, you predict that the ball will arrive there. While if you are playing in a sunny day, your prediction is much more, your feedback is much more confident and so you can interplay between what is the predictive estimation and the sensory feedback. This interplay between the estimation and the feedback is what controllers use when they apply Kalman filters. Kalman filter changes the importance of the experience with respect to the importance of the feedback. And this is what our brain does as well. Now, let me conclude with this complex picture, which is complex, I know, but if you follow, I think we can manage. So, we are disregarding the fact that we have an She is there. Okay, they are all the same. Okay, let's understand what is on each of them. On each of them we have the desired trajectory which is converted into the inverse model. It goes to motor commands to the body and then we have a feedback which goes, which produces audio. Sorry, we have a feedback coming here. The feedback is compared with the predicted sensory feedback, which is produced by the forward model. The forward model received the reference copy, so the same motor commands here goes here, actually a copy of it. The forward model produced the predicted sensory feedback. You received the sensory feedback, and then you have a prediction error. The prediction error is used to update the forward model because it's an error associated to its output and it's then converted by the feedback motor command into a motor error. This motor error is used to train, to adapt the inverse model. So this is, let's say, designed in a different way but it is... the same that we have seen a couple of slides ago. Okay? That's it. Except for the fact that the trajectory error is also adapting the feedforward, the forward model. This. But now we have all this structure above, which if you look, it's a very transversal layer down there. which is called the responsibility estimator. The responsibility estimator is giving a weight. So, a weight to what? To the error, to the error, to the motor command. And this weight depends on what? On this input, which is the comparison between the likelihood of the model and the prime responsibility predictor. What is this? the level of importance, so responsibility, the level of responsibility that this model, so this single sheet in the execution of the task. So what we are now doing is saying the brain does not have an inverse forward, so a set of internal models that works for every task, but primitives. So multiple sheets, primitives, make a specific, let's say simple task. And then there is a responsibility estimator, so a high level system that calls into play the different primitives. So sitting, talking, I'm moving my hands, I'm keeping balance for the movement of my hands. Let's split this. There is a component, there is a hand component, there is a sitting trunk control, there is a voice component. All this goes together, are running together. Each of them has different responsibility to the overall gesture. Each of them needs to have a responsibility and being corrected by the same responsibility. So if I fall down, it's not that my grasping was not proper. It's about my trunk control. So every single module is weighted in the motor command and in the importance of the error by the same responsibility weight. And then this responsibility weight is associated to the likelihood of the model with respect to the responsibility predictor. So let's do this example. This example is a walking importance for this task? No. So the prior is there is no importance or very low importance of that module. Okay? But still, responsibility predictors need to be updated. So it's all about the managing of the production of the output and the, let's say, direction of the feedback into a system which is a modular system. So it's made by multiple modules. It's not a single unique internal model. So to simplify and to prove that this is the way our brain works, the main proof is about the fact that we are very fast in recollecting previous... So for example, if you go to the... if you in Milan you come from far away, in Milan you don't have the bike. and you go by other means. And then as soon as you go back to your place where you have your wonderful bike, you start biking without. So all what you have learned in between has not changed the module of the bike, which remains there. And to account for the persistence of capacities, A modular system is essential because if you have a unique system whatever change in your think about the neural network. If you use a unique neural networks and you give back an error you are changing the whole network and this changes eyes to the next input. If you have multiple neural networks and you select which one to use and then you train them depending on the error. The same way as the way you have done in using them, you will adapt the weights of the work only for the modules that you have used and according to the responsibility you have given to each module. Okay, I think today we are done enough. Please look at everything back with your questions Monday actually. I will try to share the recordings soon but sometimes the system takes some time to give them to me. Guys from home, come.
.+0125