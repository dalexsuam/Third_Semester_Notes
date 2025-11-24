
23/10/2025
***
Hello everyone,  
today’s topic is **magnetic field sensors**, and in particular, we will study **two main types**: **Hall sensors** and **magnetoresistive sensors**.


# <span style="color:rgb(223, 109, 109)">Hall Sensors</span>

Let’s begin with the **Hall sensors**
![[Pasted image 20251021233314.png]]
Hall sensors are **simple and inexpensive** magnetic field sensors that typically have **three terminals**. Their operation is based on the **Hall effect**.
.
![[Pasted image 20251021233339.png]]

They consist of a **thin sheet of conductive or semiconductor material**. Inside this sheet, we **force a current** to flow in one direction, while we **measure a voltage** in the perpendicular direction. This voltage is **proportional to the strength of the magnetic field** applied.

However, the output voltage is usually **very small** — typically in the **microvolt range**. For this reason, most Hall sensors include an **integrated differential amplifier** directly on the same chip as the sensing element.

In some cases, a **comparator or trigger circuit** is also integrated. This allows the Hall sensor to be used as a **digital sensor** — working as an **on/off detector**. In that case:

- When the magnetic field exceeds a certain threshold, the output switches to **1**.
- When the field is below the threshold, the output stays at **0**.
## <span style="color:rgb(239, 179, 1)">Working Principle</span>

Now, let’s take a closer look at the **working principle** behind Hall sensors to better understand how they function.
 
![[Pasted image 20251021233418.png]]

Here we can see our **thin conductive sheet**.  We apply an **external voltage** $V_x$​ between two terminals of the material to **induce a current flow**. In this example, the current flows along the **x-direction**.

Now, if an **external magnetic field** $\mathbf{B}$ is applied **perpendicular** to the sheet, the **moving charge carriers** inside will experience a **Lorentz force**.  

$$F_L=q\cdot v_x \times B_z $$

The Lorentz force acts on any moving charge in a magnetic field and changes the **direction of its motion**.

In this example:
![[Pasted image 20251026084355.png]]
- The **velocity** of the charge carriers is along the **x-axis**    
- The **magnetic field** is applied along the **z-axis**,
- So the **Lorentz force** will deflect the carriers sideways — towards the **right-hand side** if the carriers are **positive charges (holes)**.

As a result, **positive charges accumulate on one side** of the material.  This **charge separation** creates a **transverse voltage** — a voltage that develops **perpendicular** to the current flow. The right side becomes **more positive** compared to the left.

Eventually, the Lorentz force is **balanced** by the **Coulomb force** due to this charge separation, and the system reaches equilibrium.
$$
F_c = q\cdot E_y 
$$

![[Pasted image 20251026084527.png]]
Now, if the **charge carriers are electrons** instead of holes, the situation looks a bit different.  
Even though the **current direction** remains the same, the **velocity of electrons** is **opposite** to the direction of the current because electrons have **negative charge**.

So, in this case:

- The **velocity** points in the opposite direction,
- The **magnetic field** still points upward (z-direction),
- According to the **right-hand rule**, the force on the moving electrons points in the opposite direction.
    

However, because the **charge q** of electrons is **negative**, the Lorentz force ends up being **in the same direction** as for the positive charges.

That means the **deflection** is still **toward the right**, but now the **accumulated charges are negative**.  
Therefore, the **Hall voltage** has the **opposite polarity** compared to the case with positive carriers — the **right side becomes more negative**.

So, when using a **Hall element**, always keep in mind that the **sign of the output voltage** depends on the **type of charge carriers** in the material — holes or electrons.

Now, let’s go a bit further and look at the **mathematical relationship** between the **measured Hall voltage $V_H$​ and the **magnetic field $B$** that we want to determine.

# <span style="color:rgb(239, 179, 1)">Magnetic Field Computation</span> 

![[Pasted image 20251026205724.png]]
At the **steady state**, the two forces acting on the charge carriers — the **Coulomb force** and the **Lorentz force** — will have **equal magnitudes**.  This means that the **net force** along the **y-direction** must be **zero**.

