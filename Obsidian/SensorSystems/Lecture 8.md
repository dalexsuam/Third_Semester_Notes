
6/11/2025
***
# <span style="color:rgb(223, 109, 109)">Displacement, Proximity and Distance Sensors (Part 1)</span>

Hello everybody!  Today’s topic is **displacement, proximity, and distance sensors**.
In this lecture, we will focus on **resistive sensors** (potentiometers), as well as **capacitive** and **inductive** sensors. In the next class, we will move on to **acoustic**, **optical**, and **magnetic** sensors.

## <span style="color:rgb(239, 179, 1)">Introduction to the Three Quantities</span>

Before analyzing the sensors, let’s clarify the three physical quantities we are interested in:

### <span style="color:rgb(161, 40, 226)">• Displacement (linear or angular)</span>

**Linear displacement** is the straight-line change in position of an object from its initial point to its final point.  
It can be measured using:

- Potentiometers
- Capacitive sensors
- Inductive sensors
- Optical or magnetic encoders
    
**Angular displacement** is the angle through which an object rotates around a fixed axis.  
It can be measured using:

- Potentiometers
- Rotary encoders
    
### <span style="color:rgb(161, 40, 226)">• Proximity</span>

A proximity sensor detects whether an object is **present or absent** within a specified range.  
This means proximity sensing is **binary**:

- Output = 1 → an object is within the detection range
- Output = 0 → no object is detected
    
Proximity sensing can be implemented using:

- Capacitive sensors
- Inductive sensors
- Acoustic (ultrasonic) sensors
- Optical sensors

### <span style="color:rgb(161, 40, 226)">• Distance</span>

Distance is the **absolute separation** between the sensor and the target object.  
Unlike proximity, it is not binary. It provides a **continuous measurement**.

Distance can be measured using:

- Acoustic (ultrasonic) sensors
- Optical sensors (e.g., time-of-flight, laser triangulation)

## <span style="color:rgb(239, 179, 1)">Potentiometers</span>
  



Let’s begin with potentiometers. Potentiometers, as mentioned earlier, are resistive sensors used to measure linear or angular displacement.

You have already worked with a potentiometer during the laboratory sessions. Their operating principle is quite simple: a potentiometer is essentially a resistor with two fixed terminals, A and B, just like any ordinary resistor. However, it also includes a third terminal, known as the _wiper_, which moves along the resistive track.

![[Pasted image 20251120094507.png]]

As the wiper changes position, the electrical node at point C shifts accordingly, creating a different resistive division of the supply voltage ($V_s$) applied across terminals A and B.

If the moving mechanical element is connected to the wiper, the wiper moves together with the object. Starting from a defined zero position, any displacement of the object corresponds to a shift in the wiper’s position, allowing us to measure the displacement (x).

The operating equation is straightforward because it relies on the concept of a voltage divider. The output voltage ($V_{\text{out}}$), associated with the object’s position, is given by:
$$  
V_{\text{out}} = V_s \cdot \frac{R_{AC}}{R_{AC} + R_{CB}}  
$$

Since ($R_{AC} + R_{CB}$) equals the total resistance ($R_{AB}$), what we effectively measure is a voltage proportional to the resistance ($R_{AC}$). This resistance is, in turn, proportional to the object’s displacement (x).

Therefore, by measuring the output voltage, we can infer the displacement of the object relative to its zero position.

### <span style="color:rgb(161, 40, 226)">Types of Potentiometers</span>


There are two main types of potentiometers: **linear potentiometers** and **rotary potentiometers**.

| Linear Potentiometer                 | Rotatory Potentiometer               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251120095858.png]] | ![[Pasted image 20251120095937.png]] |
| ![[Pasted image 20251120095947.png]] | ![[Pasted image 20251120095955.png]] |

In a **linear potentiometer**, the resistive element is arranged in a straight, linear configuration, and the wiper moves along this path in a straight line.  
In contrast, a **rotary potentiometer** features a resistive track arranged in a circular (wound) layout. In the simplified illustration, only one loop is shown, but in practice the resistive strip may be wound over multiple turns. The wiper moves rotationally along this circular track.

Depending on the type of mechanical motion involved, both linear and rotary potentiometers can be used to measure either linear or angular displacement.

For **linear displacement**, two approaches are possible:


| Linear Displacement                                                              | Angular Displacement                 |
| -------------------------------------------------------------------------------- | ------------------------------------ |
| ![[Pasted image 20251120100417.png]]<br>![[Pasted image 20251120100436.png]]<br> | ![[Pasted image 20251120100423.png]] |


1. **Using a linear potentiometer**:  
    The moving object is directly attached to the wiper, which moves linearly along the resistive strip.
2. **Using a rotary potentiometer**:  
    The linear motion of the object can be converted into rotation. This is typically achieved by attaching the object to a cable or string connected to a rotating shaft. As the object moves linearly, the cable causes the shaft to rotate, and this rotation is measured by the rotary potentiometer.


On the other hand, **angular displacement** is typically measured using rotary potentiometers.  In this case, the rotating object or shaft is mechanically coupled to the rotating shaft of the potentiometer, allowing direct measurement of angular position.

## <span style="color:rgb(239, 179, 1)">Capacitive Sensors - Distance</span>

![[Pasted image 20251120103054.png]]
Now let us move on to the next category of sensors: **capacitive sensors**.
![[Pasted image 20251120103036.png]]
Capacitive sensors are mainly used for **measuring linear displacement** or for **proximity detection**.  Before examining these applications, we first need to review the concept of **capacitance** and understand which parameters influence its value.

### <span style="color:rgb(161, 40, 226)">Capacitance Review</span>
Capacitors can be built using different geometries, but the two most common structures are the **parallel-plate capacitor** and the **cylindrical capacitor**.

To determine the capacitance for these configurations, we rely on three key relationships:

1. **Gauss’s Law**, which states that the electric flux of the electric field (E) depends on the enclosed charge (Q) divided by the permittivity $(\varepsilon$) of the medium.
$$\Phi_E= EA=\frac{Q}{\varepsilon}$$
2. The relation between electric field and voltage:  
    $$E = \frac{\Delta V}{d}  $$
    where (d) is the distance between the plates over which the voltage ($\Delta V$) is measured.
    
3. The definition of capacitance:  
    $$Q = C \cdot \Delta V$$
By combining these three equations, we obtain the capacitance expressions for different geometries.

If we take equation 1 ($EA=Q/\varepsilon$) and equation two ($E=\Delta V/d$) we obtain
$$\frac{\Delta V}{d}\cdot A=\frac{Q}{\varepsilon}
$$
Now by replacing $Q$ in equation three and clearing the $C$,  we obtain
$$
C=\frac{\varepsilon \cdot A}{d}
$$
### <span style="color:rgb(161, 40, 226)">Parallel-Plate Capacitor</span>

![[Pasted image 20251120103121.png]]
For a parallel-plate capacitor, the capacitance is given by:
$$C = \varepsilon_r \varepsilon_0 \frac{A}{d}  $$

where:

- $(A)$: area of the plates
- $(d):$ distance between the plates
- ($\varepsilon_r \varepsilon_0$): permittivity of the dielectric material between the plates
### <span style="color:rgb(161, 40, 226)">Cylindrical Capacitor</span>

![[Pasted image 20251120103136.png]]
A cylindrical capacitor consists of:

- an **inner cylinder** with radius ($R_1$)
- an **outer cylinder** with radius ($R_2$)
    
Using Gauss’s law and the same relationships as before, we can derive the capacitance formula for the cylindrical geometry. The full expression is more complex, but in the case of a **thin cylindrical capacitor**, the formula can be simplified.

Let us define:
- ($R = \frac{R_1 + R_2}{2}$), the average radius
- ($w = R_2 - R_1$), the spacing between the cylinders

