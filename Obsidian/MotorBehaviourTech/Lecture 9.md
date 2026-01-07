
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



### <span style="color:rgb(161, 40, 226)">Amplification with Instrumentational Amplifier</span>
![[Pasted image 20251016163736.png]]

Once you have a **full Wheatstone bridge**, the strain gauges convert **resistance variations** into a **small differential voltage** at the bridge output ($V_O$).  This voltage is typically **very small**, often in the **microvolt to millivolt range**, so it **must be amplified** before it can be processed or digitized.

The standard solution is to use an **instrumentation amplifier**.

An instrumentation amplifier is ideal for strain-gauge measurements because it has several key properties:

**High input impedance**

- The bridge output must not be loaded by the amplifier.
- If the amplifier input impedance were comparable to the bridge resistance (R_0), it would:
    - Alter the bridge balance
    - Introduce **nonlinearities**
    - Reduce measurement accuracy
- Instrumentation amplifiers have **very high (almost infinite) input impedance**, so the bridge behavior is preserved.
    
 **High common-mode rejection ratio (CMRR)**

- The bridge output is a **differential signal**.
- External noise (electromagnetic interference, power-line noise, cable pickup) often appears as **common-mode noise** on both output wires.
- The instrumentation amplifier strongly suppresses common-mode signals while amplifying only the **difference**.
- This makes the measurement robust against noise.

 **High and easily adjustable gain**

- The instrumentation amplifier gain can be made **very large** (hundreds or thousands).
- The gain is typically set using external resistors, for example:  
$$    G = \left(1 + \frac{2R_1}{R_G}\right)\frac{R_3}{R_2}  $$
- This allows amplification from:
    - **microvolts or millivolts**
    - up to **volts**, which is suitable for ADCs and data acquisition systems.

![[Pasted image 20260104091103.png]]

When the load cell is designed to measure **compressive forces**, the applied load compresses a cylindrical structure.

![[Pasted image 20260104091157.png|300]]
- **Strain gauges 1 and 3** are placed along the **vertical direction**
    - Under compression, they experience the **same deformation** (elongation or shortening)
- **Strain gauges 2 and 4** are placed in the **radial (horizontal) direction**
    - Their deformation is **opposite** to that of gauges 1 and 3
        

As a result:
- Two gauges increase their resistance
- Two gauges decrease their resistance
- This configuration is ideal for a **full Wheatstone bridge**, maximizing sensitivity
    
If the sign of the applied force changes (from compression to tension), the behavior of the strain gauges is reversed.

These load cell bodies are often **hollow** rather than solid.
- Removing material **reduces stiffness**
- Lower stiffness produces **larger strain** for the same applied force
- Larger strain improves the **signal-to-noise ratio**
    

If the cylinder were solid:
- The strain would be much smaller
- The measurement could be dominated by noise
- Force estimation would become less reliable

![[Pasted image 20260104091211.png|400]]

A different strain gauge arrangement is used for **tensile load transducers**.

- In this case, the load cell is **pulled rather than compressed**
- The deformation is mainly **radial**
- Strain gauges are positioned to detect this radial elongation
    

Again, the gauges are arranged so that:
- Some experience increased strain
- Others experience decreased strain
- The bridge output is maximized for tensile forces

![[Pasted image 20260104091329.png]]
Inside the enclosure, load cells can have **different shapes**, depending on the specific application.

One common example is the **S-type load cell**.  
This structure provides **very high sensitivity**.
- When a load is applied, the force acts through a **long lever arm**
- This creates a **large bending moment**
- The bending produces a **significant surface deformation**
- The strain gauges therefore experience a **larger strain**

Because of this mechanical amplification, S-type load cells are able to detect **small forces very accurately**, making them especially suitable for applications where **high sensitivity** is required.
***
***

# <span style="color:rgb(223, 109, 109)">Force Measurement - Piezoelectric and plates sensors</span>

Today’s topic introduces **piezoelectric sensors** as another type of sensor for **force measurements**.We will briefly compare: **Load cells**, **Piezoelectric sensors**

We will also see how both can be used to measure **ground-directional (ground-reaction) forces** during **movement analysis**
    
A typical application example is **dynamometric force platforms**
    
### <span style="color:rgb(161, 40, 226)">Reminder: Load Cells</span>

A classical example is the **S-shaped load cell**. Part of the metal body is removed to:
- Decrease mechanical stiffness   
- Increase strain for a given applied stress
- **Strain gauges** are attached to the structure
- Applied force → strain → **change in electrical resistance**
- The resistance change is measured using a **Wheatstone bridge**
- These sensors are called **modulating sensors** because:
    - They do not generate energy
    - They _modulate_ an electrical quantity (resistance)

### <span style="color:rgb(161, 40, 226)">Piezoelectric Sensors</span>

- A piezoelectric sensor is typically a **small disc with two electrodes**
- When **pressure or force** is applied:
    
    - The material generates an **electric charge**
    - The charge can be read as **charge or voltage** using suitable circuits
        
- Unlike strain gauges:
    - The signal is **generated by the sensor itself**
        
- For this reason, piezoelectric sensors are called **generating sensors**
    
### <span style="color:rgb(161, 40, 226)">Energy Harvesting</span>

- Piezoelectric sensors can be used for **energy harvesting** <span style="color:rgb(71, 215, 140)">(capturar energía)</span>
- This means:
    - Mechanical motion (e.g. movement, vibrations)
    - Produces electrical charge
    - The charge can be stored and used to power small electronic devices
- This process is also called **power or energy transfer**
    
### <span style="color:rgb(161, 40, 226)">Historical Background</span>

- Piezoelectricity was discovered in the **late 19th century** by the **Curie brothers**
- Piezoelectric materials also exist in nature:
    - **Quartz** is a well-known example
        
- When quartz is mechanically stressed:
    - It generates electrical charge on its surfaces
        

### <span style="color:rgb(161, 40, 226)">Applications of Piezoelectric Materials</span>
![[Pasted image 20260104153331.png|400]]
- **Acoustic guitar pickups**
- **Quartz watches**
    - Used as highly accurate **frequency stabilizers**
- **Ultrasound systems**
    - Use piezoelectric materials as **actuators**
        
### <span style="color:rgb(161, 40, 226)">Direct and Inverse Piezoelectric Effects</span>

Piezoelectric devices are **reversible**, meaning they can act as both sensors and actuators:
![[Pasted image 20260104153408.png|300]]
- **Direct piezoelectric effect (sensor mode)**
    - Applied force → generated charge
        
- **Inverse (converse) piezoelectric effect (actuator mode)**
    - Applied voltage → mechanical deformation
        

This is a key difference from load cells, which:

- Can only work as sensors
- Cannot act as actuators
    
#### <span style="color:rgb(71, 215, 140)">Ultrasound Example<br></span>
- Ultrasound systems use **piezoelectric actuators**
- Required frequencies are very high:
    - Approximately **1–10 MHz**
- These frequencies cannot be achieved with mechanical actuators (e.g. motors)
- Applying an alternating voltage to a piezoelectric crystal:
    - Produces rapid mechanical vibrations
    - Generates acoustic (ultrasound) waves

### <span style="color:rgb(161, 40, 226)">Frequency Characteristics</span>

- Piezoelectric sensors:
    - Can measure **very low frequencies**
    - **Cannot measure DC (0 Hz)** signals
    
## <span style="color:rgb(239, 179, 1)">Piezoelectric effect</span>

The **origin of the piezoelectric effect** lies in the **atomic structure of the material**, specifically in the way atoms are arranged inside the crystal lattice. <span style="color:rgb(71, 215, 140)">(red cristalina)</span>
![[Pasted image 20260104153912.png|200]]
Piezoelectric materials are either **natural crystals** or **synthetic materials**, such as ceramics. Natural crystals, like quartz, inherently possess a well-defined crystal lattice. Ceramics, on the other hand, are engineered so that the many tiny crystallites inside them are **aligned in a preferred direction**. This alignment allows the ceramic to behave, at a macroscopic level, in a way that is very similar to a single natural crystal, thus exhibiting piezoelectric properties.

Let us assume that we have such a crystal structure, whether natural or synthetic. When **no external stress** is applied to the material, the crystal is in mechanical equilibrium. At the atomic scale—on the order of angstroms or nanometers—the positive and negative charges inside each unit cell are arranged symmetrically. Because of this symmetry, the centers of positive and negative charge coincide, meaning that **no electrical dipole is formed**. As a result, no electrical signal is generated at the sensor output.

When an **external mechanical stress** is applied, the situation changes. The applied force slightly shifts the positions of the atoms inside the crystal lattice. This displacement causes the centers of positive and negative charge to separate, creating an **electric dipole**. The collective effect of many such dipoles throughout the crystal produces a measurable **electric charge on the surface of the material**.

