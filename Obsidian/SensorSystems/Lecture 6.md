
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

Let’s now consider a more complete example of a **measuring circuit**, or **readout circuit**, designed for a thermocouple.  

So far, we have understood that the essential elements of a thermocouple measurement chain include the **thermocouple itself**, **filtering stages**, and an **instrumentation amplifier**. However, the next question is: _how do we convert this analog information into a digital form and send it to a microcontroller in order to compute the absolute temperature of the measured object?_

![[Pasted image 20251020202540.png]]

Analog Devices proposes a very elegant and compact solution that involves **three key components** working together to obtain the **absolute temperature** of the object.

First, we start with the **thermocouple**, which measures the voltage corresponding to the temperature difference between the **measurement junction** and the **reference junction**. This thermocouple signal is very small and highly susceptible to electromagnetic noise, so it must first pass through a **filtering stage**. As we have already discussed, filtering is fundamental to remove high-frequency electromagnetic disturbances that could couple into the thermocouple wires and affect measurement accuracy.

After filtering, the conditioned thermocouple signal is connected to the **AD7793**, a highly integrated component that includes **both an instrumentation amplifier and an analog-to-digital converter (ADC)** within the same device. The ADC used here is a **sigma-delta ADC**, an advanced architecture known for its excellent noise performance and high resolution — ideal characteristics for low-frequency, high-precision measurements such as temperature sensing.

Once the thermocouple voltage is amplified and converted into a digital signal by the AD7793, the **output data can be sent to a microcontroller**. This communication is carried out using the **SPI protocol** (Serial Peripheral Interface), a synchronous serial communication protocol that we will study in more detail during one of the next laboratory sessions.

However, this setup alone is not sufficient. As we discussed earlier, a thermocouple does **not provide an absolute temperature**, but rather a **relative measurement** — it measures the temperature difference between the measuring junction and the reference junction. Therefore, to determine the absolute temperature of the object, we must also know the temperature of the **reference junction**.

For this purpose, a **second temperature sensor** is used — the **ADT7320**. This is an example of a **band-gap temperature sensor**, a type that we will study later in this same class. The ADT7320 is responsible for measuring the **reference junction temperature**, providing the necessary data to compute the absolute temperature of the object.

The ADT7320 also communicates with the microcontroller via the **same SPI bus** used by the AD7793. This means that both the ADC (which reads the thermocouple signal) and the reference temperature sensor share the SPI communication lines. To manage this shared communication, **SPI chip select lines** are used to determine which device the microcontroller is currently communicating with.

In this setup, we have two separate **SPI selectors**:

- **Selector B** corresponds to the **chip select of the AD7793** (the ADC and instrumentation amplifier).
    
- **Selector A** corresponds to the **chip select of the ADT7320** (the temperature sensor).
    

Meanwhile, the other SPI lines — the **clock (SCLK)**, the **master output/slave input (MOSI)**, and the **master input/slave output (MISO)** — are **shared** between the two devices.

This way, the microcontroller can alternately read data from either the ADC (which provides the thermocouple differential voltage) or from the temperature sensor (which gives the reference junction temperature) by simply toggling the appropriate chip select line.

Even though we are not focusing today on the details of the **SPI communication protocol**, it is important to keep in mind that this protocol allows the microcontroller to efficiently manage and synchronize multiple devices on the same communication bus — a key feature in modern temperature measurement systems.

## <span style="color:rgb(239, 179, 1)">Thermocouple pros and cons</span>

### <span style="color:rgb(161, 40, 226)">Advantages</span>

- **Very wide measuring range:**  
    Thermocouples can operate over an extremely large temperature range, even exceeding **2000°C**, which makes them ideal for applications in high-temperature or harsh environments where other sensors cannot function.
    
- **Fast response time:**  
    Particularly for **exposed thermocouples**, the response is quick because the sensing junction is directly in contact with the object, without needing to wait for a protective cap to reach thermal equilibrium.
    
- **Tiny measuring point:**  
    The junction between the two wires is very small, allowing **localized measurements** and minimizing the influence of the sensor on the system being measured.
    
- **Moderate cost:**  
    Thermocouples are generally affordable, which makes them practical for both industrial and laboratory use.
    
- **No self-heating effect:**  
    Unlike **resistive sensors**, which heat up due to the current passing through them, thermocouples generate their signal through the **Seebeck effect** and do not require current flow, so they **do not suffer from self-heating**.
    
- **High mechanical robustness:**  
    Especially the **insulated or grounded types** with protective caps, thermocouples are resistant to vibration, mechanical stress, and difficult environmental conditions.

### <span style="color:rgb(161, 40, 226)">Disadvantages</span>

- **Only relative temperature measurement:**  
    A thermocouple measures the **temperature difference** between its measuring junction and its **reference junction**, not the absolute temperature.  
    Therefore, a **second temperature sensor** is needed to measure the reference junction temperature and compute the absolute value.
    
- **Low sensitivity:**  
    The output voltage is only a few **microvolts per degree Celsius**, so it must be **amplified** with great care. This small signal level also makes the measurement **more vulnerable to electromagnetic interference (EMI)**.
    
