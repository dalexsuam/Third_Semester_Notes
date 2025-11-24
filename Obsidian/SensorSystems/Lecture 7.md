30/10/2025
***

# <span style="color:rgb(223, 109, 109)">Strain and Force Sensors</span>

Hello everybody!  Today’s topic is **strain and force sensors**.

In particular, we will study two main types: **strain gauges** and **piezoelectric force sensors**.Let’s begin with **strain gauges**, which are resistive sensors used to measure strain.  They can be spelled either _strain gauges_ or _strain gages_—both forms are correct. Before going into the details, let’s quickly review some basic concepts from mechanics.

---
# <span style="color:rgb(223, 109, 109)">Strain Gauges</span>

![[Pasted image 20251118104533.png|400]]

## <span style="color:rgb(239, 179, 1)">Basic Principles - Mechanics</span>
### <span style="color:rgb(161, 40, 226)">Stress</span>

![[Pasted image 20251118104559.png]]
Stress is defined as the ratio between the force applied to a material and its cross-sectional area.  If the cross-section is ($W \times H$), then:
$$\sigma = \frac{F}{WH}, \space [Pa=N/m^2]  
$$
Stress is measured in **Pascals (Pa)**.

### <span style="color:rgb(161, 40, 226)">Strain</span>

![[Pasted image 20251118104912.png]]
Strain represents the **normalized elongation** of a material.  If a material of length $(L)$ is stretched by a force in the direction of its length, it will elongate by $(\Delta L)$.
$$\varepsilon = \frac{\Delta L}{L}  $$
Strain is dimensionless, but because the values are usually very small, it is often expressed in **microstrain** $(\mu\varepsilon = 10^{-6})$.

### <span style="color:rgb(161, 40, 226)">Young’s Modulus</span>

The relationship between stress and strain is given by **Young’s modulus**, defined as:
$$
E = \frac{\sigma}{\varepsilon}  
$$
Young’s modulus is also measured in **Pascals**.

### <span style="color:rgb(161, 40, 226)">Necking</span>

![[Pasted image 20251118105030.png]]
When a material is subjected to tension, it elongates in the direction of the applied force, but it becomes thinner in the perpendicular directions.  
This thinning effect is known as **necking**.

### <span style="color:rgb(161, 40, 226)">Poisson’s Ratio</span>

Poisson’s ratio quantifies this phenomenon (Necking). It is defined as the (negative) ratio between the relative change in width or height and the relative change in length:

$$  
\nu = -\frac{\Delta W/W}{\Delta L/L} = -\frac{\Delta H/H}{\Delta L/L}  
$$
The negative sign ensures that Poisson’s ratio is positive, since elongation ($\Delta L>0$) is accompanied by a reduction in width or height ($\Delta W<0$).


## <span style="color:rgb(239, 179, 1)">Stress- Strain Curve</span>

![[Pasted image 20251118122827.png]]

Normally, for most materials we can distinguish two regions in the stress–strain curve. This curve shows how much stress must be applied to produce a given strain. As you can see, the curve is divided into two main regions: the **elastic region** and the **plastic region**.

In the **elastic region**, the relationship between stress and strain is linear. This means that the Young’s modulus remains constant, since it corresponds to the slope of this linear portion of the curve.

In the **plastic region**, the relationship is no longer linear. Instead, the curve starts to saturate until it reaches the **failure point**, which is the moment when the material breaks.

## <span style="color:rgb(239, 179, 1)">Strain Gauge - Working Principle</span>

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


![[Pasted image 20251118210501.png]]

In this table, you can see the gauge factor values for different materials.  
One important thing to notice is that the gauge factor is **not always constant** over the full strain range.

To make this clearer, the table provides values for _low strain_ (typically below about 1%) and _high strain_.

![[Pasted image 20251118210145.png]]

For some materials—an example is **constantan alloy**—the relationship between ΔR/R and strain is almost perfectly linear.  
Because of this, the gauge factor remains nearly constant for both low and high strain.

However, other materials behave very differently.  
For example, **nickel** shows a strong nonlinearity:

- at low strain, the ΔR/R–strain curve has a **negative** slope
- at higher strain, the slope becomes **positive** and more linear
    
This change of slope explains why the gauge factor for nickel is negative at low strain but becomes positive when the strain increases.

## <span style="color:rgb(239, 179, 1)">Strain Gauge Fabrication</span>

Now, regarding the structure and fabrication of strain gauges, there isn’t much new to say, because the process is essentially the same as the one used for thin-film, patterned RTDs. The fabrication is based on **photolithography**, which typically includes four main steps:

![[Pasted image 20251118211247.png]]
1. **Photoresist deposition** – A layer of photoresist is applied on top of the material.  
    The photoresist can be _positive_ or _negative_, depending on whether it becomes stronger or weaker when exposed to light.
2. **Exposure to light** – Ultraviolet light is used to define the desired pattern on the photoresist.
3. **Etching** – The unprotected areas of the underlying material are removed.
4. **Photoresist removal** – The remaining photoresist is stripped away, leaving the final patterned structure.
    
The main difference compared to thin-film RTDs lies in the **carrier material**.  
For strain gauges, the carrier must be **flexible**, because the entire strain gauge is glued onto the specimen or structure being measured.  
If the specimen undergoes elongation or compression, the carrier—and therefore the gauge itself—must deform in exactly the same way.  
This ensures that the electrical resistance truly reflects the strain experienced by the specimen.


## <span style="color:rgb(239, 179, 1)">Strain Gauge - Readout circuit<br></span>
![[Pasted image 20251118211640.png]]
When using strain gauges, we need a circuit to read their resistance changes, and the most common approach is to use a **Wheatstone bridge**, similar to what we do with RTDs.