However, this effect only occurs if the crystal is **not centrosymmetric**. A centrosymmetric crystal is one in which there exists a point of symmetry such that, for every atom located at coordinates ((x, y, z)), there is an identical atom at ((-x, -y, -z)). In materials with this property, any charge displacement caused by stress is perfectly balanced by an opposite displacement elsewhere in the lattice. Consequently, **no net electric polarization** is produced, and the material cannot be piezoelectric.

In contrast, if this centrosymmetry is absent, the charge displacement caused by mechanical stress does not cancel out. The result is a net polarization of the crystal, and the material exhibits the **piezoelectric effect**.

Finally, it is important to note that piezoelectric materials are also **sensitive to temperature changes**. A variation in temperature can cause a redistribution of charges within the crystal even in the absence of mechanical stress. This phenomenon is known as the **pyroelectric effect**. Because temperature changes can generate electrical charge at the sensor output, temperature control or compensation is often necessary when using piezoelectric sensors in precise measurement applications.
![[Pasted image 20251016165221.png]]

### <span style="color:rgb(161, 40, 226)">Centrosymmetric (symmetric) crystal lattice</span>
![[Pasted image 20260104154340.png|]]
The structure shown here is an example of a **centrosymmetric crystal lattice**. In such a lattice, for every atom located at a given position in space, there is an identical atom located at the opposite position with respect to the center of the crystal. In other words, the crystal has a point of symmetry: every coordinate (x, y, z) has a corresponding point at (-x, -y, -z).

Because of this symmetry, when the crystal is subjected to **mechanical strain**, such as compression or stretching, the internal distribution of electrical charges remains balanced. Even though the atoms may move slightly closer together or farther apart, their relative positions change in a perfectly symmetric way. As a consequence, **no net electrical dipole is formed** inside the microcrystals, and therefore no electric charge appears on the surface of the material. The overall polarization remains zero.

### <span style="color:rgb(161, 40, 226)">Non-centrosymmetric (asymmetric) crystal lattice</span>
![[Pasted image 20260104154451.png]]
The situation is very different for a **non-centrosymmetric (asymmetric) crystal lattice**. In this case, the atomic arrangement does not have a center of symmetry. When such a crystal is compressed or stretched, the deformation causes an **unequal displacement of positive and negative charges**. This displacement breaks the internal charge equilibrium and leads to the formation of an electric dipole.

For example, during compression, negative charges may be displaced toward one side of the crystal while positive charges move toward the opposite side. This separation of charge produces a measurable electrical signal at the sensor output.

The charges involved in this process originate from the **ions within the crystal lattice**. In metallic or ceramic piezoelectric materials, these are typically metal ions. In the case of natural crystals such as quartz (silicon dioxide, SiO₂), the effect is mainly due to the relative displacement of **oxygen ions** within the lattice structure.

This mechanism explains why only non-centrosymmetric crystal structures can exhibit the **piezoelectric effect**, and why centrosymmetric crystals cannot generate electrical charge under mechanical stress.

## <span style="color:rgb(239, 179, 1)">Piezoelectric Ceramics</span>


Now let us consider **piezoelectric ceramics**. One of the most commonly used ceramic structures for piezoelectric sensors is **perovskite**. Perovskite crystals have a very characteristic lattice structure.
![[Pasted image 20260104155315.png]]
At a microscopic level, the structure consists of a **cubic unit cell**. At the corners of the cube there are large **divalent metal ions**, typically barium (Ba²⁺) or lead (Pb²⁺). Along the faces of the cube there are **oxygen ions**, and at the center of the cube there is a smaller **tetravalent metal ion**, such as titanium (Ti⁴⁺) or zirconium (Zr⁴⁺).
![[Pasted image 20260104155225.png|200]]
At temperatures **above the Curie temperature**, this unit cell has a perfectly cubic shape. A cube is a **symmetric structure**, meaning that the positive and negative charges are distributed in a balanced way. Because of this symmetry, there is **no net electrical dipole**, and therefore no piezoelectric effect can be observed. In this condition, even if the material is stressed, no electrical charge is generated.

![[Pasted image 20260104155256.png|200]]
When the temperature decreases **below the Curie temperature**, typically down to ambient temperature, the situation changes. The cubic cell becomes **distorted** and turns into a prism with a square base but one side longer than the others. This distortion causes the central tetravalent ion (titanium or zirconium) to **shift from its central position** within the cell.

As a result of this displacement, the charges are no longer symmetrically distributed. The positive charge associated with the central ion becomes closer to one face of the crystal than to the opposite face. This creates a **permanent electric dipole moment** within each microcrystal.

The same phenomenon occurs when an **external mechanical force or pressure** is applied to the ceramic. The applied stress causes further displacement of the ions within the lattice, modifying the dipole moment and generating an **electric charge on the surfaces** of the material.

In summary:

- **Symmetric structures** (such as cubic perovskite above the Curie temperature) do **not** generate dipoles.
- **Asymmetric structures** (below the Curie temperature or under mechanical deformation) **do generate dipoles**.
    
This is the fundamental reason why perovskite ceramics exhibit piezoelectric behavior and are widely used in piezoelectric sensors and actuators.

![[Pasted image 20251016170843.png|600]]

These are the materials typically used in **perovskite-based piezoelectric ceramics**. The structure is mainly composed of **heavy metal ions**, such as **barium or lead**, combined with **oxygen**. The oxygen ions form a characteristic structure that can be visualized as a **double pyramid (or octahedron)** surrounding a smaller central ion.

The small ion located at the center of this structure is a **tetravalent metal ion**, usually **titanium (Ti⁴⁺)** and/or **zirconium (Zr⁴⁺)**. In most practical piezoelectric ceramics, both titanium and zirconium are present at the same time. The material is therefore not a single compound, but a **solid solution** in which titanium and zirconium coexist in specific proportions.

By **changing the ratio between titanium and zirconium**, the electrical, mechanical, and piezoelectric properties of the ceramic can be tuned. For example, the sensitivity, stiffness, Curie temperature, and overall piezoelectric response can be adjusted by modifying this composition. This is why perovskite ceramics, such as lead zirconate titanate (PZT), are extremely versatile and widely used in piezoelectric sensors and actuators.

![[Pasted image 20260104160229.png]]

Inside the **bulk of a piezoelectric ceramic**, when the material is **below the Curie temperature**, many individual microscopic dipoles are formed. Each microcrystal has its own electric dipole, and **neighboring dipoles tend to group together** because they interact electrically. In this way, clusters of aligned dipoles are created. These clusters are called **domains**.

However, this alignment occurs only **locally**, within each domain. Across the entire ceramic, the domains are **oriented randomly**, so their dipole moments cancel each other out. As a result, even though dipoles exist inside the material, there is **no net macroscopic electric polarization**.

This behavior is very similar to what happens in **ferromagnetic materials**. In an unmagnetized ferromagnet, magnetic dipoles form domains, but these domains are randomly oriented. Because of this random orientation, the material does not exhibit any net magnetization. Only when the domains are forced to align in a preferred direction does the material become magnetized.

If we can find a way to **allow the dipoles or domains to move and reorient**, then a majority of them can align along a specific direction. When this happens, the material acquires a **net polarization** (in piezoelectric ceramics) or a **net magnetization** (in magnetic materials).
![[Pasted image 20260104160151.png|200]]
This idea is nicely illustrated by a historical analogy related to the expression _“strike while the iron is hot.”_ In the Middle Ages, it was possible to create a **permanent magnet** even without modern technology. The method relied on heating a piece of iron until it became ductile and then placing it along the **north–south direction**, where it is exposed to the Earth’s magnetic field (about half a gauss). While the iron was hot, **hammering** it allowed the magnetic domains to move more freely and gradually align with the Earth’s magnetic field. When the iron cooled down, this alignment was partially preserved, resulting in a magnetized object.

This process works only if the material is **not pure soft iron**, because soft iron does not retain magnetization well. Instead, **steel**, which is iron with a small amount of carbon (commonly present in historical furnaces), can retain the aligned domains and therefore become a permanent magnet.

The same concept of **domain alignment** is fundamental for understanding how piezoelectric ceramics are polarized and made functional as sensors and actuators.

## <span style="color:rgb(239, 179, 1)">Polarization of piezoelectric ceramics</span>

![[Pasted image 20251016171159.png]]

So, what do we want to do? Do we want to **hammer piezoelectric ceramics**? Of course not. Instead of using mechanical stress, we use a **controlled electrical and thermal process** to align the dipoles inside the ceramic.
![[Pasted image 20260104160722.png]]
We start from a condition in which the **domains are completely randomly oriented**, so the material has no net polarization. Then, the ceramic is subjected to a **strong external electric field**. Unlike the magnetic case, here we are not using a magnetic field, because the dipoles we want to align are **electric dipoles**.

This process is carried out at a temperature **slightly below the Curie temperature**. At this temperature, the domains are still mobile enough to rotate and reorient, but the crystal structure is already in its non-centrosymmetric phase. While the electric field is applied, the dipoles tend to **align along the direction of the field**.

