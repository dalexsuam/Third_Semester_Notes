
16/10/2025

***

Today we will continue with the second part of the **temperature sensor** class.

In the previous lecture, we discussed **Resistance Temperature Detectors (RTDs)** and **Thermistors**.  
Today, we’ll analyze three new types of temperature sensors:

- **Thermocouples**
- **Diode and Bandgap Temperature Sensors**
- **Infrared Thermometers**

Let’s begin with **thermocouples**.
 
![[Pasted image 20251019085558.png]]
# <span style="color:rgb(223, 109, 109)">Thermocuples</span>

Thermocouples are sensors that exploit the **Seebeck effect**.  So, what is the Seebeck effect?

## <span style="color:rgb(239, 179, 1)">Seebeck Effect</span>

It’s the phenomenon by which we can **measure a voltage difference** across a material when a **temperature gradient** is applied to it.


![[Pasted image 20251019085625.png]]
Imagine we have a material with a **hot side** and a **cold side**.

At the hot side, the free charge carriers (for example, electrons) gain more energy due to the higher temperature.  These energetic carriers move toward the cold side, where their energy is lower.

As a result:
- The **hot side** ends up with fewer electrons.
- The **cold side** accumulates more electrons.

This difference in charge distribution creates a **voltage difference** between the two sides — the **Seebeck voltage**.  In this case, the voltage at the hot side is **higher** than the voltage at the cold side.

### <span style="color:rgb(161, 40, 226)">Seebeck Coefficient</span>

We define the **Seebeck coefficient** as the ratio between the change in voltage and the change in temperature across the material:
$$
S(T) = \frac{dV}{dT}​
$$
This coefficient describes the **sensitivity** of the conductor or semiconductor to temperature differences.

The **sign** of the Seebeck coefficient tells us about the type of charge carriers:

- **Negative sign (–)** → electrons are the main carriers.
- **Positive sign (+)** → holes are the main carriers.

Importantly, $S(T)$ depends on **temperature**, so it’s not a constant value.  
Therefore, to find the total voltage generated across a temperature range $T_0$ to $T$, we must integrate:

In the table below, you can see example values of Seebeck coefficients for different metals and alloys at 0 °C and 27 °C.  

![[Pasted image 20251019090739.png]]

In the table, you can see several examples of Seebeck coefficients for metallic or alloy materials such as **Al, Pt, Cu, Chromel,** and **Constantan**. The sign and magnitude of the Seebeck coefficient depend on the type of material and the temperature.  
For instance, **copper (Cu)** has **positive** Seebeck coefficient, while **aluminum (Al)**, **platinum (Pt)**, **chromel** and **constantan** exhibit **negative** ones. This means that for some materials the potential at the cold side is higher, while for others it is lower — a property determined by the nature of their charge carriers and band structure.

# <span style="color:rgb(239, 179, 1)">Thermocouple principle</span>

Okay, so let's try to understand now the thermocouple principle. In fact, as I said before, thermocouple exploits the Seebeck coefficient. Imagine to have just one material, so for instance an aluminium strip, and then you want to measure the voltage difference across this aluminium strip.

![[Pasted image 20251019092946.png]]

Then, so this is your aluminium strip, so the sensitive part, Then for sure you will have to connect with some leads, with some cables, your aluminium sensor to your sensing element, so for instance the differential amplifier, the instrumentation amplifier. If you use the same material for these leads of the sensing element, what we will measure at the at the instrumentational amplifier, will be a zero voltage at the output. Let's try to understand it better with some computation. 


![[WhatsApp Image 2025-10-19 at 10.13.20_3d1ca691.jpg]]
So we can define as $\Delta V_s$ the voltage across your sensing element. And then we can call $\Delta V_1$ and $\Delta V_2$ the voltage across your leads. 

The voltage across the sensor can be computed as:

$$\Delta V_s = \int_{T_C}^{T_H} S_{Al}(T) \, dT$$
where $S_{Al}(T)$ is the Seebeck coefficient of aluminum, which depends on temperature $T_C$ (Cold) and $T_H$ (Hot).

However, since both the **hot** and **cold** junctions are connected to the readout circuit through metallic leads (also made of aluminum in this case), the leads themselves will also experience a Seebeck effect.

For the first lead, we can write:

$$\Delta V_{1} = \int_{T_x}^{T_H} S_{Al}(T) \, dT$$

and for the second one:
$$\Delta V_{2} = \int_{T_C}^{T_x} S_{Al}(T) \, dT$$

If we add these two contributions:
$$\Delta V_{1} + \Delta V_{2} = \int_{T_C}^{T_H} S_{Al}(T) \, dT$$
which is **identical** to the voltage across the sensor, $\Delta V_s$.

Now, the voltage measured by the readout circuit ($\Delta V_out$) is given by:

$$\Delta V_{out} = \Delta V_s - (\Delta V_{1} + \Delta V_{2})$$

But since $\Delta V_s$, equals the sum of the two lead voltages, the result is:

$$\Delta V_{out} = 0$$

==So, if we use the **same material** for both the sensing element and the connection leads, the measured output voltage will always be **zero**, meaning we cannot detect any temperature difference.==

### <span style="color:rgb(161, 40, 226)"> How to build a real thermocouple sensor (why two different metals?</span>

If the sensing wire and the connection leads are the **same metal**, the Seebeck voltages produced in the leads cancel the sensor voltage and the readout sees **zero**.  To avoid that, the sensor junction must be made of **one metal** (the thermocouple “leg”) and the leads to the readout must be made of a **different metal**.

**Example setup:** sensor = **Al** (aluminium) at the hot/cold junction; leads = **Ni** (nickel) to the readout.
![[WhatsApp Image 2025-10-19 at 10.13.19_a573e31c.jpg]]

Write the contributions as integrals of the Seebeck coefficient S(T)S(T)S(T):

- Sensor (Al) voltage:
$$\Delta V_s=\int_{T_C}^{T_H} S_{\text{Al}}(T)\,dT$$
- Lead 1 (Ni) from readout temperature $T_x$ to hot $T_H$​:
    
$$\Delta V_{1}=\int_{T_x}^{T_H} S_{\text{Ni}}(T)\,dT$$

- Lead 2 (Ni) from cold $T_C$ to readout temperature $T_x$​:
$$\Delta V_{2}=\int_{T_C}^{T_x} S_{\text{Ni}}(T)\,dT$$

Measured output (readout sees sensor minus leads):

$$\Delta V_{\text{out}}=\Delta V_s - (\Delta V_{1}+\Delta V_{2})$$

Substitute the integrals and combine them:
$$\Delta V_{\text{out}} = \int_{T_C}^{T_H} S_{\text{Al}}(T)\,dT - \Big(\int_{T_x}^{T_H} S_{\text{Ni}}(T)\,dT + \int_{T_C}^{T_x} S_{\text{Ni}}(T)\,dT\Big)$$