- **Susceptibility to noise:**  
    Because of the very low signal amplitude, thermocouples are prone to pick up **electromagnetic disturbances**, which is why **proper filtering** at the input of the readout circuit is essential for accurate readings.
    
- **Low linearity:**  
    The **Seebeck coefficient** (which determines sensitivity) is **not constant with temperature**, meaning that the **voltage–temperature relationship is nonlinear**. This nonlinearity must be **corrected through calibration or compensation**.


# <span style="color:rgb(223, 109, 109)">RTD, Thermistor, Thermocouple comparison</span>

![[Pasted image 20251020223758.png]]
 
To make a brief comparison between thermocouples and the other two types of temperature sensors we studied in the previous class — **RTDs** and **thermistors** — we can highlight the following points:

- **Sensitivity:**  
    The most sensitive sensors are the **thermistors**. Although their response is highly **nonlinear**, their characteristic curve is **very steep**, which means that even small changes in temperature produce noticeable changes in resistance.
    
- **Measuring range:**  
    For applications requiring a **very wide temperature range**, especially at **high temperatures**, the **thermocouple** is the preferred choice. It can measure temperatures far beyond the range supported by RTDs or thermistors.
    
- **Accuracy and linearity:**  
    The **RTDs (Resistance Temperature Detectors)** offer the **highest accuracy** and an almost **perfectly linear output** across their working range, making them ideal for precise laboratory and industrial measurements.
    
- **Cost:**  
    In terms of price, **thermistors** are the **cheapest** option, which makes them a practical choice when cost is a priority and extremely high accuracy or temperature range is not required.

# <span style="color:rgb(223, 109, 109)">Thermal Diode</span>

![[Pasted image 20251021094154.png]]


Let’s move on to the next type of temperature sensor: **thermal diodes**, and later, their improved version — the **bandgap temperature sensors**.

As you already know, a **diode** has an **exponential current–voltage characteristic**. If we plot the current (I) against the voltage (V) applied across the diode, we get a curve that rises exponentially.

Mathematically, the diode current can be described by this equation:
![[Pasted image 20251020224042.png]]

$$I = I_s \left(e^{\frac{qV}{m k T}} - 1\right)$$

Here:

- $I_s$​ is the **reverse saturation current**,
- $q$ is the **charge of an electron**,
- $m$ is a **technology-dependent constant** (usually close to 1),
- $k$ is the **Boltzmann constant**, and
- $T$ is the **absolute temperature**.

The term “–1” at the end ensures that the current is zero when the voltage is zero (since $e^0 = 1$).

Now, we can rearrange this equation to express the **voltage** as a function of the **current**:

$$V = \frac{m k T}{q} \ln\left(\frac{I}{I_s} + 1\right)$$

From this expression, we can see that the **voltage across the diode** depends directly on the **temperature**.

So, if we apply a **fixed current** to the diode and then **measure the voltage**, that voltage will vary almost **linearly with temperature**. The **sensitivity** of the diode (how much the voltage changes for a given change in temperature) can be defined as:

$$S = \frac{\Delta V}{\Delta T} = \frac{m k}{q} \ln\left(\frac{I}{I_s} + 1\right)$$

At first glance, this term looks constant. However, it’s not perfectly constant because the **saturation current $I_s$​ itself changes with temperature.

That means the **thermal diode is not perfectly linear**, as its sensitivity slightly varies with temperature.

To overcome this limitation and obtain a **more linear response**, engineers developed an improved version called the **Bandgap Temperature Sensor** — a device based on the same diode principle but designed to achieve **perfect linearity** between voltage and temperature.

# <span style="color:rgb(223, 109, 109)">Bandgap Temperature Sensor</span>


To understand how the **bandgap temperature sensor** works, let’s simplify the structure.  
Instead of using two BJTs (as it happens in real circuits), let’s imagine we just have **two simple diodes**.
![[Pasted image 20251021095509.png]]

### <span style="color:rgb(161, 40, 226)">1. Differential measurement setup</span>

We have:

- **Two identical diodes**, for **A₁** and **A₂**.
- Each diode has a current flowing through it: **I₁** for A₁ and **I₂** for A₂.
- We measure the voltages across them:
    - $V_{EB1}$​ across the first diode
    - $V_{EB2}$ across the second diode
        
Then, using an **instrumentation amplifier**, we take the **difference** between these two voltages:

$$V_{\text{out}} = V_{EB1} - V_{EB2}$$


### <span style="color:rgb(161, 40, 226)">2. Voltage across a diode</span>

From the diode equation (simplified, assuming $m \approx 1$ and $I \gg I_s$​):

$$V = \frac{kT}{q} \ln\left(\frac{I}{I_s}\right)$$
The **saturation current $I_s$** can be expressed as:
$$I_s = J_s \cdot A$$
where:
- $J_s$​ is the **saturation current density** (same for both diodes since they are built with the same technology),
- $A$ is the **junction area** of the diode.

### <span style="color:rgb(161, 40, 226)">3. Apply to both diodes</span>

