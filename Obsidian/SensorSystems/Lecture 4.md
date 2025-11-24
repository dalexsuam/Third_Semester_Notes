
Date: 09/10/2025
***

Today’s topic is **temperature sensors**. In particular, we’ll focus on **resistive-based sensors**, that is, **Resistance Temperature Detectors (RTDs)** and **thermistors**.  
In the next class, we’ll continue with other types of temperature sensors based on different physical principles — specifically, **thermocouples**, **diode and band-gap sensors**, and **infrared thermometers**.

So, let’s start with **Resistance Temperature Detectors**, or **RTDs**.

# <span style="color:rgb(223, 109, 109)">Resistance Temperature Detectors (RTDs)</span>

![[Pasted image 20251006144314.png]]
RTDs are sensors made of **metallic elements** whose **resistance varies with temperature**. This metallic part is called the **sensing element** or **bulb**, and its resistance changes according to the temperature of the material. The exact relationship between resistance and temperature depends on the **type of metal** used.

Typical RTDs have a **nominal resistance** in the range of **100 ohms to 1 kiloohm** at a reference temperature (usually room temperature).  
Common materials for RTDs include **platinum, nickel, copper, iron, silver,** and **gold**.

Among these, the most widely used is the **PT100**, where _“PT”_ indicates that the sensing element is made of **platinum**, and _“100”_ means its nominal resistance at **0°C** is **100 ohms**.

One of the main advantages of RTDs is their **excellent linearity** — the relationship between resistance and temperature is almost linear over a wide range, typically from **-200°C to +800°C**.

Structurally, RTDs can be built in two main ways:

1. **Wire-wound types**, which can be made as **coiled** or **outer-wound** designs.
2. **Film-pattern types**, where the sensing element is deposited as a thin film on a substrate.

## <span style="color:rgb(239, 179, 1)">Wire-Wound RTDs</span>

![[Pasted image 20251006144543.png]]

As I mentioned before, in this design we use a **very thin metallic wire** that acts as the sensing element. This wire can be arranged in two main ways — either **wound into a coil inside** a ceramic structure, or **wound around** it.

In the **coil design**, the wire is **embedded inside a ceramic mandrel**. The ceramic material protects the wire, making the sensor **more robust and durable**. However, this protection also has a drawback: since the heat must first pass through the ceramic before reaching the wire, the **response time is slower**.

On the other hand, in the **outer-wound design**, the wire is **wrapped around the ceramic mandrel** instead of being enclosed within it. In this configuration, the wire is **more directly exposed** to the environment, allowing **faster response times** to temperature changes. The trade-off, however, is that this type of sensor is **more fragile** and **less resistant to mechanical stress**.

## <span style="color:rgb(239, 179, 1)">Film-pattern</span>
 
![[Pasted image 20251006201558.png|4000]]

The **second RTD structure** is known as the **film-pattern type**.

In this case, the sensing element consists of a **metal-coated substrate**, where a **resistive pattern** is created by cutting or etching the metal layer. To fabricate this kind of RTD, we use a **photolithographic process**, which is the same technique commonly used in printed circuit board and microelectronic manufacturing.

In this process, **light is projected through a patterned mask** onto a **light-sensitive material**, called **photoresist**, that covers the metal-coated substrate. The exposed areas are then developed and etched, transferring the pattern onto the metal layer.

The resulting metallic pattern behaves as a **miniaturized resistor**, whose resistance varies with temperature. Finally, a **protective glass layer** is deposited on top to **shield the conductor** from mechanical damage and environmental effects. 
  
##   <span style="color:rgb(239, 179, 1)">RTD Temperature Coefficient</span>
  
Now, if we analyze the **performance of RTDs**, one of the most important parameters is their **sensitivity**.  

### <span style="font-weight:bold; color:rgb(161, 40, 226)">Sensitivity:</span>
The **sensitivity** is defined as the **variation of the resistance (output)** divided by the **variation of the temperature (input)**, and it is expressed in **ohms per degree Celsius (Ω/°C)**. This parameter depends not only on the material used for the RTD, but also on its **geometry**.

$$
S=\frac{\Delta R}{\Delta T} \space \left[\frac{\Omega}{^\circ C}\right]
$$

### <span style="color:rgb(161, 40, 226)">Temperature Coefficient:</span>

We can also define the **temperature coefficient**, usually indicated by $α$, which is a property that depends **only on the material** (for example, platinum, nickel, or copper).  
This coefficient is defined as the **sensitivity divided by the nominal resistance**, R0R_0R0​, which is the resistance of the RTD at $0^\circ C$ 

Formally, the temperature coefficient can be written as:

$$\alpha = \frac{(R_{100} - R_0)}{100 \cdot R_0} = \frac{S}{R_0} \left(\frac{\Omega}{^\circ C \cdot \Omega} \right)$$

where $R_{100}$ and $R_0$​ are the resistances at $100^\circ C$ and $0^\circ C$, respectively.

RTDs are known for their **excellent linearity**, meaning that their sensitivity remains practically **constant across a wide temperature range**.  

Since most RTDs have a **positive temperature coefficient**, their resistance **increases** as temperature increases.