The two $Ni$ integrals join into the integral from $T_C$​ to $T_H$​, so you get the compact result:

$$\boxed{  
\Delta V_{\text{out}} = \int_{T_C}^{T_H} \big( S_{\text{Al}}(T) - S_{\text{Ni}}(T) \big), dT  
}$$
==This is the key point: the readout depends on the **difference** of Seebeck coefficients integrated over the temperature range. If the metals are different, that difference is non-zero and you measure a voltage proportional to the temperature difference.

### <span style="color:rgb(161, 40, 226)">Practical remarks (brief)</span>

- Thermocouples are always made of **two different metals/alloys** (a pair) for exactly this reason.
- Different material pairs give different sensitivity and temperature range

## <span style="color:rgb(239, 179, 1)">Thermocouple structure</span>

![[Pasted image 20251019102404.png]]
Okay, so this is the basic principle of a **thermocouple**. To create a thermocouple, we need **two sensing elements** made of **different materials**, each characterized by a different Seebeck coefficient.

Typically, the second material is **not** the wire used to connect the sensor to the readout circuit. This is important because otherwise the **sensitivity** of the thermocouple would depend not only on the sensing junction but also on the type of wire used for the connections — which would make the measurement unreliable.

For this reason, a real thermocouple is implemented using **two distinct metals or metal alloys**, which we can call **metal A** and **metal B**.  

These two metals are joined at the point where we want to measure the temperature, and the other ends are connected to a **reference junction** at a known temperature $T_R$​.

![[Pasted image 20251019102620.png]]

Then, to interface the thermocouple with our **readout circuit** (for example, an instrumentation amplifier), we can use regular **copper wires** or other materials — these will not affect the measurement as long as both leads are made of the same material and experience the same temperature gradient.

Let’s compute the measured voltage ΔVmeas\Delta V_{\text{meas}}ΔVmeas​ at the input of the readout circuit.  

Applying Kirchhoff’s law, we can express it as:

$$ \Delta V_{\text{meas}} = (\Delta V_{\text{1}} + \Delta V_B) - (\Delta V_A - \Delta V_{\text{2}})$$

Since **lead 1** and **lead 2** are made of the **same material** and both experience the same temperature gradient (between $T_R$​ and $T_X$​), their contributions cancel out:

$$\Delta V_{\text{1}} = \Delta V_{\text{2}} \Rightarrow \text{they cancel out.}$$

Therefore, the measurable voltage depends only on the two metals A and B:

$$\Delta V_{\text{meas}} = \Delta V_B - \Delta V_A$$

Now, recalling the definition of the Seebeck coefficient:

$$\Delta V_B = \int_{T_R}^{T_M} S_B(T)\,dT, \quad \Delta V_A = \int_{T_R}^{T_M} S_A(T)\,dT$$

Substituting these expressions, we obtain:

$${ \Delta V_{\text{meas}} = \int_{T_R}^{T_M} \big(S_B(T) - S_A(T)\big)\, dT }$$

We can define the **sensitivity of the thermocouple** as:

$$S_{AB}(T) = S_B(T) - S_A(T)$$
Hence, the output voltage is proportional to the **temperature difference** between the **measuring junction** ($T_M$) and the **reference junction** ($T_R$​), weighted by the **difference in Seebeck coefficients** of the two materials.

This is the fundamental operating principle of a **thermocouple sensor**.

![[Pasted image 20251019112054.png]]

Now, in this table, you can see the **most common types of thermocouples** — for example, **J, K, T, E**, and others.

The **main difference** between these thermocouples lies in the **combination of metals or metal alloys** used to form their two sensing elements.

- **Type J**: Iron – Constantan
- **Type K**: Chromega – Alomega
- **Type T**: Copper – Constantan
- **Type E**: Chromega – Constantan
    
- _(and others such as type N, R, S, B, each with specific materials)_
    

Because each pair of metals has a **different Seebeck coefficient**, each thermocouple exhibits distinct characteristics in terms of:

- **Sensitivity and linearity** of the voltage–temperature response.
- **Operating temperature range.**

==One of the key advantages of thermocouples is their **very wide measurement range**.  
As you can see, some thermocouples can measure temperatures **well above 2000 °C**, which is **far beyond the range** of most other temperature sensors such as RTDs or thermistors.

This makes thermocouples particularly suitable for **industrial and high-temperature applications**.

## <span style="color:rgb(239, 179, 1)">Thermocouple Linearity</span>
![[Pasted image 20251019112340.png]]

Regarding **linearity**, we can look at this graph, which shows the difference in Seebeck coefficients, **Sb − Sa**, representing the **sensitivity of the thermocouple**.

From the graph, we can see that the sensitivity depends on the type of thermocouple. Some thermocouples, like the **J-type** or **K-type**, have a sensitivity that remains fairly constant over a certain temperature range. Others show a strong dependence of sensitivity on temperature.

Since the sensitivity is not always constant, the thermocouple’s **output voltage does not change linearly with temperature**. Therefore, a **calibration** is needed to convert the measured voltage into the correct temperature.


## <span style="color:rgb(239, 179, 1)">Reference Junction</span>

An important point about thermocouples is that the **output voltage depends on the temperature difference** between the point we want to measure ($T_M$) and the **reference temperature** ($T_R$). This means we don’t measure the absolute temperature directly, only the temperature **relative to the reference**.

So, how can we get the **absolute temperature**? There are mainly two approaches:
![[Pasted image 20251019113850.png]]
1. **Fixed reference temperature**:  
    If the reference junction is kept at a well-known, fixed temperature, we can determine the absolute temperature. A classic example is placing the reference junction in an **ice-water bath**, which keeps it at 0°C. While accurate, this method is **not very practical**.

![[Pasted image 20251019113957.png]]

2. **Reference junction compensation**:  
    Instead of a fixed reference, we measure the temperature of the reference junction using another **temperature sensor** (like an RTD or thermistor). Then, the thermocouple measures the voltage difference between the object and the reference junction. By combining these two measurements, we can calculate the absolute temperature of the object.
    
You might ask: why not just use the temperature sensor directly to measure the object? The answer is the **temperature range**. Thermocouples can measure very high temperatures (e.g., 1000°C), where most sensors like RTDs cannot safely operate. So, ==we can measure the reference junction at a safe, ambient temperature using an RTD and use the thermocouple to measure the difference between the reference and the high-temperature object. This allows us to determine the absolute temperature safely and accurately.==


## <span style="color:rgb(239, 179, 1)">Types of Thermocouples and Readout Circuits</span>

