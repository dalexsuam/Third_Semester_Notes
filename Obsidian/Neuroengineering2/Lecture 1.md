
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
We start from the **desired trajectory**, which represents the target or the desired sensory state. This desired trajectory is processed by the **inverse model**, which generates the **feedforward motor commands**. These commands are then sent to the **body**, where they activate the **muscles** and produce movement.

As the body moves, **sensory feedback** (from proprioception, vision, etc.) provides information about the **actual trajectory** achieved. This actual trajectory is then **compared to the desired one**, and any **difference or error** is detected.

That **error signal** is processed by a **feedback controller**, which generates an additional corrective input to the motor commands — allowing fine-tuning of the movement during execution.

Moreover, this same **error** can be used to **train or adapt the inverse model**, because there is always a learning process occurring. Over time, this learning helps the brain improve the accuracy of its feedforward predictions, making future movements more precise and efficient.

Then,if a difference is detected (a _motor error_), this information can be used in two ways:

- To **update the inverse model** (learning and adaptation), or
- To **produce a feedback correction** during the movement.
    
For example, if I realize my hand is slightly off-target, I can make an adjustment — adding a feedback correction on top of my feedforward control.

In summary:

- The **inverse model** provides the anticipatory, feedforward component.
- The **feedback controller** refines the motion using real-time sensory information.
- Together, they form a closed-loop system that balances **speed** and **accuracy**.
## <span style="color:rgb(239, 179, 1)">2. Forward Model</span>


![[Pasted image 20251019235707.png]]
Now, let’s add another important element: the **forward model**. The forward model provides an **estimation of our sensory state** — it predicts what our sensory feedback will be **before** that feedback is actually received.

In other words, based on the **motor commands** being sent to the body, the brain internally predicts the **expected sensory consequences** of those commands.

For example, imagine you’re looking at a bag in front of you. Now rotate your head from side to side. Has the bag moved?  Of course not — the bag stays still.  However, on your **retina**, the image of the bag has moved dramatically. Yet your brain does **not** interpret that as the bag itself moving.

Now, if the bag actually started moving on its own, you’d immediately notice something unusual — “What’s going on?”

This demonstrates that the brain distinguishes between:

- **Sensory changes caused by our own actions** (like turning our head), and
- **Sensory changes caused by external events** (like the bag moving independently).

To make this distinction, the brain needs to **predict** the sensory consequences of its own motor commands.  This prediction is generated by the **forward model**, which receives a copy of the motor command — called an **efference copy** — and uses it to estimate the expected sensory feedback.

The **purpose** of the forward model is to provide **perceptual stability**: it ensures that when we move, the world doesn’t appear to move with us. It also helps **modulate attention**, so we can focus on relevant external events — like noticing if the bag really moves on its own.

A simple demonstration of this concept is pushing gently on the side of your own eye. You’ll see the visual scene shift slightly. Your brain tells you that the image has moved because that action wasn’t produced by your eye muscles. If, instead, someone else pushed your eye, the shift would feel even stronger.

This shows that our brain constantly predicts and filters the sensory consequences of our own actions — a process that is essential for coordinated movement and perceptual stability.

So, our question is not _if_ this mechanism exists — we know it does.   The question is _how_ and _where_ it is implemented in the brain.
![[Pasted image 20251020000312.png]]
When we want to perform an action — let’s call it a **desired behavior** — the **inverse model** in our brain transforms this desired behavior into the corresponding **motor commands**.

A **copy of these motor commands**, known as an **efference copy**, is sent to the **forward model**.

Why is it called _forward_? Because, just like the body, it takes **motor commands as input** and produces **behavior or sensory feedback as output**. In other words, the **forward model predicts the sensory consequences** of the motor commands — it tells us what we should expect to sense as a result of our movement.

So:

- The **inverse model** maps **desired sensory states → motor commands**, while
- The **forward model** maps **motor commands → predicted sensory states**.
    
Together, they form a powerful internal loop that allows the brain to plan, predict, and adapt movements with remarkable precision.