The **characteristic equation** that describes an RTD is therefore linear and can be written as:
$$
R_T = R_0 (1 + \alpha \Delta T) = R_0 + \Delta R
$$
where:

- $R_T$​ is the resistance at temperature $T$,
- $R_0$ ​is the resistance at $0^\circ C$,
- $\alpha$ is the temperature coefficient, and
- $\Delta T$ is the temperature difference.
    

We can also express the **change in resistance** as:
$$
\Delta R = \alpha R_0 \Delta T
$$
So, $\alpha R_0$​ represents the **sensitivity**, that is, how much the resistance changes per degree of temperature variation.

![[Pasted image 20251006221410.png]]

If we compare different materials such as **platinum, nickel, copper, iron, silver,** and **gold**, we can see that each one has a **different temperature coefficient (α)**. This means that the rate at which the resistance changes with temperature depends on the **material itself**.

For example, if we look at **platinum**, we notice that its **resistance–temperature characteristic** is extremely **linear**. In the graph, the **blue curve** represents the actual behavior of platinum, while the **red line** shows the **ideal linear fit**. As you can see, the two curves almost overlap, meaning that the difference between the real behavior and the linear approximation is very small.

This excellent linearity is maintained over a **wide temperature range**, approximately from **–200 °C to 600 °C or even 700 °C**. That’s why **platinum** is considered the best material for RTDs — its **temperature coefficient α remains practically constant** over this large interval.

Other materials such as **nickel, copper, iron, silver,** and **gold** also show good linearity, though not as perfect as platinum. Their resistance–temperature curves still follow a nearly straight line, with only **slight deviations** from the ideal linear trend.

## <span style="color:rgb(239, 179, 1)">Measuring Circuits</span>

Now let’s look at how we can **measure the resistance** of an RTD in practice. Understanding these measurement circuits is very important because the same principles can also be applied to **other resistive sensors**, such as **strain gauges**, which we will study later in the course.

When we want to measure the **temperature** of an object or an environment using an **RTD**, there are **two main approaches** to build the readout circuit:

1. **The simple method:**  

![[Pasted image 20251006222043.png]]
    In this approach, we simply **inject a known current** through the RTD and **measure the voltage** across it. From Ohm’s law (V = I × R), we can then calculate the resistance — and therefore the temperature — directly. This method is easy to implement but can be sensitive to factors such as lead resistance or small variations in current.
    
2. **The differential method (Wheatstone bridge):**  

![[Pasted image 20251006222105.png]]
The second approach is more accurate. It uses a circuit called a **Wheatstone bridge**, which compares two voltage branches. One branch serves as a **reference**, providing a constant voltage, while the other branch includes the **RTD**, whose voltage changes depending on temperature. By measuring the **difference between the two voltages**, we can detect very small changes in resistance more precisely.

### <span style="color:rgb(161, 40, 226)">Simple Method: 2 lead wired set-up</span>
![[WhatsApp Image 2025-10-08 at 15.11.10_c29c5dd5.jpg]]

Let’s begin with the **simplest readout configuration**, which is the **two-wire connection** between the RTD and the readout circuit.

In this setup, the circuit can be designed using a **PMOS transistor** to generate a **constant current**. For instance, if we bias the PMOS with a fixed **gate-source voltage (V<sub>SG</sub>)**, and operate it in the **saturation region**, the transistor will provide a nearly constant current that depends mainly on that bias voltage and the power supply (**V<sub>DD</sub>**). This current flows through the RTD, whose resistance varies with temperature.
![[WhatsApp Image 2025-10-08 at 15.18.06_77557eb1.jpg]]
The voltage across the RTD can then be **measured** — for example, by connecting its lower terminal to ground and using a **non-inverting amplifier configuration** to read the voltage across it. It’s important that this **amplifier has a high input impedance**, so that it doesn’t draw current and thus doesn’t disturb the current flowing through the RTD.

However, this simple two-wire configuration has a **major limitation**: the **resistance of the connection wires themselves**. Each wire has its own parasitic resistance — we call them **R<sub>L1</sub>** and **R<sub>L2</sub>** — and when you measure the voltage across the RTD, the measured voltage will also include the voltage drop caused by these lead resistances.
$$
R_{meas}=R_{L1}+R_{L2}+R_{RTD}
$$
This means that the **measured voltage depends not only on the RTD**, but also on **the resistance of the wires**, which can introduce significant errors — especially when the sensor is placed far from the readout circuit (for instance, in industrial or laboratory setups with long cables).

Sometimes, this effect can be **compensated by calibration**, if the leads are fixed and their resistances are known. However, if you change the wiring or the distance, this calibration no longer applies, and the measurement becomes unreliable.

To overcome this issue, an **improved configuration** can be used — the **three-wire connection**, which helps cancel out the effect of the lead resistances and provides a much more accurate measurement.

### <span style="color:rgb(161, 40, 226)">Simple Method: 3 lead wired set-up</span>

![[WhatsApp Image 2025-10-08 at 15.28.22_c0fcca2b.jpg]]

In the **three-wire configuration**, the goal is to eliminate the effect of the lead resistances from the measurement. Here’s how it works:  

We use **three connection wires**, labelled **lead 1**, **lead 2**, and **lead 3**. The RTD is connected between **lead 1** and **lead 2**.

