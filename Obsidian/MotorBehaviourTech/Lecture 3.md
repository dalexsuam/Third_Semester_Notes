
***
Date:18/09/2025

Resuming from last part...

![[Pasted image 20250918163529.png]]
The regulation of muscle force can be done by two means:
* By the number of fibers recruited
* To increase the force we have to rely on the frequency of fibers, having an increase on the number of fibers.

If we want to increase more, we increase the number of fibers and the frequency of the mechanism.

All of these are stochastic processes, so that's why they might be described as noise.

# The MUAPT (force regulation by increasing frequency)

![[Pasted image 20250918163916.png]]
Here we see the shape of a motor unit electrical activity, and this repeats in time almost equally no matter the shape of APs of fibers. 

Let's remember this shape is made up of the sum of all of the action potentials of single fibers APs.

We see for each line a motor unit action potential which is the summation of the several APs of the muscular fibers, their shapes vary and the reason is that they differ in motor units, and there is a timing effect. We see the shape repeats exactly during time this time is random, and makes the process stochastic. 

While the shape is the same, the time is different and it can be characterized as 
![[Pasted image 20250918164603.png]]

There is another way to manage the position of randomness in time by the use of the Dirac delta function in the convolution

![[Pasted image 20250918164812.png]]

Anyway, we start from a certain shape and we sum them up vertically as following shown

![[Pasted image 20250918164918.png]]

And this is how the electrical effect E(t) in overall time and spatial summation shows an stochastic output. Note that some cancellation between peaks take place, it makes smaller the EMG signal and the reason is because it happens to reduce the amplitude of the signal.

All of this is valid for a true iso-metric condition, the stochastic output, we do some measurements of EMG signal I should take into account I have to make an overall different measurements.

Now, up to this moment we've analyzed the signal generation, and will proceed with electrodes chemistry... 

![[Pasted image 20250918165949.png]]

# <span style="color:rgb(223, 109, 109)">EMG Electrodes</span> 

These are metallic objects placed on the body of the patient.

It allows to obtain an electrical signal from the body. And, spoiler alert, we do it with metallic electrodes.

The single electrode goes in saturation if we try to make a measurement for a long time, charges will acummulate in the electrode and will enter to a saturation stage, so that's why there should be something more in the electrode than a metallic, something that interfaces the electronic device which is interfaced with the body of the patient. 

During this interface anions and cations transduced into electrodes.

## Interface body-measurement device: Electrodes ions versus electrons as charge carriers

![[Pasted image 20250918170711.png]]
If we make current flow into this parallel of this two impedances, multiplying the current for the impedance we'll obtain the electrical information of the voltage signal coming from the body.

Having an electron impedance as just a resistor is making measurements with a galvanic current, the current crosses physically.

And then from the other scenario the capacitor would allow charges by displacement current, by alternate current (charges accumulate in one plate and bla bla...)


## Electrode-Electrolyte Interface

![[Pasted image 20250918171444.png]]

It is based on oxidation and reduction chemical reduction.

Oxidation means that neutral atoms free electrons, and

$C \rightarrow C^+ +e^-$

The cation spreads out to the electrolyte and the electron says in the electrode.

And we have the current in this sense (from left to right)

![[Pasted image 20250918171647.png]]

If we reverse the current, we'll be placing together 

$C^+ +e^- \rightarrow C$

And the current takes the opposite flow direction.

We can't use only reduction otherwise electrode would saturate without any electrones .

![[Pasted image 20250918172020.png]]

Oxidizing agents are reducing the number of electrons in the agent. These are part of the halogen family.

Reducing agents are all electropositive species. Na, K, Ca are mostly involved in the mechanism of generation of potentials in the body.

![[Pasted image 20250918172603.png]]

Here we see in each situation where reduction and oxidation is prevalent.

![[Pasted image 20250918172740.png]]