If the capacitor is thin (i.e., ($R_1$) and ($R_2$) are very close), then ($w \ll R$) and we can write:
$$C = \frac{2 \pi \varepsilon l}{\ln(1 + w/R)}  $$

Since ($w/R \to 0$), the logarithm can be approximated, giving the simplified formula:
$$C = \varepsilon \frac{2 \pi R l}{w}  $$

Here, ($2 \pi R l$) represents the **effective surface area** of the plates. The spacing between the plates is the difference between the radii, ($w = R_2 - R_1$). This final expression closely resembles the parallel-plate capacitor formula and is often easier to remember.

### <span style="color:rgb(161, 40, 226)">Displacement Sensors</span>

#### <span style="color:rgb(2, 141, 192)">Parallel-Plate Capacitive Displacement Sensor</span>

Consider a parallel-plate capacitor in which a dielectric object moves between the plates.  
The region between the plates is therefore partially filled with air (permittivity $\varepsilon_0$​) and partially filled with a material characterized by a relative permittivity $\varepsilon_r$.

As the object moves, the portion of the capacitor occupied by the material changes, and therefore the overall capacitance varies with the object’s position $x$.

**Modeling the capacitance**

![[Pasted image 20251120105651.png]]
We can represent the system as two capacitors in parallel:

- **$C_1$​**: the upper region filled only with air
- **$C_2$​**: the lower region filled with the dielectric material

Both capacitors share:

- Plate length $L$
- Plate separation $W$ (constant)

The height of the plates is $H$, but only a portion of this height corresponds to each region.

**Capacitance of each region**

***1. Upper capacitor (air only):***

![[Pasted image 20251120105830.png|200]]
$$C_1 = \varepsilon_0 \, \frac{L(H - x)}{W}$$

***2. Lower capacitor (dielectric inserted):***
![[Pasted image 20251120105924.png|200]]
$$C_2 = \varepsilon_0 \varepsilon_r \, \frac{L x}{W}$$
***Total capacitance***

Since the two regions are in parallel:

$$C_{\text{tot}} = C_1 + C_2$$
Substituting:

$$C_{\text{tot}} = \varepsilon_0 \frac{L}{W} \left( h - x + \varepsilon_r x \right)$$
Rearranging:
$$\boxed{ C_{\text{tot}} = \varepsilon_0 \frac{L}{w} \left[ h + x(\varepsilon_r - 1) \right] }$$
This expression shows that the capacitance increases **linearly** with displacement $x$.


#### <span style="color:rgb(2, 141, 192)">Cylindrical Capacitive Displacement Sensor</span>

![[Pasted image 20251120110132.png]]
A similar principle applies to the cylindrical geometry.  Here, the **moving object is mechanically connected to the inner cylinder** of a coaxial capacitor.  
As the object moves, the axial overlap length between the inner and outer cylinders changes.

Assuming the capacitor is thin (so that we can use the simplified expression for cylindrical capacitors), the capacitance is proportional to the lateral overlapping area.
***Capacitance expression***
$$C = \varepsilon_0 \varepsilon_r \frac{2\pi R x}{W}$$
Where:

- $R$: average radius of the cylinders
- $x$: overlapping length (proportional to object displacement)
- $W$: small radial separation between the two cylinders

Again, the capacitance depends **linearly** on the displacement $x$.
#### <span style="color:rgb(2, 141, 192)">Summary</span>

Both geometries—parallel-plate and cylindrical—allow us to design a displacement sensor in which the capacitance varies linearly with the position of an object:

- **Parallel-plate:** dielectric object moves between the plates
- **Cylindrical:** inner cylinder moves along its axis with the object

In both cases, the capacitance can be written as:
$$C(x) = C_0 + kx$$

where:
- $C_0$​: constant component
- $kx$: displacement-dependent component

Typical capacitive displacement sensors can achieve a resolution of around **1 µm**.
### <span style="color:rgb(161, 40, 226)">Measuring Capacitance (Single-Ended)</span>

To determine the displacement ($x$) using a capacitive sensor, we must first **measure the capacitance**.  A common and effective method is to incorporate the sensor capacitor into an **oscillator circuit** whose **oscillation frequency depends on the capacitance**.  By measuring this frequency (or its period), we can infer the value of (C), and therefore the displacement.

Below are two representative oscillator implementations: one based on **digital circuitry** and one based on **analog circuitry**. In both cases, the oscillation frequency is a function of the capacitance.

#### <span style="color:rgb(2, 141, 192)">Measuring Capacitance Using a Digital Schmitt-Trigger Oscillator</span>

![[Pasted image 20251120111158.png]]
The first example uses a **Schmitt-trigger inverter**.  A Schmitt trigger is a digital component that:

- Outputs the logical opposite of its input.
- Exhibits **hysteresis**, meaning it switches its output at two distinct threshold voltages:
    - a **higher threshold** for switching from HIGH → LOW
    - a **lower threshold** for switching from LOW → HIGH
        
***Principle of operation***

![[Pasted image 20251120111711.png]]
![[Pasted image 20251120111855.png]]
1. Assume the inverter output is initially HIGH.
    - Since the inverter outputs the opposite of the input, the capacitor voltage ($V_C$) must be LOW.
2. With the output HIGH, current flows through resistor (R) into the capacitor.
    - The capacitor charges.
    - The charging slope ($dV_C/dt$) depends on the time constant (RC).
3. When the capacitor voltage reaches the **upper threshold**, the Schmitt trigger switches.
    - The output abruptly goes LOW.
4. With the output LOW, current reverses direction and the capacitor **discharges** through the same resistor.
5. When the capacitor voltage reaches the **lower threshold**, the output switches HIGH again.
    
This charge–discharge cycle repeats indefinitely, creating a square-wave output whose **period (T)** depends on the charging and discharging slopes, therefore on:

$$T \approx RC  $$
Thus, if we measure the period (or frequency), we can deduce the capacitance:
$$C \approx \frac{T}{R}$$
#### <span style="color:rgb(2, 141, 192)">Measuring Capacitance Using an Analog Schmitt-Trigger Oscillator</span>

![[Pasted image 20251120112112.png]]
The second example uses two operational amplifiers:

1. **A Schmitt-trigger comparator** (with positive feedback).  
    This sets two voltage thresholds.    
2. **An integrator** (op-amp with capacitor in feedback).  
    This generates a linear ramp voltage across the capacitor.
    
***Principle of operation***

![[Pasted image 20251120112415.png]]
![[Pasted image 20251120112514.png]]

- When the Schmitt-trigger output is HIGH:
    - A constant current flows through the resistor into the capacitor.
    - The integrator converts this current into a **linear decrease** in the voltage $(V_C$) (a negative ramp).
- When the capacitor voltage reaches the lower threshold:
    - The Schmitt trigger switches LOW.
- With the output LOW:
    - The current reverses direction.
    - The integrator generates a **linear increase** in ($V_C$) (a positive ramp).
- When ($V_C$) reaches the upper threshold:
    - The trigger switches HIGH again.

This produces a triangle waveform at the capacitor and a square wave at the comparator output.

Since:
$$I = C \frac{dV}{dt} \quad \Rightarrow \quad \frac{dV}{dt} = \frac{I}{C}  $$


the slope of the triangle wave depends on (C), and the time required to traverse the thresholds defines the oscillation period.  
Therefore:
$$T \propto C  $$
Thus, measuring the oscillation period directly yields the capacitance.


#### <span style="color:rgb(2, 141, 192)">From Oscillation Period to Displacement</span>

If we can measure the oscillation period using, for example, a microcontroller’s digital input and a timer:

1. Count the number of oscillation cycles during a known time window.
2. Compute the period (T) or frequency (f = 1/T).
3. Use the calibrated relationship (C(x)) to calculate displacement (x).
    