1. **First measurement:**  
    We inject a known current (**I<sub>A</sub>**) between **lead 1** and **lead 2**, the path that includes the RTD.  We then measure the voltage across these same points — let’s call this **V<sub>A</sub>**.  
    With this, we can compute the apparent resistance:
    
    $R_A = \frac{V_A}{I_A}$
    
    However, this measured resistance (**R<sub>A</sub>**) includes not only the resistance of the RTD itself, but also the resistances of the two leads, **R<sub>L1</sub>** and **R<sub>L2</sub>**, so:
    
    $R_A = R_{RTD} + R_{L1} + R_{L2}$
    
1. **Second measurement:**  
    We then inject a second current (**I<sub>B</sub>**) between **lead 2** and **lead 3**, this time along a path that does **not include the RTD**.  We measure the voltage across this path (**V<sub>B</sub>**) and compute:
    
    $R_B = \frac{V_B}{I_B}$​​
    
    In this case, **R<sub>B</sub>** depends only on the lead resistances (**R<sub>L2</sub>** and **R<sub>L3</sub>**).

Now, if we assume that all three leads are made from the same material, have the same diameter, and are the same length, then their resistances are approximately equal (**R<sub>L1</sub> ≈ R<sub>L2</sub> ≈ R<sub>L3</sub> = R<sub>L</sub>**).

This allows us to estimate the true resistance of the RTD by simply **subtracting** the contribution of the leads:

$$R_{RTD} = R_A - R_B$$

In this way, the **three-wire configuration** effectively cancels out the influence of the wire resistances, providing a much more **accurate and stable temperature measurement**, even when long cables are used.

### <span style="color:rgb(161, 40, 226)">Simple Method: 4 lead wired set-up</span>

![[WhatsApp Image 2025-10-08 at 15.39.15_1dcf19b0.jpg|5000]]

 Another way to eliminate the influence of lead resistance in your measurements is by using a **four-wire configuration**.

In this setup, the current that flows through the RTD is injected using **two wires**, just like before — for example, one connected to the top of the RTD and one to the bottom (through a PMOS transistor acting as a current source, with the lower node at ground).

However, we now add **two additional wires** — these are not used to carry current, but to **sense the voltage** directly across the RTD. These wires are connected to a special type of amplifier called an **instrumentation amplifier**.

An **instrumentation amplifier** is built from three operational amplifiers. Its main feature is that it measures the **difference in voltage** between its two inputs (labeled $V^+$ and $V^-$) and produces an output voltage $V_{out}$​ that is proportional to that difference:

$$V_{out} \propto (V^+ - V^-)$$
The second important characteristic is that both of its inputs have **very high impedance**. This means that almost **no current flows** into the amplifier inputs.

Because no current flows through the sensing wires (the additional two leads), there is **no voltage drop** across their resistances. As a result, the voltage seen by the amplifier is **exactly the same** as the voltage directly across the RTD.

This makes the four-wire configuration **independent of the lead resistances**, since those resistances don’t affect the measured voltage. The amplifier only sees the voltage caused by the RTD itself, which depends on temperature.

This approach is therefore the **most accurate** among the configurations we’ve discussed (2-wire, 3-wire, and 4-wire). It is commonly used in **laboratory measurements** and other **high-precision applications**, where even small errors cannot be tolerated.

A similar principle can also be used when measuring other resistive quantities, such as **body impedance**. In that case, electrodes are used to inject current into the body, and **two separate electrodes** are used to sense the voltage. This ensures that the voltage measurement is not affected by the contact resistance between the electrodes and the skin, improving the **accuracy** of the impedance measurement.
 ***
 
![[WhatsApp Image 2025-10-08 at 15.49.22_381da6af.jpg]]

The main **limitation** of this **single-ended readout** configuration — even when using a precise four-wire setup — lies in the **nature of the voltage signal** that we are measuring.

Let’s recall that the voltage we obtain at the output is:
$$V = I \times R_{RTD}$$
and that the resistance of the RTD can be expressed as:
$$R_{RTD} = R_0 + \Delta R$$
where:
- $R_0$​ is the **nominal resistance** (for example, 100 Ω for a PT100 at 0 °C or room temperature),
- $\Delta R$ is the **small variation** in resistance due to the temperature change we want to measure.

If we substitute that into the first equation, we get:

$$V = I \times (R_0 + \Delta R) = V_0 + \Delta V$$
Here:

* $V_0 = I \times R_0$​ is a **large DC component**, corresponding to the nominal resistance,
- $\Delta V = I \times \Delta R$ is a **small signal**, the part that actually contains the information about the temperature change.

The problem is that $\Delta V$ is **much smaller** than $V_0$​.  
For example, in a PT100:

- at room temperature $R_0 = 100 Ω$,
- a temperature variation of a few degrees changes $R_{RTD}$​ by only a few ohms.

So $\Delta R \ll R_0$, and consequently $\Delta V \ll V_0$​.

This becomes a problem for amplification:
If you try to amplify the signal with an instrumentation amplifier to make $\Delta V$ easier to detect, you also amplify the large $V_0$ term.  

That means the amplifier can easily **saturate**, and the small variation due to temperature becomes difficult to isolate or measure accurately.