If we put the electrode and the electrolyte there would be an accumulation of charges and thus a capacitor in the boundary between the electrode and the skin (electrolyte). This double layer is a straight capacitor that increases the capacitive part of the impedance. It generates some kind of noise, the electrode is moving w.r.t the electrolyte and this capacitive effect will have in the measurement some noise related to the increase or decrease of the thickness of the interface, so that, if we don't take this into account we'll obtain a noise generator in low frequency associated to the electrode and this behavior would switch toward the electric capacitance and the resistance to obtain some pole...


There are two types of electrodes...

Polarizable and non-polarizable

![[Pasted image 20250918173312.png]]

For polarizable we'll never reach 0 frequency...

THE MOST USED ELECTRODE

![[Pasted image 20250918173522.png]]

This is behaved as a non-polarizable electrode. We pass through several reduction and oxidation processes and depending on the direction of the current we'll have a layer (deposit) on the electrode subtracting AgCl


![[Pasted image 20250918173846.png]]


Essentially the electrode changing the direction of the current, is corroded or is thickness is increased by the silver chloride. Silver chloride is also limited by dissociated capability.

![[Pasted image 20250918174143.png]]

This shows how the electrode is built


![[Pasted image 20250918180422.png]]

This is the equivalent circuit of the electrode. 

Nernst Equation

To compute the semi-element potential of the electrode-electrolyte interface w.r.t a standard semi-element potential Eo which corresponds to the hydrogen electrode (or helium, id remember) Eo = 0, Depending on the initial concentration of ions the semi-element potential of the electrode-electrolyte interface is positive or negative w.r.t to E0...


![[Pasted image 20250918181007.png]]
We can complicate stuff but we won't go so in depth :) 


IMPEDANCE CALCULATION.

![[Pasted image 20250918181039.png]]

The rule is making the electrode work in where the gain is constant. 

ELECTRODE TYPES

![[Pasted image 20250918181937.png]]

Intramuscular Recording also neurophysiological EMG, we need to acquire electrical information from small portions. Particularly for looking at the status of neurons, alpha-motor neurons in patient's muscles.

Surface electrodes also kinesiological EMG, also used when patient is moving. During moving, we don't using depth cos they're needles! :)


SOME ELECTRODE TYPES: NEEDLES

![[Pasted image 20250918182243.png]]

Give information of measurements of muscular fibers. We have also, this kind of electrode which is called single fiber electromyographic signal (d) which is built by a conductive electrode which make all the way of the electrode inside the body and the position of the muscle fiber, it is a metal wire, a metal needle, and the needle outside is iso-potential, outside it is only a potential, and inside there is only a spot isolated around which makes it possible to use the electrode in very small areas of the muscle, called also, working volume, cos is part of the volume around muscle within the needle where the signal is detected. This is not motor unit action potential, but single muscle fibers.

We have the classical at a, we have another (c) the fine wire electrode.

![[Pasted image 20250918182801.png]]

what a pain, the needle's electrodes are painful.


![[Pasted image 20250918182945.png]]

Fine wires... 

![[Pasted image 20250918183114.png]]

Here a bit explained how it is placed.
 After being inserted can eventually move w.r.t the insertion point and we can't reposition them. They're stable during movement, but can't be adjusted.

We just pull them off to take them out


![[Pasted image 20250918183416.png]]

Surface electrodes are most used, however, they have less resolution, they don't measure activity of a single fiber. There are re-usable and disposable electrodes... If we look at figure (a) what we see is a section of a top-hat shape, the electrode is made by Ag-AgCl and we have in the other side connection by the wire.

Something similar are electrodes (b) plastic cup, these are disposable, they're small cost, and are also Ag-AgCl electrode and inside it you find also the electrolyte and another connector to connect the Ag-AgCl amplifier gel soaked sponge (avoid corrosion)

![[Pasted image 20250918184035.png]]


So, electrodes and characteristics. Due to its diameter (1cm) there is a bad effect of crosstalk, data acquisition of collecting signals not only in one specified place where I put the electrode but also nearby muscle activity.  

![[Pasted image 20250918184520.png]]


Popular places to place correctly electrodes, with respect to the landmark.

![[Pasted image 20250918184607.png]]
Fine wire sites, and surface sites...