A key issue with strain gauges is **temperature sensitivity**. Since strain gauges are resistors, their resistance naturally changes with temperature. If we want the output of our measurement to reflect only the **strain applied to the material**, we need a way to cancel out any voltage changes caused by temperature.

![[Pasted image 20251118211754.png|400]]
One effective method is to use **two strain gauges placed orthogonally** (at right angles) to each other:

- **Strain gauge 1:** Aligned with the main length of the material, so it is parallel to the applied force.
- **Strain gauge 2:** Placed perpendicular (orthogonal) to the applied force, so it does not experience strain from the force.
    
Here’s why this works:

- When **temperature changes**, both gauges’ resistances increase by the same amount. If we place them in the same branch of the Wheatstone bridge, the voltage at the intermediate point stays roughly at half the supply voltage. This means **temperature effects are canceled out**.
    
- When a **mechanical strain** is applied:
    
    - Gauge 1, which is aligned with the force, changes its resistance.
    - Gauge 2, which is perpendicular, does **not** change.
        

This creates an **imbalance in the Wheatstone bridge**, which produces a voltage difference that we can measure. This voltage depends **only on the strain**, not on the temperature.

In short, this orthogonal strain gauge configuration allows us to measure strain accurately while compensating for temperature variations.

## <span style="color:rgb(239, 179, 1)">Strain Gauge - Bending measure</span>

![[Pasted image 20251118212425.png]]
Another important application is **measuring the bending of beams**. When a beam bends, one side experiences **tension** while the opposite side experiences **compression**:

- In the example here, the **top side** of the beam is under tension.
- The **bottom side** is under compression.
    
To measure this bending, we can place **two strain gauges**: one on the top and one on the bottom of the beam, and connect them in the **same branch of a Wheatstone bridge**.

Here’s what happens:

- The **top strain gauge** (under tension) increases its resistance.
- The **bottom strain gauge** (under compression) decreases its resistance.
- This difference creates an **imbalance in the Wheatstone bridge**, causing a measurable voltage difference at the intermediate node. This voltage tells us that bending is happening.
    
![[Pasted image 20251118212514.png|400]]
An important feature of this setup is that it is **insensitive to uniform tension or compression**:

- If the whole beam is just stretched (tension) or squeezed (compression), both top and bottom gauges change in the **same direction**.
- This causes **little to no change** in the voltage at the intermediate node, so the bridge output does not respond to overall tension or compression—only to bending.
    
![[Pasted image 20251118212610.png]]
If you want **higher sensitivity**, you can use a **full Wheatstone bridge with four resistances**:

- Place two resistors corresponding to the **top side** in opposite positions of the bridge.
- Place the other two resistors corresponding to the **bottom side** in the remaining opposite positions.
    

In this configuration:

- The two resistors on the **tension side** increase in resistance.
- The two resistors on the **compression side** decrease in resistance.
- This creates a **larger voltage difference** between the two branches of the bridge, giving a stronger signal and higher sensitivity to bending.

## <span style="color:rgb(239, 179, 1)">Strain Gauge - Possible Configurations</span>



second configuration



third 






![[Pasted image 20251118213729.png]]

Here we show **different Wheatstone bridge configurations**, ranging from the simplest (one strain gauge) to the most complete (four strain gauges). Here, we focus on **measuring tension or compression while being insensitive to bending**—the opposite of the bending-sensitive setup we discussed previously.

### <span style="color:rgb(161, 40, 226)">1. Single strain gauge</span>
![[Pasted image 20251118213749.png]]
- Simple setup with **one strain gauge**.
- Measures tension (resistance increases) and compression (resistance decreases).
- **Drawbacks:** Sensitive to **temperature** and also to **bending**, which can cause unwanted voltage changes.
    

### <span style="color:rgb(161, 40, 226)">2. Two strain gauges on opposite sides</span>


| Configuration                        | Readout Circuit                      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251118213816.png]] | ![[Pasted image 20251118213123.png]] |

- Place two strain gauges on opposite sides of the beam in **opposite positions on the Wheatstone bridge**.
- **Effect under tension:** Both resistors increase → voltage imbalance is measurable → output shows tension.
- **Effect under bending:** One resistor increases (tension side), the other decreases (compression side) → the changes **balance each other**, so output is nearly zero → insensitive to bending.
- **Temperature sensitivity:** Both resistors increase with temperature → output is still affected → **temperature is not compensated**.

### <span style="color:rgb(161, 40, 226)">3. Two gauges with one orthogonal for temperature compensation</span>

| Configuration                        | Readout Circuit                      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251118213935.png]] | ![[Pasted image 20251118213220.png]] |

- Add a second gauge **orthogonal to the first** (insensitive to tension/compression).
- **Temperature effect:** Both gauges on the same branch increase equally → intermediate node voltage remains constant → **temperature compensated**.
- **Bending effect:** The first gauge still changes with bending → output voltage changes → **sensitive to bending**.
    
### <span style="color:rgb(161, 40, 226)">4. Four-gauge configuration (optimal)</span>

| Configuration                        | Readout Circuit                      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251118214027.png]] | ![[Pasted image 20251118213433.png]] |

- Combines **temperature compensation** and **bending insensitivity**.
- Arrangement:
    
    - **Top side:** two gauges in orthogonal positions.
    - **Bottom side:** two gauges in orthogonal positions.
        
- **Temperature effect:** All four gauges change equally → bridge remains balanced → output = 0.
![[Pasted image 20251118213609.png]]

- **Tension effect:** Only the gauges aligned with the force change → creates imbalance → output shows tension/compression.
- **Bending effect:** Top gauge under tension, bottom gauge under compression → intermediate node changes **cancel each other** → output remains near zero.
    

**Conclusion:**