Because of this limitation, it’s not ideal to use a single-ended readout when you are interested only in small variations of resistance.

That’s why we move to a **differential approach**, using a **Wheatstone bridge**.
  
### <span style="color:rgb(161, 40, 226)">Wheatstone Bridge</span>

![[Pasted image 20251008161552.png]]


In the differential approach, the measurement circuit is based on the **Wheatstone bridge configuration**. This structure includes two branches that form two voltage dividers supplied by the same voltage source.


| ![[Pasted image 20251008161552.png\|4000]] | In the first branch, called the _reference branch_, we have two fixed resistors, $R_2$​ and $R_3$​. The voltage at the middle point between these two resistors is called $V^-$, and it provides a reference value that does not depend on temperature.                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![[Pasted image 20251008184856.png]]       | In the second branch, we have a fixed resistor $R_1​$ and the resistive temperature detector, represented by $R_x$​. The voltage at the middle point between $R_1$​ and $R_x$​ is called $V^+$, and in this case, the voltage depends on the resistance of the RTD, which changes with temperature. |

The output of the bridge is the **difference** between these two voltages, $V_{out} = V^+ - V^-$. This output is then typically connected to an **instrumentation amplifier**, which has a very high input impedance so that it does not disturb the voltage dividers formed by the bridge.

The goal of this configuration is to obtain an output that depends **only** on the variation of the RTD resistance ($\Delta R$), and not on its nominal value $R_{x0}$​. In other words, we want $V_{out} = 0$ when the RTD is at its nominal temperature, and a nonzero output only when the temperature changes.

To achieve this, the bridge must be **balanced** at the nominal condition. The balance condition can be written as:
$$\frac{R_3}{R_2 + R_3} = \frac{R_{x0}}{R_1 + R_{x0}}$$
This condition ensures that when $R_x = R_{x0}$​, the two voltage dividers generate the same voltage, and thus the output $V_{out}$ is zero. A common and simple way to satisfy this condition is to choose $R_1 = R_2$​ and $R_3 = R_{x0}$​. ($R_{x0}$ is the resistance of the RTD at nominal temperature. For example, $100 \Omega$ for PT100).

When the temperature changes, the resistance of the RTD becomes $R_x = R_{x0} + \Delta R$. The output voltage now depends on this small variation $\Delta R$, which is directly related to the temperature change. Since $\Delta R$ is much smaller than the nominal resistance, the resulting output voltage is also small but **proportional to the temperature variation**.

An important advantage of this differential approach compared to the single-ended configuration is that the large nominal voltage component (associated with $R_0$​) is automatically cancelled. This allows us to amplify only the small signal that represents the temperature change, without saturating the amplifier.

For this reason, the Wheatstone bridge configuration is widely used when high precision and stability are required, especially in systems where the temperature variations are small compared to the nominal resistance of the sensor.

Let's proceed with some calculations. Then...

![[Wheatstone bridge.pdf]]

Once we write the complete expression of the output voltage $V_{out}$​ for the Wheatstone bridge, we just solve it. From this point, the equation can be further reduced by considering a very reasonable assumption: the variation in resistance, $\Delta R$, is much smaller than the nominal resistance $R_{x0}$​, as well as the other resistors in the bridge, such as $R_1$.

Since $\Delta R \ll R_{x0}$​ and $R_1$​ is typically of the same order of magnitude as $R_{x0}$​ (and in many cases is chosen to be equal to it), we can neglect the small higher-order terms. This simplification allows the expression for $V_{out}$​ to become much more compact, and it now shows clearly that the output voltage is **directly proportional to** $\Delta R$.

We know that the change in resistance of an RTD can be written as:
$$
\Delta R = \alpha \, R_{x0} \, \Delta T
$$
where $\alpha$ is the temperature coefficient of resistance, $R_{x0}$​ is the nominal resistance of the sensor, and $\Delta T$ is the variation in temperature with respect to the reference point.

By substituting this relationship into our equation for $V_{out}$​, we can express the output voltage as:

$$V_{out} = k \, \Delta T$$

where $k$ is a constant that depends on the supply voltage $V_s$​, the resistors $R_1​$, $R_2$​, $R_3​$, and the sensor parameters $R_{x0}$​ and $\alpha$.

This result clearly shows that the output voltage varies linearly with the change in temperature — and, importantly, **there is no offset term** (no “+ something” as in the single-ended configuration). The bridge output depends only on the temperature variation, not on the nominal resistance of the sensor.

This is a major advantage of the differential approach: even though the signal we obtain (the differential voltage between $V^+$ and $V^-$) is small — because $\Delta R$ is typically just a few ohms — we can apply a relatively high gain in the instrumentation amplifier without the risk of saturating it. This amplified signal can then be easily digitized by an analog-to-digital converter (ADC) with good resolution.

A final point to discuss is **how to choose the resistor values** in the bridge.  
To ensure that the output depends only on $\Delta T$, we must satisfy the balance condition, which is achieved when:
$$
\frac{R_2}{R_3} = \frac{R_1}{R_{x0}}​​
$$
A simple way to meet this condition is to select $R_1 = R_2$ ​ and $R_3 = R_{x0}$​.

