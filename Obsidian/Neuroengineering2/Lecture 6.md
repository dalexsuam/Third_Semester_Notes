
31/10/2025
***
# <span style="color:rgb(223, 109, 109)">Challenge-Based Control Strategies<br></span>
### <span style="color:rgb(161, 40, 226)">1. Concept</span>

![[Pasted image 20251102225018.png]]

After exploring assistive controllers — where the robot _helps_ the patient perform the task — we now move to **challenge-based control strategies**, where the principle is essentially the opposite:

> The robot introduces _additional difficulty_ during movement to **stimulate learning and enhance neural plasticity**.

The key idea is that if a participant learns to execute a movement **under more demanding conditions** (for example, with resistance or amplified errors), then performing the same movement under normal conditions will become easier.

This approach aims to **increase the effort, engagement, and activation of neural networks** involved in motor control and learning.
### <span style="color:rgb(161, 40, 226)">2. Rationale</span>

From neuroscience and motor learning studies, we know that **active effort** and **error correction** are essential for recovery.

- When a subject is challenged, they must recruit additional motor units and cortical regions.
- This can promote **stronger synaptic reinforcement** and lead to **better long-term motor recovery**.
    
Challenge-based training also helps keep the patient **mentally engaged and motivated**, since the task feels meaningful and requires real participation rather than passive movement.

### <span style="color:rgb(161, 40, 226)">3. Two Main Categories</span>

Challenge-based controllers are typically divided into two main types:

#### a) Resistive Strategies

![[Pasted image 20251102225258.png|300]]

In this case, the robot **increases the mechanical resistance** to the patient’s movement.

- The participant must exert more force to complete the motion, which enhances **muscular activation** and **motor control effort**.
    
- Over time, this can help strengthen the impaired limb and improve voluntary control.
    

Clinical studies (e.g. _Abdel Majeed et al., J. NeuroEngineering Rehabil, 2020_) have shown that requiring **higher efforts from the impaired limb** can significantly improve motor function, even in chronic stroke patients.

This approach is similar in spirit to traditional physiotherapy resistance training — but here, the robot provides **precise, programmable resistance** that can be safely modulated and monitored.

#### b) Error-Amplification (or Error-Augmentation) Strategies

![[Pasted image 20251102225420.png|300]]

This approach is based on the principle that _you learn by your mistakes_.

In healthy motor learning, the brain uses **movement errors** as key feedback signals to update and refine motor commands. Therefore, **amplifying those errors** can accelerate the learning process.

For example:

- During a reaching task, if a stroke patient tends to deviate from a straight trajectory, the robot can apply a **force field** that _amplifies the curvature_ of that deviation.
    
- The exaggerated error helps the brain detect the mistake more clearly and triggers stronger adaptive responses to correct it.
    

Several studies (e.g. _Sharp et al., 2011_; _Casellato et al., 2012_) demonstrated that using such **error-augmenting robotic fields** made participants move more accurately — at least temporarily — as their brain recalibrated to compensate for the exaggerated errors.

However, this approach doesn’t work equally well for all patients. It requires a **minimum level of cognitive and sensory function** to perceive and correct the error, so it’s best suited for patients with moderate, not severe, impairments.


# <span style="color:rgb(223, 109, 109)">Haptic Simulation</span>

![[Pasted image 20251102225455.png]]


Closely related to these challenge-based strategies is **haptic technology**, which provides **tactile or kinesthetic feedback** to recreate the sense of touch.

Haptics work by applying **forces, vibrations, or motion cues** to the user, typically through devices such as robotic gloves or exoskeletons.

This feedback allows the patient to _feel_ virtual or physical interactions — for example, the sensation of touching, grasping, or holding an object.

When integrated with **virtual reality**, haptics complete the sensory–motor–reward loop:

1. The patient sees a virtual object (e.g. a bottle).
2. They move their arm to reach it.
3. The robotic glove provides **force feedback** when the hand “touches” the object.
4. The patient feels the contact, recognizes success, and receives a **rewarding sensory confirmation**.
    

This closed-loop interaction (vision → intention → movement → tactile feedback → reward) is crucial for engaging **multiple brain networks** and strengthening **motor learning**.

Moreover, using **virtual reality** offers practical benefits:

- Fast switching between tasks (e.g., pouring water, brushing teeth, painting).
- High motivation through gamified, varied activities.
- Reduced preparation time compared to physical setups, which is critical in clinical environments where time is limited.