If we consider only the magnitudes of these two forces, we can equate them.  Since the charge $q$ appears in both expressions, it cancels out. From this, we obtain a relationship showing that the **electric field in the y-direction** (the one responsible for the Hall voltage $V_H$​) must be equal to the **vector product** of the **carrier velocity** and the **magnetic field**:
$$|E_y| = |v_x \times B_z|$$
In our case, the **magnetic field** is **orthogonal** to the **current flow** — that is, $\mathbf{B}$ is along the **z-axis**, and the current flows along the **x-axis**.  So the vector product simplifies to a simple multiplication, and we can write:
$$E_y=v_x \cdot B_z $$
We don’t measure the **electric field** directly, but we know it is **related to the Hall voltage** through the geometry of the sensor.  In particular:

$$E_y = \frac{V_H}{W}$$

where $W$ is the **distance** between the two terminals along which we measure the Hall voltage.

Next, we can relate the **velocity of the carriers** to the **current density** $J$.  The drift velocity of the carriers is given by:

$$v = \frac{J}{q \, n}$$

where

- $q$ is the charge of each carrier,
- $n$ is the **concentration** of free carriers in the material, and
- $J$ is the **current density**, defined as the current III divided by the **cross-sectional area** through which it flows:

$$J = \frac{I}{W \, T}$$

with $T$ being the **thickness** of the material.

Now, if we substitute these relationships into our earlier equation $E_y = v \cdot B$, we obtain:

$$\frac{V_H}{W} = \frac{J}{q n} BW$$

Rearranging gives the final expression for the **Hall voltage**:
$$V_H = \frac{1}{q n} \, \frac{I B}{T}$$
The term $$\frac{1}{q n}$$$1/qn$​ depends only on the material properties and is defined as the **Hall constant** $R_H$:
$$R_H = \frac{1}{q n}$$
Thus, we can write the Hall voltage in a compact form:
$$V_H = R_H \, \frac{I B}{T}$$
This equation shows that the Hall voltage is **directly proportional** to the applied magnetic field $B$, to the **current** $I$, and **inversely proportional** to the thickness $T$ of the conductive layer.

Now, remember that the **sign of the Hall voltage** depends on the **type of charge carriers**:

- For **n-type semiconductors** (electrons as majority carriers), the Hall constant $R_H$​ is **negative**, because $q$ is negative.
    
- For **p-type semiconductors** (holes as majority carriers), $R_H$​ is **positive**.
    
Therefore, when interpreting the measured Hall voltage, it is important to consider this sign — by convention, a **positive Hall voltage** corresponds to **hole conduction**.

## <span style="color:rgb(239, 179, 1)">Applications</span>

![[Pasted image 20251026211750.png]]
**Hall sensors** are mainly used in applications where you do **not need to measure the magnetic field precisely**, but simply need to **detect whether a magnetic field is present or not**.

For example, they are commonly used for **proximity detection**, to sense whether a magnetic object is near the sensor. They can also be used as **displacement sensors**, as shown in this example where a **magnetic slide** moves under the action of a **hydraulic actuator**. By placing Hall sensors along the path, you can detect the position of the magnetic slide depending on which sensor is activated.

![[Pasted image 20251026212726.png]]

Another common use is in **magnetic switches**, which open or close a circuit when a magnet comes near the sensor. This principle is also applied in **door interlock systems** — for instance, to automatically disable hazardous equipment when a door is opened. In such systems, a small magnet rotates with the key, and the Hall sensor detects the magnet’s position, allowing the system to know when the door is being opened or closed.

![[Pasted image 20251026212625.png]]

Hall sensors can also be used for **current measurement**. When a current flows through a wire or coil, it generates a magnetic field proportional to the current. A Hall sensor can detect this field, allowing indirect measurement of the current’s presence or magnitude.

In addition, Hall sensors are used in **magnetic encoders**, which are devices that track the **movement or rotation** of mechanical components using magnetic fields.

Finally, they can also be found in **electronic compasses**, where they detect the **Earth’s magnetic field** to determine orientation.

# <span style="color:rgb(223, 109, 109)">Magnetoresistors</span>

![[Pasted image 20251026213534.png]]
## <span style="color:rgb(239, 179, 1)">Magnetoresistance</span>

Now let’s move to the next type of magnetic field sensors — the **magnetoresistive sensors**.

