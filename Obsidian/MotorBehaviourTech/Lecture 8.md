
Date: 08/10/2025
***

# <span style="color:rgb(223, 109, 109)">Force Measurement</span>
![[Pasted image 20251008083515.png]]


We are now moving to a different topic compared to what we have covered so far. We will set aside electrophysiological signals and focus instead on **force and moment signals**, which describe how the human body interacts with the external world.

These interactions are fundamental for:

- **Feeding biomechanical models**, which will be introduced in the second part of the course.
- **Diagnostic purposes**, since changes in the forces exchanged between the body and the environment can indicate pathological conditions.
    

Importantly, this interaction is not limited to the body–ground interface (as in **ground reaction forces**, which are the most common case). It can also involve:

- Forces generated when pushing against external objects, such as a wall.
- Forces measured through specialized devices, for example an **instrumented hammer**, which is used to detect structural faults in objects like pillars or other materials.
    

In all these cases, force and moment measurements provide valuable information about both human motor behavior and the properties of the external environment.

![[Pasted image 20260103213547.png|500]]

So in order to measure forces exchanged between some part of the body and environment, we need a deformation. So this is a particular kind of deformation, which is a classical car crash. and obviously we will be less obtrusive than this kind of approach. But anyway, in order to estimate the force, we need something which is deformed under that force. So you cannot measure forces if you are not deforming something.

![[Pasted image 20260103213648.png|500]]

As a general measurement principle, **we should not extract too much energy from the process we are measuring**, because doing so alters the phenomenon itself.  A classic example is temperature measurement: if the sensor removes too much heat from the body, the measured temperature is no longer representative of the original state.

The same principle applies to **force measurements**.  The energy drawn from the system can be approximated as:

**Energy ≈ Force × Displacement (deformation)**

Since the force is the unknown quantity we want to measure, we cannot minimize it. Therefore, to reduce the energy extracted from the process, **we must minimize the displacement (deformation)** of the measuring system.

This also affects **power**, because power depends on force and velocity. Minimizing deformation usually implies minimizing velocity as well.

### <span style="color:rgb(161, 40, 226)">Role of stiffness and compliance</span>

The deformation depends on the **stiffness (or compliance)** of the measuring device:

- **High stiffness** → small deformation
- **High compliance** → large deformation
    
Force-measuring systems also have **dynamic behavior** and can often be modeled as **second-order systems**. Such systems are characterized by a **natural frequency** ( $\omega_n$ ), which depends on stiffness.

For a simplified model based on Hooke’s law:  
  
$$\omega_n \propto \sqrt{\frac{k}{m}}  
$$  
where:
- ( $k$ ) = stiffness
- ( $m$ ) = moving mass
    
This means:

- Increasing stiffness → increases natural frequency
- Decreasing stiffness (higher compliance) → decreases natural frequency
    

Since the natural frequency typically defines the **upper limit of the sensor bandwidth**:

- **High stiffness → wide bandwidth**
- **Low stiffness → narrow bandwidth**

### <span style="color:rgb(161, 40, 226)">Force sensors</span>

The main types of sensors used for force measurement are:

- **Load cells**, which measure very small strains.
- **Piezoelectric sensors**, which generate electric charge and voltage when deformed. These sensors usually exhibit **very small deformations** and therefore have a **much wider bandwidth** than load cells.
    
Other sensors, such as **optical fiber–based sensors** (using reflection or refractive index changes), also exist. However, these are less common in standard biomechanical applications, such as measuring forces during walking or other simple movements.

![[Pasted image 20251008085643.png]]
Indeed, this simple example makes the concept clear.  This is a **fish scale**, a device commonly used to weigh fish after they are caught. It is essentially based on a **spring** with an index that moves along the scale.

In order to display the weight clearly, the index must move over a **large distance**. This means that the applied force causes a **large deformation** of the spring.

As a consequence:

- The sensor has **high compliance** (low stiffness)
- The deformation is large
- The **bandwidth of the measurement system is very small**
    

So, while this kind of sensor is easy to read and suitable for static or very slow measurements, it is **not appropriate for dynamic force measurements**, where high bandwidth is required.

### <span style="color:rgb(161, 40, 226)">Optical fiber sensors (brief overview)</span>

![[Pasted image 20260103214854.png]]

We will now briefly introduce **optical fiber sensors**, and then focus much more on **load cells**.