# <span style="color:rgb(223, 109, 109)">Non-Contact Coaching Robots</span>

### <span style="color:rgb(161, 40, 226)">1. Concept</span>

![[Pasted image 20251102230610.png|300]]

**Non-contact coaching** refers to the use of robots as **guiding and motivating agents** that interact with patients — and often with therapists — **without physical contact**.  
These robots act as **embodied coaches**, providing **verbal instructions, gestures, and encouragement** during rehabilitation or cognitive exercises.

Unlike assistive or haptic robots, which physically support or resist the patient’s movements, **coaching robots focus on engagement, motivation, and cognitive stimulation**.

### <span style="color:rgb(161, 40, 226)">2. Types of Coaching Robots</span>

Most coaching robots are **humanoid**, meaning they have a human-like shape (head, arms, or torso) but are **not fully anthropomorphic**.

- **Anthropomorphic robots** are designed to closely resemble and behave like real humans (e.g., realistic facial features, natural movements).
- **Humanoid robots**, instead, only share general human-like features — such as a head, eyes, or limbs — but in a **simplified, toy-like form**.
    

This distinction is important because humanoid robots often create a **friendlier and less intimidating interaction**, especially with vulnerable groups such as children or the elderly.


### <span style="color:rgb(161, 40, 226)">3. Rationale and Psychological Evidence</span>

![[Pasted image 20251102230648.png]]

Studies in psychology have shown that **embodied agents** — physical robots with a body — are **more engaging and motivating** than virtual or screen-based coaches.

For instance, an app or tablet may display the same instructions as a robot, but when the guidance comes from a **physical entity present in the room**, patients:

- Feel more socially engaged,
- Show higher motivation to perform the exercises, and
- Experience a stronger emotional connection with the activity.
    
In short, **physical embodiment enhances the therapeutic impact** of coaching.

### <span style="color:rgb(161, 40, 226)">4. Applications</span>

#### a) Elderly Care and Cognitive Training

![[Pasted image 20251102230743.png|3000]]

A practical example is the **Tiago robot**, a semi-humanoid mobile robot with a manipulator arm and a head. Tiago has been used to guide elderly people through **cognitive and physical training exercises**.

This application became especially valuable **after the COVID-19 pandemic**, when nursing homes were closed to visitors.  
The lack of social interaction and stimulation led to increased loneliness and cognitive decline among residents.

Robots like Tiago were introduced to:

- Lead simple **rehabilitation and mental exercises**,
- Encourage movement and interaction,
- Provide **companionship and engagement**,
- Support basic monitoring and simple service tasks.

The purpose is **not** to replace caregivers but to **complement human interaction**, keeping elderly individuals mentally and physically active.

#### b) Autism Therapy

Another important application is in **therapy for children with autism spectrum disorder (ASD)**.

Autistic children often respond positively to robots because:

- Robots behave in **simple, predictable, and repetitive** ways.
- They present **limited sensory input**, avoiding the overstimulation that can occur with human gestures, facial expressions, or environmental noise.
    
For example, when a therapist teaches a child to say _hello_, a human might do it with variations in tone, gesture, or body movement — which can be confusing for an autistic child.  
A robot, on the other hand, **always performs the gesture in the same way**, creating a **safe and consistent learning environment**.

The ultimate therapeutic goal, however, is **not for the child to bond with the robot**, but to **transfer the learned communication and social skills to human interaction**.  
Therefore, these sessions always involve **a triadic relationship**:

- **The therapist**,
- **The child**, and
- **The robot**, acting as a tool within the therapy.
    
### <span style="color:rgb(161, 40, 226)">5. Emerging Research Directions</span>

Some recent systems even integrate **EEG-based control** — for example, using **frontal electrodes** to monitor the patient’s mental state or engagement level, allowing the robot to adapt its behavior accordingly.

This approach shows promise for developing **personalized, adaptive coaching systems**, where the robot can modulate its encouragement or task difficulty depending on the patient’s level of attention or fatigue.
# <span style="color:rgb(223, 109, 109)">Summary of High-Level Control Strategies in Rehabilitation Robotics<br></span>