In this case, the principle of operation is based on **resistances that change their value depending on the external magnetic field**. We won’t go into detail about the **readout circuits** used for these sensors, since they are quite similar to those already studied for **resistive temperature detectors (RTDs)**. In practice, the measurement can be done either by **injecting a current and reading the output voltage**, or by using a **Wheatstone bridge configuration**, as shown in this example.

So, what exactly is **magnetoresistance**?  

It refers to a **material property** where the **electrical resistance changes** when the material is exposed to a magnetic field. These sensors are **solid-state devices**, meaning they can be **integrated directly into silicon**, allowing them to be **very small** in size. Moreover, they are **more sensitive than Hall sensors**, making them suitable for applications where a **more accurate estimation of the magnetic field** is needed.

The key performance indicator for magnetoresistive sensors is the **magnetoresistance ratio (MR)**. This ratio is defined as the **difference between the maximum and minimum resistance values**, divided by the **minimum resistance**.  

$$MR=\frac{R_{max}-R_{min}}{R_{min}} $$

Mathematically, it represents how much the resistance changes with respect to its baseline value — essentially indicating the **maximum signal variation** that the sensor can produce in response to a magnetic field.

## <span style="color:rgb(239, 179, 1)">Magneto-resistive materials</span>

All conductive materials exhibit some level of **magnetoresistance**, meaning their resistance changes slightly when exposed to a magnetic field. However, in most common conductors this effect is **very weak**, making it unsuitable for sensing applications. This weak response is referred to as **ordinary magnetoresistance**.

In contrast, **materials specifically designed for magnetic sensing** show a much stronger magnetoresistive effect and can be classified into three main categories:

1. **Anisotropic Magnetoresistance (AMR):** These materials have a magnetoresistance ratio of about **1–2%**.
2. **Giant Magnetoresistance (GMR):** These exhibit a much larger ratio, typically in the range of **20–50%**.
3. **Tunneling Magnetoresistance (TMR):** These can reach even higher values, around **50–60%**.
    

Now, let’s take a closer look at each of these three types of magnetoresistive sensors.

### <span style="color:rgb(161, 40, 226)">Anisotropic Magnetoresistance (AMR)</span>
![[Pasted image 20251026215126.png]]
	 
Anisotropic magnetoresistances are called _anisotropic_ because their properties depend on the **angle between the electrical current and the direction of magnetization** within the material.

To observe this effect, the material must be **magnetized** and a **current must flow** through it.

- When the **magnetization is parallel** to the current flow (left image), the material shows its **maximum resistivity**. This happens because the **atomic orbitals** are slightly **distorted**, increasing the **probability of electron scattering** inside the material. More scattering means higher energy dissipation, and therefore a **higher resistance**.
    
- Conversely, when the **magnetization is perpendicular** to the current flow (right image), the **interaction between the moving carriers and the valence electrons** is minimized. This reduces scattering events and results in the **minimum resistance**.

![[Pasted image 20251026221717.png]]
If we study in more detail the relationship between the **resistance** of the material and the **angle (θ)** between the current and the magnetization, we find that it follows this equation:

$$R = R_0 + \Delta R \cdot \cos^2(\theta)$$

where:

- $R_0$​ is the base resistance of the material,
- $\Delta R$ is the maximum variation of resistance, and
- $\theta$ is the angle between the current and the magnetic field direction.

From this relation:

- The **maximum resistance** occurs when $\cos^2(\theta) = 1$ → at 0°, 180°, or -180°.
- The **minimum resistance** equals $R_0$​ when $\cos^2(\theta) = 0$ → at 90°, 270°, or their negative equivalents.
- An **intermediate resistance**, $R_0 + \frac{\Delta R}{2}$​, occurs at 45°, where $\cos^2(45°) = 0.5$.

![[Pasted image 20251026222157.png]]

The **best operating point** is around **-45°**, because at this angle the resistance curve is most **linear** and the **sensitivity** (the derivative of the curve) is highest.

For this reason, AMR sensors include **conductive shunts**—highly conductive paths oriented at **45°** with respect to the magnetization direction.

- The **brown** regions in the figure represent the **magnetic material** (high resistivity).
- The **yellow** regions are the **conductive shunts** (low resistivity).