However, if we want to **maximize the sensitivity** — that is, maximize the variation of $V_{out}$ with respect to temperature — we can differentiate the output expression and find that the maximum output is achieved when all resistors are equal:
$$
R_1 = R_2 = R_3 = R_{x0}​
$$
Under this condition, the expression for the output voltage simplifies to:
$$
V_{out} = \frac{1}{4} \, \frac{\Delta R}{R_{x0}} \, V_s​
$$
It’s important to remember that $\frac{\Delta R}{R_{x0}}$​ is a small ratio, meaning that the resulting voltage at the bridge output can be quite small. Therefore, the supply voltage $V_s$​ must be high enough to generate a signal that stands out above the noise level of the circuit.

If the input signal to the instrumentation amplifier is too small — close to or below the noise — even applying a large gain will only amplify the noise together with the signal, worsening the signal-to-noise ratio. For this reason, a proper choice of $V_s$​ is essential to ensure that the measurement remains accurate and the amplified output remains meaningful.

### <span style="color:rgb(161, 40, 226)">2- and 3-wire Wheatstone bridge</span>

![[Pasted image 20251009184505.png]]

Even when using the Wheatstone bridge configuration, we can still face issues related to **lead resistance**, especially when the RTD is located far from the rest of the circuit. Imagine a situation where the three reference resistors of the Wheatstone bridge (R₁, R₂, and R₃) are placed on a board, while the RTD is physically distant — for instance, attached to a machine or a process line. In this case, long wires are required to connect the RTD to the bridge, and these wires inevitably introduce **stray resistances**.

If we start from the _ideal case_, assuming that the resistance of the leads is zero, the output voltage of the Wheatstone bridge, $V_{out}$​, is simply the differential voltage between the two branches:
$$
V_{out} = V_s \cdot \left( \frac{R+\Delta R}{R_1 + R + \Delta R} - \frac {R}{R_2+R} \right)
$$

where $R+ \Delta R$ is the total resistance of the RTD (the nominal resistance plus its temperature-dependent variation).
 
![[Pasted image 20251009184452.png]]
However, in the _real case_, we must also include the contribution of the lead resistances, which we’ll call $R_L$. Since we have two leads connecting the RTD, the total additional resistance introduced is $2R_L$​. Therefore, the actual output voltage becomes:
![[Pasted image 20251009184606.png]]


$$V_{out,real} = V_s \left( \frac{R + \Delta R + 2R_L}{R_1 + R + \Delta R + 2R_L} - \frac{R}{R_2 + R} \right)$$

This is the voltage we would measure in practice, and it clearly includes the unwanted effect of the lead resistances.

To quantify the impact of these parasitic resistances, we can define an **error term** $\varepsilon$, which represents the difference between the real output voltage (including lead effects) and the ideal output voltage (without them):
$$
ε=Vout,real​−Vout,ideal
$$

By performing the algebraic simplifications (finding the common denominator, expanding terms, and neglecting higher-order small quantities), we obtain an expression for $\varepsilon$ that reveals an important property:  
when $\Delta R$ is very small compared to R — which is typically the case — many terms cancel out, and the final error expression becomes **independent of $\Delta R$**.
![[Pasted image 20251009184821.png]]
$$
\varepsilon = V_s \cdot \frac{R_L}{2(R+R_L)}
$$
This is actually good news: if the error does not depend on the temperature variation, it means that it can be **easily compensated through calibration**. The error depends mainly on three factors:

- the **supply voltage** $V_s$,
- the **lead resistance** $R_L$​, and
- the **nominal resistance** $R$ of the RTD (which is usually chosen to be equal to the other resistors in the bridge).

Therefore, although the presence of lead resistances introduces a static offset in the output, this offset can be measured and corrected — either by adjusting the bridge balance or by compensating in software during post-processing.

In summary, when the RTD is connected with long leads, the Wheatstone bridge can still be used effectively, but calibration becomes essential to remove the systematic error introduced by the parasitic resistances of the connecting wires.

![[Pasted image 20251009185710.png]]


To reduce the error introduced by the lead resistances in the two-wire configuration, we can add an additional wire and obtain a three-wire Wheatstone bridge. In this case, we measure the differential output voltage of the bridge using a third wire, labeled as wire C. This additional wire is connected to the point where the voltage $V^+$ is sensed.
![[Pasted image 20251009185930.png]]
In this new configuration, $V^-$ remains unchanged — it is still equal to one half of the supply voltage. However, when computing $V^+$, we now consider that only one of the lead resistances affects the measurement. This happens because the resistance of wire C does not influence the voltage reading: even though wire C has its own resistance, it is connected to the high-impedance input of the instrumentation amplifier. As a result, no current flows through this wire, and therefore, there is no voltage drop across its resistance.
![[Pasted image 20251009190236.png]]
Consequently, in the numerator of the voltage divider that defines $V^+$, we only need to include the resistance of one lead (the resistance of wire B) together with the RTD resistance. On the other hand, in the denominator, we still have to consider both lead resistances (the ones from wires A and B).

![[Pasted image 20251009213555.png]]

Now, if we calculate the error for this three-wire configuration — the one that includes the additional curved wire — we can proceed exactly as before. We compare the actual output voltage obtained with the three-wire setup to the ideal voltage calculated previously, where the lead resistances were assumed to be zero. After carrying out the algebra, such as finding a common denominator and simplifying the expression, we arrive at the formula for the new error.