### <span style="color:rgb(2, 141, 192)">Limitations of the Single-Ended Approach</span>

Using a _single_ capacitor has drawbacks:
- **Geometrical tolerances**  
    Variations in ($L$) or ($w$) (plate dimensions) affect capacitance.
    
- **Temperature dependence**  
    The dielectric constant ($\varepsilon_r$) changes with temperature, causing drift in the capacitance and therefore in the measured displacement.
    
These limitations motivate the use of **differential capacitive sensors**, which greatly reduce sensitivity to temperature and mechanical tolerances.

### <span style="color:rgb(161, 40, 226)">Measuring Capacitance (Differential Approach)<br></span>
To mitigate the limitations of measuring a single capacitance—such as temperature drift, geometric tolerances, and variations in permittivity—we can adopt a **differential capacitive sensing approach**.

In this configuration, the output signal is not based on the variation of one capacitor alone, but on the **difference** between two capacitances, ($C_1$) and ($C_2$), which vary in opposite directions as the object moves.

An additional advantage of the differential approach is that we no longer require an oscillator circuit to infer capacitance. Instead, we can directly measure a **differential voltage** using a **Wheatstone bridge**, which simplifies the readout circuitry.

Both **parallel-plate** and **cylindrical** geometries can be implemented in differential form.
#### <span style="color:rgb(2, 141, 192)">Differential Parallel-Plate Geometry</span>

![[Pasted image 20251120114802.png|300]]
In this configuration we use **three plates**, where the middle plate is shared between two capacitors:
- ($C_1$): formed by plates **A** and **B**
- ($C_2$): formed by plates **B** and **C**
    
When the movable plate shifts by a displacement ($x$):

- The separation of plates A–B becomes ($W - x$).
- The separation of plates B–C becomes ($W + x$).
    
Thus, the capacitances are:
$$C_1 = \frac{\varepsilon_0 A}{w - x}, \qquad  
C_2 = \frac{\varepsilon_0 A}{w + x}  $$
where ($A$) is the fixed plate area.

Because the two capacitances vary oppositely, any common-mode effects (e.g., temperature-dependent permittivity) affect both equally and thus largely cancel out.
#### <span style="color:rgb(2, 141, 192)">Wheatstone Bridge Readout</span>
![[Pasted image 20251120114952.png]]
To extract the imbalance between ($C_1(x)$) and ($C_2(x)$), we place them in one branch of a Wheatstone bridge driven by a sinusoidal excitation voltage ($V_A$).  
The other branch contains two **fixed** capacitors equal to the nominal value at the zero-displacement position (i.e., ($\frac{\varepsilon_0 A}{W}$)).

Because capacitors have infinite impedance at DC, the bridge must be excited with an **AC voltage**, not a DC source.

Let:
- $(V_+)$ be the voltage at the midpoint of the variable branch.
- ($V_-)$ be the voltage at the midpoint of the fixed branch.

***Computation of ($V_+$)***

Using the capacitive divider rule:
$$V_+ = V_A \cdot \frac{C_1}{C_1 + C_2}$$

Substitute definitions of ($C_1$) and ($C_2$), simplify, and we obtain:
$$V_+ = V_A \frac{w + x}{2w}  $$
***Computation of $(V_-)$***

The fixed capacitors are equal, so the midpoint divides the voltage exactly in half:
$$V_- = \frac{V_A}{2}$$

***Output of the Bridge***
$$V_{\text{out}} = V_+ - V_-  
= V_A \left( \frac{w + x}{2w} - \frac{1}{2} \right)  
= \frac{V_A}{2} \frac{x}{w}$$

Thus:
$$\boxed{V_{\text{out}} = \frac{V_A}{2} \cdot \frac{x}{w}}$$

The output voltage is **directly proportional to the displacement** (x), and importantly:

- It **does not depend** on the permittivity ($\varepsilon_r$).
- It is robust against common-mode variations.
- It provides a **linear response** with respect to displacement.

#### <span style="color:rgb(2, 141, 192)">Differential Cylindrical Geometry</span>

![[Pasted image 20251120115324.png|300]]
A similar differential principle can be implemented using cylindrical plates.

Here:
- There are two **fixed outer cylinders**, forming two capacitors with a **movable inner cylinder**.
- When the inner cylinder shifts by (x), one capacitance increases and the other decreases.

The capacitances are proportional to the lateral facing area:
$$C_1 = \frac{\varepsilon_0 \varepsilon_r \pi d}{W} (L + x) $$
$$C_2 = \frac{\varepsilon_0 \varepsilon_r \pi d}{W} (L - x) $$

where:
- $(d)$ = diameter of the inner cylinder
- $(L)$ = length of overlap at the zero position

Placing these in a Wheatstone bridge exactly as before yields:
$$\boxed{V_{\text{out}} = V_A \frac{x}{2L}}  $$
Again, the output is **linearly proportional** to the displacement and **independent** of permittivity.
#### <span style="color:rgb(2, 141, 192)">Summary of Advantages</span>

The differential capacitive approach offers:

 Linear relationship between output voltage and displacement  
 Immunity to variations in dielectric constant  
 Reduced sensitivity to temperature and geometry tolerances  
 Simple readout using a Wheatstone bridge (no oscillator required)  
 Higher measurement stability and accuracy

## <span style="color:rgb(239, 179, 1)">Capacitive Sensor - Proximity</span>
  
Now let’s talk about another type of **capacitive sensor**. Unlike the ones we discussed earlier, which measure displacement, this type of sensor is used to detect **proximity** — that is, whether an object is nearby or not.

A **proximity sensor** is essentially an on-off sensor. It does not provide a continuous measurement; it simply tells you if an object is present or absent in its sensing range.
![[Pasted image 20251120120405.png|300]]

A capacitive proximity sensor is usually made using **two concentric electrodes**, forming what’s called a planar capacitor. Think of it like this:

- There is a circular **inner plate** and a surrounding **outer plate**.
- If you look at a cross-section, you can see the plates stacked. The outer plate may look like two parts in the cross-section, but it is actually one piece.
- The sensor generates an **electric field** between these two plates.
    
![[Pasted image 20251120120428.png]]
When a target object comes close to the sensor, it **interacts with this electric field**. This interaction changes the **capacitance** of the sensor. Why does this happen? Because capacitance depends on:

1. The **permittivity** of the material between the plates (how easily the material allows an electric field to pass through it).
2. The **area** of the plates.
3. The **distance** between the plates.
    

As the target approaches, the effective permittivity between the plates increases, causing the capacitance to rise.

To detect this change, the sensor is connected to an **oscillator circuit**:

- The oscillator requires a minimum capacitance to start oscillating.
- When the object is close enough, the capacitance rises, and the oscillator begins to work.
- As the object moves farther away, the capacitance drops, the oscillation slows, and eventually stops.
    
A **trigger circuit** (like a comparator) monitors the oscillator. When the oscillation passes a certain threshold, the sensor outputs a **digital signal** indicating the presence of an object. Essentially, the output is high if an object is near and low if no object is nearby.

### <span style="color:rgb(161, 40, 226)">How Material Properties Affect the Sensor<br></span>
![[Pasted image 20251120120512.png|400]]

The sensor’s behavior depends heavily on the **dielectric constant** (also called relative permittivity, εr) of the material it is detecting. Different materials affect the capacitance differently:

- **Water** has a very high dielectric constant, which makes it easy for the sensor to detect from a longer distance.
- **Air** and **vacuum** have very low dielectric constants (about 1), so they hardly change the sensor’s capacitance.
- Other materials fall somewhere in between. For example, alcohol has a dielectric constant around 25.8, while plexiglass is around 3.
    
![[Pasted image 20251120120544.png|400]]
This variation affects the **effective sensing distance** — the distance at which the sensor can reliably detect an object:

- Sensors usually provide a **digital output**, so instead of sensitivity, we talk about the distance at which detection occurs.
- Datasheets often define the sensing distance based on **water** because it has the highest dielectric constant and gives a clear reference.
    

For example:
![[Pasted image 20251120120609.png]]

- If a sensor has a **rated sensing distance of 10 mm for water**, it can detect water up to 10 mm away.
- For alcohol (εr ≈ 25.8), the effective sensing distance drops to roughly **8.5 mm**.
- For a material with εr = 10, the effective sensing distance might only be **6 mm**.
    
This is why the material in front of the sensor matters — the sensor might detect some objects farther away and others only when they are very close.

Graphs in datasheets often show the **relative sensing distance**, which is the effective distance as a percentage of the rated distance for different materials. This makes it easier to understand how the sensor behaves with various targets.

### <span style="color:rgb(161, 40, 226)">Working Principle</span>

Now, let’s go deeper into how a **capacitive proximity sensor** actually works, focusing on the **oscillator circuit** it uses.
![[Pasted image 20251120121212.png]]
In a capacitive proximity sensor, the sensor’s capacitance is connected to an **oscillator**. The ability of this oscillator to generate a signal depends on the **capacitance** of the sensor: when the capacitance is high enough, the oscillator starts oscillating; when it is too low, it does not.

The oscillator used in these sensors is usually a **parallel RLC oscillator**, meaning it is made of a **resistor (R), inductor (L), and capacitor (C)** connected in parallel.

- This oscillator has a **resonant frequency**, which is the natural frequency at which it oscillates. It is given by the formula:  
    $$\omega_0 = \frac{1}{\sqrt{LC}}  $$
However, a simple RLC circuit is not enough to maintain continuous oscillations. Why? Because **resistors dissipate energy**, which means that over time the oscillations would gradually die out. To sustain oscillation, we need a **source of energy**, and this is provided by an **operational amplifier (op-amp)** powered by an external supply.
![[Pasted image 20251120121301.png|400]]

- The op-amp provides **positive feedback** to keep the oscillation going.
- At the same time, it also uses **negative feedback** to prevent the oscillation from growing uncontrollably.

For the oscillation to remain **stable** — not too big and not zero — the **strength of the positive feedback** must exactly balance the **strength of the negative feedback**.

- In the circuit, the **negative feedback** is determined by a voltage divider (R1 and R2).
- The **positive feedback** depends on the relationship between the impedance of the RLC circuit and a resistor (R4).
    

The RLC circuit always oscillates at its resonant frequency, so to calculate the effective impedance of the RLC part, we consider:
$$Z_{eq} = R3 \parallel (sL) \parallel \frac{1}{sC}$$
- Here, ($s = j\omega_0$), corresponding to the resonant frequency.
- At resonance, this equivalent impedance simplifies to **R3**, meaning the positive feedback is controlled by R3 and R4.
- By choosing R1, R2, R3, and R4 correctly, we can balance positive and negative feedback, ensuring a **steady oscillation**.
#### <span style="color:rgb(2, 141, 192)">Role of the Damping Factor</span>

The behavior of the oscillator also depends on the **damping factor (ζ)**, which is related to the **quality factor (Q)** of the circuit:
$$\zeta = \frac{1}{2Q} = \frac{1}{2R} \sqrt{\frac{L}{C}}  $$
- If ζ < 1 → the circuit is **underdamped** and able to oscillate.
- If ζ = 1 → the circuit is **critically damped** and cannot sustain oscillation.
- If ζ > 1 → the circuit is **overdamped** and also cannot oscillate.
    

Now imagine the sensor **without any object nearby**:

- The capacitance is small (close to that of air or vacuum).
- This makes the damping factor ζ > 1 → the circuit is overdamped, and **no oscillation occurs**.

When an object comes **into proximity**:
![[Pasted image 20251120121429.png]]
- The capacitance increases because the material’s permittivity is higher than air.
- This increase **reduces the damping factor**. If it becomes smaller than 1, the circuit becomes underdamped → **oscillation starts**.
    
The oscillation then grows to a **steady amplitude**, stabilized by the balance between positive and negative feedback.

- In other words: **no object → no oscillation**, **object present → oscillation appears**, which the sensor can detect and convert into a digital signal.

#### <span style="color:rgb(2, 141, 192)">Simulation</span>

![[Pasted image 20251120155742.png|400]]

To better understand how the capacitive proximity sensor works, I simulated the oscillator circuit. In the diagram, you can clearly identify the **RLC oscillator**, the resistor that provides **positive feedback**, and the pair of resistors that set the **negative feedback** of the operational amplifier.

To reproduce the effect of a target approaching or moving away from the sensor, I added an extra capacitor (C2) in **parallel** with the main capacitor C1. This extra capacitor represents the **increase in capacitance** that occurs when an object comes close to the sensor. To control when this added capacitance is included in the circuit, I connected it through two switches.

Here’s how the switches behave:

- **Switch 1** starts as a _short circuit_ (closed).
- **Switch 2** starts as an _open circuit_.
    
![[Pasted image 20251120155947.png]]
At **2 ms**, Switch 2 closes. Since Switch 1 is already closed, the two switches now form a continuous path, and C2 becomes connected to the circuit. This moment simulates the **presence of the target**, because the total capacitance increases.

Then, at **5 ms**, Switch 1 opens. This breaks the connection and disconnects capacitor C2, simulating the moment when the **target moves away**.

The results of the simulation match exactly what we expected:

- At the beginning, with no target present and only C1 in the circuit, the capacitance is too low for oscillation to occur — so we see **no oscillation**.
- At **2 ms**, when C2 is added in parallel, the capacitance increases enough for the circuit to become underdamped, and we see a **stable oscillation** appear.
- At **5 ms**, when C2 is disconnected, the capacitance drops again, the circuit becomes overdamped, and the oscillations **disappear**.
    

You may notice a small spike at the switching moments. This spike is not a physical effect — it is simply an artifact of the simulator when a circuit parameter changes very abruptly. To reduce or eliminate these non-physical spikes, you can increase the number of simulation points. The simulation will take longer, but the waveform will look smoother and more realistic.

### <span style="color:rgb(161, 40, 226)">Applications</span>

Now let’s look at some **applications of capacitive sensors**. As we discussed earlier, capacitive sensors can be used in different ways depending on what we want to measure.

One common use is **displacement measurement**. For example:
![[Pasted image 20251120160631.png]]

- They can be used to precisely track the position of mechanical parts in machinery.  
- They are also used in precision stages, where you need to know the exact relative position between a sensor and an object.  

Capacitive sensors are also useful for measuring **dynamic motion**, especially vibrations. A vibration is basically a small and rapid displacement around a fixed central position, so capacitive sensors can capture these changes very accurately.

Another important application is **proximity sensing**. In this case, the sensor doesn’t measure a continuous value but simply detects whether an object is near or not.

Proximity sensing is especially useful in areas like **assembly testing** or for **detecting objects through barriers**.
![[Pasted image 20251120160647.png]]

For example, imagine you want to check whether a plastic bottle contains liquid (like water) or if it is empty:

- If the bottle contains only air, the permittivity (ε) around the sensor stays very low. Since air barely affects capacitance, the sensor will not detect any nearby object.
- But if the bottle contains water, the situation changes completely. Water has a very high dielectric constant, so it increases the capacitance significantly. As a result, the sensor detects the presence of a target.

This is extremely useful because the sensor does this **even though the bottle wall is between the sensor and the liquid**. The bottle acts as a barrier, but capacitive sensing is still able to “see” what is inside because capacitive fields are influenced by the dielectric properties of the material, not by light or reflection.