![[Pasted image 20251026222225.png]]

When a voltage is applied, the current follows the **path of least resistance**, which means it travels **orthogonally to the conductive shunts**, minimizing its path through the resistive magnetic material.

In this configuration, with no external magnetic field (H = 0), the **angle between current and magnetization** is **−45°**, setting the device exactly at its **optimal working point** for sensitivity.

![[Pasted image 20251026223003.png]]
 
 Now, when we apply an **external magnetic field (H)**, the **overall magnetic flux** in the material becomes the **vector sum** of two components: the **initial magnetization** of the material and the **applied external field**.

As a result, the **direction of the total magnetization** changes depending on the **strength and orientation** of this external field. This change in direction also modifies the **angle (θ)** between the magnetization and the current flow.

Since the resistance of the material depends on this angle, as we saw before, the application of an external magnetic field leads to a **variation in the overall resistance (R)**.

Let’s now analyze in more detail the **relationship between the resistance R** and the **external field H**.

![[Pasted image 20251026225057.png]]

Start from the initial condition (no external field). With $(H=0)$ the total flux $(B)$ equals the material’s initial magnetization (M). The device is biased so the current $(I)$ makes an angle $(\theta=-45^\circ)$ with $(B)$. Using  

$$  R(\theta)=R_0+\Delta R\cos^2\theta$$we get the starting resistance  
$$R = R_0 + \tfrac{1}{2}\Delta R$$
Now apply an external field (H) **perpendicular** to the initial magnetization (M). Consider these cases:

![[Pasted image 20251026225246.png]]
1. **(H = M) (same magnitude, perpendicular direction):**  
    The vector sum $(B=M+H)$ points at $(+45^\circ)$ relative to (M). Because the shunt/current geometry fixes the current direction, the angle between $(B)$ and $(I)$ becomes $(\theta=0^\circ)$. Then $(\cos^2\theta=1)$ and  
    $$R = R_0 + \Delta R  $$
    — the **maximum** resistance.

![[Pasted image 20251026225514.png]]
1. **$(H \gg M)$** (very large perpendicular $(H)$):  
    $(B)$ aligns with $(H)$; the angle between $(B)$ and $(I)$ tends to $(\theta=45^\circ)$. Thus $(\cos^2 45^\circ=1/2)$ and  
    $$
    R \to R_0 + \tfrac{1}{2}\Delta R,  $$
     
    which is the same value as the $(H=0)$ starting point (an asymptote for large positive $(H)$).

![[Pasted image 20251026225552.png]]
1. **(H) perpendicular but in the opposite direction (i.e. (-H), same magnitude):**  
    Now $(B)$ points to $(-45^\circ)$ relative to (M), which makes the angle between (B) and the fixed current (I) equal to $(\theta=90^\circ)$. Because $(\cos^2 90^\circ=0)$,  
$$    R = R_0  $$
    — the **minimum** resistance.

![[Pasted image 20251026225840.png]]
1. **$(H \ll -M)$** (very large negative perpendicular $(H)$):  
    $(B)$ is dominated by $(H)$ and the angle between $(B)$ and $(I)$ tends to $(\theta=135^\circ)$. Again $(\cos^2 135^\circ=1/2)$, so  
    
    $$R \to R_0 + \tfrac{1}{2}\Delta R$$
    the same asymptote as for large positive (H).

![[Pasted image 20251026230112.png]]
If you plot $(R)$ versus $(H)$ for $(H)$ ranging from large negative to large positive values, you get this shape:

- At very large $(|H|)$ (either sign) the curve approaches the same asymptote $(R_0 + \tfrac{1}{2}\Delta R)$.
    
- For positive $(H)$, the resistance **increases** from the asymptote, reaches a **maximum** at $(H=+M)$ $((R_0+\Delta R))$, then falls back to the asymptote as $(H\to+\infty)$.
    
- For negative $(H)$, the resistance **decreases** from the asymptote, reaches a **minimum** at $(H=-M) ((R_0))$, then rises back to the same asymptote as $(H\to-\infty)$.
    