For **diode 1**:
$$V_{EB1} = \frac{kT}{q} \ln\left(\frac{I_1}{J_s A_1}\right)$$

For **diode 2**:
$$V_{EB2} = \frac{kT}{q} \ln\left(\frac{I_2}{J_s A_2}\right)$$
### <span style="color:rgb(161, 40, 226)">4. Compute the voltage difference</span>

Subtract the two voltages:
$$V_{\text{out}} = V_{EB1} - V_{EB2} = \frac{kT}{q} \ln\left(\frac{I_1 A_2}{I_2 A_1}\right)$$
The term $J_s$ cancels out since it’s the same for both diodes.


### <span style="color:rgb(161, 40, 226)">5. Achieving a linear temperature dependence</span>

To get a **non-zero voltage difference**, we must create an **imbalance** between the two diodes — either by:

- Using **different currents** $(I_1 \neq I_2)$, or    
- Using **different areas** $(A_1 \neq A_2)$.

If we choose to keep the **currents equal** $(I_1 = I_2)$, then:

$$V_{\text{out}} = \frac{kT}{q} \ln\left(\frac{A_2}{A_1}\right)$$
Let’s call the **area ratio** 
$$r = \frac{A_2}{A_1}$$
Then the output becomes:

$$V_{\text{out}} = \frac{kT}{q} \ln(r)$$
This equation shows a **perfectly linear relationship** between the **output voltage** and the **temperature**.  
All the other quantities ($k, q, r$) are constants — so $V_{\text{out}} \propto T$.

That’s why the **bandgap temperature sensor** can provide a **highly linear and accurate temperature reading**, without needing calibration.

### <span style="color:rgb(161, 40, 226)">6. Why we use BJTs instead of simple diodes</span>

In **integrated circuits**, we typically don’t have discrete diodes available — but we **do have BJTs**.  
Fortunately, a **BJT can behave exactly like a diode** if we **short-circuit its base and collector**.

![[Pasted image 20251021100152.png]]
- In a **P–N–P transistor**:
    
    - The **emitter (P)** and **base (N)** form one junction — the same as a diode.
    - The **collector (P)** is connected to the **base (N)**, so only the **emitter–base junction** remains active.
    - The resulting voltage between **emitter and base (VEB)** acts just like the **voltage across a diode**.

Hence, the bandgap sensor uses **two BJTs in diode connection** to reproduce the behavior of **two matched diodes** with different emitter areas.

## <span style="color:rgb(239, 179, 1)">Digital Temperature Sensor</span>


![[Pasted image 20251021102704.png]]

On our sensor system board, we have a **temperature sensor based on the bandgap principle**. We’ll actually use this sensor in one of the upcoming lab sessions.

Inside this **bandgap temperature sensor’s integrated circuit**, there’s much more than just the sensing element itself. The block diagram from its datasheet shows that several additional electronic components are built into the same chip.
### <span style="color:rgb(161, 40, 226)">Main internal components</span>

- **Bandgap Temperature Sensor**  
    The core element that generates a voltage proportional to temperature.
- **Analog-to-Digital Converter (ADC)**  
    This converts the sensor’s analog output voltage directly into a **digital signal** on the same chip.  
    This is one of the major advantages of bandgap sensors — since they can be **fully integrated in CMOS technology**, the sensor, ADC, and control circuitry can all fit on the same chip.
- **Registers**  
    Several internal registers are used for configuration and data handling:
    
    - _Pointer register_
    - _Configuration register_
    - _Temperature register_
    - _Counter register_, and others.
### <span style="color:rgb(161, 40, 226)">Overtemperature monitoring</span>

This sensor can also **detect and signal when the temperature exceeds a set limit**.  
You can:

- Define a **temperature threshold**.    
- When this threshold is crossed, a **dedicated pin** activates to alert you.
- To prevent the signal from continuously turning on and off near the limit, a **hysteresis** can be configured.

    - For example, the alarm pin activates when the temperature rises above a certain value,        
    - and deactivates only after it drops below a slightly lower temperature.
        
### <span style="color:rgb(161, 40, 226)">Communication interface</span>

The sensor also includes an internal **logic control and communication interface**, allowing it to connect easily to a **microcontroller**.

It uses the **I²C (Inter-Integrated Circuit)** protocol — a common **serial communication standard** in electronics.  
We’ll study the I²C protocol in detail in one of the next labs.

Finally, the sensor has **three address pins**.  
These are used to configure its **I²C address**, which is essential because, in an I²C network, the **master device** communicates with different **slaves** using their unique addresses.


## <span style="color:rgb(239, 179, 1)">Advantages and Disadvantages</span>

### <span style="color:rgb(161, 40, 226)">Advantages</span>

- **Full CMOS Integration:**  
    They can be entirely integrated using CMOS technology. This allows combining the **sensor**, **ADC**, **digital logic**, and **communication interfaces** (like I²C or SPI) on the same chip.
- **No External Components Needed:**  
    Unlike RTDs or thermistors, which require external circuits such as Wheatstone bridges or amplifiers, bandgap sensors can operate independently with minimal external hardware.
