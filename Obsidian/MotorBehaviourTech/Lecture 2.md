
***
Date: 17/09/2025

# <span style="color:rgb(223, 109, 109)">EMG: Analytical Method in Healthcare</span>

**The following are some applications for which Electromyography signal can be used:**
Then first we have in the left column the field and in the right column specific uses.

| Field            | Uses                                                                                  |
| ---------------- | ------------------------------------------------------------------------------------- |
| Medical Research | Gait and Posture analysis \| Diagnosis of muscles, neurons and central nervous system |
| Rehabilitation   | Surgery \| Accidents \| Neuro rehabilitation \| Physiotherapy                         |
| Sports           | Biomechanics \| Rehabilitation \| Training                                            |
| Ergonomics       | Pain prevention \| Ergonomics deisng                                                  |
Gait $\rightarrow$ Marcha    

# <span style="color:rgb(223, 109, 109)">Muscular Structure: EMG and Contraction</span>


![[EMG_Signal_Hierarchichal_structure.png|500]]

The image is a detailed diagram of the **hierarchical structure of skeletal muscle**.

## <span style="color:rgb(239, 179, 1)">Attachment: Tendon and Bone</span>

![[Pasted image 20250917165849.png|300]]
Muscles connect to bones via <span style="font-weight:bold; color:rgb(2, 141, 192)">tendons</span>, which are strong connective tissues 
- **Origin** $\rightarrow$ The attachment at the [[proximal]] or fixed bone
- **Insertion** $\rightarrow$ The attachment at the [[distal]] or moving bone

## <span style="color:rgb(239, 179, 1)">Layers of Connective Tissue</span>

![[2e042f519b84277cc04106d5488386e91aae4b80-4500x3000.jpg]]
 
The muscle itself is organized like a bundle of bundles (*paquete de paquetes*), with three connective tissue coverings:
- **Epimysium** $\rightarrow$  surrounds the entire skeletal muscle.
- **Perimysium** $\rightarrow$ surrounds a fascicle (bundle of muscle fibers).
- **Endomysium** $\rightarrow$ surrounds each individual muscle fiber (cell).

These layers protect, organize, and help transmit force.

## <span style="color:rgb(239, 179, 1)">Muscle Fiber (Cell)</span>
![[Pasted image 20250917171745.png]]
Each **muscle fiber** is a long, [[multinucleated cell]].
Inside it, you find:
- **Sarcolemma** $\rightarrow$ the plasma membrane of the muscle fiber.
- **Sarcoplasm** $\rightarrow$ the cytoplasm, containing mitochondria and glycogen for energy.
- **Sarcoplasmic Reticulum (SR)** $\rightarrow$ stores calcium, essential for contraction.
- **Transverse (T) Tubules** $\rightarrow$ invaginations of the sarcolemma that carry action potentials deep into the fiber.

## <span style="color:rgb(239, 179, 1)">Myofibrils and Sarcomeres</span>

Each fiber contains **myofibrils**, long chains of repeating units called **sarcomeres**.

The **sarcomere** is the **functional unit of contraction**. It’s what gives skeletal muscle its **striated appearance**.

**Striated** just means the muscle looks like it has **stripes** when seen under a microscope. These stripes come from the way **actin (thin)** and **myosin (thick)** filaments are arranged in each **sarcomere**.


## <span style="color:rgb(239, 179, 1)">Filaments (Contractile Proteins)</span>


![[Pasted image 20250917173005.png]]


![[Pasted image 20250917085316.png]]

Within each sarcomere:
- **Actin (thin filaments)** $\rightarrow$ anchored (firmly attached) at the Z-line (boundary of sarcomere the thin filaments are anchored).
- **Myosin (thick filaments)** $\rightarrow$ located in the center.

When the muscle contracts:
- Myosin heads bind to actin.
- They “pull” the actin filaments inward, shortening the sarcomere.
- Shortening of many sarcomeres = contraction of the muscle.

## <span style="color:rgb(239, 179, 1)">Energy and Support</span>

- **Mitochondria** are abundant in muscle fibers because contraction requires a lot of ATP.
- **Capillaries** surround the fibers to supply oxygen and nutrients and remove waste.


## <span style="color:rgb(239, 179, 1)">In summary:</span>  

Muscles are structured in a hierarchical way:  
**Muscle → Fascicles → Muscle Fibers (cells) → Myofibrils → Sarcomeres → Actin & Myosin filaments.**  And functionally: **origin and insertion define movement**, while **sarcomeres generate contraction** at the microscopic level.