In the interval $(H\in[-M,+M])$ the $(R(H))$ curve is **monotone and approximately linear**, which is precisely the range where AMR sensors are used for measurement. In that range you can both **measure the magnitude** and **determine the sign** of the applied field.

### <span style="color:rgb(161, 40, 226)">Giant Magnetoresistance (GMR)</span>

![[Pasted image 20251026230400.png]]

Giant magnetoresistances are called _“giant”_ because their magnetoresistance ratio is much higher than that of anisotropic magnetoresistances.

A GMR device is made of **two or more layers of ferromagnetic metals** (shown in brown) separated by **very thin non-magnetic metal spacers** (shown in orange). These spacer layers are crucial:

- They **allow the magnetic orientation** of adjacent ferromagnetic layers to be different — even opposite.
- At the same time, they **conduct electric current**, so electrons can move from one magnetic layer to another.
    

Now, what happens depends on how the magnetic layers are aligned:

- **Opposite alignment (antiparallel, left image):**  
    The spins of the electrons in one magnetic layer are opposite to those in the next. Because of this, electrons experience more scattering when moving between layers, so the **resistance increases**.
- **Same alignment (parallel, right image):**  
    The spins of the electrons are all oriented in the same direction, allowing them to move easily from one layer to another. As a result, the **resistance decreases**.
![[Pasted image 20251027081424.png]]

When no external magnetic field is applied, the **spacer layers**—which are only a few atoms thick—create a **strong exchange coupling** between adjacent ferromagnetic layers. This coupling naturally favors an **antiparallel alignment** of their magnetic fields: the north pole of one layer attracts the south pole of the next.

![[Pasted image 20251027081452.png]]

Because of this antiparallel configuration, the **resistance of the material is high**. In the graph showing resistance versus external magnetic field, this corresponds to a **maximum resistance at zero external field**.

![[Pasted image 20251027081504.png]]

When an **external magnetic field** is applied and becomes strong enough to **overcome the interlayer coupling**, all magnetic layers align in the same direction, producing a **parallel configuration**. In this case, the resistance reaches its **minimum value**.

![[Pasted image 20251027081522.png]]
As the external field increases (either positively or negatively), the resistance decreases until it reaches this minimum. The characteristic curve is **even**, meaning it is symmetric with respect to the origin. Therefore, with **giant magnetoresistances (GMRs)**, unlike with anisotropic magnetoresistances (AMRs), we can only determine the **magnitude** of the magnetic field — not its **direction** or sign.
	 
Giant magnetoresistances can be read out using **two configurations**: **current-in-plane (CIP)** or **current-perpendicular-to-plane (CPP)**.

![[Pasted image 20251027082127.png]]
In the **current-in-plane configuration**, the voltage is applied along the longitudinal sides of the material, forcing the current to flow **parallel** to the magnetic layers. In this case, the **sensitivity is lower** because the current mainly remains within each layer — a phenomenon known as the **shunting effect**. This reduces the likelihood of electrons moving between layers, which in turn minimizes the difference in resistance between the parallel and antiparallel magnetization states.

![[Pasted image 20251027082146.png]]
In the **current-perpendicular-to-plane configuration**, the voltage is applied **perpendicular** to the layers, forcing the current to travel **through** the stacked layers. Here, electrons must cross different magnetic and non-magnetic layers, so the **difference in resistance** between the parallel and antiparallel configurations is much more pronounced, leading to **higher sensitivity**.

However, because these layers are extremely thin, the **overall resistance (R₀)** of the structure is very low. As a result, even though the **percentage variation** in resistance (the magnetoresistance ratio) is larger in the CPP configuration, the **absolute change in resistance** can still be very small and difficult to measure.

For this reason, the **current-in-plane configuration** is usually preferred, since it provides a **higher base resistance (R₀)**, making it easier to detect and measure the resistance changes in practice.

### <span style="color:rgb(161, 40, 226)">Tunneling Magnetoresistance (TMR)</span>
   
![[Pasted image 20251027082412.png]]
Finally, we have the **tunneling magnetoresistances (TMRs)**, which are sensors that use **two different magnetic layers**. One is called the **pinned layer**, which is deposited on top of an **antiferromagnetic pinning layer**.