| **Strategy**                              | **Core Principle**                                                                                                                            | **How It Works**                                                                                                                         | **Advantages / Rationale**                                                                                                                                                                                                    | **Limitations / Risks**                                                                                                                         | **Typical Applications**                                                                                 |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **1. Assistive Control**                  | The robot **helps the patient** perform the movement when they cannot complete it alone.                                                      | The system detects the patient’s intention and provides **supportive forces** to complete the task (e.g., adaptive assistance).          | - Enables task completion even with weak motor ability.  <br>- Encourages participation rather than passive movement.  <br>- Can be adapted to the patient’s evolving capability (adaptive control).                          | - Risk of **over-assistance**, reducing patient effort and engagement.  <br>- May limit active learning if not properly tuned.                  | Post-stroke upper limb rehab, walking support, exoskeletons for gait assistance.                         |
| **2. Challenge-Based Control**            | “**You learn by doing something harder.**” Patients perform movements with **extra resistance or error amplification** to stimulate learning. | The robot adds **resistance** (requiring more effort) or **amplifies movement errors**, making the task more challenging.                | - Promotes motor learning through **error-based adaptation**.  <br>- Engages larger neural networks.  <br>- Increases strength and coordination.                                                                              | - Not all patients benefit (depends on severity and tolerance).  <br>- Must be carefully tuned to avoid frustration or fatigue.                 | Stroke rehabilitation, arm reaching tasks with robotic force fields.                                     |
| **3. Haptic Control / Haptic Simulation** | Use of **tactile and kinesthetic feedback** to recreate the sense of touch and interaction with virtual or real objects.                      | The robot or wearable device applies **forces, vibrations, or motions** to simulate real interactions (e.g., grasping a virtual object). | - Enhances **sensorimotor integration** and realism.  <br>- Increases immersion and motivation, especially in VR environments.  <br>- Enables repetitive, varied, and engaging exercises.                                     | - Complex hardware setup.  <br>- Needs precise calibration for realistic sensations.  <br>- May cause sensory confusion if poorly synchronized. | Virtual reality rehab for grasping, manipulation, or hand training using robotic gloves or exoskeletons. |
| **4. Non-Contact Coaching**               | The robot acts as a **motivational coach or guide**, using **social and verbal interaction** rather than physical contact.                    | Typically humanoid robots provide **instructions, feedback, and encouragement** through speech, gestures, or expressions.                | - Enhances **motivation and engagement** through embodied interaction.  <br>- Proven psychological benefit over screen-based coaching.  <br>- Useful when physical contact is unnecessary or impossible (e.g., elderly care). | - Limited physical assistance.  <br>- Effectiveness depends on robot design and social acceptance.  <br>- Must be supervised by therapists.     | Cognitive and physical training for elderly people, autism therapy, social skill rehabilitation.         |
## <span style="color:rgb(239, 179, 1)">Overall Comparison</span>

| **Aspect**           | **Assistive**                 | **Challenge-Based**                 | **Haptic**                             | **Non-Contact Coaching**        |
| -------------------- | ----------------------------- | ----------------------------------- | -------------------------------------- | ------------------------------- |
| **Interaction Type** | Physical (supportive)         | Physical (resistive)                | Physical (sensory feedback)            | Social / Cognitive (no contact) |
| **Goal**             | Facilitate movement execution | Enhance learning through difficulty | Recreate realistic touch and immersion | Motivate, guide, and monitor    |
| **Patient Role**     | Assisted performer            | Active learner                      | Interactive participant                | Motivated trainee               |
| **Robot Role**       | Helper                        | Challenger                          | Feedback provider                      | Coach / Companion               |
| **Main Focus**       | Support & safety              | Learning & adaptation               | Sensory integration                    | Engagement & communication      |


# <span style="color:rgb(223, 109, 109)">Conclusion — From Assistance to Challenge: The Spectrum of Robotic Control in Rehabilitation<br></span>
![[Pasted image 20251103080248.png|4000]]

We have seen different control strategies in rehabilitation robotics, and they can be summarized along a continuum that represents the balance between **robot contribution** and **user contribution** during a task.

At the **left end** of the spectrum, the **robot performs most of the task** — this happens when the patient is unable to contribute actively. These are **active-assist solutions**, where the robot provides full or dominant assistance to ensure the movement is completed safely.

As we move to the **middle region**, both the **robot and the patient** contribute to the movement. Here, we find **assistance-as-needed controllers**, which dynamically adjust the robotic support according to the user’s voluntary effort. The goal is to progressively encourage active participation while still ensuring success.

