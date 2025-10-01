![[Pasted image 20250924101302.png]]
This is one possible implementation of optocouplers in order to isolate two main parts of an amplifier for EMG, to avoid them to be in contact for any hazard for the patient

![[Pasted image 20250925163555.png]]The
The main noise sources that might affect EMG detection signal:
* Interferences of the environment: before or after the measurement, bef: there are EMI noise irradiated on the body and after or during by various muscles...
* Error measurements, also depending on the wrong design of the system which might depend on variable electrodes impedances (interface between body and EMG machine) $z_1$ $z_2$ are impedances of the body and electrodes of the patient and can be unbalanced, ideally they're equal and stable in time
* After the electrode area we have the signal amplification and processing, we see we have a shadowed loop area which would create some interferences due to the variable magnetic field flux.
* Stray capacitances due to capacitance coupling which would produce stray currents.
We see there is a electrode grounded/reference voltage connected in the Left leg.

We can also classify noises as:

![[Pasted image 20250925164840.png]]

LF: double layer of electrode-electrolyte is variable thus it also produces noise.

![[Pasted image 20250925165705.png]]

Signal above has a un-stable baseline which changes due to noise.

This change on baseline could be to the motion of the patient or motion of the area.

It is LF noise and it is easy to be removed by filters.

![[Pasted image 20250925170156.png]]
By twisting the cable we change the direction of magnetic flux and it would somehow cancel out the noise produced by it.

EMG might be affected by heart crosstalk (1Hz peaks) thus stable correct electrodes placement is needed

![[Pasted image 20250925170212.png]]
Negative feedback (right leg drive circuit – safety and CMRR).

![[Pasted image 20250925172552.png]]
Here we show all the noise that we can find in any kind of electrophysiological signals.

Red block is the amplifier with all of its non-idealities which are generated in input signals.

![[Pasted image 20250925172527.png]]

![[Pasted image 20250925173810.png]]

Here we see noise coming from the environment. 

![[Pasted image 20250925174227.png]]

![[Pasted image 20250925174710.png]]


![[Pasted image 20250925175156.png]]

Inside of an INA IC, there are the three opAmps, and all of the resistors in the second stage has the same value cos it is gain 1. 

We can modify RG to get different gains, 


![[Pasted image 20250925181248.png]]


Do we connect it to the physical ground connection? 

![[Pasted image 20250925181602.png]]
![[Pasted image 20250925181929.png]]


![[Pasted image 20250925182202.png]]

There is a positive loop which would lead to un-stability. To avoid it we do the partition...

![[Pasted image 20250925182437.png]]


![[Pasted image 20250925182640.png]]


![[Pasted image 20250925182933.png]]


![[Pasted image 20250925183032.png]]

![[Pasted image 20250925183727.png]]

varicap diodes, change their capacitance by varying their voltage in reverse bias. 

Reverse bias controls the thickness of the depletion zone.

![[Pasted image 20250925184000.png]]