### <span style="color:rgb(161, 40, 226)">Types of Thermocouples</span>
There are different types of thermocouples, depending on whether the tip is **protected with a cap** or **exposed**, meaning without any protective covering. The most common types are **insulated** or **grounded thermocouples**, both of which have a cap to mechanically protect the thermocouple wires from the external environment.
![[Pasted image 20251019115232.png]]


The advantage of having this protective cap is that the thermocouple becomes more robust and resistant to mechanical damage. However, compared to exposed thermocouples, this comes with a drawback: the **temperature response is slower**. This is because the cap must first reach thermal equilibrium with the object before the thermocouple wires can register the correct temperature. As a result, the **sensor bandwidth is reduced**, and it takes longer for the measured temperature to stabilize.

![[Pasted image 20251019115244.png]]
On the other hand, with an **exposed thermocouple**, the transient response is much faster because there is no cap to heat up first. The thermocouple wires are in direct contact with the object, so the measured temperature stabilizes more quickly.


### <span style="color:rgb(161, 40, 226)">Electrical Connection</span>

When considering the **electrical connection** of a thermocouple, we can distinguish between insulated and grounded types.

![[Pasted image 20251019115232.png]]
- In an **insulated thermocouple**, the protective cap electrically separates the thermocouple from the object being measured. Imagine placing the thermocouple near the object; the cap ensures that there is no electrical contact between the object and the thermocouple tips.

![[Pasted image 20251019115825.png]]
- In a **grounded thermocouple**, the situation is different. When the cap comes into contact with the object, it reaches the same electrical potential as the object and is also connected to the central node of the thermocouple. This creates a direct electrical connection between the thermocouple and the object. The same applies to **exposed thermocouples**, which are in direct contact with the object. In terms of electrical behavior, grounded and exposed thermocouples are effectively the same: the central node of the thermocouple sits at the same voltage as the object.


### <span style="color:rgb(161, 40, 226)">Readout Circuit</span>

Because of these differences, the **readout circuit** used for insulated thermocouples cannot be the same as the one used for grounded or exposed thermocouples. 


| Insulated Termocouple                | Readout Circuit                      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251019120307.png]] | ![[Pasted image 20251019120503.png]] |


For insulated thermocouples, the central node is floating, and the **common-mode voltage** between the two wires is not fixed. Although the thermocouple generates a differential voltage (ΔV), the common-mode signal can vary, so we need a circuit that uses grounding to stabilize the common-mode voltage between the two wires. In this setup, we can measure zero volts at the minus terminal and ΔV at the plus terminal.

For grounded or exposed thermocouples, using the same circuit would be dangerous. If the object is at a non-zero voltage, connecting it directly could create a short circuit between the object voltage (for example, 3 V) and the ground, resulting in a high current flowing through the thermocouple wires and potentially damaging the system. 

| Grounded or Exposed Thermocouples    | Readout Circuit                      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251019120633.png]] | ![[Pasted image 20251019120654.png]] |
Therefore, for grounded or exposed thermocouples, we use a readout circuit that does not impose a fixed common-mode voltage because the object itself defines it. In this configuration, the measured voltages are approximately $V0 + ΔV/2$ and $V0 − ΔV/2$, where V0 is the object voltage. The exact split can vary slightly due to differences in the Seebeck coefficients of the two wires, but the principle remains the same.

![[Pasted image 20251019121028.png]]

If a readout circuit needs to be compatible with **both insulated and grounded/exposed thermocouples**, we can use a third type of circuit. This circuit introduces a **high-value resistor in series with the grounding**.

**For an insulated thermocouple:**  
The thermocouple tip is electrically isolated from the object, so both terminals are **floating relative to the readout circuit**. In this case, the series resistor allows us to **artificially fix the minus terminal at 0 V** without creating a short circuit, because no current can flow through the isolated tip. Once the minus terminal is anchored at ground, the **full thermocouple voltage appears across the terminals**. As a result, the positive terminal measures the **differential voltage** $\Delta V$ generated by the thermocouple, while the negative terminal sits at **0 V**. This setup ensures that the readout circuit can safely and accurately capture the thermocouple signal.

**For a grounded or exposed thermocouple:**  
Here, the thermocouple tip is already at the same voltage as the object, which means there is a **fixed common-mode voltage**. Connecting it directly to a standard readout circuit could be dangerous, as it would create a large current if the object voltage is nonzero. However, with the **series high-value resistor**, a small current flows from the object to the readout circuit ground, but the resistor **limits this current to a safe level**, preventing damage. Meanwhile, the differential voltage $\Delta V$ is still accurately measured.

This design is therefore **universal**:

- For insulated thermocouples, the minus terminal is grounded through the resistor, producing $0 \mathrm{V}$ at the negative pin and $\Delta V$ at the positive pin.
    
- For grounded or exposed thermocouples, the resistor limits current while allowing the circuit to read the differential voltage without shorting the object.
    

This approach allows a **single readout circuit** to work safely and effectively with **both insulated and grounded/exposed thermocouples**, without risking a short circuit or measurement errors. Essentially, the series resistor acts as a **buffer**, providing grounding for insulated thermocouples while limiting current for grounded/exposed types.

A final important point: when using grounded or exposed thermocouples, you must ensure that the object voltage V0 is **within the common-mode input range** of your instrumentation amplifier. For example, if the object is at 100 V, it could damage the readout circuit. In practice, V0 should be within a few volts of the amplifier’s acceptable range to ensure safe operation.


## <span style="color:rgb(239, 179, 1)">Measuring Circuit Example 1</span>

![[Pasted image 20251019123047.png]]
Let’s now look at an example of a **thermocouple readout circuit**. As I have mentioned several times during this class, **instrumentation amplifiers** are typically used for reading thermocouple signals.

Here, we see an instrumentation amplifier from **Analog Devices**. However, the circuit is not just the amplifier itself; it also includes **resistors and capacitors at both the input and output** to implement filtering.

==At the **output**, there is a filter designed to reduce 50 Hz interference. For instance, the filter consists of a **1 μF capacitor** and a **100 kΩ resistor**, which creates a pole at **1.6 Hz**. This ensures that the 50 Hz power-line noise is effectively attenuated before the signal reaches the output.==

At the **input**, there is another set of filters designed to reduce **radio frequency (RF) interference**, which is a common problem with thermocouples. This happens because the two thermocouple wires form a loop when connected to the readout circuit, which can easily pick up electromagnetic interference from the surrounding environment.

To understand the behavior of these filters in detail, we can simulate the circuit using **PSPICE**. This allows us to analyze how both the input and output filters affect the thermocouple signal and ensure that unwanted noise is minimized while the actual temperature signal is preserved.

### <span style="color:rgb(161, 40, 226)">Differential Mode</span>

![[Pasted image 20251019123320.png]]

Let’s now focus on the effect of the **input filters on the differential signal**. The differential signal is the **signal of interest** because the thermocouple produces a voltage between its two wires, which we denote as $\Delta V_\text{in}$​. This is the signal we ultimately want to measure.