- **Compact Size:**  
    Since the whole system is integrated on a single chip, these sensors occupy very little space — ideal for embedded and portable applications.
- **Low Voltage Operation:**  
    The required supply voltage is small, making them compatible with low-power electronic systems.
- **High Linearity:**  
    The **output voltage changes linearly with temperature**, as the sensitivity does not depend on temperature (unlike in thermal diodes).
- **Good Accuracy:**  
    They provide reliable and stable temperature readings without requiring extensive calibration.
    
### <span style="color:rgb(161, 40, 226)">Disadvantages</span>

- **Limited Temperature Range:**  
    Their operating range typically goes from **–40 °C to +125 °C**, which is sufficient for most electronic applications but not suitable for **very high-temperature** environments. This limitation comes from the characteristics of **CMOS technology**, which constrains operation at extreme temperatures.

# <span style="color:rgb(223, 109, 109)">Infrared thermometer</span>
![[Pasted image 20251021103806.png]]

The **infrared thermometer** represents the last type of temperature sensor we will study.

- The **main difference** compared to the other temperature sensors (thermocouples, RTDs, thermistors, and bandgap sensors) is that it allows **non-contact temperature measurement**.
    - This means it can **measure the temperature of an object without physical contact**, simply by detecting the **infrared radiation** emitted by the object.
        
- Another important feature is that infrared thermometers can be used to **create thermal images**.
    - In a **thermal image**, the **colors** do not indicate light intensity but rather the **temperature distribution** across the observed scene or object.

## <span style="color:rgb(239, 179, 1)">Introduction to Infrared systems</span>

![[Pasted image 20251021103915.png]]
Let’s begin with some theoretical basics about **temperature and infrared radiation**.

Every object with a certain temperature naturally emits **electromagnetic radiation**, and the **amount and characteristics** of this radiation depend directly on the object’s temperature. Most of this emission occurs in the **infrared region** of the spectrum.

If we can **detect and measure the intensity** of this emitted radiation, we can then **relate the detected power to the object’s temperature**. This is the fundamental working principle of infrared thermometers.

To recall, **infrared radiation** corresponds to **wavelengths longer than visible light**, meaning it lies beyond the red part of the visible spectrum. For temperature measurement applications, we are particularly interested in wavelengths in the range of approximately **1 to 5 micrometers (µm)**. This range is especially relevant because it corresponds to the typical emission of objects at temperatures found in everyday and industrial contexts.
![[Pasted image 20251021104201.png]]
To understand how infrared thermometers work, we first need to study the emission of an **ideal body**, known as the **blackbody**.

A **blackbody** is an _idealized object_ that **absorbs all incident radiation**—it does not reflect or transmit any of it.

- This means that if you illuminate a blackbody with radiation, **100% of that radiation is absorbed**, with **no reflection** (backscattered light) and **no transmission** (radiation passing through).
    

When the object is at a **steady-state temperature** (thermal equilibrium), the **absorbed power equals the emitted power**.

- If absorption > emission → the object’s temperature increases.
- If emission > absorption → the object’s temperature decreases.
- At steady state → absorption = emission.
    
This equality holds for **any object** in thermal equilibrium. However, for a **blackbody**, since reflection and transmission are both zero, we have:

$$\text{Absorptivity} = \text{Emissivity} = 1$$

That means the blackbody is the **perfect emitter**.

### <span style="color:rgb(161, 40, 226)">Spectral Distribution of Emission</span>

![[Pasted image 20251021104201.png]]
The **emitted radiation** from a body depends strongly on its **temperature**.

If we plot the **emitted power per unit area** (W/cm²) as a function of **wavelength**, we observe that:

- The **total emitted power** increases with temperature (the area under the curve grows).
- The **wavelength of maximum emission** shifts toward **shorter wavelengths** as temperature increases.    

For example:

- At **6000 K** (like the Sun’s surface), most radiation is in the **visible range**.
- At **300 K** (room temperature), the **peak emission** occurs around **10 µm**, which is in the **infrared region**.

### <span style="color:rgb(161, 40, 226)">Stefan–Boltzmann Law</span>

The **total emitted power density** (integral under the emission curve) is described by the **Stefan–Boltzmann law**:

$$P = \varepsilon \sigma T^4$$

where:
- $P$ = total emitted power per unit area (W/m²)
- $\varepsilon$ = emissivity (for a blackbody, $\varepsilon = 1$)
- $\sigma = 5.67 \times 10^{-8}\ \text{W/m}^2\text{K}^4 \space \text{Stefan–Boltzmann constant}$ 
- $T$ = absolute temperature (K)

This shows that emitted power increases **non-linearly** with the **fourth power** of temperature.
### <span style="color:rgb(161, 40, 226)">Wien’s Displacement Law</span>

The **peak wavelength** of the emitted radiation is given by **Wien’s displacement law**:

$$\lambda_{\text{max}} \cdot T = 2898\ \mu\text{m·K}$$

This means that as the **temperature increases**, the **peak wavelength** shifts to **shorter values** — exactly as seen in the emission spectra.
## <span style="color:rgb(239, 179, 1)">Gray Bodies and Emissivity<br></span>
In real life, **most objects are not black bodies**. Instead, they behave as **gray bodies**, which means they do not absorb all the incoming radiation.