# <span style="color:rgb(223, 109, 109)">How a Muscle Contracts?</span>

![[8fd72329-ccb0-48c0-bdcc-237d41c12fc7.png|550]]
The real contractile part of the muscle fiber is formed by the myofibrils, which contain two main groups of proteins—actin and myosin—that move relative to each other during contraction. This process is triggered electrically:  the motoneuron sends an action potential to the muscle fiber, and although there is a short delay between the neuronal signal and the fiber’s response, the sequence is very precise. The sarcomere, the basic contractile unit of the myofibril, is extremely small but plays a fundamental role.

**(1)** When the motor neuron’s action potential arrives, <span style="font-weight:bold; color:rgb(2, 141, 192)">acetylcholine</span> is released at the neuromuscular junction, **(2)** causing depolarization of the muscle cell and generating a muscle action potential. **(3)** This action potential leads to the release of calcium ions, **(4)** which activate the contractile machinery **(5)** and  allow the sarcomere to shorten. **(6)** The entire process requires energy, supplied by the hydrolysis of ATP into ADP. **(7)** ATP is continuously regenerated by mitochondria, either through aerobic metabolism (using oxygen, typical of endurance or postural muscles) or anaerobic metabolism (using glycogen and sugars, typical of fast, powerful fibers). In both cases, ATP is the essential molecule that makes contraction possible.