Later, when we look at optical proximity sensors, we’ll see the contrast:  
- An optical sensor would always detect the bottle itself, whether it is full or empty, because it only sees the surface.  
- But a capacitive proximity sensor can distinguish **full vs empty**, because it reacts differently to air and to liquid.

This is why capacitive sensors are often chosen when the goal is not just to detect the presence of an object, but to identify what the object **contains** or what material it is made of.

## <span style="color:rgb(239, 179, 1)">Inductive Sensors</span>

### <span style="color:rgb(161, 40, 226)">Self-Inductance</span>
![[Pasted image 20251120162045.png]]

Inductive sensors, like capacitive sensors, can be used to measure:

- **Linear displacement**
- **Proximity**
    

In this part we will focus on the **LVDT** (Linear Variable Differential Transformer), a very precise inductive sensor used for linear displacement.

Before studying the LVDT, we need to review the physics of **inductance** and **electromagnetic induction**.

***Faraday–Neumann–Lenz Law***

![[Pasted image 20251120162231.png|350]]
Whenever there is a **time-varying magnetic flux** linked to a coil, a voltage is induced:
$$V = -N \frac{d\Phi_B}{dt}  $$
where:

- $(N)$ = number of turns in the coil
- $(\Phi_B)$ = magnetic flux
- The negative sign means the induced voltage opposes the change in flux (_Lenz’s law_)

The **magnetic flux** is:
$$\Phi_B = \vec{B} \cdot \vec{A} = BA\cos\alpha$$
If the magnetic field (B) is **normal to the coil area**, then:
$$\alpha = 0,\ \cos 0 = 1 \Rightarrow \Phi_B = BA$$

***Magnetic Field of a Solenoid***

A solenoid carrying current *(I)* generates a magnetic field:
$$B = \mu_0 \mu_r \frac{NI}{L}  $$
where:

- ($\mu_0$) = vacuum permeability
- ($\mu_r$) = relative permeability of the core
- ($N$) = number of turns
- ($L$) = length of the solenoid
- ($I$) = current

***Combining Both Equations: Self-Induction***

If the current ($I(t)$) varies in time (i.e., it is an AC current), then:

- the magnetic field ($B(t)$) varies,
- the magnetic flux ($\Phi_B(t)$) varies,
- and the coil **induces a voltage in itself** (self-induced voltage):
    
$$V = -L \frac{dI}{dt}$$

The constant (L) is the **self-inductance**, given by:
$$L = \frac{\mu_0 \mu_r N^2 A}{L}$$
So inductance:

- increases with the **square** of the number of turns ($N^2$)
- increases with the **area** of the coil
- increases with the **permeability** of the core
- decreases with the coil length

***Why this matters for inductive sensors***

This physics is essential because inductive sensors operate by detecting:

- changes in magnetic fields
- changes in inductance
- changes in the coupling between coils
    
Examples:

- In an **LVDT**, the displacement of a movable core changes the coupling between primary and secondary coils, producing a measurable change in voltage.
- In **proximity inductive sensors**, the presence of metal changes the inductance of the coil.
    
### <span style="color:rgb(161, 40, 226)">Mutual Inductance Between Two Coils</span>

Up to this point we have dealt with the concept of self-inductance, where a varying current flowing through a coil generates a magnetic field that changes in time, and this changing magnetic field induces a voltage in the same coil.  
The same physical principles apply when we consider two separate coils placed near each other.
#### <span style="color:rgb(2, 141, 192)">Magnetic Coupling Between Two Coils</span>

Consider two coils, Coil 1 and Coil 2. Coil 1 is supplied with an alternating current ( $I_1(t)$ ). Because the current varies in time, Coil 1 generates a magnetic field ( $B_1(t)$ ).  A portion of this magnetic field reaches and links with Coil 2.
![[Pasted image 20251120205303.png]]
How much of the magnetic field produced by Coil 1 actually links Coil 2 depends on the distance between the coils, their orientation, their geometry, and the medium in which they are placed. To quantify this, we introduce the coupling coefficient ($k$).

The coupling coefficient is defined such that:
$$0 \le k \le 1 .$$
A value of ($k = 0$) means that no magnetic field from Coil 1 reaches Coil 2. This happens when the coils are very far apart or misaligned.  A value of ($k = 1$) corresponds to perfect magnetic coupling. In this case the entire magnetic field produced by Coil 1 links Coil 2.

The magnetic field from Coil 1 is given by:
$$B_1 = \mu_0 \mu_r \frac{N_1 I_1}{L_1}$$

where ( $\mu_0$ ) and ( $\mu_r$ ) are the permeability of free space and of the medium, ( $N_1$ ) is the number of turns of Coil 1, and ( $L_1$ ) is the length of the solenoid. The magnetic field effectively “seen” by Coil 2 is therefore:
$$B_2 = k B_1$$
#### <span style="color:rgb(2, 141, 192)">Voltage Induced in Coil 2</span>

Since Coil 1 carries an alternating current ( $I_1(t)$ ), the magnetic field ( $B_1(t)$ ) is time-varying, and therefore the portion of the field that reaches Coil 2, ( $B_2(t)$ ), is also time-varying.  A time-varying magnetic field linked to Coil 2 induces a voltage across it, according to the Faraday–Neumann–Lenz law:
$$V_2 = -N_2 A_2 \frac{dB_2}{dt}$$
where ($N_2$) is the number of turns of Coil 2 and ($A_2$) is its cross-sectional area.

Substituting the expression for ( $B_2$ ), we obtain:
$$V_2 = -N_2 A_2 \frac{dB_2}{dt}\left(k \mu_0 \mu_r \frac{N_1 I_1}{L_1}\right).$$
All the parameters except the current ( $I_1$) are constant, so the derivative only acts on the current. This yields:
$$V_2 = -k \mu_0 \mu_r \frac{N_1 N_2 A_2}{L_1} \frac{dI_1}{dt}.  $$
This expression shows that the induced voltage in Coil 2 is proportional to the rate of change of the current flowing in Coil 1 and to a set of geometric and physical constants of the system.
#### <span style="color:rgb(2, 141, 192)">Definition of Mutual Inductance</span>

Since all the geometric and material-dependent terms in the previous expression are constant, it is convenient to group them into a single parameter called the mutual inductance, denoted by $(M)$.  
The induced voltage can then be written in a compact and standard form:
$$V_2 = -M \frac{dI_1}{dt}$$

The mutual inductance can be expressed in terms of the coupling coefficient and the self-inductances of the two coils:

$$M = k \sqrt{L_1 L_2}$$

In this expression, ($L_1$) and ($L_2$) are the self-inductances of Coil 1 and Coil 2, respectively, and ($k$) expresses how effectively the magnetic fields are coupled between the two coils.

#### <span style="color:rgb(2, 141, 192)">Interpretation</span>
![[Pasted image 20251120205918.png]]
If the coupling coefficient is zero, then ($M = 0$), and no voltage is induced in Coil 2. This corresponds to the case where the coils do not interact magnetically.  
If the coupling coefficient is one, the magnetic coupling is perfect, and the mutual inductance attains its maximum possible value. In practical situations, the value of ($M$) increases when the coils are closer, better aligned, have more turns, have larger areas, or are placed in a medium with higher permeability.

This mutual inductance phenomenon forms the physical basis for devices such as transformers, inductive displacement sensors, and specifically the LVDT (Linear Variable Differential Transformer), which measures displacement through variations in magnetic coupling.

### <span style="color:rgb(161, 40, 226)">Linear Variable Differential Transformer</span>

Having introduced the concept of mutual inductance, we can now see how its variation can be exploited to measure displacement. The device that uses this principle is called the **Linear Variable Differential Transformer**, commonly abbreviated as **LVDT**. Sometimes it is also referred to as a *transducer*, sometimes as a *transformer*, but the operating principle is the same.