- By carefully choosing **gauge positions** and **bridge configuration**, you can design a system that is:
    
    - Sensitive **only to tension/compression**,
    - Insensitive to **bending**,
    - And/or **temperature variations**, depending on the configuration.
        
- The specific choice depends on the measurement objective for your application.
    

## <span style="color:rgb(239, 179, 1)">Strain Gauges - Applications</span>

Strain gauges are used to measure small deformations or changes in length in various structures and devices. Their main applications include:

![[Pasted image 20251118214809.png|400]]
1. **Railroad Maintenance:** Strain gauges can be installed along railway tracks to monitor changes in the length of the rails. This helps track how the rails expand or contract with temperature changes and ensures timely maintenance.
    
2. **Structural Monitoring:** They are used in “smart” infrastructure, like bridges, to monitor stress and detect potential problems. Strain gauges can also be applied to structures such as wind turbine panels to measure stress on their walls.
    
3. **High-Precision Robotics:** In medical or delicate robotic applications, strain gauges provide feedback on the stress experienced in different parts of the robot. This helps control the force applied with high accuracy.
![[Pasted image 20251118214829.png]]

4. **Bathroom Scales:** Strain gauges are commonly used in scales to measure weight. The scale has a fixed base and a free end where the load is applied. The connecting beam bends depending on the load, and the strain gauge measures this bending. From this measurement, the scale can calculate the weight applied.

# <span style="color:rgb(223, 109, 109)">Piezoelectric Force Sensor</span>

![[Pasted image 20251118215300.png|300]]

The second type of sensor we will study today is the **piezoelectric force sensor**. Like strain gauges, it is used to measure force. However, unlike strain gauges, piezoelectric sensors measure force **more directly**. Remember that strain gauges measure strain, and we calculate stress from strain using the material’s Young’s modulus. Piezoelectric sensors, instead, generate an electrical signal directly from the applied force.

## <span style="color:rgb(239, 179, 1)">Piezoeletric Effect</span>
![[Pasted image 20251118215315.png]]

In piezoelectric materials, we find a very useful property: **when an external force is applied, the material generates a voltage difference across its terminals**.

Materials that show this piezoelectric behaviour include **quartz, many types of crystals, ceramics, and even some biological materials**.

When **no force** is applied, the internal arrangement of charges inside the material is perfectly balanced. But if we apply a **force**, either tension or compression, the internal structure deforms, and this deformation causes the charges to become **unbalanced**.  
As a result, there is a **separation of charges**, and we can measure a voltage across the two terminals of the material.

- A **tensile force** produces a voltage with one sign.
- A **compressive force** produces a voltage with the opposite sign.
    

The interesting part is that the **reverse effect** is also true: if you apply a voltage to a piezoelectric material, you can cause a small deformation in it.

- Applying voltage in one direction makes the material **elongate**.
- Applying voltage in the opposite direction makes it **compress**.
    

>[!important] This deformation only responds to **changes** in the applied force.  
If you apply a constant force, the material will generate a voltage at the moment when the force changes, but then it will gradually **relax** and return toward its original configuration. As a result, the voltage disappears even if the force remains applied.


## <span style="color:rgb(239, 179, 1)">Piezoelectric Sensor - Electric Model</span>

![[Pasted image 20251118222721.png]]
For this reason, we can model a piezoelectric material using a **capacitor in parallel with a resistor and a current source**.

- The **current source** represents the charge generated inside the material when it is stressed.
- This current “injects” charge into the **capacitor**, and the voltage across the capacitor represents the **voltage generated by the piezoelectric material**.
- The **resistor** models the fact that the material slowly **relaxes** and returns to its original, unstressed state. This relaxation causes the capacitor to discharge over time.

We also know that the current needed to represent how the charge changes is related to the **derivative of the charge**.  
In the Laplace domain, this becomes:
$$I(t) = \frac{dQ(t)}{dt}$$
$$I(s) = s \cdot Q(s)$$

Please keep this relation in mind, because we will use it later when studying the **readout circuit** for this sensor.

This model corresponds to the **Norton equivalent** of the sensor.  

![[Pasted image 20251118222915.png]]

Of course, we can also build the **Thevenin equivalent**, but its equations are more complicated. For this reason, we usually prefer to work with the Norton model.

![[Pasted image 20251118223355.png|300]]
As mentioned before, piezoelectric sensors are very sensitive to **changes** in the applied force.  This means that when the force varies, the sensor generates an **equivalent current**, which can be expressed as:

$$I = \frac{\Delta Q}{\Delta t}  $$

The typical amount of charge generated by these sensors is around **10–20 picocoulombs per newton**.

This charge (Q) accumulates on the **equivalent capacitance** of the material, and the voltage you measure across the sensor is:
$$V = \frac{Q}{C}  $$

However, as we said earlier, if the force stays constant over time, the material will slowly **relax** back to its original state.  Because of this relaxation, the voltage across the piezoelectric material will also decrease and eventually return to zero. In our electrical model, this relaxation is represented by the **time constant** of the circuit, which is:
$$\tau = C_p \cdot R_p  $$

In theory, if we can measure the **peak voltage** generated by the sensor, we can determine the charge (Q), and from that, the value of the applied force.

### <span style="color:rgb(161, 40, 226)">The practical problem: stray capacitances</span>

The difficulty is that we do not only have the well-defined capacitance of the piezoelectric material. There are also **stray (parasitic) capacitances** in the system—coming from cables, connectors, or the environment.

These stray capacitances appear **in parallel** with the piezoelectric capacitance, so the voltage we measure depends not only on the charge and the sensor’s own capacitance, but also on these unwanted extra capacitances.
$$V = \frac{Q}{C_p+C_{stray}}$$

Since stray capacitances are not perfectly controlled or predictable, they introduce **uncertainty** in the estimation of charge, and therefore in the estimation of force.