An **optical fiber** is essentially a flexible glass or plastic waveguide that can transmit light along **non-linear paths**. Normally, light propagates in straight lines, and bending it requires extreme conditions, such as the massive gravitational fields that bend light from stars (a cosmological effect). Optical fibers, however, allow light to bend and propagate thanks to a different physical principle.

The working principle of optical fibers is **multiple total internal reflections** of light rays inside the fiber. This is different from mirror-based reflection. Even mirrors with very high reflectivity (e.g. 99.999%) would still lead to significant power losses after many reflections, making them unsuitable for long-distance light transmission.

Optical fibers rely instead on **total internal reflection**, which occurs due to **different refractive indices** in the fiber materials. This phenomenon is governed by **Snell’s law**.

#### <span style="color:rgb(2, 141, 192)">Structure of an optical fiber</span>

- **Core**: the inner region (a few micrometers in diameter) where light propagates
- **Cladding**: surrounds the core and has a **lower refractive index**
    

Because of the refractive index difference, there exists a **critical angle** for total internal reflection. This defines an **acceptance cone** at the fiber input:

- Light entering within this angle is fully guided inside the fiber
- Light entering outside this angle is rapidly lost
    
Thanks to this mechanism, optical fibers exhibit **extremely low power losses**, on the order of a few decibels over **kilometers of fiber**. This high efficiency is the reason why optical fibers are widely used in **telecommunications and broadcasting systems** (TV, internet, etc.).

In sensing applications, these properties can be exploited to measure force, deformation, or strain with **very small mechanical deformation** and potentially **very wide bandwidth**.

### <span style="color:rgb(161, 40, 226)">The Load Cell</span>
![[Pasted image 20251008090737.png]]
**Load cells – basic principle (summary)**

- A **load cell** is a mechanical structure designed to **measure strain** in specific regions of the structure.
- **Strain** is the deformation produced by **stress**, which in turn is generated by an **applied force**.
- Measurement chain:
    - Apply a force →Force generates **stress** in the structure →Stress produces **strain** →Strain is measured →Force is estimated from the measured strain.
        
- Load cells usually have **multiple strain measurement points**, not just one.
    
- This allows measurement of up to **six degrees of freedom**:
    - Forces: **Fx, Fy, Fz**
    - Moments: **Mx, My, Mz**
    
- Six is the maximum number of degrees of freedom in the physical world.
    

**Cantilever example**
![[Pasted image 20260103225058.png|300]]

- A **cantilever** is fixed at one end and loaded at the other.
- When a force (e.g. a weight) is applied:
    
    - One side of the beam undergoes **tension (elongation)**
    - The opposite side undergoes **compression**
        
- By measuring the **local variations in length** at specific points, the applied force can be estimated.
    

**Key measurement aspects**

- The measured deformations are **extremely small**.
- This is desirable because:
    - The measurement is **minimally invasive**
    - The displacement $S$ required to extract information is very small
        
- In reality, deformations are **not visible**, but strain can still be accurately detected.
    
**Structural design of load cells**

- Load cells are often made of **steel or aluminum alloys**, which are very stiff.
- To measure **small forces**, the structure is intentionally shaped (e.g. holes, reduced sections):

    - This **reduces stiffness locally**
    - Increases strain for the same applied force
        
- This makes small forces easier to detect.

### <span style="color:rgb(161, 40, 226)">The Strain Gauge</span>
![[Pasted image 20251008090746.png]]
**Strain gauges – construction and working principle (summary)*
- **Structure**
    - A strain gauge consists of:
        - A **backing (support)** glued to the deforming structure
        - A **thin conductive wire** (or foil) patterned in a zig-zag shape
            
    - The zig-zag pattern:
        - Packs a **long wire length into a very small area**
        - Makes the gauge sensitive to deformation along a specific direction
            
    - Typical size: **a few millimeters**
    - **Large pads** at the ends are used to **solder connection wires**
        
- **Why the zig-zag wire**
    
    - Even if folded, the wire is **oriented along the strain direction**
    - Deforming the structure stretches or shortens the wire **as if it were straight**
    - Longer effective length → higher sensitivity to deformation


![[Pasted image 20251008090839.png]]

- **Physical quantity used for measurement**
    - What we actually measure is the **change in electrical resistance**
    - Resistance ( $R$ ) of a wire depends on:
        - **Length** ( $L$)
        - **Cross-section area** ( $A$ )
        - **Material resistivity** ( $\rho$ )
            
    - Basic relation:  
        $R = \rho \frac{L}{A}$
        