Once a sufficient alignment has been achieved, the electric field is removed and the material is **cooled down**. During cooling, the domains lose their mobility, and the aligned configuration becomes “frozen” into the material. As a result, most of the dipoles remain oriented in the same direction, which is determined by the direction of the applied electric field.
![[Pasted image 20260104160736.png|200]]
After this treatment, the piezoelectric disk (or ceramic element) has a **permanent polarization**. In addition, the material becomes **permanently elongated** at the microscopic level. As shown in the previous figure, when the crystal is below the Curie temperature, the lattice is no longer perfectly cubic but distorted. This distortion of the microcrystals is reflected at the macroscopic level as a small elongation of the ceramic itself.

In summary, after poling, the piezoelectric ceramic is **permanently polarized and slightly elongated**, with most of its internal dipoles aligned in a common direction. This is the condition that allows the material to effectively operate as a piezoelectric sensor or actuator.

### <span style="color:rgb(161, 40, 226)">What can piezoelectric ceramics do?</span>
![[Pasted image 20251016171852.png]]

**Poling and piezoelectric behavior**

_Poling_ refers to the process of heating a piezoelectric material and applying a strong electric field in order to align its internal electric dipoles. This treatment defines a **preferred polarization direction** in the material.

If a piezoelectric sensor element is poled in a given direction, its electrical response depends on how it is mechanically stressed:
![[Pasted image 20260104161051.png|300]]
- When the material is **compressed along the poling direction**, it generates a voltage with the **same polarity as the poling voltage**.
- When the material is **stretched (tension) along the poling direction**, it generates a voltage with the **opposite polarity**.
    

This behavior describes the **direct piezoelectric effect**, which is exploited when piezoelectric devices are used as **sensors or generators**.

**Inverse piezoelectric effect (actuators)**

![[Pasted image 20260104161109.png|300]]
Piezoelectric materials can also operate as **actuators**, exploiting the **inverse piezoelectric effect**:

- If an applied voltage has the **same polarity as the poling voltage**, the piezoelectric element **elongates**.
- If the applied voltage has the **opposite polarity**, the element **contracts**.
    
By continuously alternating the applied voltage, the piezoelectric element repeatedly elongates and shortens.

A practical example is an **ultrasound transducer**: an array of piezoelectric disks is driven by an alternating electric field at very high frequencies (typically in the megahertz range). The rapid mechanical deformation of the elements generates ultrasonic waves that propagate into the medium.

**Other applications**

Piezoelectric actuators are also used in **high-performance motors and positioning systems**. These devices are:

- Extremely fast,
- Highly precise,
- Free from magnetic fields.
    
Because they do not rely on magnets, piezoelectric actuators are suitable for **magnetically sensitive environments**, such as medical imaging systems or scientific instrumentation.

**Common piezoelectric materials**

Examples of widely used piezoelectric materials include:

- **Barium titanate (BaTiO₃)**
- **Lithium niobate (LiNbO₃)**
- **Polyvinylidene (di)fluoride (PVDF)**
- **Lead zirconate titanate (PZT)**
    

In all these materials, mechanical compression or tension applied to a **poled** element changes the dipole moment, generating an electric charge (and therefore a voltage across the electrodes). Compression or tension along the polarization direction produces voltages whose polarity depends on whether the stress aligns with or opposes the original poling field.

## <span style="color:rgb(239, 179, 1)">Commonly used Piezoelectric materials</span>

![[Pasted image 20251016172126.png|500]]
Piezoelectric materials can be divided into **natural crystals**, **piezoelectric ceramics**, and **polymers**.

Some materials are **naturally piezoelectric**, meaning they do not require any special treatment to exhibit the piezoelectric effect. Typical examples include:

- **Quartz**, which is historically and practically the most important piezoelectric material for electrical applications
- **Tourmaline**
- **Rochelle salt**
- **Lithium niobate (LiNbO₃)**
- **Lithium tantalate (LiTaO₃)**
- **Langasite-type crystals**, which are complex compounds based on lanthanum, gallium, silicon, and oxygen
- **Lithium borate**
- **Zinc oxide (ZnO)**
    
Examples of such natural crystals include **SiO₂ (quartz)**, **langasite**, and **lithium borate**. These materials already possess a non-centrosymmetric crystal lattice, so they exhibit piezoelectric behavior without any additional processing.

### <span style="color:rgb(161, 40, 226)">Piezoelectric ceramics</span>

Piezoelectric ceramics, unlike natural crystals, **do not exist in nature** in their active form. Their piezoelectric properties are obtained through a **poling process**, as previously described.

Common piezoelectric ceramics include:

- **Barium titanate (BaTiO₃)**
- **Lead titanate (PbTiO₃)**
- **Lead zirconate titanate (PZT)**
    

PZT is a perovskite-based ceramic composed of **lead, zirconium, titanium, and oxygen**. Its general chemical formula includes a mixture of zirconium and titanium, often expressed as a fraction _x_ and _(1 − x)_. By changing the Zr/Ti ratio, it is possible to tailor the material’s properties, such as sensitivity, stiffness, and temperature stability.

Another example is **lead niobate**, which is also used in specialized applications.

### <span style="color:rgb(161, 40, 226)">Piezoelectric polymers<br></span>
Interestingly, there are also **piezoelectric polymers**, which are neither natural crystals nor ceramics. These materials are:

- Flexible
- Very thin (film-like)
- Lightweight
    
A well-known example is **polyvinylidene fluoride (PVDF)**.

Like ceramics, piezoelectric polymers **require poling** to become piezoelectric. They are not intrinsically piezoelectric at birth; instead, they are made piezoelectric by heating them close to their Curie temperature and applying a strong electric field in the desired polarization direction.

PVDF is particularly attractive for applications where rigid materials cannot be used. For example, it is well suited for **pressure sensing between the foot and the shoe**, where a thin, flexible sensor can be inserted without altering the natural movement. This would not be feasible with rigid materials such as quartz or langasite.
## <span style="color:rgb(239, 179, 1)">Commonly used piezoelectric materials properties</span>
![[Pasted image 20251016172512.png]]
**Interpretation of material properties**

The values shown in this table refer to the characteristics of some of the piezoelectric materials introduced earlier. From the table alone, it is possible to immediately distinguish **natural crystals** from **ceramics and polymers**, even without prior knowledge of the materials.

The key observation is that **not all materials have a Curie temperature listed**.  
The Curie temperature is only relevant for materials that must be **poled** in order to become piezoelectric. Natural crystals **do not require poling**, so a Curie temperature is either not defined or not meaningful for them. For this reason, materials **1, 2, and 3** in the table can be identified as **natural piezoelectric crystals**.

**Density and mechanical properties**

The **density** values are all within a similar range for most materials.  
The **Young’s modulus** varies from one material to another, but remains within a reasonable and expected range; no material shows extremely anomalous mechanical stiffness compared to the others.

**Dielectric constant (relative permittivity)**

One of the most interesting parameters in the table is the **dielectric constant**, also known as **relative permittivity**. Piezoelectric ceramics—especially **lead zirconate titanate (PZT)** and related lead-based ceramics—exhibit a **very high dielectric constant**.

A high dielectric constant means that, if the material is placed between the plates of a capacitor, the resulting **capacitance will be very large**. This happens because the material develops strong internal electric dipoles that partially counteract the applied electric field between the capacitor plates.

We focus on capacitance because, when modeling piezoelectric sensors in electrical circuits, the sensor is often represented as a **charge source in parallel with a capacitor**. As a result, materials with very high dielectric constants—such as PZT—lead to **capacitance values that can be hundreds or even thousands of times larger** than those of materials like quartz. This strongly affects the electrical behavior and frequency response of the sensor.

**Electromechanical coupling factor**

Another important parameter is the **electromechanical coupling factor**, which measures how efficiently energy is converted between the electrical and mechanical domains.

This parameter is especially relevant for **ultrasound applications**, where the same piezoelectric element acts both as:

- an **actuator**, generating acoustic waves, and
- a **sensor**, receiving reflected waves.
    
A high coupling factor indicates good reversibility and efficiency in both operating modes.

**Curie temperature of polymers**

Finally, it is worth noting that the **Curie temperature of the polymer PVDF is relatively low**. This is expected, since polymers soften and melt at much lower temperatures than ceramics or crystals. This low Curie temperature limits the operating and processing temperature range of PVDF-based piezoelectric sensors.

![[Pasted image 20251016173258.png]]

In this table, for each of the four materials, three rows are reported. These rows indicate:

- the **type of material**,
- the **manufacturing or deposition technology** (which is not particularly relevant for our purposes),
- and the parameter labeled **d₃₃**.
    
**Meaning of the d₃₃ coefficient**

The **d₃₃ coefficient** represents the **piezoelectric sensitivity** of the material when a **compressive force is applied along a specific direction**, which will be defined later.