## <span style="color:rgb(239, 179, 1)">Readout Circuits</span>

As mentioned, we will examine two readout circuits:

1. **The first circuit** gives an output directly proportional to the piezoelectric voltage ($V_p$).  
    This circuit is affected by stray capacitances.
2. **The second circuit** provides an output that does **not** depend on stray capacitances, making it the preferred solution.

### <span style="color:rgb(161, 40, 226)">First Readout Circuit (Voltage Mode Readout)</span>

Let’s begin with the first circuit. In this configuration, the piezoelectric material is modeled using its **Norton equivalent**, which includes:

- a current source (representing the generated charge),
- a capacitance ($C_p$),
- and a resistance ($R_p$) (representing relaxation).
![[Pasted image 20251118224152.png]]

This sensor is followed by an **operational amplifier** in a **non-inverting configuration**.

#### <span style="color:rgb(2, 141, 192)">1. Gain of the amplifier</span>
In a non-inverting amplifier, the **low-frequency gain** is:
$$G_{LF} = 1 + \frac{R_f}{R_g}  $$
This matches what we see in the circuit. A capacitor ($C_f$) is connected in parallel with ($R_f$) to provide **high-frequency filtering**.

#### <span style="color:rgb(2, 141, 192)">2. Cable capacitance</span>

![[Pasted image 20251118224242.png]]
The capacitance of the cable, ($C_c$), appears **in parallel** with the sensor capacitance ($C_p$).  
This is the stray capacitance we discussed before, and it affects the final output because it changes the effective capacitance seen by the sensor.

#### <span style="color:rgb(2, 141, 192)">3. Biasing the circuit<br></span>
![[Pasted image 20251118224242.png]]
The op-amp is powered with a **single supply** (0 V to $V_{cc}$).  
However, we want to measure both:

- tension → positive ($V_p$)
- compression → negative ($V_p$)

To allow this with a single supply, we **bias the entire circuit at half the supply**, ($V_{cc}/2$).  This makes ($V_{cc}/2$) the “resting point” when the sensor is not stressed.

Here’s what happens when ($V_p = 0$):

- There is no voltage difference across the sensor.
- Both sensor terminals sit at the bias level ($V_{cc}/2$).
- By negative feedback, the op-amp forces the **inverting input** to also be at ($V_{cc}/2$).
- No current flows through ($R_g$) or ($R_f$).
- Therefore, the output ($V_o$) is also equal to ($V_{cc}/2$).
    
When a force is applied, a voltage contribution is added on top of this ($V_{cc}/2$), and the output can move up or down depending on the direction of the force.

Here is your full text rewritten in **clear, smooth, easy English**, keeping all the technical content but making the explanation much clearer and better organized. I did _not_ change the meaning—only the readability.


#### <span style="color:rgb(2, 141, 192)">4. Transfer Function: From Input Charge to Output Voltage</span>

To analyze how this circuit processes the signal from the piezoelectric sensor, we first consider the sensor’s behavior in terms of **input current**, and then we convert the result to a function of **input charge**.

Normally, in circuit analysis we look at the transfer function between **voltage and current**, but piezoelectric sensors naturally generate **charge**, so the transfer function we ultimately want is:
$$\frac{V_o}{Q}  $$

To get there, we follow these steps:

1. **First**, compute the relation between the output voltage ($V_o$) and the input current (I).
2. **Then**, since in the Laplace domain  
    $I(s) = sQ(s)$ 
    we convert the result by simply multiplying by (s), which gives us  
    $\frac{V_o}{Q} = s \cdot \frac{V_o}{I}$. 
    
Also, because the bias voltage ($V_{cc}/2$) does not affect the circuit’s frequency behavior, we set it to zero during the AC analysis.

#### <span style="color:rgb(2, 141, 192)">5. Circuit for AC Analysis</span>

When we draw the simplified AC model:
![[Pasted image 20251118230014.png]]
- The sensor is represented by:
    
    - a current source (I),
    - a capacitance ($C_p$),
    - a resistance ($R_p$).
        
- In parallel with this, we have the cable capacitance ($C_c$) and the bias resistor ($R_b$).
- The amplifier is a standard non-inverting configuration with gain:  
    $1 + \frac{R_f}{R_g}$    
- The feedback includes a capacitor ($C_f$), providing high-frequency filtering.
#### <span style="color:rgb(2, 141, 192)">5. Poles and Zero of the Circuit</span>

**Pole 1 — due to ($C_p + C_c$)**
The first pole is created by the **total capacitance at the input**, which is:
$$C_p + C_c  $$
The equivalent resistance seen by this capacitance is:
$$R_p \parallel R_b  $$
So the first pole frequency is:
$$f_{p1} = \frac{1}{2\pi (C_p + C_c)(R_p \parallel R_b)}  $$

**Pole 2 — due to ($C_f$)**

The second pole comes from the feedback capacitor ($C_f$).  To find its frequency, we “turn off” all input sources.  This sets the op-amp inputs to 0 V, so no current flows through ($R_g$).  Thus, ($C_f$) only sees ($R_f$).

So:
$$f_{p2} = \frac{1}{2\pi C_f R_f}  $$
**Zero — due to ($C_f$)**

A zero appears when a capacitor becomes a **short circuit** but does _not_ force the output to zero.

- When ($C_p$) and ($C_c$) are shorted at high frequencies → the input node is forced to 0 V → **no zero** from them.
- When ($C_f$) is shorted → the output is _not_ forced to zero → this introduces a **zero**.

To find the zero’s frequency, we set the output node to 0 V and find the equivalent resistance seen by ($C_f$):
$$
R_f \parallel R_g  
$$
So the zero is at:

$$f_z = \frac{1}{2\pi C_f (R_f \parallel R_g)}$$