- **Effect of deformation**
    
    - **Tension (elongation)**:
        - Wire length increases → **resistance increases**
            
    - **Compression (surface shortening)**:
        - Effective wire length decreases → **resistance decreases**
            
    - The wire itself is not “compressed”:
        - It follows the **surface deformation** of the structure it is glued to
            
- **Material aspects**
    
    - Resistivity ( $\rho$ ) mainly depends on:
        - Wire material
        - Temperature (important source of error, handled later)
            
- **Use in load cells**
    
    - Multiple strain gauges are placed:
        - In **tension regions**
        - In **compression regions**
            
    - Their resistance changes are used to:
        - Estimate **strain**
        - From strain, compute the **applied force or moment**
            

👉 In short: **force → stress → strain → resistance change → electrical signal**
***
***
## <span style="color:rgb(239, 179, 1)">Strain Gauge - Working Principle - Extracted from Sensor Systems notes</span>

![[Pasted image 20251118123606.png]]

Now let’s better understand the working principle of strain gauges. A strain gauge is simply a resistor whose resistance changes when the material is strained. You know that the resistance $(R)$ of a conductor is:
$$R = \rho \frac{L}{A} = \rho \frac{L}{W \cdot H}  $$
If we apply tension to the material:

- its length $(L)$ increases,
- its cross-section $(A)$ decreases due to necking (both $(W)$ and $(H)$ shrink),

and both effects cause the resistance to **increase**.

If instead we apply compression:

- the length decreases,
- the cross-section increases,

and the resistance **decreases**.

For some materials, resistivity $(\rho)$ also changes with stress. This is the **piezoresistive effect**, where the normalized change in resistivity is proportional to the stress applied:

$$\frac{\Delta \rho}{\rho} = \beta \cdot \sigma = \beta \cdot E \cdot \varepsilon = \beta \cdot E \cdot \frac{\Delta L}{L}$$
and this can also be written using strain $(\Delta L / L)$ by including the Young’s modulus.
### <span style="color:rgb(161, 40, 226)">Sensitivity to strain direction</span>

The material is sensitive to strain **only when it is applied along the main length** of the resistor. If the stress is applied in the orthogonal direction, the resistance change is negligible.

This remains true for **bonded strain gauges**, which are the most common type.  
In these devices, the resistor is folded many times (zig-zag pattern) to increase the effective length. The sensor still responds mainly to tension or compression along its principal axis and remains almost insensitive to lateral forces applied perpendicular to that axis.

### <span style="color:rgb(161, 40, 226)">Gauge Factor (Sensitivity of a Strain Gauge)</span>

The **gauge factor (G)** represents the sensitivity of a strain gauge.  
It is defined as:
  
$$G = \frac{dR/R}{\varepsilon} =\frac{dR / R}{dL / L}  $$
where:
- ($dR / R$) = relative change in resistance
- ($dL / L$) = axial strain
    
**Deriving the Gauge Factor**

The resistance of a conductor is:
$$R = \rho \frac{L}{W H}$$
Let's do some variations and apply $ln$ in both sides
$$ ln(R)=ln(\rho)+ln(L)-ln(W)-ln(H)$$
And if we make the derivative of all these we would get
$$ d(ln(R))=d(ln(\rho))+d(ln(L))-d(ln(W))-d(ln(H))$$
We finally obtain the relative variation of this expression gives:
$$\frac{dR}{R}  
= \frac{dL}{L}-\frac{d\rho}{\rho}-\frac{dW}{W}-\frac{dH}{H}$$
(The width (W) and height (H) terms have negative signs because they are in the denominator)

**Using Poisson’s Ratio**
Poisson’s ratio is defined as:
$$\nu = -\frac{dW/W}{dL/L} = -\frac{dH/H}{dL/L}$$
Therefore:
$$  -\frac{dW}{W} = \nu \frac{dL}{L}$$
$$-\frac{dH}{H} = \nu \frac{dL}{L}  $$

Substituting these into the expression for ($dR/R$):

$$  
\frac{dR}{dR}  
= \frac{dL}{dL} + \frac{d\rho}{\rho}+2\nu \frac{dL}{L}  
$$
**Including the Piezoresistive Effect**