More precisely, d₃₃ expresses how much **electric charge is generated per unit of applied force** along the polarization axis. Its unit is **coulombs per newton (C/N)**, typically reported in **picocoulombs per newton (pC/N)**.

**Examples of d₃₃ values**

- **Quartz**  
    Quartz is a natural piezoelectric material obtained from a **bulk single crystal**, which must be properly cut along specific crystallographic directions.  
    Its d₃₃ value is approximately **2.33 pC/N**.  
    This means that applying a force of **1 N** produces only about **2.33 picocoulombs** of charge.
    
- **PZT (lead zirconate titanate)**  
    PZT is one of the most widely used piezoelectric ceramics.  
    Its d₃₃ coefficient is around **110 pC/N**, which is **about 50 times higher** than that of quartz.  
    This high sensitivity explains why PZT is preferred in many sensing and actuation applications.
    
- **Piezoelectric polymer (e.g., PVDF)**  
    The polymer shows a much lower sensitivity, with a d₃₃ value of about **1.6 pC/N**, even lower than quartz.
    

**Key takeaway**

The d₃₃ coefficient directly determines how much electrical charge a piezoelectric sensor produces for a given applied force. Materials such as **PZT**, with high d₃₃ values, are therefore much more suitable for applications requiring **high sensitivity**, while materials like quartz or polymers are used when other properties (stability, flexibility, frequency behavior) are more important.

## <span style="color:rgb(239, 179, 1)">Definition of piezoelectric coefficients and directions </span>

![[Pasted image 20251016173441.png]]

### <span style="color:rgb(161, 40, 226)">Why is the sensitivity constant called <b>d₃₃</b>?</span>

The sensitivity constant is called **d₃₃** because it refers to the **reference coordinate system used for piezoelectric materials**.

Instead of the usual **X, Y, Z** axes, piezoelectric materials use a **numbered coordinate system**:

- **Axes 1, 2, and 3** correspond to the three **principal directions** of the material (analogous to X, Y, and Z).
- **Indices 4, 5, and 6** represent **shear components**, which are associated with **moments (or shear stresses)** around axes 1, 2, and 3, respectively.
    
This notation comes from the concept of **generalized forces**, meaning that:

- **1, 2, 3** describe **normal forces (or normal stresses)**,
- **4, 5, 6** describe **shear forces or moments**.

### <span style="color:rgb(161, 40, 226)">Meaning of the index “33”</span>

The coefficient **d₃₃** specifically means:
- The **mechanical stimulus** (force or stress) is applied along **axis 3**, and
- The **electrical response** (charge or electric field) is measured along **the same axis 3**.
    
In other words, **both excitation and response are aligned with the polarization (poling) direction** of the piezoelectric material.
### <span style="color:rgb(161, 40, 226)">Relevance for sensors and actuators</span>

![[Pasted image 20251016173627.png]]
This notation is important not only for **sensor applications**, but also for **actuator applications**.

When working with actuators, you must carefully consider:

- The **direction of the poling field**, and
- The **direction in which you expect mechanical deformation (strain)**.
    

These directions do not always coincide and depend on:

- The **material properties**, and
- Which **piezoelectric coefficient** (d₃₃, d₃₁, d₁₅, etc.) is being used.
    
### <span style="color:rgb(161, 40, 226)">Validity of the piezoelectric coefficients</span>

An important point to highlight is that coefficients such as **d₃₃** (more generally **dᵢⱼ**) describe the material behavior **only for small deformations**.

This means:

- The piezoelectric response is assumed to be **linear**.
- These coefficients **must not be used** to predict large or macroscopic displacements.
- Piezoelectric materials are therefore suitable for **precise, small-scale actuation and sensing**, not for large movements.
    
### <span style="color:rgb(161, 40, 226)">Key takeaway<br></span>
- **d₃₃** identifies the coupling between mechanical and electrical effects **along axis 3**.
- Indices **1–3** represent normal directions, while **4–6** represent shear components.
- Piezoelectric coefficients are **material properties valid in the small-signal (linear) regime**.


![[Pasted image 20251016173737.png]]

In practice, **only two piezoelectric modes are commonly used** for poling and sensing:

#### **1. 3–3 mode**
![[Pasted image 20260104164002.png|200]]
- The material is **poled along direction 3**.
- The **mechanical force (or stress)** is applied **along the same direction (3)**.
- The electrical response (charge or voltage) is also measured along direction 3.
    

This is the **most intuitive and widely used mode**, where:

- You **compress or stretch the ceramic in the same direction as the poling**.
- It provides **high sensitivity**, making it suitable for force and pressure sensors.
    

#### **2. 3–1 mode**
![[Pasted image 20260104164022.png|200]]
- The material is **poled along direction 3**.
- The **mechanical force (or strain)** is applied along an **orthogonal direction (direction 1)**.
- The electrical response is still measured along direction 3.
    
In this case:

- You **pull or stretch the sample perpendicular to the poling direction**.
- This mode is often used in **bending sensors and actuators**, where lateral strain is easier to generate than direct compression.
    
### <span style="color:rgb(161, 40, 226)">Key takeaway</span>

- **3–3 mode**: force and poling are **aligned** → maximum sensitivity.
- **3–1 mode**: force is **perpendicular** to poling → useful for bending and structural applications.
- These two modes cover **most real-world piezoelectric sensor and actuator designs**.
    

## <span style="color:rgb(239, 179, 1)">Constitutive equations of piezoelectric materials</span>

### <span style="color:rgb(161, 40, 226)">1. Piezoelectric sensor behavior (direct effect)</span>
![[Pasted image 20251016174039.png|500]]
The first equation describes how a **mechanical stress** applied to a piezoelectric sensor generates an **electrical polarization**:

- **Input:**  
    A **stress vector** ( $\mathbf{T}$ ) (forces per unit area, in N/m²), applied by compression or tension.
    
- **Transformation:**  
    The stress is converted into electrical polarization through the **piezoelectric coefficient matrix** ( $\mathbf{d}$ ).  
    Typical coefficients are:
    - ( $d_{33}$ ): stress and polarization along the same axis
    - ( $d_{31}$ ): stress perpendicular to the poling direction
- **Output:**  
    The **electrical polarization vector** ( $\mathbf{D}$ ), expressed as charge density (C/m²), along the x, y, and z directions.
    
Mathematically, this relation can be written as:

- Electrical polarization = piezoelectric effect (stress → charge)
- Plus a second term that depends on the **external electric field**, multiplied by the **dielectric permittivity** ( \varepsilon )
    
If **no external electric field is applied**, this second term can be neglected.

📌 **Key point:**  
This equation models the **sensor mode**: mechanical input → electrical output.

### <span style="color:rgb(161, 40, 226)">2. Piezoelectric actuator behavior (inverse effect)</span>
![[Pasted image 20260104164309.png|500]]
Piezoelectric materials are **reversible**, so they can also work as actuators.

In this case:
- **Input:** an **electric field vector** ( $\mathbf{E}$ )
- **Output:** a **strain vector** (mechanical deformation)
    

The strain is given by:

- A **mechanical term** (stress multiplied by the compliance matrix)
- Plus a **piezoelectric term**, where the electric field is converted into strain via the same piezoelectric coefficients
    

📌 **Important:**
- The **same coefficients** are used for sensing and actuation
- The only difference is that the piezoelectric matrix is **transposed**
- These equations are valid **only for small deformations**

### <span style="color:rgb(161, 40, 226)">3. Structure of the piezoelectric matrices</span>
![[Pasted image 20251016174518.png|500]]
For real materials such as:

- PZT (lead zirconate titanate)
- Barium titanate
- Hexagonal crystal systems
    
the piezoelectric matrices are **sparse**, meaning:
- Only a **few coupling terms are non-zero**
- Not all stress directions produce polarization in all directions
    
For example:

- The ( $\mathbf{d}$ ) matrix often contains only **5 independent coefficients**
    
This simplifies both **modeling** and **practical sensor design**.

### <span style="color:rgb(161, 40, 226)">4. Standards and a historical anecdote (just for context)</span>

These matrix definitions follow **ANSI / IEEE standards**, similar to ISO standards.

A fun historical note:

- Oliver Smoot, former president of ANSI and ISO, was once used by his MIT classmates as a **unit of length** (“the Smoot”) to measure the Harvard Bridge.
- One Smoot ≈ **1.7 meters**
- Ironically, someone once used as a “measurement standard” later became head of an international **standardization organization**.


![[Pasted image 20251016174916.png]]

This is a **quartz crystal**, a bulk single crystal of quartz. By cutting the crystal in different orientations, it is possible to obtain **different sensitivities** from the same material.

You can see four different **cuts** (not _cats_, but _cuts_ 😄). Each cut determines how the crystal responds to mechanical stress.

- The first one is the **compression cut**.  
    It has the shape of a disk, essentially a hollow disk. When this disk is **compressed or stretched**, it produces the **maximum electrical charge output**. This cut is therefore mainly sensitive to **normal forces**.
    