The LVDT is a sensor designed to measure **linear displacement** by making use of the fact that the **coupling coefficient** between coils can be altered by moving a ferromagnetic core. Since the coupling coefficient directly affects the mutual inductance, and therefore the induced voltage in the secondary coils, the position of the core can be detected by analyzing these induced voltages.
#### <span style="color:rgb(2, 141, 192)">Structure of the LVDT</span>

The LVDT consists of three coils wound on a cylindrical structure:
![[Pasted image 20251120210829.png]]
1. **A primary coil**, located at the center.
2. **Two secondary coils**, symmetrically placed on either side of the primary.

The primary coil is excited by an alternating current. This AC excitation creates a time-varying magnetic field, which can link with the two secondary coils. However, the amount of magnetic field that links each secondary coil depends on the presence and the position of a **ferromagnetic core** that can slide along the axis of the coils.

This movable core is mechanically connected to the object whose displacement we want to measure. Usually, a rigid rod transmits the movement of the object to the core so that the core moves exactly as the object moves.

The core is made of a high-permeability material. Its function is to channel and concentrate the magnetic field. For this reason, the position of the core strongly influences how much magnetic flux reaches the first or the second secondary coil.

#### <span style="color:rgb(2, 141, 192)">Operation of the LVDT</span>

When the core is exactly centered with respect to the primary coil, the magnetic field produced by the primary is equally distributed toward the two secondary coils. As a consequence, the induced voltages in the two secondaries (often denoted as $(V_1)$ and $(V_2)$ have equal magnitude. In this condition, the LVDT is said to be at its *null position*, where $(V_1 = V_2)$.

If the core is displaced toward the left, the magnetic coupling between the primary and the left secondary coil increases, because the core channels more magnetic flux toward that side. As a result, the induced voltage $(V_1)$ becomes larger than $(V_2)$. The opposite occurs if the core moves toward the right; then the coupling is stronger with the right secondary coil, and so the induced voltage $(V_2)$ becomes larger than $(V_1)$.

This means that:

- the **difference** between the two induced voltages indicates the magnitude of the displacement;
- the **sign** of the difference (i.e., which voltage is greater) indicates the direction of the displacement.

Because the LVDT operates with alternating current, the induced secondary voltages are AC signals as well. The position is determined by comparing their amplitudes, not by comparing their instantaneous values.
#### <span style="color:rgb(2, 141, 192)">Summary of the Sensing Mechanism</span>

To summarize the operating principle:

![[Pasted image 20251120210648.png]]
1. The primary coil is excited by an alternating current, producing a time-varying magnetic field.
2. A ferromagnetic core shapes the distribution of this magnetic field.
3. Two secondary coils receive different amounts of magnetic flux depending on the core’s position.
4. The resulting induced voltages in the two secondaries are compared:
   - equal voltages mean the core is centered,
   - higher voltage in the first secondary means the core is displaced toward it,
   - higher voltage in the second secondary means the core is displaced toward the opposite direction.
5. The relationship between displacement and voltage difference is linear over a certain range, which makes the LVDT an accurate and highly reliable displacement sensor.

Here is a **clearer, more textually explained** version of your content, still in **English**, without emojis, and keeping the technical meaning intact. I rewrote it so it reads smoothly, logically, and with stronger explanations.

### <span style="color:rgb(161, 40, 226)">How to measure the imbalance?</span>

![[Pasted image 20251120211629.png]]
To measure the imbalance between the two voltages $( \Delta V_1)$ and $( \Delta V_2 )$, we need a specific circuit configuration. This is necessary because these voltages are **not constant**: each is an **AC signal**, typically a sinusoid. What we want is **not** the instantaneous value of each sinusoid, but rather **their amplitude**, since the amplitude is what depends on the position of the ferromagnetic core.

The general structure is the following:

- The primary coil is driven by an oscillator.
- Two secondary coils generate $( \Delta V_1)$ and $( \Delta V_2)$.
- Each of these secondary voltages is then processed to extract only its **peak value**, using a circuit known as a **peak stretcher**.

#### <span style="color:rgb(2, 141, 192)">Understanding the Peak Stretcher</span>

Let us focus on only one secondary coil, since both sides work identically.

Assume the secondary coil generates a sinusoidal voltage whose amplitude changes with the displacement of the ferromagnetic core. To capture the amplitude, we use a circuit consisting of:

- A diode
- A capacitor
- A resistor (which we add later to improve performance)

***Circuit With Only a Diode and Capacitor***

![[Pasted image 20251120214102.png]]
Imagine the sinusoidal input voltage $(\Delta V_1)$ is applied through a diode to a capacitor.

- When the sinusoid increases (positive peak), the diode becomes forward-biased, and the capacitor charges up.
- Due to the diode’s threshold voltage (typically around 0.7 V for standard diodes, or 0.2–0.3 V for Schottky diodes), the capacitor voltage will be slightly lower than the peak of the sinusoid.
- Once the sinusoid starts to decrease, the diode becomes reverse-biased.  
  At this point the capacitor **cannot discharge** because the diode blocks current in that direction.

As a result, the output voltage remains **constant**, equal to the peak reached previously. This gives us a voltage that represents the amplitude of the sinusoid.

However, this represents a problem:  
If the amplitude of the sinusoid later **decreases**, the capacitor voltage **cannot follow** this decrease because it has no path to discharge. Therefore, the circuit cannot track a decreasing envelope.

***Adding a Resistor to Track Decreasing Amplitude***

To solve this, we add a resistor in parallel with the capacitor.
![[Pasted image 20251120214133.png]]
Now:

- The diode charges the capacitor during each positive peak of the sinusoid.
- When the sinusoid decreases and the diode turns off, the capacitor can slowly discharge through the resistor.
- The resistor value is chosen to make this discharge **slow**, so that the output still tracks the general envelope, but does not fall to zero between every cycle.

This way, the output voltage always closely follows the amplitude of the sinusoid, even when that amplitude decreases.

Thus, the output voltage represents the **true envelope** of the sinusoidal signal.

#### <span style="color:rgb(2, 141, 192)">Applying This to the Differential Measurement</span>

![[Pasted image 20251120214159.png]]

The same peak-stretcher circuit is applied to each secondary coil:

- At node ($V_+$), we obtain a voltage proportional to the amplitude of ($\Delta V_1$).
- At node ($V_-$), we obtain a voltage proportional to the amplitude of ($\Delta V_2$).

The final output is the difference:
$$V_{\text{out}} = V_+ - V_-$$
This provides the following behavior:

- If the ferromagnetic core moves upward, the coupling to the first secondary increases.  
  Therefore, ( $\Delta V_1 > \Delta V_2$ ), so $( V_{\text{out}} > 0)$.
- If the core moves downward, then ($\Delta V_2 > \Delta V_1)$, and thus $(V_{\text{out}} < 0)$.
- If the core is exactly centered, the amplitudes are identical, so the output is exactly zero.

#### <span style="color:rgb(2, 141, 192)">Result</span>

With this arrangement, we obtain a circuit where:

- The output is **zero** when there is **no displacement**,
- **Positive** for displacement in one direction,
- **Negative** for displacement in the opposite direction.

This allows the system to detect both the **direction** and **magnitude** of the displacement in a continuous and highly sensitive way.
 

Here is a **more textually explained**, clean, structured version of your content in **English**, without emojis, and keeping all the technical meaning intact. I made it clearer, more formal, and easier to read while preserving your message.

### <span style="color:rgb(161, 40, 226)">Inductive Proximity Sensors</span>

Now we move to a different type of inductive sensor, this time used specifically for **proximity detection**.  Although these sensors share some conceptual similarities with capacitive proximity sensors, their **output behavior is essentially the opposite**.
#### <span style="color:rgb(2, 141, 192)">Opposite Behavior Compared to Capacitive Proximity Sensors</span>

- In capacitive proximity sensors, the presence of a target generally **increases** the effective capacitance, changing the oscillation conditions in one direction.
- In inductive proximity sensors, the effect is reversed:  
  - When **no target** is present, the sensor’s internal circuit **oscillates normally**.  
  - When a **metallic target** approaches the sensor, these oscillations **stop or are significantly attenuated**.  
  - When the target is removed, the oscillations **resume**.

Thus, the detection mechanism is based on whether the oscillation produced by the sensor is maintained or suppressed.
#### <span style="color:rgb(2, 141, 192)">Physical Principle</span>

In this type of sensor, we replace the capacitive element with an **inductor**, typically implemented as a coil.

![[Pasted image 20251120220753.png|100]]

1. **Generation of Magnetic Field**  
   When current flows through the coil, it creates a magnetic field $(B)$.  
   In this case, we supply an **alternating current**, so the magnetic field varies over time.

2. **Interaction With Nearby Materials**  
   This time-varying magnetic field can interact with conductive or ferromagnetic materials placed in front of the sensor.  
   Such a material is called the **target**.

3. **Effect of the Target**  
   Metallic targets, in particular, affect the magnetic field in two major ways:
   - They induce **eddy currents** inside the metal due to the alternating magnetic field.
   - These eddy currents generate their **own magnetic field**, which opposes the original field.

The result is that the presence of the metal modifies the impedance of the coil.  
When this modification becomes significant enough, it **prevents the sustaining of oscillations** in the oscillator circuit connected to the coil.

#### <span style="color:rgb(2, 141, 192)">Sensor Output</span>

![[Pasted image 20251120220820.png|400]]

The sensor’s electronics monitor whether the oscillator is running or not.

- **Oscillation present** → **No target detected**  
- **Oscillation suppressed** → **Target detected**

This binary change is then processed and used as the output signal of the inductive proximity sensor.
 
Here is a clearer, more textually explained version of your paragraph. I kept all the physics intact but made it smoother, more structured, and easier to read. No emojis.

#### <span style="color:rgb(2, 141, 192)">Detailed Explanation of the Working Principle</span>
![[Pasted image 20251120221046.png]]

Let us go deeper into how an inductive proximity sensor actually works.  
As previously described, the sensor contains an **inductor**, usually implemented as a coil. This coil generates a **time-varying magnetic field**, represented here by the red arrows.

Now imagine that a **metallic target** approaches the region where this magnetic field exists. When the metal enters the influence of the alternating magnetic field, a specific electromagnetic phenomenon takes place.
##### <span style="color:rgb(71, 215, 140)">Eddy Current Formation</span>

![[Pasted image 20251120221108.png]]
If the magnetic field through the metal is **increasing** (due to the AC excitation of the coil), Faraday’s law tells us that a changing magnetic flux induces currents in conductive materials.  Inside the metal, these induced currents take the form of **closed circular paths**, known as **eddy currents**.

These eddy currents always act in such a way that they **oppose the change** in the magnetic field that created them. This follows from **Lenz’s law**:

- If the external magnetic field is increasing upward,  
- the eddy currents will generate their own magnetic field **in the opposite direction**, attempting to counteract that increase.

So the eddy currents create an opposing magnetic flux that tries to resist the variation imposed by the coil

##### <span style="color:rgb(71, 215, 140)">Energy Dissipation and Effect on the Oscillator</span>

These eddy currents are not stable or lossless. They circulate inside the metal and **dissipate energy as heat** due to the electrical resistance of the target material. Because of this dissipation:

- The eddy currents continuously absorb energy from the coil’s alternating magnetic field.
- This means that energy is effectively taken away from the **oscillator circuit** that drives the coil.

If the target is close enough, the energy lost through eddy current dissipation becomes so significant that:

- the oscillator can no longer maintain its oscillation,
- its amplitude collapses,
- and the oscillation **stops**.

This transition—from a sustained oscillation to no oscillation—is precisely the mechanism that the sensor uses to detect the presence of the metallic target.
#### <span style="color:rgb(2, 141, 192)">Detailed Explanation of the Oscillator Circuit Used in Inductive Proximity Sensors</span>

To understand how an inductive proximity sensor detects a metallic object, we first look at the **oscillator circuit** that drives the sensing inductor.  
This circuit is typically built around an **RLC network** and an operational amplifier.

 ***Structure of the RLC Oscillator***

![[Pasted image 20251120221846.png|240]]
The core of the circuit is an **RLC parallel oscillator**, composed of:
- **L:** the inductor that generates the magnetic field used for sensing.
- **C:** the capacitor of the oscillator.
- **R:** the intrinsic resistance of the RLC network (representing losses).
    

In addition to these elements, there is a second resistance, called **Rp**, which is _not_ a physical resistor soldered in the circuit. Instead:

- **Rp models the energy dissipated by eddy currents** when a metallic target comes close.
- In other words, Rp represents the **additional losses** introduced by the presence of the target.
    
When no target is present, Rp is effectively infinite.  
When a metal object approaches, Rp becomes finite and reduces the total effective resistance.

##### <span style="color:rgb(71, 215, 140)">Why the Oscillator Needs Energy Compensation</span>

Both the coil's resistance and Rp (when a target is present) dissipate energy. If the circuit relied only on the passive RLC network, it would eventually stop oscillating: all the stored energy in L and C would be lost through R and Rp.

To prevent that, the circuit uses an **operational amplifier** configured to:
![[Pasted image 20251120221934.png|200]]
- Continuously feed energy back into the RLC network.
- Maintain stable oscillation when no target is present.
    
The op-amp is connected in a **negative feedback configuration**, but the inductive coupling between the coils introduces an **additional positive feedback path**.

##### <span style="color:rgb(71, 215, 140)">Origin of the Positive Feedback</span>

Besides the standard negative feedback, the circuit also includes **mutual inductance** between two inductors. These inductors are marked with the two dots indicating the polarity of the mutual coupling.

The mechanism is as follows:
![[Pasted image 20251120222025.png|300]]
1. Suppose the output voltage decreases.
2. Because the reference ground is fixed, a decrease at the output means the voltage across the primary inductor increases.
3. This changing voltage in the primary induces a voltage in the secondary.
4. Due to the orientation of the polarity dots, the induced voltage at the secondary **increases the voltage fed into the negative input of the op-amp**.
5. Increasing the voltage at the negative input further decreases the output.
    

This forms a **positive feedback loop**: A small decrease at the output causes an even larger decrease, reinforcing the change.
##### <span style="color:rgb(71, 215, 140)">What Determines the Strength of the Positive Feedback</span>

The overall loop gain depends on two factors:

***(a) The coupling coefficient k***

This is the ratio between the induced voltage and the primary voltage:
$$k = \frac{V_2}{V_1} $$
The closer the coils are magnetically coupled, the larger k becomes.

***(b) The gain of the op-amp in the inverting configuration***

At the operating frequency, the RLC impedance is dominated by its resistive part.  
Thus the gain is approximately:
$$g = -\frac{R_{feedback}}{R_1}  $$

But since the feedback impedance at resonance becomes purely resistive:

- With no target: ($R_{feedback} = R_L$)
- With a target present: ($R_{feedback} = R_L \parallel R_P$), which is smaller

Thus, the gain decreases when a target is present.

##### <span style="color:rgb(71, 215, 140)">Barkhausen Criterion and Oscillation Condition</span>

According to the **Barkhausen criterion**, an oscillator will sustain oscillation only if the loop gain is:
$$g \cdot k > 1$$

This forms the basis of detection:

***Without a target***

- $(R_P \to \infty)$    
- The total feedback resistance is high.
- The gain g is high.
- So $(g \cdot k > 1)$
- **The circuit oscillates normally.**

***With a metallic target***

- Rp becomes finite.
- The effective resistance becomes $(R_L \parallel R_P)$, reducing the feedback gain.
- Thus g decreases.
- Eventually ($g \cdot k < 1$)
- **The oscillation stops.**

The electronics simply monitor whether the oscillator is active or not.  The presence of the target is detected when oscillation collapses.
#### <span style="color:rgb(2, 141, 192)">Explanation of the Simulation Results</span>

In the simulation we reproduced the same circuit that was previously analyzed theoretically. The structure includes:

![[Pasted image 20251120222904.png|300]]
- A **primary coil**, driven by the op-amp and responsible for generating the oscillation;
- A **secondary coil**, magnetically coupled to the primary through a coupling coefficient (k = 0.7 in your setup);
- The **capacitor and resistor** forming the RLC network of the oscillator;
- A resistor **R3**, which corresponds to the previously defined ($R_P$), modeling the *energy dissipation caused by a metallic target*;
- Two switches used to connect and disconnect R3 during a specific time interval, simulating the appearance and disappearance of a target.
##### <span style="color:rgb(71, 215, 140)">Behavior of the Oscillator Without a Target</span>  

![[Pasted image 20251120222959.png]]
(From the start until 20 ms) At the beginning of the simulation, the oscillator needs a short **startup time**. During this interval, the op-amp reinjects energy into the RLC tank until the oscillation reaches a steady amplitude.

Once the transient is over, the oscillator behaves as expected:

- ($R_P$) is not connected (the simulated target is absent).
- The total resistive loss is low, and therefore:
$$g \cdot k > 1$$
- The oscillator sustains a stable, continuous sinusoidal output.

This corresponds to the normal operating condition of an inductive proximity sensor when no target is nearby.

***Insertion of the Target (Between 20 ms and 35 ms)***

At **20 ms**, the switch connects R3 (the simulated ($R_P$) into the circuit. This mimics the physical effect of a metallic target entering the sensing zone:

1. The target introduces eddy-current losses.
2. These are modeled by the resistance R3 placed in parallel with the oscillator.
3. Parallel combination: ($R_L \parallel R_P$) reduces the effective resistance of the RLC branch.
4. The gain of the feedback loop drops accordingly.

Because of this, the loop-gain condition becomes:
$$g \cdot k < 1$$
Once this inequality is satisfied, the oscillator **cannot maintain oscillation**, and the sinusoidal output collapses.

This is exactly what the simulation shows: between 20 ms and 35 ms no oscillation is present. The amplitude falls rapidly to zero because the RLC tank loses energy faster than the op-amp can replenish it.

***Removal of the Target (After 35 ms)***

At **35 ms** the switch disconnects R3, simulating that the target moves away.

At that instant:

- The effective resistance of the oscillator returns to its original higher value.
- The gain increases again, making:
$$g \cdot k > 1$$
Therefore, the circuit is again capable of sustaining oscillation.

However, the output does not immediately jump to the steady sinusoid.  Instead, you correctly observed a **restart transient**:

- Energy must be gradually built up in the inductor and capacitor.
- Because the oscillator is driven by feedback, the oscillation amplitude increases progressively.
- After a certain time, the steady oscillation is restored.

This behavior is exactly what happens physically in real inductive proximity sensors: even in real circuits, the oscillations collapse in the presence of a target and require some time to rebuild once the target leaves.

#### <span style="color:rgb(2, 141, 192)">Circuit with better restart time</span>

You want the oscillator to **restart faster** after a metallic target leaves the sensing zone. To do that, the circuit briefly increases the loop gain when the detector indicates the oscillation has collapsed, so the tank (L and C) builds up energy quickly and the oscillator comes back to steady operation.

##### <span style="color:rgb(71, 215, 140)">Basic blocks in the improved circuit</span>

![[Pasted image 20251120223932.png]]
1. **RLC oscillator** (the sensing coil L, tank capacitor C, and the loss resistance RL).
2. **Peak detector / rectifier** that converts the oscillator’s AC amplitude into a DC envelope voltage.
3. **Two comparators** with two thresholds (Vref1 and Vref2) to detect “oscillation present” and “oscillation absent” with hysteresis.
4. **A controllable switch** in the feedback path (the switch changes the input resistance seen by the amplifier). Closing the switch temporarily changes the feedback network to give higher loop gain.
5. **A control feedback loop** that closes the switch when the envelope is below the lower threshold and opens it when the envelope recovers above the higher threshold.
    
##### <span style="color:rgb(71, 215, 140)">How it operates step by step</span>
![[Pasted image 20251120224435.png]]
1. **Normal condition — no target present**
    - The oscillator runs at its steady amplitude.
    - The rectifier output (the envelope) is high.        
    - The comparators see the envelope above Vref1 so the switch is **open**.
    - Loop gain is the normal value:  
        $|g| \approx \frac{R_L}{R_1}$
        and $(k\cdot|g| \gtrsim 1)$ so the oscillator sustains.
        
2. **Target arrives**
    - The target introduces losses (modeled by ($R_P$)), so the effective feedback resistance becomes ($R_L \parallel R_P$).
    - Loop gain falls:  $$ 
        |g| \approx \frac{R_L \parallel R_P}{R_1}  
        $$
    - The envelope drops and eventually falls below the lower comparator threshold Vref2.
    - The comparator output goes high (logic “1”) and **closes the switch**. This is the control signal that enables the fast-restart path.

![[Pasted image 20251120224820.png]]
1. **Switch closed — temporary high-gain mode**
    - Closing the switch places an additional resistance (R) in parallel with ($R_1$) (so the input resistance becomes ($R_1 \parallel R$).
    - The effective gain becomes:  
        $$|g| \approx \frac{R_L \parallel R_P}{R_1 \parallel R},  $$
        which is **larger** than before if (R) is chosen appropriately.
    - Because the denominator is reduced, the loop gain jumps well above 1 and the oscillator **restarts quickly** — the tank charges faster and the AC amplitude rises fast.

2. **Return to steady mode**
    - As the oscillator amplitude rises, the rectifier output rises.
    - When the envelope exceeds the upper threshold Vref1, the comparator output goes low and **opens the switch**.
    - The circuit returns to the original feedback network and settles to a normal, stable oscillation (with (k\cdot|g|) close to 1).
        
##### <span style="color:rgb(71, 215, 140)">Why two thresholds (hysteresis) are important</span>
The two thresholds (Vref2 < Vref1) create hysteresis:
- They prevent chatter: once the switch closes at the low threshold, the envelope must rise above the higher threshold before the switch reopens.
- This prevents the switch from rapidly toggling if the envelope hovers near a single threshold.

### <span style="color:rgb(161, 40, 226)">Applications</span>

Now that we have examined the inductive proximity sensor and its operating principle, we can briefly review some typical applications of inductive sensing.

![[Pasted image 20251120224959.png|300]]

First, inductive sensors are used in LVDTs, or Linear Variable Differential Transducers. These devices can achieve resolutions down to approximately one millimeter, making them useful in many industrial, military, or aerospace contexts. For example, the illustration here shows an LVDT integrated into an aircraft system to monitor the displacement of wing flaps.

![[Pasted image 20251120225018.png|300]]
Inductive sensors are also commonly employed as proximity detectors. Their ability to detect metallic objects without physical contact makes them suitable for safety and warning systems, for parking assistance, and for presence monitoring in automated production lines. In the example shown, the proximity sensor is used to confirm the position of a machine component as it moves along the line.

With this, we have completed our discussion of potentiometers, capacitive sensors, and inductive sensors. In the next class, we will move on to acoustic and optical sensing technologies, particularly those used for distance and proximity measurement. We will also introduce magnetic sensors and their role in encoder systems.

See you next time.