Again, by observing the result, we can simplify it further because the term $\Delta R$ is much smaller than $2R$. Therefore, $\Delta R$ can be neglected in both places where it appears in the expression. After simplification, we notice that the sign of this error is opposite to that in the two-wire bridge case. However, this difference in sign is not relevant, since what matters is the magnitude of the error — whether it increases or decreases the output voltage slightly is not important.


| Error from two-wire bridge           | Error from three-wire bridge         |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251009213710.png]] | ![[Pasted image 20251009213721.png]] |

In this case, the error depends on ΔR, which makes calibration a bit more complex. But looking closely at the expression, we can see that the first part of the error is the same as the one obtained for the two-wire bridge. The difference is that now it is multiplied by a factor of $\Delta R$ divided by $2R$. Because $\Delta R$ is much smaller than $2R$, this factor is much smaller than 1, which means the resulting error is nearly zero. In practice, this error becomes so small that it is typically negligible compared to the noise level of the system.

To summarize, the Wheatstone bridge configuration offers a key advantage: it provides a differential measurement, so the output depends only on $\Delta R$ — the variation in resistance — and not on the fixed lead resistance $R_L$​. This allows us to use an amplification stage with much higher gain compared to the single-ended approach, resulting in more accurate detection of the small resistance changes that correspond to temperature variations.

## <span style="color:rgb(239, 179, 1)"> Self Heating</span>

When we use resistive sensors to measure temperature, we have to consider an unwanted effect called **self-heating**. Self-heating occurs because, whenever a current passes through a resistor, it dissipates power and generates heat. If the current is too high, the heating caused by the current itself can be larger than the actual temperature change we want to measure — that is, the heating can dominate over the environmental or object temperature variation.

As a general guideline, the current through an RTD is typically limited to a maximum of around **1 mA**. However, this value is not universal for all RTDs. Thin-film RTDs, which are made using photolithographic processes, are more sensitive to self-heating, so it is better to keep the current well below 1 mA. Wire-wound RTDs, being more robust, can typically tolerate currents up to 1 mA or slightly higher. Datasheets for specific sensors usually provide recommended current limits.

It is also worth noting that self-heating can sometimes be used **advantageously**. By monitoring the change in resistance caused by self-heating, it is possible to estimate the current flowing through the resistor. This principle is exploited in certain applications, and we will see examples of this when we study **thermistors**, which are also resistive temperature sensors. Like RTDs, thermistors experience self-heating, but in some cases this effect can be deliberately used to our benefit.

## <span style="color:rgb(239, 179, 1)">Pros and Cons of RTDs</span>

### <span style="color:rgb(161, 40, 226)"><b>Advantages:</b></span>

- **High linearity:** As we saw, platinum RTDs show an almost perfectly linear relationship between resistance and temperature over a wide range — approximately from **−200°C to +700°C**.
- **High accuracy and repeatability:** RTDs provide very precise and consistent measurements.
- **Good sensitivity:** They can detect small changes in temperature effectively.
- **Moderate cost:** RTDs are relatively affordable considering their performance.
    

### <span style="color:rgb(161, 40, 226)"><b>Disadvantages:</b></span>

- **Limited measuring range:** Although a range from **−200°C to +800°C** is sufficient for most applications, it may not be enough for very high-temperature environments — for example, in processes exceeding 1000°C.    
- **Need for external power:** Unlike some other temperature sensors, RTDs require an external power source. In single-ended circuits, a current source is needed, and in differential (Wheatstone bridge) configurations, a supply voltage **Vs** is required.
- **Slow response time:** RTDs tend to respond slowly to temperature changes because not only the resistive element but also its insulating parts (like the ceramic mandrel in wire-wound RTDs) must reach thermal equilibrium.
- **Self-heating:** As discussed, the current passing through the resistor can cause self-heating, which introduces measurement errors — a common issue with all resistive temperature sensors.

## <span style="color:rgb(239, 179, 1)">RTD Applications</span>

RTDs are mainly used in situations where **precise temperature measurement** is required within a **limited temperature range**. Some of the most common applications include:

- **Air conditioning and refrigeration systems:** RTDs are ideal for monitoring temperatures around room temperature, ensuring accurate climate control.
- **Food processing:** They are used to monitor and regulate temperatures during cooking, storage, or preparation, where temperatures typically range up to 100–200°C.
- **Household appliances:** RTDs are commonly found in **stoves, ovens, and grills**, providing precise control of heating elements.
- **Plastic material processing:** These applications do not require extremely high temperatures, making RTDs suitable for controlling the heating phases during molding or extrusion.
- **Microelectronics:** RTDs can be used to monitor and stabilize the **temperature of electronic circuits**, preventing overheating and ensuring performance stability.
- **Measurement of air, gases, and liquids:** RTDs are also used to monitor environmental or process conditions in systems where accurate fluid temperature measurement is essential.

# <span style="color:rgb(223, 109, 109)">Thermistors</span>

![[Pasted image 20251010214555.png]]
Let’s now move to the second type of resistive temperature sensors — the **thermistors**. Like RTDs, thermistors are **resistive temperature sensors**, but they differ mainly in the **materials used for their fabrication**.