**Typical ordering of singularities**

- ($C_p + C_c$) is usually quite large → **low-frequency pole**.   
- ($C_f$) is small → **high-frequency pole**.
- The zero comes at an even higher frequency because ($R_f \parallel R_g < R_f$).

Thus, the order is:
$$f_{p1} < f_{p2} < f_z  $$
#### <span style="color:rgb(2, 141, 192)">6. Transfer Function in Different Frequency Regions</span>

**1. Low Frequency (before the first pole)**

At low frequency, all capacitors behave as open circuits.
$$V_p = I \cdot (R_p \parallel R_b)  $$
The output voltage is simply the input voltage multiplied by the non-inverting gain:
$$V_o = V_p \left(1 + \frac{R_f}{R_g}\right)  $$
So the low-frequency gain is:
$$\frac{V_o}{I} =  
(R_p \parallel R_b)\left(1 + \frac{R_f}{R_g}\right)  $$
 **2. Medium Frequency (after pole 1, before pole 2)**

After the first pole, ($C_p + C_c$) behave like short circuits.  This forces the input node to **0 V**, so:
$$V_p = 0 \quad\Rightarrow\quad V_o = 0  $$
Thus:
$$\frac{V_o}{I} = 0  $$
**3. High Frequency (after the second pole and after the zero)**

At high frequency, both:

- ($C_p + C_c$) are shorted → input = 0 V    
- ($C_f$) is shorted → feedback forces output = 0 V

Therefore:
$$\frac{V_o}{I} = 0  $$
#### <span style="color:rgb(2, 141, 192)">7.  Sketch of the Bode Plot</span>

The magnitude of $\dfrac{V_o}{I}$ looks like this:

![[Pasted image 20251119081433.png]]
- A constant gain at low frequency.
- A first roll-off of **−20 dB/dec** after the first pole.
- Then a second roll-off of **−40 dB/dec** after the second pole.
- Then, after the zero, the slope returns to **−20 dB/dec**.
#### <span style="color:rgb(2, 141, 192)">8. Compact transfer-function expression</span>

Start from the current-to-voltage form (useful for circuit algebra). The current-to-voltage transfer function of the voltage-mode readout is:
 $$ \boxed{\,\frac{V_o}{I}(s) = (R_p\!\parallel\!R_b)\left(1+\frac{R_f}{R_g}\right)\cdot \frac{1 + s\tau_z}{(1 + s\tau_{p1})(1 + s\tau_{p2})}\,}$$
where the time constants are:

![[Pasted image 20251119194909.png]]
- low-frequency pole (sensor + cable):
$$\tau_{p1} = (C_p + C_c)\,(R_p\!\parallel\!R_b)$$
- high-frequency pole (feedback $C_f$ with $R_f$​):    
$$\tau_{p2} = C_f\,R_f$$
- zero (feedback $C_f$​ sees $R_f\parallel R_g$​ when $V_o=0$):
$$\tau_z = C_f\,(R_f\!\parallel\!R_g)$$
#### <span style="color:rgb(2, 141, 192)">9. Convert to charge-to-voltage</span>

Because in the Laplace domain $I(s)=s\cdot Q(s)$, the desired transfer function is simply
  $$\boxed{\,\frac{V_o}{Q}(s) = s\cdot\frac{V_o}{I}(s)\,}$$
So explicitly:

$$\frac{V_o}{Q}(s) = s\,(R_p\!\parallel\!R_b)\left(1+\frac{R_f}{R_g}\right) \frac{1 + s\tau_z}{(1 + s\tau_{p1})(1 + s\tau_{p2})}$$

#### <span style="color:rgb(2, 141, 192)">10. Useful frequency-region approximations</span>

Take $s=j\omega$. 
***Low frequency ( $\omega \ll 1/\tau_{p1}$​ )***

![[Pasted image 20251119194629.png]]
All $1+s\tau\approx1$. 
Then
$$\frac{V_o}{Q}(s)\approx s\,(R_p\!\parallel\!R_b)\left(1+\frac{R_f}{R_g}\right)$$
Since $s\to0$, the transfer tends to **0** (zero at origin). Physically: piezo responds to changes, so DC/very low frequencies give no steady output.

***Mid frequencies (after $f_{p1}$​, before $f_{p2}$​: $1/\tau_{p1}\ll\omega\ll 1/\tau_{p2}$​)

![[Pasted image 20251119194648.png]]

Here $1+s\tau_{p1}\approx s\tau_{p1}$, but $1+s\tau_{p2}\approx1$ and $1+s\tau_z\approx1$ (zero not yet reached). Substitute and simplify:
$$\frac{V_o}{Q}(s)\approx \frac{(R_p\!\parallel\!R_b)\left(1+\dfrac{R_f}{R_g}\right)}{(C_p+C_c)(R_p\!\parallel\!R_b)} = \frac{1+\dfrac{R_f}{R_g}}{C_p + C_c}$$

So the mid-band response is **flat** (frequency independent) and equal to:
$$\boxed{\ \frac{V_o}{Q}\ \Bigr|_{\text{mid}} = \frac{1 + R_f/R_g}{C_p + C_c}\ }$$ 
Interpretation: amplifier gain multiplies the charge→voltage conversion set by the total input capacitance.

***High frequency ( $\omega \gg 1/\tau_{z}$  and $\omega\gg 1/\tau_{p2}$ )***

![[Pasted image 20251119194703.png]]
All $1+s\tau$ dominated by the $s\tau$ terms. After cancellation (work shown below), the limit is:
 $$\boxed{\ \frac{V_o}{Q}\ \Bigr|_{\infty} = \frac{1}{C_p + C_c}\ }$$