- Another configuration is the **shear cut**.  
    In this case, the generated electrical charge (or voltage) is proportional to the **shear stress** applied to the disk, rather than to compression. This type of cut is useful when you want to measure **shear forces**.
    
- There are also other types of cuts, each designed to be sensitive to different stress components.
    
**Key point:**  
The way the quartz crystal is cut determines the **type of mechanical quantity** the sensor is sensitive to:

- compression or tension,    
- shear stress,
- or stresses related to **moments**.
    
Therefore, choosing the correct crystal cut is essential to design a piezoelectric sensor suited for the intended application.

## <span style="color:rgb(239, 179, 1)">Actual Operation of Piezoelectric Materials</span>

![[Pasted image 20251016180617.png]]
Now that we have introduced **piezoelectric sensors**, let us see how they are **interfaced with electronics** in order to read information proportional to the applied **strain or stress**.

Consider a **piezoelectric sensor mounted as a cantilever beam**, fixed on one side to a support. When strain is applied to the beam, a **charge appears on the two opposite faces** of the piezoelectric material.

If we imagine the sensor as a beam with a **rectangular cross-section**:
- the **upper surface** experiences one type of charge,
- the **lower surface** experiences the opposite charge.
    
This charge imbalance produces a **voltage across the material**.
### <span style="color:rgb(161, 40, 226)">Metallization and capacitor model</span>

To measure this voltage, the two surfaces where charges appear must be **metallized**:

- a conductive layer is deposited on the upper surface,
- another conductive layer is deposited on the lower surface.
    
By doing this, each surface becomes **isopotential**, and the structure effectively becomes a **capacitor**:

- upper metallized surface → first plate,
- piezoelectric material → dielectric,
- lower metallized surface → second plate.
    
Because of this, the piezoelectric sensor can be **modeled electrically as a capacitor**.

### <span style="color:rgb(161, 40, 226)">Effect of capacitance</span>

The voltage generated by the sensor depends on its **capacitance**:

- for a given amount of charge, **higher capacitance means lower voltage**.
    
In materials like **PZT**, the relative permittivity is very high (around 1500), which:

- greatly increases the capacitance,
- significantly reduces the output voltage for the same generated charge.
    
### <span style="color:rgb(161, 40, 226)">Charge leakage and time behavior<br></span>
However, this voltage is **not permanent**.

Charges tend to redistribute and neutralize over time. An analogy is static electricity:

- on a very **dry day**, charge imbalance can persist and cause sparks,
- on a **humid day**, charges quickly leak away through the environment.
    

The same happens in piezoelectric sensors:

- the dielectric is **never perfect**,
- a very small leakage current always exists,
- over time, the generated charge **slowly discharges**.
    
As a result, even if the sensor is kept under constant strain, the output voltage will eventually go to **zero**.

### <span style="color:rgb(161, 40, 226)">Consequence for measurements</span>

This leads to a crucial conclusion:

- **Piezoelectric sensors are not suitable for DC measurements**.
    
For example:

- if a person stands on a piezoelectric sensor platform and remains still for a long time,
- after some time, the measured signal will return to zero,
- not because the applied force has changed, but because the charge has leaked away.
    

In contrast:

- **load cells** (resistive sensors) can measure static loads indefinitely,
- piezoelectric sensors can only measure **dynamic or time-varying forces**.
    
**Key takeaway:**  
Piezoelectric sensors are excellent for **dynamic measurements** (vibrations, impacts, acoustic waves), but they **cannot measure static or DC forces**.

## <span style="color:rgb(239, 179, 1)">Electric Model</span>

![[Pasted image 20251016180914.png]]

This is the **electrical model of a piezoelectric sensor**, shown using one of the commonly adopted schematic symbols. Other equivalent symbols exist; for example, instead of the cross, a small square may be drawn between the two plates.

The model consists of:

- a **charge generator** $Q_p$​, representing the charge produced by the applied mechanical stress,
- a **capacitor** $C_p$, corresponding to the capacitance between the two metallized surfaces of the piezoelectric element,
- a **resistor** $R_p$​, with a very large resistance, accounting for the non-ideal dielectric behavior of the material.

Because the dielectric is not perfect, a small leakage current exists, which is modeled by this high-value resistor.

The generated charge $Q_p$​ produces a voltage $V_p$​ across the capacitor $C_p$​, which is the **output voltage of the piezoelectric sensor**.

![[Pasted image 20251016181316.png]]

Now we are going to see **how to extract useful information from the charge generator**. Before doing that, however, we need to understand **what voltage levels we should expect** at the output of a piezoelectric sensor.

These voltages can vary widely. In some applications, such as the **pickup of an acoustic guitar**, the generated signal is only **a few millivolts**. In other cases, the voltage can be much higher—**up to hundreds of volts**.

A familiar example is a **piezoelectric lighter**. Inside the lighter, a small mechanical hammer strikes a piezoelectric element. In order to generate a spark, the piezoelectric material must produce an electric field of at least **about 100 V/mm**, which results in output voltages on the order of **100 volts**.

Of course, in measurement applications we do not use lighters. Instead, we work with **much smaller piezoelectric devices**, whose output voltages are typically in the **millivolt range**, and sometimes up to a few volts, but generally not higher than that.

![[Pasted image 20251016181420.png]]
If we solve the circuit we saw before, it is more convenient to work **in terms of current instead of charge**, since current is the time derivative of charge:
$$I(t) = \dfrac{dq(t)}{dt}$$
The generated charge is proportional to the applied force:
$$q(t) = k,F(t)$$
where:
- ( $k$) is the selected **piezoelectric coefficient** (for example ( $d_{33}$ )),
- ( $F(t)$ ) is the applied force.
    
Taking the derivative:
$$I(t) = k,\dfrac{dF(t)}{dt}$$
Alternatively, instead of force, we can use **pressure**, introducing a proportionality constant ( $\gamma$ ).

### <span style="color:rgb(161, 40, 226)">Circuit solution and transfer function<br></span>
In the equivalent circuit:

- The current ( $I$ ) splits into:
    - the current through the capacitor ( $C_p$ ),
    - the current through the resistor ( $R_p$ ).

By solving the circuit and moving to the **Laplace domain**, we can derive the relationship between the output voltage ( $V(s)$ ) and the input force ( $F(s)$ ).

Defining:$$\tau = R_p C_p$$
the transfer function becomes:

![[Pasted image 20260104172015.png|300]]

- A **zero at the origin** ($( s = 0 )$),
- A **pole at** ( $s = \dfrac{1}{\tau}$ ),
- A gain proportional to ( $\dfrac{k}{C_p}$ ).
    
This behavior is expected because:

- The output voltage increases with the piezoelectric coefficient ( $k$ ),
- The voltage decreases as the capacitance ( $C_p$ ) increases (since ( $V = Q / C$ )).
### <span style="color:rgb(161, 40, 226)">Frequency response interpretation</span>
![[Pasted image 20260104172102.png]]
- The system behaves as an **electrical high-pass filter**.
- At low frequencies:
    - The magnitude increases at **+20 dB/decade**, starting from zero frequency.
        
- The cutoff frequency is:

$$f_c = \dfrac{1}{2\pi \tau} = \dfrac{1}{2\pi R_p C_p}  $$
- Because ( $R_p$ ) is extremely large, ( $\tau$ ) is very large:
    - The cutoff frequency ( $f_c$ ) is therefore **very low**.
        
- In the passband:
    - The gain is approximately ( $\dfrac{k}{C_p}$ ).

This explains **why piezoelectric sensors cannot measure DC or very low-frequency signals**, and why their output is proportional to the **time variation of the applied force**, not to its static value.

### <span style="color:rgb(161, 40, 226)">Behavior at high frequencies</span>
![[Pasted image 20251016181746.png]]
What happens at **high frequencies**?

From a **purely electrical point of view**, at high frequency the gain remains approximately constant and equal to:
$$\frac{k}{C_p}  $$
However, in the **real world**, this is no longer true because **mechanical effects** become dominant. At high frequencies, the piezoelectric sensor exhibits **resonance and anti-resonance phenomena** that are due to its **mechanical properties**, not its electrical ones.
#### <span style="color:rgb(2, 141, 192)">High-frequency equivalent model</span>

At high frequency, the piezoelectric sensor can be modeled using a more complex equivalent circuit:

- A **series R–L–C branch**, which represents the **mechanical behavior** of the sensor:
    - The inductance models the equivalent mass,
    - The capacitance models the mechanical stiffness,
    - The resistance models mechanical losses.
        
- A **parallel capacitor**, which mainly represents:
    - the intrinsic capacitance of the piezoelectric material,
    - the capacitance of the leads and wiring connected to the transducer.
        
The resistance in the series branch is very small, which means that the system has a **high quality factor (Q factor)**. As a consequence:

- The resonance peak is **very high**,    
- The resonance bandwidth is **very narrow**.
#### <span style="color:rgb(2, 141, 192)">Consequences for sensor behavior</span>

Because of this, piezoelectric sensors are limited in frequency in two different ways:

- **At low frequencies**:  
    They are limited by **electrical effects** (charge leakage through the internal resistance).
- **At high frequencies**:  
    They are limited by **mechanical resonance effects**.
    
In practice, this distinction is not always so clear-cut, because piezoelectric sensors are usually mounted on real mechanical structures. Very often, the **resonances of the structure itself** dominate the high-frequency behavior rather than the intrinsic resonance of the sensor.

Nevertheless, if structural resonances are not dominant, the sensor’s own mechanical resonance determines the upper frequency limit.

#### <span style="color:rgb(2, 141, 192)">Use in oscillators and frequency stabilization</span>

Because piezoelectric crystals exhibit:
- very sharp resonance and anti-resonance peaks,
- extremely stable resonance frequencies,

they are widely used to **stabilize electronic oscillators**.

Generating a precise and stable clock using only discrete electronic components is difficult. Instead, a piezoelectric crystal is inserted into the oscillator circuit. The oscillator naturally locks onto one of the crystal’s mechanical resonance frequencies.

In this case:

- Electrical energy is converted into mechanical vibration,
- The mechanical vibration is converted back into an electrical signal,
- The result is a **highly stable oscillation frequency**.
    

This is why piezoelectric crystals are commonly used as **time references and clock sources** in electronic devices.

## <span style="color:rgb(239, 179, 1)">Requirements for a piezoelectric sensor system</span>
![[Pasted image 20251016182216.png]]

When designing or selecting a piezoelectric sensor and its readout electronics, several key requirements must be considered.
### <span style="color:rgb(161, 40, 226)">1. Bandwidth and frequency of operation</span>

First of all, we must define the **bandwidth** of interest, that is, the frequency range in which the sensor is expected to operate.

This bandwidth depends strongly on the **material** used for the piezoelectric element. Different materials have different dielectric constants, which directly affect the value of the internal capacitance of the sensor. Since the low-frequency behavior of the sensor is determined by the RC time constant:
$$\tau = R_p \cdot C_p$$
changing the capacitance also changes the **low-frequency pole**. As a result, the usable frequency range of the sensor is material-dependent.
### <span style="color:rgb(161, 40, 226)">2. Signal amplitude</span>

Another important requirement is the **expected signal amplitude**. This depends on:

- the piezoelectric coefficient of the material,
- the geometry of the sensor,
- and the magnitude of the applied force, pressure, or strain.

Some materials generate only a few picocoulombs per newton, while others generate much larger charges. This directly affects the output voltage and the requirements of the amplification stage.
### <span style="color:rgb(161, 40, 226)">3. Input impedance of the readout electronics</span>

The **input impedance of the amplifier** is a critical parameter.

In general, high input impedance is desirable, but in the case of piezoelectric sensors it is **absolutely essential**. The reason is that the sensor is electrically modeled as a **capacitor in parallel with a very large resistance** (R_p), often on the order of gigaohms or even teraohms.

If the amplifier input impedance is low, it will appear in parallel with ($R_p$). For example:
- if ($R_p$) is on the order of thousands of megaohms,
- and the amplifier input impedance is only 100 ohms,
    
then the effective resistance seen by the sensor becomes approximately 100 ohms. This dramatically reduces the time constant (\tau), pushing the low-frequency pole toward much higher frequencies and severely degrading the sensor’s low-frequency response.

Therefore, a **very high input impedance amplifier** is mandatory to preserve the sensor’s intrinsic behavior.

### <span style="color:rgb(161, 40, 226)">4. Modes of operation: voltage vs charge amplification</span>

There are two main ways to interface a piezoelectric sensor with electronics:

1. **Voltage amplifier mode**
2. **Charge amplifier mode**
    
As the names suggest:

- a voltage amplifier directly amplifies the voltage across the sensor,
- a charge amplifier converts the generated charge into a voltage using a feedback capacitor.
    
In many practical applications, especially when dealing with long cables, varying capacitances, or low-frequency signals, the **charge amplifier** offers better performance and stability than the voltage amplifier.
### <span style="color:rgb(161, 40, 226)">5. Amplifier choice</span>

Both approaches typically rely on an **operational amplifier with extremely high input impedance**, so that the sensor is not loaded. An example of such an amplifier is the **LV2771**, which is specifically designed for low input bias currents and high input impedance, making it suitable for piezoelectric sensor applications.


## <span style="color:rgb(239, 179, 1)">Voltage amplifier configuration for a piezoelectric sensor</span>

This is the **first interface configuration**, known as the **voltage amplifier**.

It is called a voltage amplifier because the circuit directly amplifies the **voltage developed across the piezoelectric sensor**.
### <span style="color:rgb(161, 40, 226)">Electrical model and connections</span>
![[Pasted image 20260104173057.png]]
The piezoelectric sensor is modeled as:

- a **charge generator**,
- a **capacitance ($C_p$)**, representing the intrinsic capacitance of the piezoelectric material,
- a **large resistance ($R_p$)**, representing dielectric leakage.
    

The sensor is connected to the amplifier through cables. These cables introduce an additional **parasitic capacitance ($C_c$)**, which appears in parallel with the sensor capacitance.

The signal is then applied to the **non-inverting input** of an operational amplifier. On the amplifier side:

- ($R_f$) and ($R_g$) form the feedback network that sets the gain,
- a capacitor in parallel with ($R_f$) is used to limit the **upper cutoff frequency** and improve stability.
    
### <span style="color:rgb(161, 40, 226)">Low-frequency behavior</span>

At low frequencies, the circuit behaves as a **non-inverting amplifier**, with a voltage gain given by:
$$A_v = 1 + \frac{R_f}{R_g}$$  
The **input impedance** of the amplifier is mainly determined by the resistor ($R_b$).

Why is ($R_b$) needed?
The leakage resistance ($R_p$) of the piezoelectric sensor is extremely large and cannot reliably provide a return path for the **input bias current** of the operational amplifier. Therefore, a resistor ($R_b$) is added to provide a controlled bias path, similar in purpose to the reference electrode used in electrophysiological signal measurements.

### <span style="color:rgb(161, 40, 226)">Sensitivity to capacitance variations</span>

In this configuration, the input voltage depends on the **generated charge divided by the total capacitance** seen by the sensor:

$$C_{\text{total}} = C_p + C_c  $$
This means that the output voltage is not only proportional to the applied force, but also inversely proportional to the **sum of the sensor capacitance and the cable capacitance**.

As a consequence, this configuration assumes that both ($C_p$) and ($C_c$) are **constant over time**.

In practice, this can be problematic:

- long cables have significant capacitance,
- cable capacitance can change if the cables are moved or bent.
    
If the cable capacitance changes, the effective gain of the system changes as well. For example, a force that today produces a reading of 1 kg might produce 1.01 kg tomorrow simply because the cable position has changed. This makes the measurement **unstable and poorly repeatable**.

### <span style="color:rgb(161, 40, 226)">Practical implications<br></span>
Because of this sensitivity to parasitic capacitance, the voltage amplifier configuration is suitable **only when**:

- the cables are very short,
- the cable geometry is mechanically stable,
- and high measurement accuracy over time is not critical.

For more demanding applications, especially when long or flexible cables are required, this configuration is generally not recommended.
### <span style="color:rgb(161, 40, 226)">Frequency-domain behavior of the voltage amplifier</span>
![[Pasted image 20251016183319.png]]
This is the operational amplifier chosen as an example. As shown in the datasheet, the **differential input impedance** is on the order of  
$$10^{12}\ \Omega,  $$
which is extremely high and therefore well suited for interfacing with piezoelectric sensors.

### <span style="color:rgb(161, 40, 226)">Transfer function in the frequency domain</span>

Let us now analyze the behavior of the circuit in the **frequency domain**, starting from the transfer function derived previously.

1. **Zero at the origin**

As already discussed, the transfer function contains a **zero at the origin**. This is expected and reflects the fact that piezoelectric sensors cannot measure DC signals.

2. **Low-frequency pole**

The first pole appears at low frequency and is determined by:

- the parallel combination of the leakage resistance of the sensor and the bias resistor:  
$$R_{\text{eq}} = R_p \parallel R_b \approx R_b  $$
    (since ($R_p$) is extremely large),
- and the total capacitance seen at the input:  
$$C_{\text{eq}} = C_p + C_c  $$

This pole defines the **low-frequency cutoff** of the system.

3. **High-frequency pole**
    
At high frequencies, the circuit behaves as a **low-pass filter**. This introduces a second pole, determined by the feedback components:
- the feedback resistor ($R_f$),
- the feedback capacitor ($C_f$).
    
This pole limits the **upper bandwidth** of the amplifier and is mainly introduced for stability and noise reduction.
### <span style="color:rgb(161, 40, 226)">High-frequency gain behavior</span>