While **RTDs are made of metallic materials**, **thermistors are typically made from ceramic materials**. This difference in material composition leads to a fundamental difference in behavior: thermistors exhibit a **strongly nonlinear relationship between resistance and temperature**, unlike the nearly linear response of RTDs.

Thermistors are generally classified into two main types:

1. **NTC thermistors (Negative Temperature Coefficient):**  
    These are usually made from **ceramic semiconductors composed of metal oxides**. Their resistance **decreases as temperature increases**, meaning they have a **negative temperature coefficient**.
    
2. **PTC thermistors (Positive Temperature Coefficient):**  
    These are typically made from **polycrystalline ceramic materials**. In contrast to NTC thermistors, their resistance **increases as temperature increases**, giving them a **positive temperature coefficient**.
    

In both cases, thermistors exhibit **strongly nonlinear characteristics**, which is one of the main distinctions between thermistors and RTDs.

## <span style="color:rgb(239, 179, 1)">NTC Thermistors</span>

Let’s now take a closer look at **NTC thermistors**.

As mentioned earlier, NTC thermistors are made from **metal oxides**, typically oxides of **manganese, nickel, cobalt, iron, copper, or aluminum**. These materials give the thermistor its characteristic **negative temperature coefficient**, meaning the resistance decreases as temperature increases.

NTC thermistors are available in a variety of **package types**, such as **disk**, **bead**, **chip**, or **surface-mount devices (SMDs)** that can be directly soldered onto printed circuit boards (PCBs).
![[Pasted image 20251010215150.png]]

- **Large disk NTCs** are often used in applications that exploit **self-heating**, where the temperature rise due to power dissipation is intentional. In these cases, the variation in resistance is used to monitor or control the **power (or current)** flowing through the device.
    
- **Bead, chip, and SMD NTCs**, on the other hand, have **smaller packages** and are more sensitive to the **ambient or contact temperature**. These are commonly used for measuring the temperature of the **environment** or the **object** they are in contact with.

### <span style="color:rgb(161, 40, 226)">NTC Characteristic</span>

![[Pasted image 20251010215241.png]]
As you can see, the **characteristic curve of an NTC thermistor** is **strongly nonlinear**. It can be mathematically described by an **exponential decay equation**, where the resistance decreases exponentially as the temperature increases. In this equation, the $\beta$ (beta) coefficient is a constant that depends on the specific **material composition** of the thermistor — that is, on the type of metal oxide used.

Because of this nonlinear behavior, when using NTC thermistors to **measure temperature**, you need to **invert** the equation in order to calculate temperature from the measured resistance. This inversion isn’t straightforward to do analytically, so in practice it’s often handled using **microcontrollers or computational devices** capable of performing this calculation, or more simply, by using **lookup tables** that map resistance values to their corresponding temperatures.

### <span style="color:rgb(161, 40, 226)">NTC Applications</span>

The **main applications of NTC thermistors** are typically found in **low-cost temperature measurement systems**, since thermistors are **cheaper** than RTDs. However, because of their **nonlinear response**, they also offer **lower accuracy**, which makes them less suitable for precise temperature measurements.

In many cases, NTC thermistors are used for **temperature compensation** rather than for direct temperature measurement. This means they are integrated within **feedback control loops** where the goal is to **maintain a stable temperature**, rather than to know its exact value. For example, they are commonly used together with **thermoelectric coolers** (like **Peltier cells**) to stabilize temperature in sensitive electronic circuits. Such stability is essential for components like **oscillators**, where frequency depends on temperature, or for **LCD displays**, where brightness can vary with temperature.

Another application of NTC thermistors is in **fluid level detection**, where their **nonlinear resistance behavior** is exploited to act as a **switch or detector** — producing a noticeable change in resistance when the thermistor is surrounded by a fluid versus air.

![[Pasted image 20251010215855.png]]

Finally, NTCs are also used by taking advantage of the **self-heating effect**, particularly in **inrush current limiters**. In this application, an NTC is placed in series with the circuit (for instance, with a motor). When the circuit is first powered on, the NTC is **cold**, so its resistance is **high**, which limits the inrush current. As current starts to flow, the thermistor heats up, its resistance **decreases**, and it eventually allows **normal current flow** once the system reaches a steady state. In this way, the NTC protects the circuit during start-up without affecting normal operation later.

## <span style="color:rgb(239, 179, 1)">PTC Thermistors</span>

![[Pasted image 20251011135326.png]]
 
 Now let’s take a closer look at **PTC thermistors**, or **Positive Temperature Coefficient thermistors**.

As mentioned before, PTCs are made of **polycrystalline ceramic materials**, typically composed of **oxalates or carbonates** mixed with **doping elements** that modify their electrical behavior. These materials give PTC thermistors a **strongly nonlinear resistance–temperature characteristic**.

| Before Curie Temperature             | After Curie Temperature              |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251011135407.png]] | ![[Pasted image 20251011135448.png]] |
If you look at the graph (on the left), you can see that over a **certain temperature range**, the **resistance changes only slightly** as temperature increases — and these variations are sometimes **non-monotonic**, meaning the resistance might first decrease and then slightly increase again. However, once the temperature reaches a specific **threshold point**, known as the **switching point**, the resistance **rises very sharply**.