![[Pasted image 20251019123357.png]]
When we simulate the **transfer function between the differential input** and the **differential voltage at the instrumentation amplifier input**, we observe a **single-pole behavior**. In particular, a **pole appears at around 758 Hz**. This pole arises from the combination of the capacitors $C_1, C_2, C_3$​ and the resistors in the input circuit. Let’s analyze this in more detail.

![[Pasted image 20251019123714.png]]
We can **redraw the input stage** for clarity. To study the pole, we can switch off the input generator, effectively replacing it with a wire. The relevant components are:

- Resistors$R_1, R_2$​ and $R_3$​
- Capacitors $C_1, C_2, C_3$​
    
Because we are analyzing the **differential signal**, the circuit is symmetric. This allows us to simplify $C_1$ and $C_3$ as **series capacitors**. Then, this series combination is in **parallel with $C_2$​**.

The **equivalent resistor** for the pole calculation is $R_1 + R_2$​, as the input current at the node sums to zero (Kirchhoff’s current law).

The **equivalent capacitance** is calculated as follows:
- $$C_\text{series} = (1/C_1 + 1/C_3)^{-1} = (1\,\text{nF}^{-1} + 1\,\text{nF}^{-1})^{-1} = 0.5\,\text{nF}$$
- $$C_\text{eq} = C_\text{series} + C_2 = 0.5\,\text{nF} + 10\,\text{nF} = 10.5\,\text{nF}$$
With $R_\text{eq} = R_1 + R_2 = 20\,\text{k}\Omega$, the **pole frequency** is:

$$f_\text{pole} = \frac{1}{2 \pi R_\text{eq} C_\text{eq}} \approx 758 \text{ Hz}$$

When we plot the **output voltage versus the input**, the behavior is as follows:

![[Pasted image 20251019123756.png]]
- The **first significant attenuation** appears at **1.6 Hz**, corresponding to the **output filter** designed to remove 50 Hz interference.
- The **next pole** at 758 Hz comes from the **input filter stage** we just analyzed.
- Additional poles are introduced by the **instrumentation amplifier itself**, further shaping the transfer function.

Thus, the total transfer function of the system is a combination of **multiple filtering stages**, each contributing a pole at a specific frequency. This careful filtering ensures that the **thermocouple signal is preserved** while unwanted noise from both power lines and RF interference is significantly reduced.

### <span style="color:rgb(161, 40, 226)">Common Mode</span>
![[Pasted image 20251019124456.png]]
Now let’s examine the **common-mode behavior** of the thermocouple readout circuit. For common mode, we apply the **same voltage to both wires of the thermocouple**. The common-mode signal is **not the signal of interest**, but it can still appear between the two wires due to various environmental or circuit effects.

Ideally, we would expect the **output of the instrumentation amplifier** to be zero for a pure common-mode input because instrumentation amplifiers are specifically designed to **reject common-mode signals**.

![[Pasted image 20251019124647.png]]

When we simulate the output voltage $V_\text{out}$​ versus the applied common-mode voltage, we notice that the **gain is very small at low frequencies**, starting at around **−70 dB**, which reflects strong common-mode rejection.

However, something unexpected occurs: as the frequency increases, the **common-mode output starts to rise** instead of remaining suppressed. This increase is not caused by the input stage filters (the resistors and capacitors we added at the input), but rather by the **instrumentation amplifier itself**.


![[Pasted image 20251019124716.png]]

Looking at the **datasheet** of the amplifier confirms this behavior. The datasheet shows the **common-mode rejection ratio (CMRR) versus frequency**. At low frequencies, the CMRR is very high (around 100–120 dB), meaning the amplifier rejects common mode effectively. However, above roughly **100 Hz**, the CMRR decreases, so the amplifier becomes less capable of rejecting common-mode signals. This explains the rise in output voltage seen in our simulation.

![[Pasted image 20251019124854.png]]

To illustrate this, if we plot $V_\text{out}$​ versus the input common-mode voltage, the behavior matches the datasheet: **high rejection at low frequencies**, followed by a reduction in rejection starting around 100 Hz. The output begins to increase, and eventually we see a change in the trend (an inversion), which is consistent with the amplifier’s frequency-dependent characteristics.



![[Pasted image 20251019124647.png]]
Another important observation comes when we consider the **effect of the input filters** on common mode. If we analyze the transfer function from the input common-mode voltage to the output, the increase in gain is **less pronounced** because another **pole intervenes** at a higher frequency, around **16 kHz**, introduced by the input circuit.

![[Pasted image 20251019130024.png]]
For the common-mode signal, the analysis is simplified: **capacitor $C_2$​ has no effect** because both inputs see the same voltage. The voltage across $C_2$​ remains zero, so it does not influence the common-mode behavior. Meanwhile, capacitors $C_1$​ and $C_3$​ each see the same equivalent resistance due to the symmetry of the circuit ($C_1$​ with $R_1$​ and $C_3$​ with $R_2$​). Since $C_1 = C_3$​ and $R_1 = R_2$​, there is effectively **one common-mode pole**, calculated as:

$$f_\text{pole} = \frac{1}{2 \pi R_1 C_1} = \frac{1}{2 \pi R_2 C_3} \approx 16 \text{ kHz}$$

This analysis demonstrates why **piece-by-piece simulation** is crucial: some behaviors, like the expected pole frequencies for differential and common-mode signals, can be computed analytically from the circuit. Other effects, such as the **frequency-dependent common-mode rejection of the instrumentation amplifier**, are harder to predict and require simulation or datasheet reference.

## <span style="color:rgb(239, 179, 1)">Measuring Circuit Example 2</span>