Then, there is a zone where the **user performs the entire task**. The robot, in this case, may not assist but still plays an important role — for instance, in **transparent mode**, where the exoskeleton allows the user to move freely while continuously **measuring and monitoring** the performance. Achieving true transparency is technically demanding, since the robot must perfectly compensate for its own weight and dynamics to remain “invisible” to the user.

Finally, at the **right end of the spectrum**, we find **challenge-based controllers**, where the robot deliberately increases task difficulty — by adding resistance or amplifying errors — to promote greater voluntary effort and motor learning.

The **non-contact coaching robots** also belong to the area where the user fully performs the task, as they act as **motivational guides** rather than physical assistants.

Overall, the **progress in therapy** — or more precisely, **patient progress** — can be visualized as a gradual movement from the left to the right of this continuum:

- starting from strong robotic assistance when impairment is severe,
- moving toward adaptive and then transparent modes as the patient improves,
- and eventually introducing challenge-based training to consolidate recovery.

# <span style="color:rgb(223, 109, 109)">Detecting the Subject’s Intention</span>

![[Pasted image 20251103080650.png]]
Now we move to our final topic — **the detection of the subject’s intention**.

For a robot to operate properly in rehabilitation or assistive contexts, it must be able to **understand what the user intends to do**. This concept of “intention detection” is fundamental, because it allows the system to decide _when_ and _how_ to assist or respond.

The sensors and methods used to collect human intention can be applied in both **rehabilitation robotics** and **neuroprosthetics**, since both aim to interpret voluntary commands from the user’s body or brain. In this sense, the two fields are **converging** toward similar technological solutions.

A robot that detects intention can serve two main purposes:

1. **As a functional assistive device** – helping the user perform daily activities, promoting independence, and improving quality of life in chronic or home-based conditions.
2. **As a therapeutic device** – supporting **task-specific training** to facilitate motor relearning during rehabilitation.


# <span style="color:rgb(223, 109, 109)">Interfacing Humans and Robots</span>

## <span style="color:rgb(239, 179, 1)">Detecting Intention through Sensors</span>

![[Pasted image 20251103082711.png]]
To enable communication between the **robot** and the **human subject**, we need **sensors**.  A **sensor** is a device that converts a physical stimulus into a measurable and recordable signal.

![[Pasted image 20251103082737.png|300]]

In a rehabilitation or assistive setup, sensors allow an **exchange of information** between the robot and the user. Essentially, the robot must receive two types of information:

1. **Where we are** – this refers to the _status_ of the robot, the subject, and the environment.
    - It can be obtained through **internal sensors** (inside the robot) or **environmental sensors**, such as **cameras**, **RFID tags**, **magnetic sensors**, or other tracking systems that monitor the subject’s position and movements.
        
2. **Where to go or what to do** – this defines the _goal_ or _intended action_.
    - It can be pre-programmed within the system (for example, a virtual environment that instructs the robot to “grasp the bottle”),
    - or it can be inferred directly from the **subject’s intention**.
        

![[Pasted image 20251103082830.png|300]]
This last point is particularly important.  If the **robot responds to the participant’s intention**, it creates a **natural and continuous link between intention and action** — a principle that is essential for **neuroplasticity** in rehabilitation and equally crucial in **assistive devices for daily life**.  
The more smoothly the device follows the user’s intention, the more effective and intuitive the interaction becomes.
## <span style="color:rgb(239, 179, 1)">Where Can We Detect Human Intention?</span>

![[Pasted image 20251103082948.png|300]]

To detect human intention, we can extract signals along the **sensorimotor pathway** — from the **brain**, through the **spinal cord**, and finally to the **muscles**. Different methods correspond to different levels of invasiveness:

- **EEG (Electroencephalogram)** – Records field potentials from scalp electrodes; a **non-invasive** technique used in Brain-Computer Interfaces (BCI).
- **ECoG (Electrocorticogram)** – Measures local field potentials from **epidural or subdural electrodes** placed on the surface of the brain; **semi-invasive**.
- **Implanted Brain Arrays (MEA)** – Use **microelectrode arrays** inserted **deep into the brain** to record neural populations; used in **Brain-Machine Interfaces (BMI)**.
- **ENG (Electroneurogram)** – Captures electrical signals from **peripheral nerves**, representing neural activity before reaching the muscles.
- **EMG (Electromyogram)** – Measures **muscle activation** through surface or implanted electrodes, providing an indirect but practical estimation of intention.

In summary, the choice of sensor depends on the desired **balance between invasiveness, precision, and practicality**.


