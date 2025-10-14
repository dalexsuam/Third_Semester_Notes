
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

![[Pasted image 20251012185016.png]]
The total force **F** experienced at the ends of the muscle is the result of the interaction of:

- The **parallel elements** (CE = Contractile Element, DE = Damping Element, PE = Passive Elastic).
- The **series element** (SE = Series Elastic), which represents the tendon and transmits the force outward.

==When the muscle is **not changing length** (no motion), the damping element (**DE**) has **no contribution** (because velocity = 0)==

The total muscle force is determined by the **elastic** and **contractile** elements only.

So:
$$F = F_{SE} = F_{CE} + F_{PE}$$
where

- $F_{SE}$​: Force in the **tendon (series element)**
- $F_{CE}$​: Force produced by the **contractile fibers**
- $F_{PE}​$: Force from the **passive tissues**

The **series element (SE)** follows a **non-linear spring law**:
$$F_{SE} = \left(k_{SE}(L_{SE0} - L_{SE})\right)^2$$

It means the tendon’s restoring force grows **quadratically** with stretch — the further it stretches beyond its rest length $L_{SE0}$​, the stronger the restoring force.

## <span style="color:rgb(239, 179, 1)">Dynamic Conditions</span>
![[Pasted image 20250917091603.png]]

$$
F_{DE}​ = k_D​ \cdot \left(\frac{dL_{DE}}{dt} \right)^a ​​
$$
where $\frac{dL_{DE}}{dt}$​​ is the **speed of elongation** (the derivative of length).

When the muscle **changes length** (contracts or extends), the **damping element (DE)** becomes active. It produces a velocity-dependent force (often modelled proportional to the length rate $L$), so the full dynamic balance is:
$$F_{SE} = F_{CE} + F_{PE} + F_{DE}$$

$_{DE}$ thus captures viscous, rate-dependent resistance: it increases the force required when the muscle shortens or lengthens quickly.

## <span style="color:rgb(239, 179, 1)">Plot Analysis</span>

### <span style="color:rgb(161, 40, 226)">Static Conditions curve</span>

| ![[Pasted image 20251012192751.png]] | ![[Pasted image 20251012192722.png]] |
| ------------------------------------ | ------------------------------------ |
In steady-state conditions, stretching and contraction are shown

This plot shows how **muscle force** varies with the **static length** of the **contractile (CE)** and **passive elastic (PE)** elements during **isometric contraction**, where the total length of **SE + CE** remains constant.

- The **contractile element (CE)** generates **active force** (brown curve).  
    It reaches its **maximum** around the **resting length**, where the overlap between actin and myosin filaments is optimal.  
    When the CE is **too shortened** or **too stretched**, this overlap decreases and the force drops.
- The **passive elastic element (PE)** (blue curve) represents tissues like collagen that resist stretching.  
    It exerts **almost no force** when the muscle shortens or stays near its resting length, but once the muscle is **stretched beyond** that point, the PE generates a rapidly increasing force.  
    This response prevents excessive muscle elongation.
- The **total force** (green curve) is the **sum** of both contributions:  
    near the resting length it is mainly due to **CE**, while at greater extensions it is dominated by **PE**
- The **damping element (DE)** is **not active** in this static (isometric) condition, since it only generates force when the muscle **changes length over time** (i.e., during motion).


The **active component (brown curve)**, representing the **contractile element (CE)**, reaches its **maximum force** at a specific muscle length close to the **resting length**. This happens because the overlap between actin and myosin filaments is optimal. If the CE becomes too short or too stretched, this overlap is reduced and the active force decreases.

The **passive component (blue curve)**, generated by the **parallel elastic element (PE)**, remains almost **inactive** when the muscle shortens or stays near its resting length. However, when the muscle is stretched beyond that point, the PE begins to generate force, increasing rapidly and opposing further elongation. This behaviour prevents excessive stretching of the muscle.

The **total force (green curve)** is the **sum** of both active and passive contributions: it remains dominated by the active component near the resting length, and by the passive component at larger stretches.

Finally, in this **isometric (steady-state) condition**, the **damping element (DE)** does **not contribute**, since it only produces force when the muscle length changes over time (i.e., during motion).

### <span style="font-weight:bold; color:rgb(161, 40, 226)">Dynamic conditions curve</span>
![[Pasted image 20250917092340.png]]

This model describes how a muscle behaves when it is actually moving (shortening), as opposed to when it is holding a static position.

The fundamental rule is that there is a trade-off between force and speed. The muscle can produce its **maximum force when the speed of contraction is zero**. This is an **isometric contraction**, where the muscle is activating and trying to move but cannot shorten, like pushing against a wall.

However, as the **speed of the contraction increases**, the amount of **force the muscle is able to generate decreases**. This means a muscle contracting very quickly cannot produce as much force as it can when it is moving slowly or not at all.

This inverse relationship between force and speed is what creates the characteristic downward-sloping curve on the graph. The x-axis shows increasing speed (e.g., from 0.5 m/s to 2.0 m/s), and as you follow the curve to the right, the force level drops.

From this basic force-velocity relationship, we can identify different performance zones:

- **Maximum Strength (100%):** This is the peak of the curve, representing the maximum force the muscle can produce, which occurs at zero speed.
- **Strength-Speed (75-90%):** In this zone, the muscle is still generating high levels of force, but is now moving at a moderate speed.
- **Power (40-60%):** Power is the product of force and velocity. This mid-range zone is where this product is optimized, meaning the muscle is generating the highest possible power output by balancing a good level of force with a good speed of movement.    
- **Speed-Strength (30-40%):** Here, the priority is on moving quickly. The muscle is contracting at high speeds, but the force it can produce at this pace is relatively low.


# <span style="color:rgb(223, 109, 109)">Electrophysiology and Anatomy of the motor unit: MU</span>

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