So at very high frequency the gain given by the amplifier cancels out and the response tends to $1/(C_p+C_c)$.
$$(1+R_f/R_g)\cdot\frac{(R_f\parallel R_g)/R_f}{C_p+C_c}$$ But $(R_f\parallel R_g)/R_f = 1/(1+R_f/R_g)$, so the amplifier gain cancels.

#### <span style="color:rgb(2, 141, 192)">11. Bode-shape summary</span>

![[Pasted image 20251119194754.png]]
- At very low freq: starts at **0** (zero at origin, slope +20 dB/dec from origin if plotted vs. freq because of the multiplying sss).
- Midband: **flat** plateau at $(1+R_f/R_g)/(C_p+C_c)$.
- Above $f_{p2}$​ and after the zero $f_z$​: slope changes and the final high-freq plateau equals $1/(C_p+C_c)$.

(Equivalent verbal description: zero at origin → midband flat → second pole rolls off → zero restores slope → high-freq limit.)

![[Pasted image 20251119194935.png]]
#### <span style="color:rgb(2, 141, 192)">12. Additional Physical Insight</span>

In this voltage-mode readout circuit, we can only use the sensor signal reliably **in the frequency range where the transfer function is flat**—that is, **between the low-frequency pole and the high-frequency pole**.  
In this region, the gain depends on the amplifier ratio $1 + R_f/R_g$​, which is good: both $R_f$​ and $R_g$​ are chosen by the designer and have well-controlled values.

However, the gain in this midband also depends on the **total input capacitance**:
$C_p + C_c$

Here:

- $C_p$ is the piezoelectric capacitance (known and stable)
- $C_c$​ is the **stray capacitance**, which is not well controlled and can vary with cables, connectors, layout, humidity, etc.
- 
Because the output voltage in this architecture is essentially:
$$V_\text{out} \propto \frac{Q}{C_p + C_c}$$

any uncertainty or change in $C_c$​ directly changes the output.  
This means:

- $V_\text{out}$​ depends on how much unknown parasitic capacitance is present.
- Therefore, the circuit **cannot accurately recover the charge Q***.
- And since Q is proportional to the applied force, the circuit also **cannot reliably estimate the force**.
    
In other words:

>[!info] This voltage-mode readout suffers from the fact that the voltage across the piezoelectric element, $V_p$​, changes with stray capacitance. Because of this, the final output $V_\text{out}$​ is sensitive to parasitic effects, making precise force measurement impossible.

This is the main limitation of this architecture and the reason why, in practice, designers prefer a different readout circuit (the charge-mode amplifier), which removes the dependence on $C_c​$.


### <span style="color:rgb(161, 40, 226)">Second Readout Circuit (Charge mode amplifier)</span>

![[Pasted image 20251119200236.png]]

To eliminate the limitations of the first circuit, we can use a **charge amplifier** as the readout stage.

Unlike the previous non-inverting configuration, the charge amplifier uses the operational amplifier in an **inverting topology** with a feedback capacitor $C_f$​.  
Here, $C_f$​ is not simply a high-frequency compensation component—**it is the core element of the measurement**, because:

#### <span style="color:rgb(2, 141, 192)">1. Goal of the charge amplifier<br></span>
We want **all the charge produced by the piezoelectric sensor** to be **integrated on $C_f$​**.

In the ideal case, the sensor—modeled by a Norton source (current generator + capacitor $C_p$​ + resistor $R_p$​)—is connected directly into an op-amp input that sits at **virtual ground (0 V)**.

#### <span style="color:rgb(2, 141, 192)">2. Why we want Ri=0 (ideally)</span>

Ideally, the input resistor $R_i$​ should be **zero ohms**.

- With $R_i = 0$, the sensor is directly connected to virtual ground.
- So **all current produced by the sensor flows into $C_f$​**.
- This ensures that _100% of the charge_ is integrated, giving:
    
$$V_\text{out} = -\frac{Q}{C_f} + \frac{V_{cc}}{2}$$

This equation is extremely important:  
➡️ **The output depends only on the feedback capacitor—not on the sensor capacitance or stray capacitance.**

This is the key advantage of charge-mode readout.

#### <span style="color:rgb(2, 141, 192)">3. Why we cannot actually make Ri=0</span>

In practice, we must add a **small resistor $R_i$​** at the input. This resistor is _not_ part of the sensing model—it is purely for **stability compensation**.

***Reason: Large sensor capacitance makes the op-amp unstable***

The piezoelectric element has a large internal capacitance $C_p$​, and connecting a large capacitance directly to the inverting input of an op-amp is known to cause **instability** or even oscillation.

You have already seen this effect with photodiode circuits:

- Photodiode capacitance caused instability.
- A feedback capacitor was added for compensation.

Here the situation is similar, but the compensation method is different:

#### <span style="color:rgb(2, 141, 192)">4. Compensation method</span>

- We insert a small resistor $R_i$​ in series with the input.    
- This resistor shifts the pole created by $C_p$​ from **infinite frequency** to a **finite, stabilizing frequency**.
- The value of $R_i$​ can be _very small_, but it must be **non-zero** to guarantee phase margin.
    
And importantly:

$$R_i \ll R_p$$
So most of the piezoelectric current still flows into the charge amplifier, not into $R_p$.

This will simplify our transfer-function calculations later.

#### <span style="color:rgb(2, 141, 192)">5. Biasing at VCC​/2</span>

Just like in the first circuit, the op-amp uses a **single supply** (0–VCC), but we must measure both:

- positive charge (compression)
- negative charge (tension)
    
Therefore:
- We shift the operating point to **$V_{CC}/2$**.
- This ensures the output can swing both above and below the midpoint.
    
During transfer-function analysis, however, this constant bias does not affect the dynamics, so we “turn it off” (set it to 0 V).

#### <span style="color:rgb(2, 141, 192)">6. Transfer Function Strategy</span>

