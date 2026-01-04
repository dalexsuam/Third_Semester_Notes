
Date: 16/10/2025
***


![[Pasted image 20251016163558.png]]
In strain-gauge systems, you usually find **four main wires**:
- **Two wires for bridge excitation** (bridge supply: $V^+$ and $V^-$)
- **Two wires for the bridge output** (differential output voltage)

This corresponds to a **full-bridge configuration**.

#### <span style="color:rgb(2, 141, 192)">Why an extra “compensation” (sense) wire is sometimes used</span>

In practice, strain-gauge bridges often have **low resistance values**, typically around **100 Ω or even less**.  Because of this, when the bridge is powered, a **non-negligible current** flows through the supply wires.

Since the supply wires have their own resistance, a **voltage drop** occurs along the wires:
- You may _set_ the excitation voltage to **5 V** at the power supply,
- But the actual voltage at the bridge terminals may be only **4.8 V**.
    

This voltage drop depends on:
- The current flowing in the bridge
- The resistance of the supply cables
    

If not compensated, this causes an **error in the excitation voltage**, which directly affects the accuracy of the force or strain measurement.

#### <span style="color:rgb(2, 141, 192)">Compensation (sense) wire principle</span>

To correct this problem, an **additional wire**, called a **compensation wire** or **sense wire**, is used.
Key idea:

- The sense wire **does not carry current**
- Therefore, **no voltage drop** occurs along it
- It measures the **actual voltage at the bridge terminal**
    
This wire is connected directly to the **positive bridge supply point V+V^+V+** at the bridge.

#### <span style="color:rgb(2, 141, 192)">How compensation works</span>
![[Pasted image 20260103232853.png|400]]
1. The system measures:
    
    - The **desired excitation voltage** (e.g. 5 V)
    - The **actual voltage at the bridge** via the compensation wire (e.g. 4.8 V)
        
2. An **operational amplifier** compares:
    
    - The reference voltage (what you want)
    - The sensed voltage (what you really have at the bridge)
        
3. If the sensed voltage is too low:
    
    - The amplifier **increases the supply voltage**
    - This compensates for the voltage drop along the supply wire
        
4. The loop continues until:
    
    - The voltage at the bridge terminal $V^+$ is exactly equal to the desired value
        
When the two inputs of the operational amplifier are equal, the system is correctly regulated.
#### <span style="color:rgb(2, 141, 192)">Why this is important</span>

- The bridge output voltage is **proportional to the excitation voltage**
- Any error in the excitation voltage directly introduces **measurement error**
- Remote sensing ensures:
    - Accurate excitation
    - Better repeatability
    - Higher measurement precision



1.37.27.09.30
![[Pasted image 20251016163736.png]]

If we're measuring the common mode of the bridge V0. 1/2 of the voltage, this means that we have 1/2 of Vi. We should expect ~mV or less and have some volts of common-mode noise. Thus, we use INA which has a higher CMRR. The other reason is that all analysis assumes no resistance on the output terminals of V0. When, we are going to read the deformation, we'll load the output with the resistor as shown below...

![[Pasted image 20251016164020.png]]

Here, the best way to avoid the problem of the non-linear output of the bridge is putting a resistor of higher value, a high input impedance of the INA.

![[Pasted image 20251016164124.png]]

Concluding with load cells, here there are some possible realizations on the type of cannister shaped device and button shaped device, we see inside depicted the positions in which are based the strain gauges. The difference is that we have a compression load transducer on the left or on the right a extension type transducer. 

![[Pasted image 20251016164532.png]]

Piezo electric sensors can reach very low frequencies but no 0. 

They might work as two states:
As sensor: you apply a force and produces a charge
The inverse: When you apply a voltage to the transducer, you cannot indicate sensor in this case, the interest is the electric effect, it answers with deformation. 

So, direct and inverse depending on the direction.

Piezoelectric crystals are also used to stabilize frequencies with very high accuracy. 

![[Pasted image 20251016165221.png]]

There are different types of materials: crystals, ceramics, polymers. 

Advantage of the polymers w.r.t the others is that they're deformable and might fit in other surfaces (like the sole of a shoe)