This rapid change happens (on the right) over a **very narrow temperature range**, where the resistance can increase by **orders of magnitude**, even with a small temperature change. The temperature at which this sudden rise begins is called the **Curie temperature (Tc)**. By definition, Tc is the temperature at which the resistance value becomes **twice the minimum resistance** observed before the sharp increase.

Because of this behavior, PTC thermistors are very useful as **switch-like temperature sensors**. Below the Curie temperature, their resistance remains **low**, allowing current to flow easily. Once the temperature **exceeds Tc**, their resistance becomes **very high**, effectively **limiting the current** or acting as an **automatic cutoff**. This makes them ideal for applications where you want to detect or control whether a system has **exceeded a certain temperature threshold** — essentially working as **on/off temperature switches**.

### <span style="color:rgb(161, 40, 226)">PTC Applications</span>

#### <span style="color:rgb(2, 141, 192)">Overcurrent Protection (Polyfuse)</span>
Another common application of **PTC thermistors** is in **overcurrent protection**. This function is crucial to prevent **damage to sensitive or expensive equipment** and to ensure the **safety of electronic circuits** when abnormally high currents occur.

Traditionally, this protection is achieved using **fuses**. A fuse behaves as a **short circuit** under normal conditions but becomes an **open circuit** when excessive current flows through it, effectively cutting off the current. However, once a fuse blows, it must be **replaced**.


| Normal Operation                     | Overcurrent                          |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251011140224.png]] | ![[Pasted image 20251011140300.png]] |


A **PTC thermistor**, on the other hand, can be used to create a **reversible fuse**, often called a **polyfuse**. Imagine placing a PTC thermistor **in series** with the circuit you want to protect.

- Under **normal operation**, the current is moderate, and the PTC remains relatively cool. Its resistance stays **very low**, allowing current to pass freely to the circuit.
- If an **overcurrent** occurs — for example, due to a fault in the power supply — the higher current causes **self-heating** in the PTC.
- As the temperature of the PTC rises and exceeds the **Curie temperature (Tc)**, its resistance increases **drastically**, effectively becoming **almost an open circuit**.

This sudden increase in resistance **limits the current** and prevents it from damaging the protected circuit. Since the voltage at the node rises as resistance increases, the **current source can no longer maintain the same current flow**, thereby reducing power dissipation in the protected components.

Unlike a traditional fuse, a **PTC-based polyfuse is self-resetting**. Once the fault is cleared and the current decreases, the PTC cools down, its resistance **returns to its low value**, and the circuit resumes **normal operation** — without the need to replace any components.

#### <span style="color:rgb(2, 141, 192)">Battery Management</span>

![[Pasted image 20251011140832.png]]

Another typical application of **PTC thermistors** is found in **battery management systems**. In these circuits, it is important to **control the charging current** according to the state of the battery — providing **high current** when the battery is nearly empty and **lower current** as it approaches full charge.

Here, the PTC thermistor can act as a **self-regulating element**. When the battery is first connected for charging, the **temperature of the system is low**, and consequently, the **resistance of the PTC is also low**. ==This allows a **high charging current** to flow==, which is desirable for quickly restoring the battery’s charge in the initial phase.

As charging continues, the **temperature of the circuitry increases**, partly due to self-heating and partly because of the energy conversion processes inside the battery. When this happens, the **resistance of the PTC rises**. As a result, the **current flowing into the battery automatically decreases**, preventing overheating and **protecting the battery from overcharging**.

This self-regulating behavior makes PTC thermistors particularly useful in **simple and low-cost battery management designs**, where they can provide **automatic current control** without requiring complex active regulation circuits.

## <span style="color:rgb(239, 179, 1)">Pros and cons of Thermistors</span>

To summarize, **thermistors** present both clear advantages and limitations when used as temperature sensors.

### <span style="color:rgb(161, 40, 226)">Advantages</span>
- **High sensitivity** — particularly in **PTC thermistors**, where the sensitivity is so strong that they can operate effectively as **switching sensors**, behaving almost like on/off devices.
- **Low cost** — thermistors are **cheaper than RTDs**, making them attractive for many practical applications.    
- **Strong signal response** — their non-linear behavior can actually be beneficial in **control and feedback loops**, where a large change in resistance for a small temperature variation makes the system’s response more robust and easier to detect.

### <span style="color:rgb(161, 40, 226)">Disadvantages</span>
- **Narrow operating temperature range**, typically around **–100°C to 500°C** for **NTCs**, and even more limited for **PTCs**, which work best near their **Curie temperature**.
- **Low long-term stability** and **high nonlinearity**, meaning that precise temperature measurements are more difficult compared to RTDs.
- **Only fair accuracy and response time**, suitable for many practical but not high-precision applications.
- **Self-heating issues**, common to all resistive sensors — although, as seen, in certain cases this effect can be **intentionally exploited** for specific applications like inrush current limiting or fluid detection.


So, this concludes the discussion on **resistive temperature sensing methods**.  
In the next class, we’ll explore **other approaches for temperature measurement**, focusing on **thermocouples**, **diode-based sensors**, **bandgap temperature sensors**, and **infrared thermometers**.

**Thank you for your attention — see you next time!**