**Why Is This Important?**
![[Pasted image 20251020075328.png]]


A clear everyday example of how forward and inverse models operate is given by the **ketchup bottle experiment**. To prevent a ketchup bottle from slipping, a sufficient **grip force** must be exerted to counteract the **load force** that occurs when the bottle is tapped.

When the load is **self-generated** — for example, when your **left hand strikes the bottle** while your **right hand holds it** — the brain can use an **efference copy** of the motor command to **predict the upcoming load**. As a result, the **grip force** increases _in parallel_ with the **load force**, showing _no temporal delay_.

This precise synchronization occurs because the **forward model** anticipates the sensory consequences of the motor command, allowing the nervous system to generate a perfectly timed adjustment.

However, when the load is **externally generated** — for example, when **another person** strikes the bottle — the brain has **no efference copy** to rely on, and therefore the load **cannot be predicted**. As a consequence, the **grip force lags** behind the load force and, to avoid slippage, the **baseline grip force** is **increased** as a compensatory mechanism.

This experiment elegantly illustrates the functional role of the **forward model**:  it uses the efference copy to **predict the sensory consequences** of our own actions, enabling **anticipatory adjustments** and **stable control** of movement.  In contrast, in the absence of such prediction, control becomes **reactive**, slower, and energetically less efficient.

![[Pasted image 20251020080213.png]]

![[Pasted image 20251020080240.png]]
Another very interesting example that highlights the importance of forward models comes from experiments investigating **sensory attenuation** — the reduced perception of sensations caused by our own actions.

Empirically, it has been observed that **physical interactions tend to escalate**: for instance, when two people take turns pressing each other’s finger with the same perceived intensity, the actual force applied tends to increase at every step. This happens because, when we perform an action ourselves, our brain **predicts** its sensory consequences through the **forward model** and **attenuates** the resulting perception. Therefore, to reproduce the same _felt intensity_ of a touch applied by someone else, we unknowingly apply **a stronger force**.

This mechanism is crucial for **attention modulation** — our brain saves resources by reducing sensitivity to the predictable consequences of our own actions, while remaining highly sensitive to **unexpected external stimuli**, which may signal potential danger or relevant changes in the environment.

The experimental setup for this study is elegantly simple:  
two fingers (one applying pressure, one receiving it) are connected by a **force sensor** that measures the actual applied force. Participants are first touched by an external source and then asked to reproduce the same pressure themselves. Consistently, the measured self-produced forces are higher, confirming the presence of **sensory attenuation**.

![[Pasted image 20251020080400.png]]
A similar demonstration of this principle is found in the question: **why can’t you tickle yourself?**  Tickling involves a specific sensory perception that is **strongly dependent on unpredictability**.  

When we attempt to tickle ourselves, the brain already has a **prediction** — via the efference copy — of the sensory feedback that will follow our own movement.  
Because the brain expects this stimulation, the sensation is **canceled** or **greatly reduced**.

This has been verified experimentally using a **robotic interface**: participants control a small robot that produces tickling movements.
![[Pasted image 20251020080416.png]]
When the robot reproduces their movements **without delay** or **rotation**, the sensation is strongly attenuated. 

However, when a **delay** or **rotation** is introduced between the subject’s movement and the robot’s action, the tickling sensation **reappears**. This shows that the more the feedback **deviates from the predicted sensory outcome**, the more it is perceived as **external**, and thus capable of generating the full tickling sensation.
![[Pasted image 20251020080610.png]]

These findings also provide insight into **pathological impairments of motor control**, such as those observed in **schizophrenia**. Some patients with schizophrenia experience the so-called **passivity phenomena**, in which they feel that their own movements are **controlled by someone else**.  

In these cases, the **forward model** and its **efference copy** seem to be impaired, disrupting the normal ability to distinguish **self-generated** from **externally generated** sensations.
![[Pasted image 20251020080718.png]]
Experiments show that schizophrenia patients **with active passivity symptoms** can experience **self-tickling** in the same way as external tickling — they do not show the typical sensory attenuation. 