The **pinning layer** itself does not have intrinsic magnetization, but its purpose is to **lock the magnetization direction** of the adjacent ferromagnetic layer (the pinned layer). This means that the orientation of the pinned layer’s magnetization depends only on the properties of the pinning layer and **does not change** when an external magnetic field is applied.

The second layer, called the **free layer**, is also ferromagnetic, but unlike the pinned layer, its magnetization **can rotate** in response to an external magnetic field. In the initial state, the free layer is typically designed so that its magnetization is **perpendicular** to that of the pinned layer.

![[Pasted image 20251027082934.png]]

Now, if we apply an external magnetic field, we can modify the orientation of the magnetization in the **free layer**. Between the pinned layer and the free layer, however, there is an **insulating layer**. This layer does not block the magnetic field — so the two magnetic layers can still have different orientations — but it **does block the flow of electrical current**.

In classical physics, an electron cannot cross this insulating barrier. However, according to **quantum mechanics**, there is a small probability that an electron can pass through the insulator — a phenomenon known as the **tunneling effect**. This is why this type of sensor is called a **tunneling magnetoresistance (TMR)** sensor: it relies on the quantum tunneling of electrons.

In particular, when the magnetizations of the pinned layer and the free layer are **parallel** (as in the plot on the left), the probability that an electron with a given spin will tunnel through the barrier is relatively **high**, because there are many available electronic states in the upper layer that match the spin of the tunneling electrons. As a result, the **resistance is low**.

Conversely, when the magnetizations of the two layers are **antiparallel** (as in the plot on the right), the available spin states in the upper layer do not correspond to those in the lower layer. Therefore, the **tunneling probability decreases drastically**, leading to a **much higher resistance**.

![[Pasted image 20251027083011.png]]

So, **to summarize**, in the **rest condition**, that is, without any external magnetic field, the magnetizations of the pinned layer and the free layer are **perpendicular** to each other. In this state, the sensor exhibits a certain resistance, which we can call **R₀**.

When an **external magnetic field** is applied and causes the magnetization of the free layer to **rotate** toward the **same direction** as the pinned layer, the overall resistance **decreases**, reaching a **minimum value** once the external field fully overcomes the perpendicular rest magnetization.

On the other hand, if the external field is applied in the **opposite direction**, aligning the magnetization of the free layer **antiparallel** to that of the pinned layer, the **resistance increases**.

Therefore, in this case, the resistance–magnetic field characteristic is **monotonic**, unlike in giant magnetoresistance sensors. This means that tunneling magnetoresistance (TMR) sensors allow us to measure not only the **magnitude** but also the **direction** of the external magnetic field.

![[Pasted image 20251027083255.png]]

Tunneling magnetoresistance (TMR) sensors are **always used in a current-perpendicular-to-plane configuration**. This means that the external voltage is applied **perpendicular to the layers**, forcing the current to flow **from one magnetic layer to the other**. This configuration is necessary because, as mentioned earlier, there is an **insulating layer** between the pinned layer and the free layer. If we used a current-in-plane configuration, **no electrons would be able to tunnel** through the insulator, and the tunneling effect would not occur.

In the perpendicular configuration, we must be careful with the **applied voltage**, which is typically limited to a few **millivolts** to avoid damaging the thin insulating barrier. For this reason, a **manual resistor** is often added **in series** with the sensor to control the overall resistance and **limit the voltage drop** across the tunneling barrier.

<span style="color:rgb(2, 141, 192)"><b>Applications of Magnetoresistive Sensors</b></span>

Magnetoresistive sensors are mainly used in applications that require **high sensitivity** and the ability to **measure the actual magnitude of the magnetic field**. For example, they are used for **eddy current sensing**. Eddy currents are circular currents that appear in metallic materials when these materials are exposed to varying magnetic fields. These currents generate **secondary magnetic fields**, which can be detected using magnetoresistive sensors.

They can also be employed to measure **very weak magnetic fields**, such as those produced by stressed ferromagnetic materials. This property makes them useful for **detecting defects or non-uniformities** within magnetic structures. In addition, magnetoresistive sensors are used to **monitor stress** in metallic reinforcements or fasteners by measuring the magnetic field inside these materials.

Finally, they are commonly used in **displacement encoders**, a topic that will be explored in one of the next classes.