For piezoresistive materials:
$$\frac{d\rho}{\rho} = \beta E \frac{dL}{L}  $$
Substitute this:
$$\frac{dR}{R}  = \left(1 + 2\nu + \beta E\right)\frac{dL}{L} $$
Finally:
$$\boxed{ G= 1 + 2\nu + \beta E  }$$
> [!info] **Special Cases** Non-piezoresistive materials (most metals)
$$\beta = 0 \quad \Rightarrow \quad G \approx 1 + 2\nu  $$
Typical values:  
 $$G ≈ 2$$

> [!error] Piezoresistive materials (e.g., silicon)  
$$G = 1 + 2\nu + \beta E $$
The term ($\beta E$) is large → G can be 50–150 or higher

***
***

![[Pasted image 20251008092926.png]]

**Material properties for strain gauges – key points (summary)**
- **Metals**
    - **Platinum**
        - Gauge factor ≈ **6**
        - Temperature coefficient (αᵣ) ≈ **0.38**
        - High elastic modulus
    - **Alloys**
        - **Constantan**
            - Gauge factor ≈ **2–2.5**
            - **Very low temperature coefficient** → good thermal stability
            - Name reflects this: _almost constant with temperature_
        - **Nickel–chrome**
            - Gauge factor ≈ **2**
            - Higher temperature sensitivity than Constantan
                
    - **Elastic modulus**
        
        - Metals typically have **high stiffness**
        - Example: **Aluminum ≈ 70 GPa**
            
- **Semiconductors**
    - **Silicon (p-type)**
        - Very high gauge factor: **100–170**
        - High elastic modulus: **≈ 190 GPa**
        - **Much higher temperature coefficient** (≈ **0.7**)
            
- **Main trade-offs**
    - **Metal strain gauges**
        - Lower sensitivity (low gauge factor)
        - **Better temperature stability**
        - More reliable for practical force measurements
            
    - **Semiconductor strain gauges**
        - **Very high sensitivity**
        - Strongly affected by temperature
        - Require careful temperature compensation
        
👉 **Bottom line**:
- Metals (especially Constantan) are preferred for **stable, accurate measurements**
- Semiconductors offer **high sensitivity** but at the cost of **thermal robustness**
![[Pasted image 20251008094246.png]]

**Strain-gauge materials – temperature stability (summary)**
- **Constantan**
    - Alloy of **nickel + copper**
    - Numbers indicate the **percentage of Ni and Cu** in the alloy
    - Gauge factor ≈ **2.1**
    - Temperature coefficient ≈ **±2**
    - Widely used because of **good thermal stability**
        
- **Karma**
    - Special alloy **designed for temperature stability**
    - Used when **low thermal drift** is critical
        
- **Manganin**
    - Another alloy with **good temperature stability**
    - Often used in precision measurements
        
- **Pure metals**
    - **Nickel (pure)** has a **very high temperature coefficient**
    - Strongly affected by temperature → **not ideal** for strain gauges
        
- **Semiconductors**
    - Very **high gauge factor**
    - Also **very high temperature sensitivity**
        
- **Key takeaway**
    - For strain gauges, **alloys specifically designed for thermal stability** (Constantan, Karma, Manganin) are preferred
    - Goal: minimize **resistance variations due to temperature**, not strain

### <span style="color:rgb(161, 40, 226)">Data Processing: The Wheatstone Bridge</span>
![[Pasted image 20260103231115.png]]

![[Pasted image 20251008094852.png]]
Let us consider the four resistors of a **Wheatstone bridge** as the resistances of **four strain gauges**, each having a nominal (resting) resistance $R_0$​.  When the load cell is deformed by an applied force, each strain gauge experiences a **strain**, and its resistance changes by a small amount $\Delta R$.

Because of the mechanical structure of the load cell:

- Two strain gauges are subjected to **tension**, so their resistance **increases**:
    $$R_1 = R_3 = R_0 + \Delta R$$
- The other two strain gauges are subjected to **compression**, so their resistance **decreases**:
    
    $$R_2 = R_4 = R_0 - \Delta R$$

The key point is **how these strain gauges are connected in the Wheatstone bridge**.  
To maximize sensitivity and obtain a useful output voltage, the strain gauges whose resistance **increases** must be placed on **opposite arms of the bridge**, and the same must be done for the strain gauges whose resistance **decreases**.