Okay, let's see another example of a more complete example of a measuring circuit, a redoubt circuit for a thermocouple. So for sure we understood that it's very important to have your thermocouple, some filtering, the instrumentation amplifier. But then, how to digitalize this information and send the information, for instance, to a microcontroller to compute the absolute temperature of your object? Okay, in this case, ANO devices suggest to use these three components in order to arrive to have something that is the final temperature, the absolute temperature of your object. So here you have your thermocouple and you can connect the thermocouple to some filtering. We have already seen that the filtering is very important to filter the electromagnetic disturbances. And then you can connect it to this component, which is a component that directly includes both the instrumentation amplifier and an ADC. In particular, in this case, we have a sigma delta ADC, which is an advanced type of ADC. Then the output data can be sent to a microcontroller, for instance using this protocol, which is an SPI protocol. We will study the SPI protocol, serial peripheral interface protocol, during one of the next labs. But this is not enough because, as we already mentioned, the thermocouple provides you just a relative temperature relative to the reference junction. So we need another temperature sensor, and here is the other temperature sensor, in order to measure the temperature of the reference junction. And this is an example of a temperature sensor based on the Bang-Gap temperature sensor, so the next type of temperature sensor that we will study today during this class. Then the temperature measured by this temperature sensor can be sent to your microcontroller using the same SPI bus. So this SPI bus is connected to the SPI bus of the microcontroller. just to do an arbitration between the two SPI buses, so the bus of the ADC and the bus of the other temperature sensor, we need a selector. So you see we have just two separate SPI selector B in order to speak with the chip select of the ADC and then we have the SPI selector A to speak with the temperature sensor. But then instead the clock, the data master output slave input and the master input slave output is shared between the ADC and the temperature sensor. But I don't want to focus too much today on the SPI protocol because we will study it during the labs. So just to summarize about thermocouples, so for sure the most important advantage of thermocouples is the very extended measuring range, which includes very high limits. So we said we can exceed even the 2000 degree. Then we have a relatively fast response time, especially for the exposed thermocouples. Another advantage is that we have a very tiny measuring point because the tips of the thermocouple is very small, the price is moderate. Thermocouple does not suffer from self-heating. Do you remember during past class we mentioned many times that resistive sensors suffer from the self-heating because we have a character that is crossing the resistor? Instead Instead, in the case of thermocouple, we have no currents inside the thermocouple and so they do not suffer from self-heating. And then they are robust to mechanical stress, especially the one with the cap. Obviously we also have some disadvantages and the most important disadvantage is that we can measure only relative temperatures, so no absolute temperature, and so we need another thermometer to measure the temperature of the reference junction. Another disadvantage is that the sensitivity of the thermocouple is very low. So the output voltage of the thermocouple is in the order of a few microvolts. And so you need to amplify very well. And this is a disadvantage if you also consider that the thermocouple are prone to electromagnetic interference disturbances. So for this reason it is very important that the filtering that we put at the input of the readout circuit in order to reduce the effect of the electromagnetic interference. And also we have seen that thermocouple have a low linearity because the Siebeck coefficient is not constant in temperature. And so also the sensitivity of the thermocouple, which is given by the difference of the Siebeck coefficients of the two materials that we use for thermocouple, is dependent on temperature. Just to do a comparison between thermocouple and the other two types of temperature sensor that we have seen during last class, we can say that about sensitivity the best are the thermistors because you remember the characteristic of thermistors was very non-linear but it was very steep. About the range, for sure we will choose thermocouple because they have a very extended range, especially at high temperatures. About accuracy and linearity, RTDs are the best because they have perfect linear output. And about cost, thermistors are the cheapest. Okay, let's move to the next temperature sensor and in particular we will study now the thermal diodes and then their evolution which is the Van Gap temperature sensors. So, as you perfectly know, a diode has a characteristic which is an exponential characteristic, so it's something like that if we plot current versus the voltage that we provide across the diode. So this is the voltage V and this is the current I that we have in the diode. How can we write with an equation this characteristic? The equation is the one that I provided here. So the current is equal to a certain Is, which is the reverse saturation current, multiplied by this exponential. which depend obviously on the voltage that we have across the diode. And then it depends also on some fixed parameters. So Q, the charge of the electron, M, which is a technology parameter that is typically almost equal to one, K, the Boltzmann constant, but it also depends on T, so on the temperature. Then we have this minus 1 because you know the current at 0 volt is equal to 0. So the E to the 0 would be equal to 1 minus 1 and we obtain E to the 0. So we can reverse this equation in order to find the relation between the voltage and the current. So the voltage is equal to m by kT over Q by the logarithm of I over Is plus 1. So you see that the voltage directly depends on the temperature. And so we can provide a fixed current to our and then we can measure the voltage across the diode and we know that the voltage linearly depends on the temperature. And so we can say that the sensitivity of this sensor can be defined as the output, so the delta V out over the input, over the delta T, and it is equal to mk over Q by logarithm of I over Is plus 1. So, apparently, this term, m by k over q by log of i over is plus 1, seems to be constant. To be honest, it's not perfectly constant because the saturation current depends on temperature. So this sensor, the thermal diode, is not a perfectly linear sensor because there is in the sensitivity this dependence on IS and IS depends on temperature. how to solve this issue, so how to make a sensor similar to the thermal diode, so based on the thermal diode, but with a perfectly linear characteristic, we can move to the Banget temperature sensor. So now for simplicity, imagine not to have this tube BJT here and there, but to have just a simple diode. So imagine to be able to have there a simple diode. So this is a diode and also this one is. So you see if we use this differential approach we can measure the voltage across the first diode that we call VAB1 and the voltage across the second diode that is called the VAB2. And then, with an instrumentation amplifier, for instance, we can do the difference between these two voltages. So let's try to compute VAB1 and VAB2. We can use the general equation that we found for the thermal diodes. on which we can consider that m is almost, we can do some simplification because m is almost equal to 1, and then we can consider to bias our two diodes with the current I1 and I2, which are much bigger than the saturation current of the reverse saturation current of the of the diode and so this factor I over IS is much bigger than one and so you can we can neglect this one And so the equation is simplified and become KT over Q multiplied by the logarithm of the current for AB1, we will consider a current 1, divided by IS. If we want IS, which is the saturation current, can be written as the product of JS, which is the current density, so the current divided by the area and multiplied by the area. a1 where a1 is the area of the diode one then we can compute in the same way vab2 so it will be kt over q logarithm of I2, so the current that we use to bias the second diode, divided by the saturation current that is the same, the saturation current density which is the same for diode 1 and diode 2 because they are in the same technology, they are in very close proximity, so they also have the same temperature, and then multiplied by the area of the second diode. If we do the difference between these two voltages, so VAB1 minus VAB2, here I put a plus and here a minus, Then, exploiting the properties of the logarithm, we obtain that this difference is equal to kt over q logarithm of the ratio between I1 by A2 and I2 by A1. So you see that the Js simplify each other in this difference. Obviously, if we put I1 equal to I2 and area 2 equal to the area 1, we would obtain here 1 in the logarithm and the logarithm 1 is 0, so the difference would be equal to 0. So obviously, if we provide the same current and the same area of the diode, we will have no voltage difference. So we must create an imbalance between the two diodes. So imagine for instance that you want to provide the same current, then you should have two different areas. And we can say that for instance the ratio between area 2 and area 1 can be called R, and so the difference between the two will be kT over Q, then inside the logarithm I1 is simplified by I2 because we put them to be the same, and then and then we have the ratio a2 a1 that we call R and so we have here the logarithm of R. So in this case you see that the voltage that we measure just depend on the temperature. So we have a linear behavior between the temperature and the voltage. Okay, because we just have constant values Q, which is constant independent from temperature, and then K, the Boltzmann constant, and the logarithm of the ratio of the area. And so in this way, using this differential approach, we manage to obtain an output that is an output voltage that is perfectly linear with the temperature of the object and so we don't need calibration or reversing equation and so on. So just a last curiosity why do we put here instead of the diode this 2BJT in trans diode configuration? mainly because in standard technologies we have typically we have BJT available but we don't have diodes especially small sized diode but these two BJT in which you connect the base with the collector behaves exactly as a diode in fact a BJT and in this case they are P and P BJT means that you have the junction between the P zone, then you have the N, and then you have P again. This P part is the one that we have here, and it is called the emitter. Then the N part represents this, so the base, and finally the last P part represents this part, which is the collector. Then you see if we do a short circuit between this N and P junction, we just have the first junction, the one between the base and the emitter, that implements exactly a diode. And this is the reason why I call it VAB, so it's the voltage between the emitter and the base. It's the base-emitter voltage, the emitter-base voltage. which correspond to the voltage across our diode. In our sensor system board we have a temperature sensor which is exactly based on a bank temperature sensor. We will use it in one of the next labs during the course. Inside our integrated circuit of the banger temperature sensor, we don't have just the temperature sensor, this is a block scheme from the data sheet of our sensor, but as you see we have a lot of other electronics. In particular you see we have the analog to digital converter, which directly on the same chip of the sensor converts the output voltage of the bangap temperature sensor to a digital world. And this is very important because it's one of the main advantages of the bangap temperature sensor because they can be integrated in CMOS technology and so on the same chip I can have both the sensor but also the analog digital. digital converter or and as in this case also many register you see we have the pointer register configuration register we have a counter also we have a temperature register and so on And for instance, in this integrated circuit we can also monitor for over temperature. So we can put a threshold and when this threshold is exceeded, then a dedicated pin will alert you that the temperature has been exceeded. We can also fix some hysteresis in order not to have continuous re-triggering, but a certain interval in which you will you will mark the temperature, the over temperature if you exceed a certain voltage, sorry, a certain temperature and then you deactivate this over temperature pin only if the temperature go below another threshold which is lower than the previous threshold. Then we also have this logic control and interface that is very useful for the communication with standard protocol with, for example, our microcontroller. In particular, this sensor implements an I2C interface. We will study I2C, which is a standard serial communication protocol, in one of the next labs. Then you have these three inputs that, as we will see during the labs, are used in order to adjust the address of our sensor, because in the I2C communication protocol it's very important that each slave has his own address, because the master calls and communicates with different slaves using their address. So advantages and disadvantages of band-gap temperature sensors. The main advantage is that they can be integrated in CMOS technology. So as we have seen, it is possible to integrate together with the sensor also the ADC, some logics and also the peripheral for communication protocols. And we don't need, so consequently we don't need for any external components differently, for instance, from RTDs in which we have seen that we need to have the without circuit, so for instance the Winston Bridge and so on. They are small size because they can be integrated in a chip and also low voltage because we don't have to provide big voltages to read out the circuit. They have high linearity, we have seen because the sensitivity does not depend on the temperature itself, especially for the Banget temperature sensor, this is not true, instead for the thermal diode. And they have also good accuracy. The main limitation is the temperature range, which is limited only between -40°C and +125°C, and this is a typical limitation of CMOS circuitry. Ok, let's move to the last type of temperature sensor that we will study, which is the infrared thermometer. As you see even from this picture, the big difference of the infrared thermometer in respect to the other temperature sensor that we have studied is that it is possible to do thermal images. In fact, in this image the colors does not represent the intensity of the light, but they represent the temperature of the object. The other main difference is that they are non-contact sensors so you can measure the temperature of an object even without putting anything in contact with your object. So let's start from some theoretical basics about temperature and the working principle of the infrared thermometers. So every object that has a certain temperature will emit some radiation and the radiation which is emitted depends on the temperature of the object itself and the emission is typically in the infrared range. So we can, we could measure this radiation emitted by the object with a detector and in this way if we are able to measure the this emitted power, we will be able to associate the emitted power to the temperature of the object. So just to review the infrared radiation is the radiation at wavelengths which are longer than the visible range. And in particular for this temperature sensor we are interested in the wavelength around 1 micron, 2 micron, 5 microns. So this is about the order of the range of wavelengths in which we are interested in. So, if we go a little bit more in detail, we can start to study the emission of an ideal kind of body, which is the black body. So in a black body is an ideal body in which we don't have transmissivity and reflection. So it means that if you illuminate your black object with a certain radiation, then this radiation is fully absorbed by the black body and we have no radiation that is reflected, so backscattered by the object, or transmitted, so that can pass through the object. If your object is at a steady state for the temperature, so is at a stable temperature, it means that the radiation that is absorbed is equal to the radiation that is emitted. Otherwise, if the absorption is higher than emission, it means that the temperature of your object is increasing, or vice versa, if emission is higher than absorption, it means that the temperature is decreasing. But if we consider an object at a steady state for the temperature, then we can always say that absorption is equal to the emission. This equality is not because we are considering a black body, it's true for every kind of body at the temperature equilibrium. But then, in a black body, since reflection and transmission is equal to zero, it means that absorption and emissivity is equal to one. because it means that all the radiation incoming is absorbed and not transmitted or repaired. In this graph we can study the specific radiation. So this is the power emitted by a body normalized for the area, so over a centimeter square, and represented for each wavelength. In fact, here on the x-axis we represent the wavelength. What we can notice is that the radiation emitted by a body strongly depends on its temperature, you see at 6000K the emission is much higher than for instance at 300K, 800K, 300K or 77K. So both we have a variation in the overall, so in the integral of the emitted power. And also we can notice a shift in the maximum wavelength of emission and in particular the hotter is the object, the shorter is the wavelength. If we consider temperature around close to the room temperature, so around 300 Kelvin, we see that the peak emission is about 10 micrometers. So there are some physical equations that can describe this behavior of the emission of a black body. In particular, the Stefan-Boltzmann law provides us the overall power density emitted by a body. Overall power density means that is the integral of this curve. and it is equal to the emissivity, that for a blackboard is equal to one, and then multiply by sigma, so the Stefan-Boltzmann constant, and multiply by T to the fourth. So we see that there is, in the emitted power, there is this dependence of temperature, which is not a linear dependence, but it is a dependence with T to the fourth. And so the Stefan-Boltzmann is used to know the integral of this curve. Instead, in order to find the peak of this characteristic, we can use the Vn displacement law. that in particular say that the lambda max, so the lambda corresponding to the peak of the emission, multiplied by the temperature is a constant value equal to 2,898 micrometer by Kelvin. And so we can notice that if temperature is increasing, the lambda max is decreasing exactly as we see here in a linear way. But normally the body that we want to measure are not black bodies, but they have a behavior that can be better described with a gray body. So what is a gray body? A gray body is a body in which if we try to provide the radiation to eat, a portion of this radiation is absorbed, a portion is transmitted, and another portion is reflected. So in particular, we know that for a generic body, we have reflectivity, transmission, and absorption, and there's some all of them are different from zero and their sum obviously must be equal to one because they must provide the overall incoming radiation. But since R and T are different from zero, it means that A is smaller than one and at the steady state for the temperature, A is equal to epsilon. So epsilon will be smaller than one and so you understand that if we want to apply the Stefan-Moltzmann law to reconstruct the temperature from the radiation, so if you can measure the power, the emitted power, and you want to obtain the temperature, you should have to reverse the Stefan-Boltzmann law, but you need to know epsilon, okay? And for for a gray body, the epsilon is smaller than one and different for each body. So we start to understand that it is very important for the infrared thermometer to know the value of epsilon in order to be able to reconstruct and to obtain the temperature of the object. Because our sensor will measure the emitted power, but then we need epsilon to obtain the temperature. A particular type of gray body is the solid gray body and it's the body that we most commonly have to measure. So the solid body. In the solid body we have the transmission that is completely negligible and we just have the reflection and absorption. So transmission is zero, reflection is different from zero. So again, the absorption is still not equal to one, and so also the emissivity is smaller than one. For solid debris body, we can mainly distinguish non-metallic materials and metals instead. In non-metallic materials like wood, plastic, rubber, organic materials and so on, we have a low reflectivity. so reflectivity is close to zero and so the absorption consequently also the emissivity is close to one so we can have in the order of 0.8 0.95 instead for the metallic object especially if they have polished their shiny surfaces the reflectivity is very big It's very important the effect of the reflectivity and so we have absorption and emissivity which are very small in the order even of 0.1. So you see that for different objects you can have very different epsilon and so you need a calibration to estimate the epsilon before using the infrared thermometers. And the problem is even worse with a non-gray body because if a gray body has a constant emissivity, so it means that in respect to the emission spectrum of the black body, they have the same shape, the gray body has the same shape of the black body, but with a smaller intensity because epsilon is smaller. Then non-grey body have a spectrum that is completely unpredictable. So they can be sometimes, they have an epsilon that changes with the wavelength because the epsilon can be seen as the ratio between the absorption, between the power that you emit for a body divide by the equivalent of the black body at the same temperature. And so you see this ratio for the blue line, the one that represents the grey body, is always constant. Instead, for the orange line, it completely changes because we have a different shape of the emission in respect to the wavelength. and typically in a gray body there are no oxidized metals or glasses or plastic films. So for this reason in general it is better not to have a broadband sensor, so a sensor which quite measures the radiation in the entire spectrum, but it's better to use sensor at a single wavelength, at a specific wavelength. And so imagine to have a sensor which can sense the radiation only at, let's say, this specific wavelength, then we will know that the epsilon of my body, even if it's a non-grey body, has a specific value, okay? So the ratio between this and this. Okay, but how to determine the emissivity of a body? Mainly we can use two methods. The first one is to do a preliminary calibration with a contact sensor, so imagine to use a thermocouple or an RTT and so on. and to measure the temperature of your object with the contact and then measure the temperature also with your infrared temperature sensor. Then you can adjust the emissivity in your temperature sensor until you see the same temperature on the two instruments. After this preliminary calibration, then you can measure the temperature of that object in non-contact conditions just with the infrared thermometer. And so you can monitor during time the variation of the temperature of that object just doing a first calibration at the beginning with the contact sensor. Another way, if it's possible, you can stick, you can attach to your object a plastic sticker with a well-known emissivity. So the plastic sticker will go at the thermal equilibrium with your object, so we reach the same temperature of the object, and then with your infrared thermometer you can measure the temperature of the sticker with the well-known emissivity, but the temperature of the sticker will be the same temperature of the object. Sometimes you don't perform a real calibration like these two that I presented, but you just have an a priori know-how about the material. So imagine that you want to measure the temperature of your silicon chip, then you know from literature which is the emissivity of silicon. Okay, just some notice: with infrared temperature sensor we can have either single spot sensors, so for instance for thermometer for the fever when you measure in one spot the temperature of your forehead, or you can have cameras like the one that I showed you at the beginning with the picture of the dog. When you use a single spot sensor, you must be careful that the field of view of your sensor is smaller than the object that you want to measure. So imagine to want to measure the temperature of a very tiny object and then the field of view of your sensor is much bigger than your tiny object, then you will have an estimation of the temperature which does not depend only on your object but also on the surrounding as in this example in which the object that you want to measure the temperature is this square but then your field of view is much bigger and so you will be influenced also by the temperature of the surrounding object. Sometimes in some single spot sensor, in order to help you to identify exactly which is the object that you are looking at with your field of view, you also have a laser pointer. This is the reason why, for instance, with the thermometer for the fever, you see the red spot. The red spot is not used to measure the temperature. So for measuring the temperature you measure the radiation emitted by your skin. The laser pointer just is useful for the person that is doing the measurement to know that you are looking at this particular point. Typically the laser spot that is emitted is the one here represented with this dotted line is a little bit larger than the field of view. So this way you are sure that if the laser spot is in the correct position, so within the object, also the field of view is within your object. Be careful because typically you suffer from parallax error, so it means that if you are at very short distances, the the point that is indicated by the laser pointer is not perfectly coincident with the field of view. So you see at long distances our field of view is internal to the laser spot and it is true also at medium distances, for instance at 1 meter. If instead you stay very close, so for instance at about 30 cm, then your field of view is not perfectly included inside the laser spot. There exist also some very precise infrared temperature sensor with coaxial pointers. Coaxial pointers means that you don't have this parallax error. Okay, but how to implement the infrared sensors, infrared detectors? Mainly we have two types of sensors: the so-called thermal detectors and the quantum detectors. In the thermal detectors mainly you have a double stage conversion. So first of all you have a material which is called absorber, which absorbs the light, so the infrared radiation that arrives on the sensor and it is emitted by your body and then with a second sensor you measure the temperature of the absorber. And then this sensor provides you a current or air voltage which is proportional to the temperature of the absorber and obviously the temperature of the absorber depends on the light, on the radiation emitted by your body. And we will analyze briefly different types of thermal detectors, in particular thermopile, volumeters and pyroelectric detectors. Then the second way to implement an infrared detector is to use quantum detectors. Quantum detectors mainly are very similar to photodiodes, so diodes used to detect the light, but they are done with materials with lower energy gap in respect to silicon in order to be able to detect wave-frames which are longer than 1 micrometer. So let's go a little bit more in detail about thermal detectors. So as I mentioned, the first type of thermal detector that we can have is the thermopile detector. So in the thermopile you see we have an infrared absorption film, which is our absorber. So a material capable to absorb the infrared radiation. And then we use many thermocouples put in series to measure the temperature of the infrared absorber. So the radiation, the incoming radiation will be absorbed here in this infrared absorber. The infrared absorber will increase its temperature depending on the absorbed radiation and then with the thermocouple you measure the temperature of the infrared absorption film. We have seen today that thermocouple have a very low sensitivity, so the output of the thermocouple is very small, in the order of microvolts. For this reason, in this kind of sensor, we don't use just one thermocouple, but we use a thermopile. So many thermocouples in series. So imagine that this is your absorber, and that you have here your reference junction instead, so at a fixed temperature you can put your thermocouples with the two different materials of the thermocouple all in series. Okay, so like this, let me draw just another one. And so, if you measure the overall voltage, in this case it will be three times the voltage measured by just one thermocouple. And this helps you to increase the sensitivity of the thermocouple. Typically with ThermoPile, since we have many thermocouples in series, we can do just single element, so single spot infrared detectors, or we can do arrays but with a limited number of elements. So we cannot do a beautiful image like the one that we have seen for the dog. If you want to do an imager, then you have to use another type of thermal detector which is the bolometer. So also in the monometer obviously you have your absorber, the infrared absorber that absorbs the infrared light radiation and then you use a resistance which is called the bolometer resistance here to measure the temperature of the infrared absorber. Typically the volumetric resistance is made with a metallic object, so it's similar to an RTD, or semiconductor with positive temperature coefficient. The BOLOMETER RESISTANCE can be easily integrated in CMOS technologies and this structure can be replicated many times in CMOS technologies and we can easily do array of this in order to have thermal pictures. In fact, you can integrate on the same chip also the readout circuitry. So you can have a redoubt integrated circuit which measures the variation of the resistance. It is very important to have a good thermal isolation between the bolometer and the silicon readout circuit because otherwise you run the risk to measure the temperature of the readout circuit instead of the temperature of the infrared absorber which is proportional to the temperature of your object. So this is the one pixel of a standard thermal camera. Finally, for the thermal detectors we have the pyroelectric detectors. So in pyroelectric detectors we have, as for the other thermal detectors, an absorber. And then the temperature of the sorbet is measured using a pyrolytic material. So a pyrolytic material is a material that provides a voltage difference across it when you apply a temperature step, a temperature variation. In particular, pyrolytic materials are made by dipoles and at the steady state these dipoles distributes in a way that you don't see any voltage difference across the pyroelectric material across these two electrodes. But then if you apply a step of temperature or in general a temperature variation, then this depose polarizes and provides a voltage across the two electrodes. So you see a voltage increase at the two electrodes. Then if you keep the temperature constant, the depots reorganize in the original states and so we see that the voltage decreases and comes back to be zero. So in this way we can use pyrolytic material just to measure variation of temperature. If you want to measure a fixed temperature, then you need to put an optical shutter in order to prevent the radiation to arrive to the absorber. and then when you open it the radiation will hit the absorber and so you will register a variation. Then you stop again and measure many times. Then we can move to the second type of infrared sensor which are the quantum detectors. As I already mentioned quantum detectors are very similar to photodiode. So also in this case we have a junction and we have the electron per generation so we can measure a current when the radiation is absorbed. Obviously infrared radiation has less energy than visible radiation and so we cannot use silicon because the energy gap of the silicon is higher than the energy of the infrared photons. But we can use other materials with lower energy gap. So for instance we can use materials from the second and sixth group like mercury, cadmium, telluride, which have a very low energy gap in the order of 0.1-0.4 eV. Or we can use materials of the third fifth group like indium arsenide, gallium antimonyde, And in particular in this case of heterojunctions, so junction of two different materials, we can get at the heterojunction a very low energy gap in the order of 0.15 eV. What about the responsivity of the infrared sensors? So, first of all, the responsivity is the sensitivity of the sensor, so it's defined as the variation of the output divided by the variation of the input. For the thermal detectors, so thermopiles, volumeters and pyroelectric, the responsivity is independent from the wavelength. because the absorber film typically is a material made to absorb a wide range of wavelengths. So instead it is different from the quantum detectors. So in quantum detectors we can define the responsivity as the output current divided by the incoming power of the of the radiation. And in this case the responsivity depends on lambda. In fact, if we try to write this equation, we can say that the sensitivity is the output current divided by the input power. The output current can be seen as the rate of the generated photoelectrons multiplied by the charge of the electron. while the input power can be seen as the rate of the incoming photons multiplied by the energy of the photon that you can write as h/ν or h/c divided by λ. And in the second case we put in evidence the dependence on λ. Then we can define the ratio between the generated photoelectrons divided by the ratio of the incoming photons with the terms which is the detector efficiency. So the detector efficiency by definition is the ratio between the generated electrons and the ratio between the incoming photons. And so you see that we can find the relation between the responsivity and the lambda. So we have this linear dependence of responsivity with lambda because we explicitly have lambda in the energy of the photon. But then the resource another dependence because the photodetector detection efficiency depends on lambda. So we have seen this for photodiodes, but obviously it is the same also for diodes in other materials that is not silicon. Okay, here we see some other problem that we can have with the infrared thermometers. First of all, is the possibility that the medium in which your radiation propagates can absorb a part of your radiation. And so it is very important to know the transmissivity of the air, that I represented here, in order to make your sensor to work at a wavelength in which the transmissivity of the air is very high. So for instance we can work at around 4 micrometer in order to have an high transmissivity or we can work even around 10 micrometer and so on. So when you select the the working bandwidth of your infrared thermometer, it's important to select a wavelength in which the transmissivity of air is high enough. Then we have to be careful also to the ambient radiations, because the ambient radiation can be reflected by your object and then detected by the sensor itself. So, especially in an environment in which the ambient radiation is very strong, imagine this case inside an oven, the radiation of the oven itself is very high, but then you see the radiation. of the oven can be reflected by the target and then can reach your sensor. And so you can confuse the radiation of the target itself with the radiation just reflected of the surrounding. So it's very important to try to do some compensation, some calibration for the radiation of the ambient or do some shielding to protect your target from the environmental radiation. And then another typical problem that we have is the presence of dust or particles on the lenses of your sensor and to mitigate this problem many sensors have an auto polishing of the lenses. So the main application of infrared temperature sensors are for surveillance, so just to monitor if people are moving in some environment because people obviously can be detected by from the object because they have higher temperature. They can be used in industrial applications to monitor the temperature of big environments or machinery, or they can be used for integrated circuits or circuits in general to measure the temperature of the circuit. And also sometimes they are used to detect, to localize defective cables because if you have defective cables you will have some hot spots inside the cable. Okay, so we have concluded our overview about temperature sensors and so let's see in the next class. Bye!

Transcribed by https://www.uniscribe.co