We might face also changes in charge not only of change of pressure but also temperature.

![[Pasted image 20251016165657.png]]

As example. Let's look at the upper panel, we see a lattice a crystal lined, we have a symmetry which is also present when it is compressed. Then below, we have another behaviour that if you compress or stretch the material , the would be a variation in the position of the atoms which form the crystals and this variation generates piezoelectricity, 
voltage upon the extremities of the crystal. 
![[Pasted image 20251016165902.png]]
There is another example. Here, we change one of the charges of this crystal line lattice, and this mean we're displacing charges on the material and are propagated to the surface of the material. and this is smt valid for anything: crystals, ceramics, ...

![[Pasted image 20251016170013.png]]

In the case of ceramic, we have this behaviour, as before, obtaining voltage when compressed but we see the material moving.

Here unlike the crystals we can exploit curie temperature. 


![[Pasted image 20251016170615.png]]

Atom is asymmetrically displaced from a to b and would generate voltage.

Perovskite crystals are the most used. which require to be polarize to function properly. 
![[Pasted image 20251016170843.png]]

We see here where atoms are located. 

![[Pasted image 20251016170914.png]]

poling... If you wanna impose stimulation from outside, this breaks this domains all in the same direction. Also, the right pic shows how to obtain a magnet... 


![[Pasted image 20251016171159.png]]
Here we see what happens with the polarization of the poling of the crystal ceramics. 

![[Pasted image 20251016171852.png]]

![[Pasted image 20251016172126.png]]
![[Pasted image 20251016172512.png]]

Why the permitivity (dielectric constant) is importat? Cos it is an electric generator behaves as capacitor which are generated by two plates of the surface of the sensor and has a value which depends on the dielectric constant and it will change depending on the material. 

Why there are some materials with ** in curie temperature? Cos it has to do with poling and these materials shouldn't be poled cos they're natural crystals. 

Density of the material

Young Modulus...high in the quartz, low in the polymer 

![[Pasted image 20251016173258.png]]

K takes also the name of d33. 

d33 = 12pC/N ceramic
110pC, quartz

and 1.59 the polymer

![[Pasted image 20251016173441.png]]

![[Pasted image 20251016173627.png]]

![[Pasted image 20251016173737.png]]

![[Pasted image 20251016174039.png]]
![[Pasted image 20251016174518.png]]


![[Pasted image 20251016174916.png]]

We cut on the correct way the crystal, so there area different ways, and each has a different behaviour. The compression cut, a ring, or the shear in which if we compress nothing happens but if you apply stress you'll have an output. 

![[Pasted image 20251016180617.png]]

![[Pasted image 20251016180914.png]]


![[Pasted image 20251016181316.png]]

![[Pasted image 20251016181420.png]]

If we look at the tf, we find a high-pass model. k is the dielectric factor and C is the capacitance. 

![[Pasted image 20251016181746.png]]
At high freq we discover the effect is no longer electrical but is smt it depends on the mechanical properties. This can be modelled by a series of RLC. These three element model the mehanical behaviour of the device. 

![[Pasted image 20251016182216.png]]

![[Pasted image 20251016182732.png]]

![[Pasted image 20251016183319.png]]
Very small bias current. and other characteristic is that we have a part on the input of the amplifier which gets rid of the bias current, thus, a very large input resistance.

![[Pasted image 20251016183613.png]]

![[Pasted image 20251016183917.png]]

![[Pasted image 20251016183933.png]]

![[Pasted image 20251016184451.png]]

![[Pasted image 20251016184506.png]]


![[Pasted image 20251016184933.png]]

![[Pasted image 20251021124828.png]]


![[Pasted image 20251016184921.png]]

History
![[Pasted image 20251016184953.png]]
![[Pasted image 20251016185332.png]]

![[Pasted image 20251016185349.png]]

![[Pasted image 20251016185412.png]]

![[Pasted image 20251016185916.png]]

![[Pasted image 20251021125023.png]]
plate that contains sensor. Usually sensors are placed in the four corners

![[Pasted image 20251021125703.png]]

![[Pasted image 20251021130543.png]]