Which strain gauge increases or decreases its resistance is determined by the **geometry of the load cell** and by where each gauge is glued (tension or compression regions). Once this is known, the electrical wiring is simply a matter of connecting each gauge to the correct arm of the bridge.

**Output voltage of the full bridge**

If we insert these resistance values into the Wheatstone bridge equation (derived earlier), we obtain the output voltage:

$$V_{out} = V_{exc} \cdot \frac{(R_0 + \Delta R) - (R_0 - \Delta R)}{2R_0}$$
Simplifying the numerator:

$$(R_0 + \Delta R) - (R_0 - \Delta R) = 2\Delta R$$
and therefore:
$$V_{out} = V_{exc} \cdot \frac{\Delta R}{R_0}$$
This result shows that the output voltage is:
- **Proportional to the excitation voltage** $V_{exc}$​
- **Proportional to the relative resistance change** $\Delta R / R_0$
    
Since $\Delta R$ is very small (typically a few ohms or less over a base resistance of about 100–350 Ω), the output voltage is also small.  The resistance change $\Delta R$ is directly related to the **strain** through the **gauge factor**, which links mechanical deformation to electrical variation.

**Full-bridge configuration**

This configuration, where **all four arms of the Wheatstone bridge are active strain gauges**, is called a **full bridge**.
Advantages of the full bridge:
- Maximum sensitivity
- Good temperature compensation
- Better rejection of common-mode effects
    
It is also possible to use fewer strain gauges (half-bridge or quarter-bridge configurations), but the **full bridge** is the classical and most effective solution for force and load-cell measurements.


![[Pasted image 20260103231756.png]]
#### <span style="color:rgb(2, 141, 192)"><b>Full bridge</b></span>

The **full bridge** uses **four active strain gauges**, one in each arm of the Wheatstone bridge.

- It requires **four wires**, connecting each strain gauge to the bridge (these are often shown in red in schematics).
- All four resistances change with strain.
- The output voltage is:
    
$$V_{out} = V_{exc} \cdot \frac{\Delta R}{R_0}$$
This configuration provides:

- **Maximum sensitivity**
- **Excellent temperature compensation**
- **Linear response**
    
Because all strain gauges are glued to the same metallic structure, and metals are good heat conductors, all four gauges are at nearly the same temperature. This naturally compensates temperature variations.


#### <span style="color:rgb(2, 141, 192)"><b>Half bridge</b></span>

In the **half-bridge configuration**, only **two strain gauges** are active.

- It requires **three wires**.
- Two strain gauges are placed in one arm of the bridge.
- The other arm is completed using **two fixed resistors** with the same nominal resistance $R_0$​.
    

For proper **temperature compensation**, it is important that:

- The strain gauges and the fixed resistors experience the **same temperature**.
- If temperature changes affect all four elements equally, their effects cancel out and the output remains stable.
    
This condition is easier to satisfy in a full bridge than in a half bridge, but at least the ambient temperature is typically the same for all components.

The output voltage of the half bridge is:
$$V_{out} = V_{exc} \cdot \frac{\Delta R}{2R_0}$$

So:

- The **gain is half** that of the full bridge.
    

#### <span style="color:rgb(2, 141, 192)"><b>Quarter bridge</b></span>

In the **quarter-bridge configuration**, only **one strain gauge** is used
- It requires **two wires**.
- The remaining three arms of the bridge are completed using fixed resistors.
    

The exact output voltage expression is:

$$V_{out} = V_{exc} \cdot \frac{\Delta R}{4R_0 + 2\Delta R}$$

This expression is **nonlinear**, but since $\Delta R \ll R_0$, the term $2\Delta R$ in the denominator can be neglected.  
With this approximation, the output voltage becomes:

$$V_{out} \approx V_{exc} \cdot \frac{\Delta R}{4R_0}$$

This means:

- The sensitivity is approximately **one quarter** of the full-bridge sensitivity.
- Small nonlinear effects are present.
- Temperature compensation is poorer unless special techniques are used.
    

#### <span style="font-weight:bold; color:rgb(2, 141, 192)">Summary</span>

- **Full bridge**: highest sensitivity, best temperature compensation, four wires
- **Half bridge**: half sensitivity, moderate temperature compensation, three wires
- **Quarter bridge**: lowest sensitivity, nonlinear response, two wires
    
The choice of configuration depends on the required sensitivity, temperature stability, and hardware complexity.