[Video of muscular contraction](https://www.youtube.com/watch?v=0JF4yQbk490) $\rightarrow$ Look for more complete explanation

# <span style="color:rgb(223, 109, 109)">Muscular Mechanical Model: The Hill Model</span>


![[Pasted image 20250917090751.png]]
This diagram represents a **non-linear mechanical model** of muscle, because real muscle behavior is not simply linear. Muscles show damping and elastic properties that can’t be described with a single spring constant.

- **F**: The external force applied to the muscle ends. The two terminals (left and right) represent the extremities of the muscle.
- **SE (Series Elastic component)**: This is a spring in series with the contractile element. It represents the elasticity of tendons and parts of the muscle itself that stretch when force is transmitted. It’s not a simple linear spring; instead, its behavior is non-linear, because tendons and muscle tissue resist stretching more and more as they lengthen.
- **PE (Parallel Elastic component)**: This spring is in parallel with the rest of the muscle. It represents the passive elasticity of the muscle fibers and connective tissue. Like SE, it is non-linear, because you can’t stretch muscle indefinitely—it stiffens progressively.
- **CE (Contractile Element)**: This represents the active force generated by the actin–myosin interaction in the sarcomere. It’s the “engine” of contraction, controlled by neural activation and dependent on ATP and calcium.
- **DE (Damping Element)**: This represents viscous, velocity-dependent resistance within the muscle. It accounts for the fact that muscle doesn’t contract freely—it has an internal resistance (damping) that makes its force-velocity relationship nonlinear.

## <span style="color:rgb(239, 179, 1)">Static (isometric conditions)</span>


![[Pasted image 20250917091128.png]]
Force F experience across the fiber, from one part to the other of the muscle are constituido by the parallel (CE, and DE) and serial (SE), and contractile element (PE).

Contractile element, represent the contractile capability of the muscle, before exerted by the serial element, we represent tendon force represented by linear SE.

![[Pasted image 20250917091345.png]]
The total force **F** experienced at the ends of the muscle is the result of the interaction of:

- The **parallel elements** (CE = Contractile Element, DE = Damping Element, PE = Passive Elastic).
- The **series element** (SE = Series Elastic), which represents the tendon and transmits the force outward.
    

So:

$F=FSE=FCE+FDE+FPEF = F_{SE} = F_{CE} + F_{DE} + F_{PE}$





F_SE_ is squared which answers the non-linear spring. and it depends on the difference w.r.t the linear resting position times the elastic constant.

Static isometric condition (components), what abt dynamics? speed of elongation of the model.

![[Pasted image 20250917091603.png]]

It is take into account by the damping element DE which increases the resistance by the derivate. The force is generated by the damper during motion (first derivate of the length of the damper which exponential a-value) which has also an elastic constant.


Now all forces together,

![[Pasted image 20250917091833.png]]

Active (brown) part (contractile element) has a maximum force exerted depends on the length relative to the length at the resting position. Maximum state of contraction depends on the length of the parallel element (active part).

We can add the pasive element which is the force generated by the parallel element PE, it practically exerts no force in a reduction of length relative to the resting condition, so that for the first part there is contraction generated by contractile while when you try to stretch further the muscle it will respond with a step force which avoid an easy stretching of the muscle. 

This model represent behavior of contractile-pasive characteristics of the muscle. 

The damping element is out because in isometric conditions the dumper doesn't generate any force. 

![[Pasted image 20250917092340.png]]

In dynamic conditions we have the maximum force exerted when the speed is null. In isometric condition would be at a maximum strenght of contraction, x-axis represent increasing speed, it has an increasing power generated by the model. The faster the contraction, the lower the force that will be generated by the model

With two characteristics together, it is what represent this kind of muscles. The force that can be exerted at isometric condition or a given speed by the overall model.

# Electrophysiology and Anatomy of the motor unit: MU

![[Pasted image 20250917092805.png]]

Motor unit, it is the one connected with how the signal is generated by a-motor neurons and the effect of the shape of the motor unit in the signal we want to catch.

It is conformed by the soma, the dendrites, the motor neuron. The soma of these motor neuron are inside of the spinal cord. The image represent the section of a muscle in which we see the muscle fibers and inside it there are cells and there is one motor neuron in each muscle fiber is attached, fibers which a-motor neuron innervate.

#review 
==Innervation ratio of MU:: represent the number of motor neurons and their connection to the muscular fibers (10-1000, ten motor neuron innervates= thousand muscular fiber)==

In order to have some kind of force distribution along the muscular fiber to generate contraction of muscular fiber, not only is generated by a single motor neuron connected by a single fiber. It is related to the capability of controlling the contraction (starting with the a-motor neuron)

**Where Motor Unit are located?**

![[Pasted image 20250917093652.png]]

They are present in the spinal cord. right part shows 7 segments of the spine, each vertebra body has a function of supporting the spinal cord but also (on left), there is a green region which contains motor-neurons coming from the upper part of the CNS (Central nervous system) and they go to peripheral nerves that control the movement of muscles which are innervated  in that location.

![[Pasted image 20250917094008.png]]

what we see is the gray matter that contains the motor-neurons soma (previously the green region), there are two root, the ventral root which contain the motor neuron soma, and the white matter is compound essentially with axons from the dorsal root we've sensory neuron soma...

Motor unit start from the gray matter and go towards the peripheral nerves 


![[Pasted image 20250917094253.png]]

Each one of motor unit innervate a group of muscular fibers, and innervation correct for each motor unit.

depending on the task a different innervation ratio. (no high accuracy, bigger innervation ratio) depending on the activity of the muscles there is a certain innervation ratio.

It is no longer true that the end plate isn't in the middle of the fiber thus action potential will be bidirectional.

![[Pasted image 20250917094928.png]]

A model which pretends to show the maximum resolution of the fired potential in the motor unit depending on the number of motor neurons. The action potential is possibly moving in two directions. if we put a couple of electrons E+ and E-. Yellow spots represent the places of the fibers which receive excitation from the P (black plates) closer to the electrodes. This set of several muscular fibers is related to a single a-motor neuron, what happens is that we'll have a ...
![[Pasted image 20250917095331.png]]

A series of action potentials. In red and blue arrows there is the direction of propagation of the action potentials. Changing the direction of propagation will arise the typical shape of a single motor fiber APs. And they start from left to right. There are different shapes on each single fiber, but the complete measurement takes them all summed up (a+b+c+d), if we would like to take them individually it would have to be done with single-fiber electrodes, but what we take in the sum of all single fiber, thus the AP contained in the motor unit. This action potential of this particular motor unit (MOTOR UNIT ACTION POTENTIAL)

![[Pasted image 20250917095706.png]]


# The motor unit action potential (MUAP)

![[Pasted image 20250917095828.png]]

One source of electrode measurement w.r.t other will include a delay.
Amplitude of the individual fiber AP's depend on the distance between the electrode and where the AP is taking place. 

tau_d, distance between end-plates / conduction velocity (constant)
![[Pasted image 20250917100607.png]]



![[Pasted image 20250917100622.png]]

If we sum all the AP's we have longer duration and higher amplitude - property of the sum, which also change the shape, it goes from a purely biphasic phase to show two negative regions and one positive regions.

Also, changing the number of fibers recruited will change the regulation of the muscle force.

If I increase the frequency, I would theoretically increase the force. 



