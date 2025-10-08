
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

$$
\alpha = \frac{(R_{100} - R_0)}{100 \cdot R_0} = \frac{S}{R_0} \left(\frac{\Omega}{^\circ C \cdot \Omega} \right)
$$

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

34:37



Then we can do the common denominator here and we obtain this simplified equation. This equation can be far simplified if we consider that delta R is always much smaller than the Rx0. and also of r1 that is typically the same order of magnitude of rx0 or as we will see in a while it is chosen to be equal to rx0. So considering so that here the numerator delta r is much smaller than the denominator r1 plus rx0 we can consider that this part this contribution is almost zero. And so this equation can be simplified and become this one, in which you see that the output is directly related to the delta R. We know that delta R can be written as alpha, so the temperature coefficient, multiplied by the nominal resistance, so Rx0, and then multiplied by the variation of temperature. And so we can rewrite the equation in this way substituting instead of delta R, alpha Rx0 delta T. And so we clearly see that there is a linear dependence between Vout and delta T. And furthermore, we see that all of this part is a constant value because Vs is the supply voltage which is fixed, the resistance R1, the nominal resistance and the coefficient α are fixed coefficients, so we can say that Vout is directly proportional with a certain coefficient k. Differently from the single-ended circuits we don't have plus something. So we just have a relation between, so the devout is only related to the delta t, so to the delta r also. And this is a big advantage of the differential approach. In fact in this case having a voltage, a differential voltage at the input of the instrumentation amplifier that depends only on delta t Even if we will have very small voltages here, because the variation of delta R due to the variation of temperature are expected to be small, we can apply a gain of the ENA which is high enough to provide an output voltage from the ENA which can be quantized easily by an ADC, so can be easily measured. Ok, just a last notice: how to size R1 and then R2 and also R3? So we already said that we have to respect this equality in order to have an output which is independent from Rx0, which depends only on the delta T. So we decide, for instance, to take R1 equal to R2 and R3 equal to Rx0. But if we want to maximize the Vout in respect to the variation of temperature, we can do the derivative of this equation in order to find where is the maximum and we will discover that the maximum can be found when R1 is equal to R2 equal to R3 and equal to Rx0. So when we keep the constant resistor, R1, R2, R3 to be equal to the nominal value of the RTD. And in this case, so we can simplify our equation because R1 is equal to Rx0 and so we obtain this final equation in which Vout is equal to 1/4 delta R over Rx0 multiplied by Vx. Be careful because the ratio delta R divided by Rx0 is expected to be a small ratio, so if you want to have a Vout, so a voltage at the input of the instrumentation amplifier that is at least equal but higher than the noise that we expect from this resistance, we have to select a Vs that is high enough to have a signal strong enough at the input of the instrumentation amplifier because if the signal that you provide at the input of the instrumentation amplifier is lower than the noise or similar to the noise you can even apply a big gain at the instrumentation amplifier but you will amplify the noise together with the signal and so the signal to noise ratio must be high enough also before the instrumentation amplifier. Then also with the Wheatstone bridge you can have the issue related to the Leeds resistance in the case the RTD is far away in respect to the remaining part of the Wheatstone bridge. So imagine to have in this case, which have the free resistor of the Whiston bridge that I kept of the same value as seen in the slide before, which are far away in respect to the RTD. So you need this long wiring to connect the RTD. Okay, also in this case, we will have some stray resistance associated to the link. So ideally, if we consider the lead resistance to be equal to zero, the output voltage in this case, the output voltage, I mean the output voltage of the of the wisdom bridge will be given by the difference as we said before V plus minus V minus. So it will be equal to Vs multiplied by the voltage divider of the branch with the RTT minus the voltage divider in the branch without the RTT that provides you this minus one alpha. So this is expression of the ideal Vout considering the lead resistance to be equal to zero. If we instead also consider the contribution of RL, you see that here to R plus delta R which is equal to to the resistance of the RTD, so I consider the resistance of the RTD equal to R plus delta R, I have to add also the contribution of the two lead resistances. It appears in the equation also this contribution plus 2 RL. So this is the output voltage that we will really measure if we consider also the two lead resistances. We can compute which is the error that I call epsilon between the measurement that we do with a little resistance, so Vout to wire, in respect to the ideal Vout that I should see if the resistance of the lead, the straight resistance, is equal to zero. So I can simply do the difference between Vout to wires that I computed here minus the ideal Vout that I computed there. Okay, so doing some computation, common denominator and so on, we obtain this equation. That can be simplified if you consider that the delta R is very small in respect to 2R, to the nominal resistance, so I can consider this to be almost zero. And also in this part, since delta R is summed to 2R, delta R can be neglected. So neglecting this delta R which are summed to a much bigger resistance, we obtain this equation in which we see that the error epsilon is independent from delta R and this is good because it means that it can be compensated with a calibration and its value mainly depends on the supply voltage and on the lead resistance and also on the nominal value of your RTD which is equal to the value that we choose for the other three resistances. How can we decrease this error? So how can we proceed if we want to have an error that is smaller than this that we obtain with a simple two-wire configuration? Ok, we can do something similar to the lesson we learned for the single-ended approach. So to use an additional wire and we can obtain this Whiston bridge with three wires. So in this case you see we read the differential voltage of the Whiston bridge with a V+ that is kept with the third additional wire, wire C. So, also in this case we can compute which is the voltage that we obtain at the output of the Whiston bridge, so which is the voltage V+ minus V-. So obviously V- is unchanged, so it is still 1/2. Instead, for the voltage V+, we will have to consider at the numerator only the voltage that we have on the lead resistance and the resistance RTT, because the lead resistance of the wire C does not impact on our measurement because remember that even if we have here a lead resistance, we read out our voltage with an high impedance of the instrumentation amplifier and so we will have no current flowing in the input of the instrumentation amplifier and so no current, so this current is equal to zero in the lead resistance. So in this case instead of having 2 RL we have the contribution only of 1 RL so which is the lead resistance of the wire B. Instead, at the denominator I will have 2RL because I have to consider also the contribution of the lead resistance of the lead A. So, now if we try to compute the error in this case, so in the case in which we use this additional curved wire, We can proceed as we proceeded before, so computing the voltage difference of the output that we have in this free wire configuration in respect to the ideal voltage that we have computed here, considering the lead resistance to be equal to zero. Also in this case, doing some computation, common denominator and so on, we can arrive to this expression of the error. And also in this case we can do some simplification, so we see that delta R is negligible in respect to 2R and also here delta R is negligible in respect to 2R. So, simplifying the expression, we find this new expression. So first of all we can notice that the sign is different in respect to the two wire bridge but the sign mainly is not critical because this is an error introduced and it's not important if the error is positive so increase the output voltage or negative so you have a slightly decreased voltage. So we are mainly interested in the absolute value of this error. Ok, this time the error depends, actually depends on delta R, so calibration is more difficult, but if we look in detail we can notice that this first part of the error is exactly the same of the error that we obtained with the two bridge configuration. But then this error, the one of the 2-wire bridge configuration, is multiplied by this coefficient, delta_r over 2r, which is a coefficient which is much smaller than 1, because delta_r is much smaller than 2r. And so you see that overall this error is almost equal to 0, because this coefficient tends to 0. So in this case almost the calibration is not needed so this error is really a negligible error that is typically much lower than the noise level for instance. So, we have seen also this second important configuration which is the Whiston bridge. So please remember the main advantage of the Whiston bridge is that you have a differential approach and so your output will not depend on RL0 but it will depend just on delta R. And so we can use an amplification stage that that has a much higher gain in respect to the one that we can have in the single-ended approach. And so we can measure in a more accurate way the variation of the resistance, which depends on the variation of temperature. When we use resistive sensors in order to measure temperature, we have to consider that we have an unwanted effect, which is the self-heating. What is the self-heating? You know very well that when a resistance is crossed by a current, this current will heat the resistance itself because we dissipate power. So, if the current passing through the resistance is too high, then we could have an effect of self-heating, so heating due to the current passing through the resistor, that can be even higher than the variation of temperature that we have due to the variation of temperature of the ambient or the object that you are measuring. So typically a rule of thumb is to limit the current to a maximum value of 1 mA. But obviously this threshold is not universal and true for all the RTDs. So for instance for RTDs which are made with thin film, so the one with the photolithographic process and so on, these RTD are more susceptible to self-heating and so it's better not to exceed the 1mA but keep much lower than 1mA. Instead, the well-worn RTDs typically can dissipate more the heat and so we can also ride to 1mA or a little bit more. But typically you find this information on the datasheet of the sensor that you are buying. Ok, just a last notice, remember that sometimes instead self-heating is exploited as an advantage. So mainly we can use self-heating to have, so the variation of the resistance, to have a forced estimation of the current that is flowing inside the resistor itself. But we will see some examples of use cases in which we exploit self-heating as an advantage, especially a little bit later during this class when we will study the thermistors, which are still resistors that we use to measure temperature, and so they has RTDs they will experience the problem of self-eating. But we will see how with thermistors sometimes we exploit self-eating for some advantages in some particular application. So just to summarize which are advantages and disadvantages of RTDs. The main advantage of RTD is the high linearity. So remember the characteristics that we have seen for the platinum, that is a characteristic with a very extended range of linearity in temperature from about -200°C up to 700°C. Then for RTDs we have also very good accuracy, repeatability, so precision and we have quite high sensitivity and they can be found at a moderate price. The main disadvantage is that the measuring range is quite narrow. So measuring range from -200 to 800 is enough in many applications But it could be not enough, especially the high end, the 800 degree in some applications, so for instance inside even if you want to monitor temperature during some processes in which you need to exceed the 800 degree to thousands of degree. Then another disadvantage in respect to other temperature sensors that we will study during next class is that they require an external power supply, an external power source. So we have seen for the single-ended readout, for instance, we need to provide a current source and in the differential approach in the Whistler bridge we need the Vs, so the voltage supply. Another disadvantage in respect to other type of sensor is the quite slow response time because we have to heat the resistor, not only the resistor but only the insulating part, so for instance the ceramic mandrel for the wire wound approach. And then we have seen that the problem related to the self-heating which is a common problem to all the resistive sensors. Which are the main applications in which RTDs are used? Mainly when you want to precisely measure the temperature of an object in a limited range. So for instance for air conditioning and refrigeration service in which typical temperature across the room temperature. Also in food processing, in which you don't need to reach very very high temperature, but typically 100, 200 degree are enough. So for instance also for stoves and grills and also for the processing of plastic material, because for plastic material very high temperature are not needed. Instead if you want to process metallic materials, for instance, then you can reach high temperature. and then we use it in microelectronics, so sometimes to monitor the temperature of our circuits, and then we can use also to monitor the temperature of air, gas and liquids in general. Now let's move to the second type of resistive temperature sensor, which are the thermistors. So basically thermistors are resistive temperature sensor like RTDs but they differ from RTDs for the materials that are used to fabricate them. So if you remember RTDs were fabricated with metallic materials. Instead thermistors are mainly fabricated with ceramic materials. And the difference in the materials also then causes differences in the characteristics resistance versus temperature of RTDs in respect to the thermistors. And in particular we will see that thermistors have strongly nonlinear characteristics and this is the main difference in respect to RTDs. In particular, we can distinguish two basic types of thermistors: the NTC thermistors, so negative temperature coefficient thermistors, and the PTC thermistors, so positive temperature coefficient thermistors. These are mainly made with ceramic semiconductors that are typically metal oxides. they are characterized by the fact that they decrease in resistance as the temperature increases. So we have a negative temperature coefficient. Instead, PTC remistors are typically made with polycrystalline ceramic materials and they increase the resistance if the temperature increases. So they have a positive temperature coefficient. So typically for both NTC and PTC we have characteristics which are strongly nonlinear. So let's go a little bit more in detail about NTC thermistors. As I said before NTC are made with metal oxides, typically oxides of manganese, nickel, cobalt, iron, copper or aluminium. we can find NTC in different packages. So in particular we can have disk NTCs or bead or chip NTCs or surface mounting devices that you can directly solder on your PCB, on your printing circuit board. In particular large disk NTC are used to function to exploit the self-heating mode. So in those applications in which self-heating is the objective of your measurement. So for instance if you want to measure the variation of resistance due to the wattage, so due to the power dissipation. So, if you want to measure a value of the resistance which strongly depends on the current that is flowing in this resistance. Instead, bit cheaper SMD devices has a smaller package so they are more sensitive to the environmental temperature or to the object temperature in which they are in contact to. and so they are mainly used when you want to measure the temperature of the environment or of an object. As you see, the characteristic of the MTC is strongly nonlinear. In particular, it can be described by this equation, which is a decreasing exponential characteristic. in which this coefficient beta is a coefficient that depends on the material, so on the metal oxide that you are using. So if you want to use NTCs to measure a temperature obviously you will have to apply the reverse of this equation, so you need some devices with some computational capability to reverse this equation or you can use lookup tables in order to find the value of the temperature in respect to the measured resistance. Which are the main applications in which MTCs are used? Mainly they are used to measure temperature for low cost applications because thermistors are cheaper in respect to RTDs. But due to the non-linear characteristics also the accuracy is lower in respect to the RTDs. In many cases they are used for temperature compensation, so they are used inside the loop, in which we are not interested in the precise value of the temperature, because they are just used inside the loop as the feedback to control that the temperature is kept stable. So for instance we use NTC with thermoelectric coolers which are coolers that are used to keep a stable and cool temperature like with a Pelletier cell. Because for some circuitry, electronic circuitry, it's very important to have a very stable temperature. So for instance, it is important for oscillators to keep the oscillation frequency to be stable, or to LCD display to have intensity of the light to be stable, and so on. And sometimes we use it to monitor the level of a fluid. So we use more like a switch detector to see if the fluid exceeds a certain level or not. And so we exploit the nonlinear characteristic in order to have a huge difference in the value of the resistance in case you have the fluid or if you have a liquid or if you have a gas. Sometimes we use NTC exploiting the self-heating effect. In particular we exploit it when we want to do some inrush current limiter. So imagine to have your circuit and you want to provide a current to your circuit, can be for instance a motor, you want to provide some current to your motor, you can put in series this NDC you can provide then with your current supply a current but you don't want to have a too much high current at the inrush so when you start up for instance your motor that can require a very high quadrant but you could want to put a limitation so So at the beginning, so when your circuit is off, the temperature will be low and so your resistance NTC will have a high value of resistance because the resistance with temperature has an inverse proportionality. When you switch on your circuit, the current will start to pass to the resistance and so the resistance will heat and then the resistance value will start to decrease. And so at the steady state this resistance will be a low value resistance so it will offer any more limitation to the current. So this resistance will act only when the temperature is low, so at the start-up of your circuit, to limit the current. Okay, let's now analyze the PTC thermistors, so the positive temperature coefficient thermistors. As I said in the introduction, they are made with polycrystalline ceramic, so for instance composed of oxaliate or carbonate with some additional doping materials. PTC exhibit a very non-linear characteristic. As you see, in a certain range of temperature, like this one, we have a very reduced variation of resistance due to temperature variation and these variations are even not monotone, you see here we have decreasing in value and then increasing. But let's say these variations are very reduced, almost negligible, until we reach a switching point, so a point in which promptly and steeply the characteristics start to be very steep. So we have very huge variation in resistance of order of magnitude, so this is in a logarithmic scale, in a very reduced range of temperature. So even if you modify really a little bit the temperature, you will have a big modification in the value of the resistance. and the temperature corresponding to this switching point is called Tc, so it is called Curie temperature. And by definition the Curie temperature is the temperature at which the resistance reaches two times the minimum value of the resistance. So you see due to this very steep characteristic we can use PTC as let's say switching, so on/off sensors. So we we can use in those applications in which we want to monitor if we exceed a certain temperature, so the Curie temperature. If we don't exceed the Curie temperature, the value of the resistance is very low. If we exceed the Curie temperature, the value of the resistance will be very high. Another typical application of the PTC is to protect for overcurrents. So overcurrent protection is very important in order to avoid to damage some expensive instrumentation or in general to protect your circuit from very high currents. So sometimes in some instrumentation we put some fuse. A fuse is an element that normally is a short circuit but it becomes an open circuit when a too high current flows inside this component, inside the fuse. With a PTC we can make a reversible fuse, we call it polyfuse. So imagine to have your circuit here that you want to protect from high currents, then you can put in series a PTC. So if the current, so in the normal operation, so with a normal current, the PTC will not self-heat too much and so the value of the PTC will be very low and so your current can reach actually the circuit. If instead the current becomes too high due to some fault for instance in the supply that you are providing to your circuit the self heating will increase a lot the temperature of your PTC and if the temperature exceeds the Curie temperature the value of the PTC will become very high, so almost an open circuit. and so you prevent this current to reach your circuit. Because if this resistance becomes very high also the current source will not be able to still provide the current because this node will increase a lot in voltage. Differently from a normal fuse, in a normal fuse when a too high current crosses the fuse it becomes an open circuit and it is not reversible. Then in PTC if you reduce, so if you adjust the fault and you reduce the current, then the PTC does not have to be changed, but it naturally comes back to the low value of resistance. Another example of application is also for battery management. So inside the circuits for battery management, typically we want to provide high currents when your battery still have to be charged and low currents when the charge is almost completed. So typically when you connect your battery to be charged the temperature at the beginning is low and so we can provide this high current because we have low value of the PTC resistor and then when we reach instead a good charge the temperature of the circuitry start to increases and so the value of the PTC increase reduces the value of the current that we are injecting in our battery. So, just to summarize the advantages and disadvantages of thermistors. The main advantage is the high sensitivity, especially for the PTC is so high that we can use them as switching sensors, so either very low or very high value of resistance. Another advantage is that they have a very moderate price, so they are cheaper than RTDs. They can provide a robust signal because the sensitivity is very high. So for instance in feedback and loops for monitoring and controlling the temperature of something, having this nonlinear characteristics with a high sensitivity can be an advantage. The main disadvantage is that we can use them in a very narrow range, especially NTC can be used in a range between -100 up to 500 degrees. Instead for PTC the range is even narrower, so it's limited to stay close to the cooling temperature. Then the other disadvantage is that we have a very low stability and completely they are not linear sensors. The accuracy is fair and also the response time is fair. As RTDs they suffer from self-heating, but we have seen that in some applications we exploit the self-heating itself. So we concluded to analyze the resistive approaches during next class instead we will analyze other different approaches used to measure temperature and in particular we will focus on thermocouple, diode and bank temperature sensor and infrared thermometer. So thank you very much for your attention and see you in next class. Bye!