## <span style="color:rgb(239, 179, 1)">EEG-Controlled Neuroprostheses (BCI – Brain-Computer Interfaces)<br></span>
**Setting:**  
EEG-based BCIs rely on _scalp electrodes_ (wet or dry), typically placed according to the _international 10–20 system_. These electrodes record brain rhythms and event-related potentials (ERPs) to interpret user intentions without requiring any muscle activation.

**Principle and Data Processing:**  
The EEG signal can be analyzed to detect:

- **Motor imagery** patterns (event-related synchronization/desynchronization – ERS/ERD),
- **Movement-related potentials (MRP)**, or
- **Visual event potentials**, such as **Steady-State Visual Evoked Potentials (SSVEP)** and **P300** responses.

For instance, in SSVEP, the user focuses attention on flickering stimuli at different frequencies (e.g., 8 Hz vs. 16 Hz). The brain’s response frequency reveals where the user is looking, allowing for command selection.  
The **P300 paradigm**, on the other hand, detects a characteristic brainwave occurring roughly 300 ms after the user sees an _expected_ stimulus—often used in _spelling interfaces_ for ALS or locked-in patients.

**Challenges:**  
EEG BCIs require long setup times (often over 15 minutes) to check electrode impedance and calibrate the system. Each session demands recalibration, and users must undergo extensive training to learn to modulate their brain rhythms effectively.  
Another challenge is **BCI illiteracy**, meaning that not all users can generate reproducible EEG patterns suitable for control.

Despite these difficulties, EEG remains the **most non-invasive and widely applicable** technique, suitable for users with no residual motor control.

## <span style="color:rgb(239, 179, 1)">Multi-Electrode Array-Controlled Robots (BMI – Brain-Machine Interfaces)</span>

**Setting:**  
Invasive BMIs employ **microelectrode arrays (MEAs)** surgically implanted in the **motor cortex (M1)**, typically over areas corresponding to specific body parts (e.g., the hand area). Each array (about 4×4 mm) records the activity of individual or small groups of neurons.

**Data Processing:**  
Signal processing includes **spike detection**, **sorting**, and **classification** to extract meaningful neural firing patterns.  
A **neural decoder** then translates firing rates into control signals for robotic arms, often using _linear models_ that relate neuronal activity to movement velocity or direction.

**Challenges:**  
While MEAs provide the _most direct_ link between neural activity and robotic control, they involve **highly invasive surgery**, **infection risk** (due to bypassing the skull and blood-brain barrier), and **long, intensive training** — often months of practice (e.g., 3 sessions per week, 4 hours each).  
Moreover, they capture only a **very limited portion** of the brain’s full activity—“a keyhole view of a huge system.”  
Thus, while performance can be impressive (as in Collinger et al., _Lancet_, 2013), such systems currently remain **research-oriented** rather than clinically practical.


## <span style="color:rgb(239, 179, 1)">ENG-Controlled Robots (Electroneurograms)</span>

**Setting:**  
ENG systems record signals directly from **peripheral nerves** using **cuff electrodes** or **TIME electrodes**. This approach captures action potentials from nerve fibers, offering a middle ground between invasive and non-invasive systems.

**Applications and Processing:**  
ENG recordings can be used to trigger specific **motor actions**—for example, stimulating the **peroneal nerve** to correct _drop foot_, or controlling prostheses for **amputees** by reading efferent motor activity from the stump nerves.  
Machine learning algorithms are often applied to classify the recorded signals into specific movement commands.

**Challenges:**  
Although less invasive than cortical implants, ENG still requires surgery and fine positioning of electrodes around nerve bundles.  
Signal specificity can be both an advantage and a limitation: controlling multiple fine movements may require **multiple implants**.  
Training and calibration remain essential, and so far only **few pilot studies** have demonstrated its clinical applicability.



## <span style="color:rgb(239, 179, 1)">EMG-Controlled Robots (Electromyograms)</span>

**Setting:**  
EMG systems record electrical activity produced by **muscle contractions**, typically via **surface electrodes** placed over residual muscles.  
Signals are generally filtered within the **10–500 Hz** band and processed to extract the **myocontrol envelope** or to implement **ON/OFF** and **impedance-based** controllers.

**Advantages and Applications:**  
EMG is **non-invasive, inexpensive, and easy to use**, making it the most practical option when the user retains _some residual muscle activity_.  
It is commonly used for **prosthetic control** and **rehabilitation robots**, where muscle activity is sufficient to trigger or modulate assistance.