![[Pasted image 20251021105110.png]]
When radiation reaches a gray body, it is divided into three components:

- **Reflectivity (R):** the portion of radiation reflected by the surface
- **Transmissivity (T):** the portion transmitted through the material
- **Absorptivity (A):** the portion absorbed by the material

These three components satisfy the **energy conservation relation**:

$$R + T + A = 1$$

Since both **R** and **T** are different from zero in a gray body, the **absorptivity (A)** is **less than one**.  

At **thermal equilibrium**, the **absorptivity (A)** equals the **emissivity (ε)**:
$$A = \varepsilon < 1$$
This means that a gray body emits **less radiation** than a black body at the same temperature.
### <span style="color:rgb(161, 40, 226)">Applying the Stefan–Boltzmann Law to Real Bodies</span>

When we measure temperature using an infrared thermometer, the sensor measures the **emitted power**.  
To convert that power into a temperature value, we use the **Stefan–Boltzmann law**:

$$P = \varepsilon \sigma T^4$$

However, because $\varepsilon$ depends on the material, we must **know the emissivity** of the object to calculate its true temperature correctly.  If we assume a wrong emissivity, the temperature reading will be inaccurate.  

That’s why **calibration** or **emissivity adjustment** is a key step when using infrared thermometers.
### <span style="color:rgb(161, 40, 226)">Solid Gray Bodies</span>

A particular and very common case is the **solid gray body**, where the **transmission (T)** is negligible:

$$T = 0 \quad \Rightarrow \quad R + A = 1$$

So, the emitted power depends only on reflection and absorption.
We can classify solid gray bodies into two main categories:

#### 1. Non-metallic materials

- Examples: wood, plastic, rubber, organic materials, ceramics, etc.
- **Low reflectivity (R ≈ 0)** → **High absorptivity/emissivity (ε ≈ 0.8–0.95)**
- These materials are generally good emitters of infrared radiation.
#### 2. Metallic materials

- Especially those with **polished or shiny surfaces**
- **High reflectivity (R large)** → **Low absorptivity/emissivity (ε ≈ 0.1 or even lower)**
- They are poor infrared emitters, and their measurement requires careful emissivity compensation.
### <span style="color:rgb(161, 40, 226)">Conclusion</span>

Because different materials have very different **emissivity values**, it is essential to:

- **Know or estimate ε** before measurement    
- **Calibrate** the infrared thermometer accordingly

Otherwise, the measured radiation could correspond to a very different temperature than the real one.

## <span style="color:rgb(239, 179, 1)">Non-Gray Bodies and Their Implications<br></span>
The situation becomes **even more complex** when the object we want to measure is **not a gray body**.

### <span style="color:rgb(161, 40, 226)">Gray body vs. Non-gray body</span>

![[Pasted image 20251021105912.png]]

- In a **gray body**, the **emissivity (ε)** is **constant** across all wavelengths.  
    This means its **emission spectrum** has the **same shape** as that of a black body, but with a **lower intensity**, because $\varepsilon < 1$.  
    In other words:
    $$P_{\text{gray}}(\lambda) = \varepsilon \cdot P_{\text{black}}(\lambda)$$
    The two curves are similar in shape, differing only by a scaling factor.
    
- In a **non-gray body**, instead, the **emissivity varies with wavelength**:
    $$\varepsilon = \varepsilon(\lambda)$$
    
    As a consequence, its **emission spectrum has a different shape**, not just a scaled version of the black-body curve.  
    This behavior makes the emitted power **unpredictable** across the wavelength range.
    
### <span style="color:rgb(161, 40, 226)">Typical examples of non-gray bodies</span>

Non-gray bodies include materials such as:

- **Non-oxidized metals**    
- **Glasses**
- **Plastic films**
    

These materials exhibit emissivity that changes significantly with wavelength, making their radiative behavior difficult to model precisely.

### <span style="color:rgb(161, 40, 226)">Consequences for infrared thermometry</span>

Since in non-gray bodies $\varepsilon$ depends on $\lambda$, using a **broadband infrared sensor** (i.e., one that measures radiation over a wide spectral range) can lead to **large measurement errors**, because the sensor integrates radiation with **varying emissivity**.

![[Pasted image 20251021110230.png]]
To reduce this uncertainty, it is **preferable to use a narrowband or single-wavelength sensor**.

- If the sensor detects radiation only at a **specific wavelength**, then the emissivity $\varepsilon(\lambda)$ can be considered **constant** at that wavelength.
- This allows a more accurate conversion between **measured radiation** and **temperature**.

## <span style="color:rgb(239, 179, 1)">Determining the Emissivity of a Body</span>

Knowing the **emissivity (ε)** of an object is crucial for accurate temperature measurement using **infrared thermometers**, since the sensor measures **emitted radiation** and not temperature directly.  There are **three main approaches** to determine ε:

### <span style="color:rgb(161, 40, 226)">1. Calibration with a Contact Sensor</span>