Again, we want the final result:

$$\frac{V_\text{out}(s)}{Q(s)}$$

But as before, we start with something more familiar:

1. **First compute** the transfer function
    $$\frac{V_\text{out}(s)}{I(s)}$$
2. Then use the fundamental relation in the Laplace domain:
    $$I(s) = s Q(s)$$
3. So,
    $$\frac{V_\text{out}(s)}{Q(s)} = s \cdot \frac{V_\text{out}(s)}{I(s)}$$
This is exactly the same reasoning as in the previous circuit.

#### <span style="color:rgb(2, 141, 192)">7. Computation</span>

![[Pasted image 20251119202521.png]]
Okay, so let’s start with the analysis. We have our current source representing the piezoelectric sensor.  After that, we see the sensor’s internal capacitance, which is the parallel combination of ($C_p$) and the stray capacitance ($C_c$).  Then we have the resistor ($R_p$), which models the piezoelectric material’s leakage.  In series with this, we add the small compensation resistor ($R_i$).  Finally, the signal enters the charge amplifier: the non-inverting input is grounded, and the feedback network includes ($R_f$) and ($C_f$).

Our goal is to compute the output voltage.

#### <span style="color:rgb(2, 141, 192)">8. Singularities of the Circuit</span>

As in the previous example, we start by identifying the poles and zeros.

 ***Pole from ($C_p \parallel C_c$)***
 
The parallel combination ($C_p + C_c$) produces one pole.  Because of the presence of ($R_i$), this pole is **not** at infinite frequency.  
Its frequency is:
$$f_{p1} = \frac{1}{2\pi (C_p + C_c) \left( R_p \parallel R_i \right)}  $$


Since the inverting input is at virtual ground, the capacitors and resistors are referenced to ground, so the parallel combination is valid.

Because ($R_i \ll R_p$), the parallel resistance is dominated by ($R_i$). Thus, we can approximate:

$$f_{p1} \approx \frac{1}{2\pi (C_p + C_c) R_i }  $$

 ***Pole from the feedback capacitor $(C_f)$***

The second pole arises from the feedback network:
$$f_{p2} = \frac{1}{2\pi R_f C_f}  $$
Although ($C_p$) is physically much larger than ($C_f$), the corresponding pole is at a very high frequency because ($R_i$) is very small and close to zero.  
Therefore:

- The pole associated with ($C_p + C_c$) is the **high-frequency pole**.
- The pole associated with ($C_f$) is the **low-frequency pole**, which determines the integration range.

***Zeros***

There are **no zeros** in this circuit.  If ($C_p$) or ($C_c$) were short-circuited, they would force the input voltage ($V_p$) to zero, and consequently the output would be zero.  
Similarly, if ($C_f$) is shorted, the output node is directly tied to virtual ground.  
Thus, neither ($C_f$) nor ($C_p \parallel C_c$) produces zeros.

So the transfer function contains **only poles**.

#### <span style="color:rgb(2, 141, 192)">9. Transfer Function</span>

We start by computing the low-frequency gain.

Let ($I_f$) be the current flowing through ($R_i$) and therefore through the feedback network.  This current comes from the input current ($I)$, split between $(R_p)$ and $(R_i)$.  Using the current divider:
$$I_f = I \cdot \frac{R_p}{R_p + R_i}  $$
Since ($R_i \ll R_p$), this ratio is very close to 1.

At low frequency, the output voltage is:
$$V_\text{out} = -I_f R_f  $$

Thus:
$$\frac{V_\text{out}}{I} =-\frac{R_p}{R_p + R_i} R_f  $$

This gives the low-frequency constant gain.

***Mid frequencies***

At mid frequencies, we are above the pole of ($C_f$), so ($C_f$) behaves as a short circuit.  This shorts the output node to virtual ground, giving:
$$\frac{V_\text{out}}{I} = 0  $$
 ***High frequencies***

At high frequency, the capacitors $(C_p)$ and $(C_c)$ also behave as shorts.  
Thus:

- The input current flows through the short created by $(C_p \parallel C_c)$.
- $(C_f)$ is also a short.

Therefore, again:
$$\frac{V_\text{out}}{I} = 0  
$$


#### <span style="color:rgb(2, 141, 192)">10. Bode Plot Interpretation</span>

If we plot the magnitude of $(V_\text{out}/I)$:

- We start at the low-frequency gain  
    $\left| \frac{-R_p}{R_p + R_i} R_f \right|$
- Then we encounter the pole due to ($C_f$).
- Afterwards, we encounter the high-frequency pole from ($C_p + C_c$).

![[Pasted image 20251119203315.png]]

So the final shape is:
- **Flat** at low frequency
- **-20 dB/dec** after the first pole
- **-40 dB/dec** after the second pole

with no zeros.


#### <span style="color:rgb(2, 141, 192)">11. Transfer function dependent on Q</span>
Up to now, we have computed the transfer function between the output voltage and the **input current**, $\frac{V_{\text{out}}}{I}$​​.  
However, what we actually want is the transfer function between the output voltage and the **input charge**, $\frac{V_{\text{out}}}{Q}$​​.

To move from one to the other, we simply recall that in the Laplace domain:
$$I(s)=sQ(s)$$

Therefore:
$$\frac{V_{\text{out}}}{I} = \frac{V_{\text{out}}}{sQ} \quad \Rightarrow \quad \frac{V_{\text{out}}}{Q} = s \cdot \frac{V_{\text{out}}}{I}$$

So we now write the full Laplace expression of VoutI\frac{V_{\text{out}}}{I}IVout​​, and then multiply by sss to obtain the charge transfer function.


 **Transfer Function $\frac{V_{\text{out}}}{I}$​​ in the Laplace Domain**