At very high frequencies, the impedance of the feedback capacitor (C_f) becomes very small, effectively short-circuiting (R_f). As a result, the feedback ratio tends to zero, and the gain approaches:

$$A_v \rightarrow 1 + 0 = 1  $$
Therefore, the gain of this amplifier configuration **never drops below unity**.

### <span style="color:rgb(161, 40, 226)">Overall frequency response</span>
![[Pasted image 20251016183613.png]]
In summary, the frequency response of the voltage amplifier:

- starts from zero gain at DC (due to the zero at the origin),
- increases with frequency,
- reaches a flat mid-band region,
- and finally rolls off at high frequency due to the feedback low-pass filter.
    
This behavior is consistent with a **band-pass response**, bounded at low frequency by the sensor’s electrical properties and at high frequency by the amplifier design.


## <span style="color:rgb(239, 179, 1)">Charge amplifier configuration for a piezoelectric sensor</span>

This is the **second possible interface circuit**, known as the **charge amplifier**.

In this configuration, the piezoelectric sensor is again modeled by its charge generator, intrinsic capacitance ($C_p$), and leakage resistance. The cable capacitance ($C_c$) is also present, but—as we will see—its effect on the measurement is fundamentally different from the voltage amplifier case.

![[Pasted image 20251016183933.png]]
### <span style="color:rgb(161, 40, 226)">Circuit operation principle</span>

The sensor signal is connected to the **inverting input** of the operational amplifier.

The key idea behind the charge amplifier is the behavior of an operational amplifier in **closed-loop operation**:  
the amplifier forces the voltages at its inverting and non-inverting inputs to be equal (virtual short).

Since the non-inverting input is typically connected to ground, the inverting input is held at **virtual ground**.

### <span style="color:rgb(161, 40, 226)">Charge conservation and signal conversion</span>

If we momentarily imagine that the series resistor ($R_i$) were replaced by a short circuit, then:
- the voltage at the inverting input would remain at 0 V,
- there would be **zero voltage across the sensor capacitance and cable capacitance**.
    
As a result, **all the charge generated by the piezoelectric sensor must flow into the feedback capacitor ($C_f$)** in order to keep the inverting input at virtual ground.

Therefore, the output voltage depends **only on the charge accumulated on ($C_f$)**:

$V_{\text{out}} = \frac{Q}{C_f}$

This is the key advantage of the charge amplifier:  
the measurement depends on ($C_f$), **not on ($C_p$) or ($C_c$)**.

### <span style="color:rgb(161, 40, 226)">Role of the series resistor (Ri)<br></span>
In practice, the resistor ($R_i$) is required and cannot be removed.

Its main purposes are:

1. **Electrostatic discharge (ESD) protection**  
    The sensor and cables form a very high-impedance system, similar to the situation of a charged human body or a car. When connecting the sensor, it is possible to have tens or even hundreds of volts stored on it.  
    Without (R_i), this voltage could cause a very large current and permanently damage the amplifier input.
    
2. **Controlled current limiting**  
    The resistor ensures that any sudden voltage results in a limited and safe current.
    
### <span style="color:rgb(161, 40, 226)">Frequency-domain behavior</span>

In the frequency domain, the charge amplifier exhibits:

1. **A zero at the origin**  
    As with all piezoelectric sensors, DC signals cannot be measured.
2. **A low-frequency pole**, determined by:  
$$    R_i \cdot C_f $$
3. **A high-frequency pole**, determined by:  
$$    R_i \cdot (C_p + C_c)  $$
### <span style="color:rgb(161, 40, 226)">Gain of the charge amplifier</span>

The mid-band gain of the charge amplifier is:
$$A = \frac{1}{C_f}  $$
This means that the sensitivity of the system is set **only by the feedback capacitor (C_f)**, making the circuit highly stable and repeatable, even in the presence of long or moving cables.

### <span style="color:rgb(161, 40, 226)">Key advantage over the voltage amplifier</span>

Unlike the voltage amplifier configuration, the charge amplifier:
- is **insensitive to cable capacitance variations**,
- provides **stable calibration over time**,
- is therefore the preferred solution for most practical piezoelectric sensor applications.
    

# <span style="color:rgb(223, 109, 109)">Dynamometric platforms: classical applications of force sensors</span>

Today we introduce a **classical application of load cells and piezoelectric sensors**:  
the **dynamometric platform**.

Dynamometric platforms are widely used to measure forces exerted on the ground by:

- human subjects,
- patients in clinical analysis,
- athletes during sports activities,
- and, in general, any object interacting with the floor.
## <span style="color:rgb(239, 179, 1)">What is a dynamometric platform?</span>

A **dynamometric platform** is a rigid plate—usually metallic—inside which **multiple force sensors** are embedded.

The platform is typically installed flush with the floor and is designed to measure the **action forces** exchanged between the body and the ground, commonly referred to as **ground reaction forces**.

### <span style="color:rgb(161, 40, 226)">Measurement of three-dimensional forces</span>
![[Pasted image 20260104184102.png|300]]
The sensors are placed at specific locations, usually near the **edges or corners** of the plate.  
By combining the signals from these sensors, the platform can measure the three components of the force vector:

- ($F_x$): force along the anterior–posterior direction,
- ($F_y$): force along the medial–lateral direction,
- ($F_z$): force along the vertical direction.
    
Together, these components define a **three-dimensional ground reaction force vector**.
### <span style="color:rgb(161, 40, 226)">Center of pressure (CoP)</span>
![[Pasted image 20260104184135.png|300]]
Through appropriate signal processing, it is also possible to determine the point at which the **resultant force vector intersects the surface of the platform**.  
This point is known as the **Center of Pressure (CoP)**.

It is important to clarify a common misunderstanding:
- The platform does **not directly measure** the center of pressure.
- What the platform actually measures are **forces and moments**.
- The CoP is then **computed** from these measurements using mechanical relationships.
### <span style="color:rgb(161, 40, 226)">Interpretation of the force vector</span>

The ground reaction force defines a **line of action** in space.  Any point along this line is mechanically equivalent as a point of application of the force.

For convenience and standardization, this line of action is typically represented as intersecting the **top surface of the platform**, and that intersection point is defined as the center of pressure.

### <span style="color:rgb(161, 40, 226)">Why dynamometric platforms are useful</span>

By tracking:

- the magnitude and direction of ground reaction forces,
- and the movement of the center of pressure over time,
    
it is possible to analyze:
- walking and running patterns,
- balance and postural control,
- jumping and landing mechanics,
- pathological gait behaviors.
    
These measurements are fundamental in **biomechanics**, **clinical assessment**, and **sports science**.


## <span style="color:rgb(239, 179, 1)">From ground reaction forces to body accelerations</span>

![[Pasted image 20251016184933.png]]
By measuring the **ground reaction forces**, it is possible to compute the **accelerations of the body** along horizontal and vertical directions. Consider the point of contact between the body and the external world (the dynamometric platform).  

If the components of the reaction force acting on the platform are known, these forces can be decomposed along the coordinate axes.

For simplicity, let us consider motion in the **sagittal plane**:
![[Pasted image 20260104185211.png|200]]
- No force components act along the axis perpendicular to the plane (out of the screen).    
- Only two force components are present:
    - ($F_y$): horizontal force,
    - ($F_z$): vertical force.
        
### <span style="color:rgb(161, 40, 226)">Application of Newton’s laws</span>

Using the **cardinal equations of mechanics** (Newton’s second law), the body accelerations can be computed:

- In the horizontal direction:  
    $$F_y = m , a_y $$
- In the vertical direction, gravity must also be considered:  
    $F_z - m g = m , a_z$

where:
- ($m$) is the body mass,
- ($g$) is the gravitational acceleration.
    
If a subject stands still on the platform (no acceleration in any direction), the platform still measures a **vertical force equal to body weight**, due entirely to gravity.
### <span style="color:rgb(161, 40, 226)">Importance of gravity in biomechanical analysis</span>
![[Pasted image 20260104185333.png|200]]
In early applications of force platforms, the gravitational term was sometimes neglected, especially when analyzing **distal (far from the medial line) body segments** with small masses. However, gravity generates a large force and **must always be taken into account**, particularly in vertical dynamics.
### <span style="color:rgb(161, 40, 226)">From external forces to internal joint mechanics</span>

Starting from the ground reaction forces and applying Newton’s laws, it is possible to:
1. Decompose the body into rigid segments,
2. Compute the **internal reaction forces** between adjacent segments at each joint,
3. Determine the **joint moments (torques)** responsible for those reactions.
    
These joint moments are extremely important because, through appropriate biomechanical models, they allow us to:

- estimate **muscle forces**,
- identify **abnormal joint loading**,
- analyze pathological gait or movement patterns.
    
This approach is used in activities such as walking, running, standing up from a chair, jumping, and many clinical and sports applications.