![[Pasted image 20251021110937.png]]
- Use a **contact temperature sensor** (e.g., **thermocouple** or **RTD**) to measure the **true temperature** of the object.
- Simultaneously, measure the **temperature with the infrared thermometer**.
- Adjust the **emissivity setting** in the infrared thermometer **until both readings match**.
- Once calibrated, the **infrared thermometer** can then be used **alone** to measure the same object’s temperature in **non-contact conditions** over time.
    
 _Advantage:_ High accuracy after calibration  
 _Limitation:_ Calibration must be done in contact once before measurement


### <span style="color:rgb(161, 40, 226)">2. Using a Reference Sticker with Known Emissivity</span>
![[Pasted image 20251021110953.png]]
- Attach a **plastic or adhesive sticker** with a **well-known emissivity value** onto the object’s surface.
- Wait until **thermal equilibrium** is reached (the sticker and the object reach the same temperature).
- Measure the **temperature of the sticker** with the infrared thermometer, using its **known emissivity value**.
- The measured temperature corresponds to the **object’s temperature**.
    

 _Advantage:_ No need for contact temperature sensors  
 _Limitation:_ Requires physical access to place the sticker


### <span style="color:rgb(161, 40, 226)">3. Using Known Emissivity from Material Data</span>

- For **common materials**, emissivity values can be found in **literature or datasheets**.
- Example: If you measure the temperature of a **silicon chip**, you can directly use the **known emissivity of silicon** from reference tables.
    

 _Advantage:_ Quick and convenient  
 _Limitation:_ Less accurate, since surface finish, oxidation, and contamination can change emissivity

## <span style="color:rgb(239, 179, 1)">Measurement Spot</span>

| Single Spot sensor                   | Single spot Sensor + Laser spot      |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251021140953.png]] | ![[Pasted image 20251021141003.png]] |
When using **infrared temperature sensors**, it’s important to distinguish between **single-spot sensors** and **infrared cameras**.

- **Single-spot sensors** are like the thermometers used for measuring **forehead temperature**. They focus on one small point at a time.

- **Infrared cameras** capture an entire thermal image, like the example of the dog you saw earlier, giving a **full thermal map** of the scene.
    
For **single-spot sensors**, the **field of view (FOV)** is critical. The FOV is the area from which the sensor collects infrared radiation to measure temperature. If the FOV is **larger than the object** whose temperature you want to measure, the sensor will capture not only the object’s radiation but also the surrounding environment. This leads to an **inaccurate temperature reading**, because the measured temperature will be influenced by both the object and its surroundings.

To help the operator **aim at the correct spot**, some single-spot sensors include a **laser pointer**. Importantly:

- The **laser spot is only for visual guidance** and is **not used for temperature measurement**.
- The radiation measured by the sensor comes only from the object’s surface.
- Typically, the **laser spot is slightly larger than the actual FOV**. This ensures that when the laser spot is positioned over the object, the FOV is fully contained within the object, providing a correct reading.

However, **parallax error** can occur:

- At **long distances**, the FOV usually lies well within the laser spot, so the measurement is accurate.
- At **short distances** (e.g., 30 cm), the FOV may no longer fully align with the laser spot, and the temperature reading can be affected.
    
Some high-precision infrared sensors use **coaxial laser pointers**, which means the laser beam and the sensor’s FOV are perfectly aligned. This **eliminates parallax errors**, ensuring that the FOV always coincides exactly with the point indicated by the laser, regardless of distance.

## <span style="color:rgb(239, 179, 1)">How to implement Infrared sensors?</span>

Infrared sensors, also called **infrared detectors**, can be implemented mainly in two ways: **thermal detectors** and **quantum detectors**.

![[Pasted image 20251021141934.png]]
**Thermal detectors** work through a **two-stage conversion**:

   - First, an **absorber material** captures the infrared radiation emitted by the object.
   - Second, a sensor measures the **temperature of the absorber**. This temperature depends on the incoming radiation, and the sensor converts it into a **voltage or current proportional to the temperature**.
   - There are several types of thermal detectors, including **thermopiles, bolometers, and pyroelectric detectors**.

![[Pasted image 20251021142005.png]]

**Quantum detectors** operate similarly to **photodiodes** but are made from **materials with a smaller energy gap than silicon**, which allows them to detect infrared wavelengths longer than 1 micrometer.

### <span style="color:rgb(161, 40, 226)">Thermal Detectors</span>

#### Thermopile Detectors
![[Pasted image 20251021142059.png]]

- In a **thermopile**, the infrared radiation is absorbed by an **infrared absorption film**, which heats up depending on the intensity of the radiation.

![[Pasted image 20251021142153.png]]
- The temperature of the absorber is measured using **multiple thermocouples connected in series**. This arrangement is necessary because a single thermocouple has **very low sensitivity**, generating only a few microvolts per degree of temperature change.
- By connecting many thermocouples in series, the total output voltage increases, improving sensitivity.
- Thermopiles can be used for **single-spot measurements** or **small arrays**, but the array size is limited, so they are not suitable for detailed thermal imaging like infrared cameras.
    

#### Bolometers