Patients **without such symptoms**, on the other hand, behave similarly to healthy subjects, confirming the link between **motor prediction mechanisms** and **the sense of agency**.

## <span style="color:rgb(239, 179, 1)">How to train the inverse model?</span>

![[Pasted image 20251020080859.png]]
As we’ve seen, the **inverse model** converts a desired trajectory (or desired sensory feedback) into the appropriate **motor commands**. However, to make this mapping accurate, the system must **learn** from experience — it must adjust its internal parameters whenever the produced trajectory doesn’t match the desired one.

The **feedback controller** plays a key role in this learning process. The actual trajectory generates **sensory feedback**, which is compared to the desired trajectory to compute a **trajectory error**.  But this trajectory error exists in _kinematic_ or _sensory_ space, while corrective motor commands exist in _muscle_ (motor) space.  

Therefore, the brain needs another transformation — the **feedback controller** — to translate trajectory errors into motor corrections.

Over time, the corrections provided by the feedback controller are used to **train** the inverse model, just like in a **supervised learning** process.  

In machine learning terms:
- The **desired trajectory** acts as the _label_ or desired output.
- The **actual trajectory** is the _prediction_.
- The **error** between them is used for **backpropagation**, updating the inverse model so it can produce more accurate feedforward motor commands in the future.


![[Pasted image 20251020081619.png]]


Motor control is not static — the **relative importance** of feedforward and feedback control changes according to the reliability of sensory information.  
For example:

- In a **foggy tennis match**, visual feedback is unreliable, so the player must rely more heavily on **prediction** (feedforward control).
- On a **sunny day**, when sensory feedback is precise, **feedback corrections** become more dominant.

This dynamic balance is conceptually equivalent to a **Kalman filter**, where the system continuously adjusts the **weight** between prediction (the prior estimate) and feedback (the sensory evidence) according to their **respective uncertainties**. Our brain performs a similar computation — modulating trust in its internal models depending on the context and sensory reliability.

![[Pasted image 20251020081707.png]]
In the most comprehensive view, the brain doesn’t operate with a single monolithic inverse–forward model pair. Instead, it uses a **set of modular internal models** — or **primitives** — each specialized for specific motor subtasks.

Each module (or “sheet” in the diagram) contains:
- An **inverse model**, which generates motor commands.
- A **forward model**, which predicts the sensory consequences of those commands.
- Feedback pathways that update both models through prediction errors.

| ![[Pasted image 20251020081707.png]] | ![[Pasted image 20251020080859.png]] |
| ------------------------------------ | ------------------------------------ |
![[Pasted image 20251020081707.png]]
Above these modules lies a **responsibility estimator** — a higher-level mechanism that assigns **weights** (or responsibilities) to each module depending on their **relevance and reliability** for the current task. This estimator uses a Bayesian-like computation:

$$\text{Responsibility} \propto \text{Likelihood (model performance)} \times \text{Prior (expected importance of the module)}$$

In other words:
- The **likelihood** measures how well a given module’s predictions match the actual feedback.
- The **prior** encodes how relevant that module is expected to be for the current context.
    

For example:
- When **walking**, the leg-control module has a **high prior responsibility**, while the hand-control module has a **low one**.
- When **writing**, the inverse is true.  
    Yet all modules remain active to some degree, maintaining readiness for potential coordination demands.

A modular organization explains a fundamental feature of human motor learning:  the ability to **retain and recall specific skills** even after learning new ones.

If the brain had a single, global internal model, every new learning experience would overwrite previous mappings — similar to **catastrophic forgetting** in a single neural network.  
Instead, having **multiple internal models**, each trained independently according to their **responsibility weights**, allows for:

- **Selective adaptation:** only the active modules are updated.
- **Skill persistence:** previously learned modules remain intact.

That’s why, for example, you can **resume cycling** immediately after months of not riding — the **“bike control” module** is still stored and ready to be reactivated, unaffected by learning other unrelated tasks.