### <span style="color:rgb(161, 40, 226)">Physical construction of a dynamometric platform</span>
![[Pasted image 20251021124828.png]]
A force platform consists of at least **two rigid metal plates**:

1. **Base plate**
    - Fixed to the ground,
    - Must be perfectly rigid, grounded, and horizontal.
        
2. **Upper plate**
    - In contact with the subject,
    - Moves only by an extremely small amount (microstrains).
        
The small displacement requirement is crucial:  a compliant platform would behave like a soft surface, altering natural movement patterns and corrupting the measurement.
### <span style="color:rgb(161, 40, 226)">Role of sensor stiffness and bandwidth</span>

The platform stiffness is mainly determined by the sensors:

- **Piezoelectric sensors** have very high stiffness → extremely small displacements,
- **Load cells** can be designed with different stiffness values.
    
Sensor stiffness directly affects the **bandwidth** of the measurement.  
For a second-order mechanical system, the natural frequency (\omega_n) depends on stiffness and mass:

- Higher stiffness → higher natural frequency → wider bandwidth.
    
For this reason, **piezoelectric platforms generally have a larger bandwidth** than load-cell-based platforms.

### <span style="color:rgb(161, 40, 226)">Importance of alignment and leveling</span>

The base of the platform must be:
- perfectly horizontal,
- rigidly fixed to the ground.
    
If the platform is tilted, the gravitational acceleration is incorrectly decomposed into multiple components, introducing systematic measurement errors in horizontal and vertical forces.

### <span style="color:rgb(161, 40, 226)">Sensor configuration</span>

The upper plate is connected to the base through **force sensors**, which measure the pressure transmitted between the two plates.
Typical configurations include:

- **Four sensors** (hyperstatic configuration):
    - most common,
    - requires excellent flatness and alignment.
        
- **Three sensors** (isostatic configuration):
    - mechanically simpler,
    - less accurate near the edges, especially for center of pressure estimation.

### <span style="color:rgb(161, 40, 226)">Sensor embedding and mechanical isolation</span>

Piezoelectric sensors are usually housed inside **metal containers** embedded in the platform.

A small **gap** must exist between the upper and lower plates:

- to prevent unwanted force transmission,
- to avoid parasitic interactions between the platform and the floor.
    
Without this gap, measurements would include non-physical forces, corrupting the ground reaction force data.

## <span style="color:rgb(239, 179, 1)">Two possible implementations of dynamometric platforms</span>
![[Pasted image 20251021125023.png]]

There are two common structural implementations of dynamometric platforms.

### <span style="color:rgb(161, 40, 226)">1. Classical plate-based configuration</span>

The **classical configuration** consists of a rigid plate with **four sensors embedded at its edges**.
In this design:
- The upper plate is supported at its corners by the sensors.
- Each sensor measures the force transmitted at its location.
- By combining the signals from the four sensors, it is possible to compute:
    - the three components of the ground reaction force (($F_x, F_y, F_z$)),
    - the moments generated by these forces,
    - and, consequently, the **center of pressure**.

This configuration is mechanically simple and widely used in biomechanics and clinical applications.
### <span style="color:rgb(161, 40, 226)">2. Pillar-based configuration</span>
![[Pasted image 20260104185923.png|200]]
The second implementation is more mechanically complex.

In this design:
- The platform is mounted on a **single central pillar**.
- **Strain gauges** are placed on the pillar.
- The applied forces and moments cause the pillar to deform.
- By measuring this deformation, it is possible to **reconstruct the forces and moments** that generated it.

Although this configuration can provide accurate measurements, the force and moment reconstruction is more complex and requires careful calibration and modeling of the pillar’s mechanical behavior.
### <span style="color:rgb(161, 40, 226)">Comparison</span>

- The **plate-based configuration** is simpler and more intuitive to analyze.
- The **pillar-based configuration** requires more advanced mechanical modeling but can offer a compact and robust solution.
    

Both implementations are used in practice, depending on the required accuracy, bandwidth, and application constraints.

## <span style="color:rgb(239, 179, 1)">Example of specifications of a commercial piezoelectric force platform</span>
![[Pasted image 20251021125703.png]]

This slide shows an example of the specifications of a **commercial piezoelectric force platform**.
### <span style="color:rgb(161, 40, 226)">Reference frame and force directions</span>

The first important aspect to observe is the **reference frame**:
- The **X and Y axes** lie on the horizontal plane of the platform.
- The **Z axis** is perpendicular to the platform and points upward.

The measurable force ranges are different along these axes:
- **Horizontal forces**:  
    $$F_x, F_y \in [-2.5 \text{ kN}, +2.5 \text{ kN}] $$
- **Vertical force**:  
    $$F_z \in [0, 10 \text{ kN}]  $$
The reason for this difference is that, along the **vertical direction**, the platform must also measure the **gravitational force**, i.e., the weight of the subject.

If a person stands still on the platform, a force equal to their **body weight** is measured along the Z axis.  
In contrast, horizontal forces arise only from **inertial effects** due to body motion (e.g., walking, swaying, or jumping), and are therefore much smaller than the vertical force.
### <span style="color:rgb(161, 40, 226)">Measurement range and calibrated range</span>

Another important specification is the distinction between:

- the **maximum measurement range**, and
- the **calibrated range**.
    
The calibrated range is smaller than the maximum range and represents the region where the platform provides **high accuracy and low measurement error**.

Beyond this region:

- measurement errors increase,
- and eventually an **overload range** is reached.
    
Exceeding the overload range may cause **permanent damage** to the device.  
Therefore, these limits must be carefully considered during system design and experimental planning.

### <span style="color:rgb(161, 40, 226)">Accuracy-related specifications<br></span>
Key accuracy parameters include:

- **Linearity**: ±0.5% of full scale
- **Hysteresis**: ±0.5% of full scale
    
These values indicate how closely the measured force follows the ideal linear behavior and how much the output depends on the loading history.

### <span style="color:rgb(161, 40, 226)">Crosstalk</span>

**Crosstalk** refers to the fact that a force applied along one axis is not detected exclusively by the sensor corresponding to that axis.

For example:

- A purely vertical force (such as body weight) should ideally be measured only along the Z axis.
- In practice, small components of this force may also appear in the X and Y measurements.
    
This coupling between axes introduces an additional source of error that must be taken into account when designing and interpreting measurements.
### <span style="color:rgb(161, 40, 226)">Natural frequency and bandwidth</span>

The **natural frequency** of the platform determines its usable **bandwidth**.

For this piezoelectric platform:
- Horizontal directions: approximately **350 Hz**
- Vertical direction: approximately **200 Hz**

Thanks to the high stiffness of piezoelectric sensors, the bandwidth is relatively large compared to platforms based on strain-gauge load cells.
### <span style="color:rgb(161, 40, 226)">Practical considerations</span>

Finally, from a practical standpoint:
- The platform has a mass of approximately **17 kg**.
    
This is an important factor to consider when moving the device within the laboratory or installing it in experimental setups.
## <span style="color:rgb(239, 179, 1)">Butterfly Diagrams</span>

![[Pasted image 20251021130543.png]]

### <span style="color:rgb(161, 40, 226)">The butterfly (Pedotti) diagram of ground reaction forces</span>

This representation, which was very popular in the **1980s**, was developed to convey **more information within a single graph**.

The diagram is obtained by projecting the **ground reaction force vector** onto the **sagittal plane**, which is the plane of forward progression of the subject. For this reason, only **two axes** are shown:
- the **vertical axis**, and
- the **horizontal axis**, aligned with the direction of progression.
### <span style="color:rgb(161, 40, 226)">Construction of the diagram</span>

Each vector in the diagram represents a **sample of the ground reaction force**, built from:
- the **vertical component**, and
- the **horizontal (antero–posterior) component**.

For example, if the force platform is sampled at **100 Hz**, one vector is available every **10 ms**. Over one second, this produces a sequence of vectors.

These vectors appear **inclined and curved** because:
- the original force is **three-dimensional**,
- it is projected onto a **two-dimensional plane**,
- and its direction and magnitude change throughout the gait cycle.
### <span style="color:rgb(161, 40, 226)">Interpretation during walking</span>

If the **body weight** is drawn as a reference, several characteristic phases of walking become evident:

- An initial **braking phase**, in which the horizontal component of the vectors points opposite to the direction of progression, slowing the body down.
- A phase where **inertial effects** cause the vertical force to exceed body weight.
- A phase where the vertical force drops **below body weight**.
- A subsequent phase where the force again **exceeds body weight** during push-off.
These features allow the identification of **distinct gait patterns**.
### <span style="color:rgb(161, 40, 226)">Applications and historical context</span>

In the 1980s, this method was proposed as a tool for **biometric identification**.  
The idea was to recognize individuals entering banks based on their **butterfly diagram**, since this pattern is relatively **repeatable for the same person**.

Today, biometric recognition has shifted largely toward **facial recognition**, but at the time this approach was considered innovative.
***
***
***