![[Pasted image 20251021142335.png]]
- **Bolometers** are used for thermal imaging. They also have an **absorber** to capture infrared radiation.
- The temperature of the absorber is measured using a **resistive element**, which can be metallic or semiconductor-based. The resistance changes with temperature, similar to an RTD.
- Bolometers can be **easily integrated in CMOS technology**, allowing the creation of large arrays for **thermal imaging**.
- The **readout circuitry** can also be integrated on the same chip.
- It is critical to **thermally isolate the bolometer from the readout circuitry** to ensure the sensor measures the absorber’s temperature, not the temperature of the electronics.
- Each pixel in a standard thermal camera corresponds to one bolometer element.
    

#### Pyroelectric Detectors

![[Pasted image 20251021142528.png]]

- Pyroelectric detectors also have an **absorber**, but the temperature of the absorber is measured using a **pyroelectric material**.
![[Pasted image 20251021142651.png]]
- Pyroelectric materials generate a **voltage difference across electrodes when subjected to a temperature change**.
- At steady state (constant temperature), the dipoles inside the material are balanced, and no voltage is observed.
- When the temperature **varies**, the dipoles polarize, creating a measurable voltage.
- Pyroelectric detectors are mainly used to **measure temperature variations** rather than absolute temperatures.
- To measure a fixed temperature, an **optical shutter** can be used to block the radiation periodically, allowing the detector to register changes each time the shutter opens.
### <span style="color:rgb(161, 40, 226)">Quantum Detectors</span>

Now we can move on to the **second type of infrared sensors**, which are the **quantum detectors**.

As already mentioned, **quantum detectors** operate in a way that is **very similar to photodiodes**. They are based on a **p–n junction**, where the absorption of radiation leads to the **generation of electron–hole pairs**, producing a measurable **current**.

However, there is a fundamental difference between quantum detectors for visible light and those for infrared radiation:

- **Infrared photons** have **less energy** than visible photons.
- The **energy gap (bandgap)** of **silicon**—commonly used in visible light photodiodes—is **too large** to be excited by infrared photons.
    
To detect infrared radiation effectively, we need **semiconductors with smaller energy gaps**, allowing the lower-energy infrared photons to excite electrons across the bandgap and generate current.

Some commonly used materials include:

- **Group II–VI compounds**, such as **mercury cadmium telluride (HgCdTe)**, which have very small bandgaps (around **0.1–0.4 eV**).
- **Group III–V compounds**, such as **indium arsenide (InAs)** and **gallium antimonide (GaSb)**.
    
In particular, **heterojunctions**—junctions made by combining two different semiconductor materials—can be engineered to achieve **even smaller effective bandgaps**, often around **0.15 eV**.

These materials enable the detection of **longer wavelengths**, extending well beyond 1 µm, making quantum detectors highly sensitive and suitable for **high-speed, high-precision infrared applications**.

## <span style="color:rgb(239, 179, 1)">Responsivity of Infrared Sensors<br></span>
Now that we have seen the main types of infrared detectors, we can discuss an important performance parameter — **responsivity**.

The **responsivity** represents the **sensitivity of a sensor**, that is, how much the sensor’s output changes in response to a change in the input. Mathematically, it is defined as the **variation of the output** divided by the **variation of the input**.
$$
\text{Spectral Responsivity: } S=\frac{\Delta out}{\Delta in}
$$
Let’s distinguish how responsivity behaves for the two families of infrared detectors:

- **Thermal detectors** (such as thermopiles, bolometers, and pyroelectric sensors):  
    In this case, the responsivity is **independent of the wavelength**.  
    This happens because the **absorber film** used in thermal detectors is typically designed to **absorb radiation over a wide spectral range**, so the output does not vary with the wavelength of the incoming radiation.
    
- **Quantum detectors:**  
    For quantum detectors, the situation is different. Here, the responsivity **depends on the wavelength (λ)** of the incoming radiation.
    
    The responsivity $R$ can be expressed as:
    $$R = \frac{I_{\text{out}}}{P_{\text{in}}}$$
    
    where $I_{\text{out}}$​ is the output current and $P_{\text{in}}$​ is the input optical power.
    
    The output current can be written as the **rate of generated photoelectrons** multiplied by the **electron charge (q)**.  
	$$
	I_{out}= n_e \cdot q
	$$
    The input power, on the other hand, can be seen as the **rate of incoming photons** multiplied by the **energy of each photon**, given by:
    $$n_p\cdot E_{\text{photon}} = n_p \cdot\frac{hc}{\lambda}$$
    where $h$ is Planck’s constant, $c$ is the speed of light, and $\lambda$ is the wavelength.
    
    We can also define the **detector efficiency** (or quantum efficiency, $\eta$) as the **ratio between the number of generated electrons and the number of incident photons**.
    
    Combining these relations gives:
    $$S=\frac{I_{out}}{P_{in}}=\frac{n_e\cdot q}{n_p\cdot \frac{hc}{\lambda}} =\eta \cdot \frac{q \lambda}{hc}​ = \eta \cdot \frac{\lambda}{1.24}$$
    
    From this expression, we can see two main factors influencing the responsivity:
    
    1. There is an **explicit linear dependence on λ**, because longer wavelengths correspond to lower photon energy.
    2. There is an **implicit dependence through the quantum efficiency (η)**, which itself varies with wavelength, depending on the material and structure of the detector.
        