We know the low-frequency gain is:
$$\frac{V_{\text{out}}}{I} = - \frac{R_p}{R_p + R_i} R_f$$
In this circuit there are two poles:

![[Pasted image 20251119204252.png]]
- the low-frequency pole from $C_f R_f$​,
- the high-frequency pole from $(C_p + C_c)(R_p \parallel R_i)$.
    
Since there are no zeros, the Laplace form is:
$$\frac{V_{\text{out}}}{I}(s) = - \frac{R_p}{R_p + R_i} R_f \; \frac{1}{(1 + s R_f C_f)\left[1 + s (C_p + C_c)(R_p \parallel R_i)\right]}$$

***Now Multiply by $s$ to get $\frac{V_{\text{out}}}{Q}$​​***

$$\frac{V_{\text{out}}}{Q}(s) = s \cdot \left[ - \frac{R_p}{R_p + R_i} R_f \; \frac{1}{(1 + s R_f C_f)\left[1 + s (C_p + C_c)(R_p \parallel R_i)\right]} \right]$$
Now we analyze the three frequency regions.

 ***1. Low Frequency ($s \to 0$)***
![[Pasted image 20251119205651.png]]

When $s \to 0$:

- The denominators → 1
- The numerator contains a factor $s$, so:

$$\frac{V_{\text{out}}}{Q} \to 0$$
Thus the transfer function **starts at zero**.  
This looks like a zero at the origin—but it is _not_ a physical circuit zero; it only appears because we multiplied by sss.

***Mid Frequency (after the first pole, before the second)***

![[Pasted image 20251119205643.png]]
In this region:

- For the first pole: $s R_f C_f \gg 1$
    ⇒ $1 + s R_f C_f \approx s R_f C_f$
- For the second pole: $s (C_p + C_c)(R_p \parallel R_i) \ll 1$  
    ⇒ $s(\ldots) \approx 1$
Then:

$$\frac{V_{\text{out}}}{Q} \approx s \left[ - \frac{R_p}{R_p + R_i} R_f \; \frac{1}{s R_f C_f} \right]$$

The $s$ cancels, $R_f$​ cancels, and since $R_i \ll R_p$​:

$$\frac{R_p}{R_p + R_i} \approx 1$$
Therefore the mid-band gain becomes:

$$\frac{V_{\text{out}}}{Q} \approx -\frac{1}{C_f}$$
This is the key result:  **the transfer function in the useful bandwidth is completely independent of the sensor capacitance.**

***High Frequency (after both poles)***

![[Pasted image 20251119205620.png]]
In this region:

- For both poles:  
    $s R_f C_f \gg 1$ and  
    $s (C_p + C_c)(R_p \parallel R_i) \gg 1$
    
Thus:
$$\frac{V_{\text{out}}}{Q} \approx s \left[ - \frac{R_f}{s R_f C_f \; s (C_p + C_c)(R_p \parallel R_i)} \right]$$

One $s$ cancels, leaving a remaining $1/s$:

$$\frac{V_{\text{out}}}{Q} \propto \frac{1}{s} \to 0 \quad \text{as } s \to \infty$$

So the high-frequency gain goes to **zero**, as expected.

![[Pasted image 20251119205604.png]]

#### <span style="color:rgb(2, 141, 192)">9. Final Shape of the Bode Magnitude Plot</span>

The magnitude of $$\left|\frac{V_{\text{out}}}{Q}\right|$$
![[Pasted image 20251119205711.png]]

## <span style="color:rgb(239, 179, 1)">Applications</span>

In conclusion, piezoelectric sensors are useful in any application where we need to measure a **dynamic force** or a **rapidly varying mechanical stimulus**.  
Since piezoelectric materials cannot measure static forces (their response goes to zero at low frequency), they are ideal for applications involving **impact, vibration, acceleration, or periodic loading**.

### <span style="color:rgb(161, 40, 226)">1. Force and pressure measurement</span>

Piezoelectric elements are commonly used when we want to measure how force is applied to a surface.  

![[Pasted image 20251119210004.png]]

For example, **force plates** used in rehabilitation, sports science, and gait analysis often rely on piezoelectric sensors to capture how the load is distributed when someone walks, runs, or jumps.

### <span style="color:rgb(161, 40, 226)">2. Energy harvesting</span>

![[Pasted image 20251119210031.png]]

Piezoelectric materials can convert mechanical vibrations or fluid flow into electrical energy. This capability makes them suitable for low-power energy harvesters, where ambient vibrations are transformed into voltage that can be stored or used to power small electronic devices.

### <span style="color:rgb(161, 40, 226)">3. Ultrasonic technology (sensing and actuation)</span>

![[Pasted image 20251119210018.png]]

We will see in the next class that piezoelectric materials are fundamental in **ultrasonic systems**, where they serve both as:

- **Sensors**, converting ultrasonic waves into electrical signals
- **Actuators**, generating ultrasonic vibrations when a voltage is applied
    

This dual property enables applications such as medical ultrasound imaging, ultrasonic cleaning, nondestructive testing, and sonar.


### <span style="color:rgb(161, 40, 226)">4. Precision actuators</span>

Piezoelectric elements are also used as **high-precision actuators**.  
By applying a controlled voltage, the material expands or contracts by a very small and predictable amount.  
This is particularly useful in:

- Precision dosing and pumping
- Microfluidics
- Optical alignment systems
- High-resolution positioning stages
    

These actuators are valued for their accuracy, fast response, and ability to produce extremely fine displacements.


### <span style="color:rgb(161, 40, 226)">Final remark</span>

So overall, piezoelectric materials are extremely versatile components that can function as **sensors**, **actuators**, or even **energy sources**, depending on how we exploit their electromechanical properties.

That concludes today’s topic—see you in the next class!