**Challenges:**  
However, EMG suffers from **signal instability**, **cross-talk** from adjacent muscles, and **sensitivity to electrode placement**.  
Furthermore, when control must be achieved through muscles unrelated to the desired movement, the resulting actions can feel **unnatural** and cognitively demanding.
## <span style="color:rgb(239, 179, 1)">Summary Table</span>

|Technique|Level of Invasiveness|Signal Source|Key Advantages|Main Challenges|
|---|---|---|---|---|
|**EEG (BCI)**|Non-invasive|Brain (scalp potentials)|Safe, widely applicable|Long setup, training, low signal quality|
|**MEA (BMI)**|Highly invasive|Cortical neurons|High precision, direct brain link|Surgery risk, infection, intensive training|
|**ENG**|Moderately invasive|Peripheral nerves|Natural control, sensory feedback|Surgery, signal specificity, few studies|
|**EMG**|Non-invasive|Muscles|Simple, low-cost, reliable if residual control|Crosstalk, instability, limited functionality|

# <span style="color:rgb(223, 109, 109)">Clinical Guidelines for Clinicians</span>

**Definition and Purpose:**  
Clinical guidelines are official documents published by recognized **medical associations**—such as **ESMO** (European Society for Medical Oncology) or **ASCO** (American Society of Clinical Oncology)—that summarize the _best available scientific evidence_ to guide physicians in making clinical decisions.  They provide structured recommendations on which treatments or interventions are **strongly recommended**, **fairly recommended**, or **not recommended** for specific medical conditions.

![[Pasted image 20251103085541.png|500]]
## <span style="color:rgb(239, 179, 1)">Role and Importance:</span>  
For clinicians, guidelines act as both a **scientific reference** and a **legal and regulatory framework**.  
When a doctor proposes a treatment, following the corresponding guideline ensures that the decision is supported by the medical community and current standards of care.  
If a physician decides to go _against_ the guidelines, they must be able to provide solid clinical reasoning—otherwise, they could be held accountable in legal or regulatory reviews.  
Therefore, working _within_ the guidelines provides a kind of **protective shield** for the clinician, guaranteeing that their actions are justified according to accepted medical practice.

However, this also means that guidelines can sometimes act as **constraints**.  
For complex patients, where individualized treatment might require innovation or deviation from standard approaches, rigid adherence to guidelines could limit creativity and potentially overlook personalized solutions.

## <span style="color:rgb(239, 179, 1)">Economic and Administrative Impact:</span>  
Guidelines also have strong **economic implications**, since **health insurance systems** and **public healthcare providers** often base their **reimbursement policies** on these documents.  
If a treatment is listed and approved within a guideline, it is generally reimbursed.  
In contrast, off-guideline treatments may not be covered, meaning the patient (or provider) must bear the cost.  
Thus, guidelines influence not only clinical decisions but also **healthcare accessibility and funding**.

## <span style="color:rgb(239, 179, 1)">Updating and Evidence Integration:</span>  
Because medical knowledge evolves rapidly, guidelines are **regularly updated**, typically every few years, to integrate new evidence, technologies, and therapeutic options.  
This ensures that they reflect the **current state of the art** in medicine.

## <span style="color:rgb(239, 179, 1)">Example: AHA/ASA Guidelines for Stroke Rehabilitation (2021)</span>

An example mentioned in the lecture is the **AHA/ASA Scientific Statement** on the _Primary Care of Adult Patients After Stroke_ (Kernan et al., _Stroke_, 2021).  
These guidelines classify recommendations based on the **strength of evidence and clinical indication**, using a hierarchical system:

- **Class I** – Strongly recommended interventions (clear benefit).
- **Class IIa** – Reasonably recommended interventions (moderate benefit).
- **Class IIb** – May be considered (less robust evidence).
- **Class III** – Not recommended (lack of benefit or potential harm).
    
In these 2021 stroke care guidelines:

- **Robotics** and **Functional Electrical Stimulation (FES)** are included under **Class II** recommendations—meaning they are supported by evidence and considered beneficial in many cases.
- **Assistive devices** for balance and mobility training, by contrast, are classified as **Class I**, indicating _strong clinical support_ for their use in stroke rehabilitation.
    
This shows that **robotic and assistive technologies** are now recognized as integral components of modern neurorehabilitation, validated by leading health authorities such as the **American Heart Association** and **American Stroke Association**.


  