Thus, while **thermal detectors** provide a nearly constant response over a wide spectral range, **quantum detectors** exhibit a **wavelength-dependent responsivity**, determined by both the photon energy and the efficiency of photoelectron generation.





![[Pasted image 20251021143715.png]]

Okay, here we see some other problem that we can have with the infrared thermometers. First of all, is the possibility that the medium in which your radiation propagates can absorb a part of your radiation. And so it is very important to know the transmissivity of the air, that I represented here, in order to make your sensor to work at a wavelength in which the transmissivity of the air is very high. So for instance we can work at around 4 micrometer in order to have an high transmissivity or we can work even around 10 micrometer and so on. So when you select the the working bandwidth of your infrared thermometer, it's important to select a wavelength in which the transmissivity of air is high enough. 

![[Pasted image 20251021143658.png]]

Then we have to be careful also to the ambient radiations, because the ambient radiation can be reflected by your object and then detected by the sensor itself. So, especially in an environment in which the ambient radiation is very strong, imagine this case inside an oven, the radiation of the oven itself is very high, but then you see the radiation. of the oven can be reflected by the target and then can reach your sensor. And so you can confuse the radiation of the target itself with the radiation just reflected of the surrounding. So it's very important to try to do some compensation, some calibration for the radiation of the ambient or do some shielding to protect your target from the environmental radiation. And then another typical problem that we have is the presence of dust or particles on the lenses of your sensor and to mitigate this problem many sensors have an auto polishing of the lenses. 

![[Pasted image 20251021143843.png]]
So the main application of infrared temperature sensors are for surveillance, so just to monitor if people are moving in some environment because people obviously can be detected by from the object because they have higher temperature. They can be used in industrial applications to monitor the temperature of big environments or machinery, or they can be used for integrated circuits or circuits in general to measure the temperature of the circuit. And also sometimes they are used to detect, to localize defective cables because if you have defective cables you will have some hot spots inside the cable.

## <span style="color:rgb(239, 179, 1)"> Practical Considerations and Applications of Infrared Thermometers<br></span>



When using infrared thermometers, there are several practical issues that must be taken into account to ensure accurate temperature measurement.

### <span style="color:rgb(161, 40, 226)">1. Absorption by the medium (air transmissivity)</span>
![[Pasted image 20251021143715.png]]
One of the first problems is that the **medium through which the radiation propagates**, such as air, **can absorb part of the emitted infrared radiation** before it reaches the sensor.  
To minimize this effect, it is very important to know the **transmissivity of air** as a function of wavelength.

As shown in the figure, there are specific wavelength ranges where air transmissivity is higher. Therefore, the **working wavelength of the infrared thermometer** should be chosen in one of these “transmission windows” to reduce signal attenuation.  
Typically, **wavelengths around 4 μm or 10 μm** are selected, because in these regions the air transmissivity is particularly high.


### <span style="color:rgb(161, 40, 226)">2. Influence of ambient radiation</span>

![[Pasted image 20251021143658.png]]
Another important factor to consider is the **effect of ambient radiation**.  Infrared thermometers can detect not only the radiation emitted by the object itself but also radiation that is **reflected from surrounding sources**.

For example, in environments where ambient radiation is very strong—such as inside an oven—the hot surroundings emit intense infrared radiation. This radiation can be reflected by the surface of the target and then reach the sensor.  
As a result, the thermometer may detect a temperature that does not correspond to the actual temperature of the target but rather to a combination of the **object’s emission** and the **reflected ambient radiation**.

To reduce this problem, one can:
- Perform **compensation or calibration** for ambient radiation,
- Use **optical shielding** to protect the target from unwanted reflections,
- Or design the system so that reflections are minimized through proper positioning and surface treatment.

### <span style="color:rgb(161, 40, 226)">3. Dust and contamination on the sensor lens</span>  
A further source of measurement error can be **dust or small particles deposited on the sensor lens**.  
These particles can scatter or absorb part of the incoming radiation, leading to a lower detected signal.  To mitigate this effect, many modern infrared sensors are equipped with **self-cleaning or lens-polishing mechanisms** that periodically remove dust and maintain optimal optical transmission.

## <span style="color:rgb(239, 179, 1)">Applications of Infrared Temperature Sensors</span>

Infrared thermometers and cameras are widely used in many practical contexts, such as:


![[Pasted image 20251021150156.png|200]]

- **Surveillance systems:** detecting human presence or movement by sensing the higher body temperature compared to the surroundings.
![[Pasted image 20251021150209.png|200]]

- **Industrial monitoring:** measuring the temperature of machinery, furnaces, or large equipment in a non-contact way.
- **Electronics:** analyzing the thermal behavior of integrated circuits or components to prevent overheating.
- **Fault detection:** locating **hot spots** in electrical cables or connections, which can indicate defects or excessive current flow.
