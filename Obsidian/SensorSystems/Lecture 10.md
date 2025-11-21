
13/11/2025
***

# <span style="color:rgb(223, 109, 109)">Displacement, Proximity and Distance Sensors (Part 2)</span>

Hello everybody. Today we will continue with the second part of our lecture on displacement, proximity, and distance sensors.

In the previous class, we examined potentiometers, capacitive sensors, and inductive sensors. Today our attention will shift to acoustic and optical sensors, followed by magnetic sensors.

We have already discussed the conceptual differences between displacement, proximity, and distance measurements. With the acoustic and optical sensors presented today, we will see how these technologies allow us to measure proximity and distance effectively.

Finally, in the last part of the class, we will introduce encoders—devices that enable precise measurement of linear or angular displacement.
So let's start with acoustic sensors.  
  
## <span style="color:rgb(239, 179, 1)">Acoustic Sensors</span>

![[Pasted image 20251120225728.png|200]]
Acoustic sensors are mainly used to measure proximity and distance, although they can also be applied to displacement measurements. These sensors consist of a source, which generates ultrasound waves, and a receiver, which detects the returning waveform.

Before analyzing the sensor operation, let’s review some basics about ultrasound. Humans can hear sounds in the range of 20 Hz to 20 kHz. Sounds with frequencies above 20 kHz are considered ultrasounds, meaning they are inaudible to humans, though some animals can perceive them.

The speed of sound in air depends on temperature and is given by the equation:
$$c = 331 + 0.6 \cdot T$$

where $c$ is in meters per second and $T$ is the temperature in degrees Celsius. This dependence on temperature is important because many acoustic sensor measurements rely on the sound velocity. Therefore, temperature compensation is often necessary. For reference, at 20°C, the speed of sound in air is approximately 344 m/s.

Another important consideration is the wavelength of the ultrasound, which is related to the frequency by:
$$\lambda = \frac{c}{f}$$

Shorter wavelengths allow for better resolution. This is because sound waves can only interact with objects that are roughly the same size as the wavelength or larger. For example, a small dust particle will not affect the propagation of low-frequency audible sounds.

To illustrate:

- A 20 kHz sound has a wavelength of approximately 17 mm. This means the sensor can detect objects that are 17 mm or larger.
- Increasing the frequency to 80 kHz reduces the wavelength to 4.3 mm.
- At 200 kHz, the wavelength is 1.7 mm, allowing detection of even smaller objects.
    

Finally, the reflectivity of the target material affects the sensor’s performance. Materials like metal, wood, concrete, glass, rubber, and paper reflect nearly all the incident ultrasound, providing a strong return signal. On the other hand, materials such as cloth, cotton, and wool absorb much of the ultrasound, resulting in low reflectivity and weaker signals.



Another very important parameter is that we need to consider is the ultrasound attenuation in air.  For sure we know that all the sounds that are propagating inside the medium.  In the air in particular in this case.  Experience the diffusion loss. So you know that the sound is propagating on a spherical surface and so the more far away you are and more attenuated is the sound that you perceive and this is due to the diffraction phenomena.  But then there is also a second phenomena that is more related to frequency. In fact the diffusion loss.  So the one for the spherical attenuation, is independent from the wavelength.  
  
### <span style="color:rgb(161, 40, 226)">Ultrasound attenuation in air</span>
  
![[Pasted image 20251121094539.png|300]]
The second phenomenon—**absorption loss**—is related to the amount of acoustic energy that is **absorbed by the propagation medium**.

![[Pasted image 20251121094601.png]]
In air, for example, small particles such as dust or other suspended contaminants can absorb part of the ultrasonic energy. This effect becomes **significant at higher frequencies**. For this reason, in the graph you can observe that, especially at **larger propagation distances**, higher-frequency ultrasound waves exhibit **greater attenuation** compared to lower-frequency waves.

For low frequencies such as **20 kHz**, the attenuation due to absorption is almost negligible. As a result, the measured attenuation closely follows the curve associated with **diffusion loss alone**.

At higher frequencies, however, absorption losses become increasingly relevant. Consequently, the higher the frequency, the greater the absorption, and the shorter the effective propagation distance of the ultrasound signal.

This leads to a fundamental **trade-off**:

- **Higher frequencies** → better spatial resolution (because smaller objects can be detected), but reduced maximum measurable distance due to stronger absorption.
- **Lower frequencies** → longer measurement range, but poorer resolution.

### <span style="color:rgb(161, 40, 226)">Sound Pressure Level (SPL) and Sensitivity</span>

#### <span style="color:rgb(2, 141, 192)">Sound Pressure Level (SPL)</span>
To quantify the amount of sound that reaches a sensor, a commonly used figure of merit is the **Sound Pressure Level (SPL)**.  SPL is expressed in **decibels (dB)** and is defined as the logarithmic ratio between:
$$SPL=20\cdot Log \left( \frac{P}{P_o} \right) \space (dB)$$
- the **sound pressure** measured at the sensor, and    
- a **reference sound pressure**, which is conventionally set to **20 μPa**.
    
Mathematically, SPL is obtained by taking the logarithm of this ratio and multiplying it by 20.

#### <span style="color:rgb(2, 141, 192)">Sensitivity</span>

$$S_{lin} = \frac{V_{out}}{P_{in}} \space (V/Pa)$$
Another important parameter—common to many types of sensors, including ultrasonic sensors—is the **sensitivity**.  The sensitivity describes how effectively the sensor converts the **input sound pressure** into an **output voltage**. For ultrasonic sensors, it is therefore expressed in **volts per pascal (V/Pa)**.
$$S_{dB} = 20\cdot Log \left( \frac{S_{lin}}{S_{ref}} \right) \space (dB)$$

However, instead of using a linear scale, the sensitivity is typically expressed in **decibels**. To do this, the linear sensitivity is divided by a reference sensitivity of **1 V/Pa**, and the logarithm of this ratio is taken and multiplied by 20. This yields the **sensitivity in dB**.
 
### <span style="color:rgb(161, 40, 226)">Different Ultrasound Structures</span>

How can we detect sound, and how can we generate it? As discussed earlier when studying force sensors, **piezoelectric materials** have a unique dual capability:

1. **Detection:** they generate a voltage proportional to an applied pressure variation.
2. **Actuation:** they vibrate when an AC voltage is applied to them.

For this reason, piezoelectric materials are ideal both for **ultrasound detection** and **ultrasound generation**.

#### <span style="color:rgb(2, 141, 192)">Typical Sensor/Actuator Structures</span>

Several structural configurations exist for piezoelectric ultrasonic devices.
##### <span style="color:rgb(71, 215, 140)">1. Open Structure</span>
![[Pasted image 20251121095919.png]]

One of the most common designs is the **open structure**, which includes:

- A **housing** with openings that allow ultrasound waves to reach the piezoelectric element (for sensing) or to exit the device (for actuation).
- A **mechanical assembly** called the _motive vibrator_, composed of:
![[Pasted image 20251121100045.png|300]]
    - A **resonator**, usually a conical metal diaphragm that focuses or amplifies the acoustic energy.
    - A **vibrator**, typically a circular disc of piezoelectric ceramic that performs the actual sensing or actuation.
        

The conical metal sheet concentrates acoustic energy toward the piezoelectric disc, improving efficiency.

##### <span style="color:rgb(71, 215, 140)">2. Enclosed Structure</span>

![[Pasted image 20251121100122.png|300]]
Another configuration is the **fully enclosed structure**, which is well suited for outdoor applications.  
In this case:

- The metallic housing is completely sealed to prevent dust, moisture, or rain from entering.
- The piezoelectric ceramic is mounted directly in contact with the housing.
- Sound waves propagate through the metal casing to the ceramic element.
    
This design offers higher environmental robustness.

##### <span style="color:rgb(71, 215, 140)">3. High-Frequency Structures</span>

![[Pasted image 20251121100243.png|300]]
For applications requiring the detection of **very high-frequency ultrasound**, the design must be adapted further. Standard piezoelectric sensors typically operate efficiently only up to approximately **70 kHz**. This limitation is caused by the **acoustic impedance mismatch** between:

- The piezoelectric ceramic (≈ ($10^7$) acoustic impedance)
- Air (≈ ($10^2$))
    
Because of this five-order-of-magnitude difference, most of the ultrasound energy is **reflected**, resulting in poor transmission.

To address this issue, high-frequency sensors incorporate **ultrasonic radiation surfaces**, also known as **acoustic impedance matching layers**. Their purpose is to gradually match the impedance of air to the impedance of the ceramic, improving energy transfer.

This concept is analogous to **anti-reflection coatings** used in optics, which help match refractive indices to reduce reflection between air and silicon.  
Here the same principle is applied to **acoustic waves** instead of light.

### <span style="color:rgb(161, 40, 226)">Use in Proximity and Distance</span>

How can we use ultrasonic sensors to measure proximity or distance?

#### <span style="color:rgb(2, 141, 192)">Proximity Measuring using Ultrasonic Sensors</span>

To perform proximity sensing, we typically use a configuration consisting of a **source** and a **receiver**. As previously discussed, both components can be made from **piezoelectric materials**:
![[Pasted image 20251121101126.png|400]]

- In the **source**, the piezoelectric material receives an applied voltage and vibrates, generating ultrasound that propagates through the medium.
- In the **receiver**, the piezoelectric material acts as a sensor: variations in pressure due to incoming sound waves produce a voltage proportional to those pressure changes.
    
The source emits an ultrasonic wave with a certain amplitude. This wave travels through the air until it reaches an object, which **backscatters** part of the acoustic energy toward the receiver.

The receiver detects this **returning ultrasound**, whose amplitude depends on:

1. The distance the wave travelled in the medium.
2. The reflectivity of the target object.
    
If a returning signal is detected, we can conclude that an object is present. The detection threshold must be selected according to the required sensing range of the proximity sensor. As with capacitive proximity sensors, the **sensitivity depends on the material** of the target. For this reason, datasheets typically provide a **relative sensing distance** curve that shows how detection distance varies with the reflectivity of different materials.


#### <span style="color:rgb(2, 141, 192)">Distance Measurement Using Ultrasonic Sensors</span>

Ultrasonic sensors can also be used to **measure distance**. As before, a source generates the ultrasound and a receiver detects the reflected wave. However, in this case, the source emits **short acoustic pulses**. These pulses propagate through the medium, reflect from the object, and return to the receiver.
![[Pasted image 20251121101256.png|500]]
For distance measurement, we are **not interested in the amplitude** of the reflected signal, because amplitude depends strongly on the target’s reflectivity and therefore cannot reliably indicate distance. Instead, we measure the **time of flight (ToF)**: the time delay between the emission of the pulse and the detection of the reflected signal.

The distance to the target is given by: 
$$d = \frac{C(T) \cdot T_{\text{ToF}}}{2} $$

where:
- $(d)$ is the distance to the object,
- $(T_{\text{ToF}})$ is the measured time of flight,
- ($C(T)$) is the speed of sound in the medium at temperature ( T ).
    
Since the pulse travels **from the source to the object and then back to the receiver**, the total measured time corresponds to twice the actual one-way distance, hence the division by 2. To obtain accurate results, **temperature calibration is required**, because the speed of sound varies with temperature.

##### <span style="color:rgb(71, 215, 140)">Example of Circuit Setup to Measure Distance</span>
Here we can examine in more detail a typical setup used to measure distances with ultrasonic actuators and sensors.
![[Pasted image 20251121101850.png|600]]
The system consists of a **source** (also called the *transmitter*) and a **receiver**. The transmitter is connected to a **pulse-generation circuit**, which produces the voltage pulses that drive the piezoelectric element. This oscillating voltage is converted into ultrasonic waves. These ultrasound pulses travel through the medium, reach the target object, and are backscattered toward the receiver.

The receiver is connected to its dedicated **front-end circuitry**, which conditions and amplifies the electrical signal generated by the piezoelectric sensor when it detects the incoming acoustic wave.

Above the transmitter and receiver electronics, the system includes additional circuitry capable of measuring the **time delay** between:
- the emission of the electrical pulse that excites the transmitter (start signal), and  
- the detection of the returned acoustic pulse at the receiver (stop signal).

A straightforward way to measure this delay is to use a **counter** that counts the number of cycles from a reference **clock oscillator**. For example, consider a clock running at 100 MHz—a frequency that is easy to generate. A 100 MHz clock has a period of 10 ns. Using this value in the distance equation, we obtain a **minimum measurable distance (i.e., the resolution)** of approximately **2 µm**, which is already extremely good for many applications.

In applications where even higher resolution is required, the counter can be replaced by a **Time-to-Digital Converter (TDC)**. A TDC uses a more advanced architecture than a simple counter, allowing timing resolutions in the **picosecond** range. This improvement in temporal resolution translates directly into **better spatial resolution**.

Below is an example of a transmitter/receiver pair that can be used for distance-measurement applications.
![[Pasted image 20251121102116.png|340]]


#### <span style="color:rgb(2, 141, 192)">Distance Measurement Ultrasound Tx Circuit - More detail</span>

We will look in more detail at the circuits used in an ultrasonic distance measurement system. The example circuits shown are taken from real datasheets and correspond to actual components, but we can treat them as a combination of simpler functional blocks.
![[Pasted image 20251121102744.png]]
##### <span style="color:rgb(71, 215, 140)">1. Enable Signal Generation</span>

| Circuit                              | Signal                               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251121102827.png]] | ![[Pasted image 20251121102842.png]] |

The first block is responsible for generating the **enable signal**.  This signal defines **when** we want to emit an ultrasound burst.

For example:
- One enable pulse may trigger the first burst here,  
- Another enable pulse may trigger a second burst later in time.

So the enable signal essentially “opens” time windows during which the transmitter is allowed to generate ultrasound.

##### <span style="color:rgb(71, 215, 140)">2. Oscillator Block</span>

| Circuit                              | Signal                               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251121102923.png]] | ![[Pasted image 20251121102953.png]] |

The second block is an **oscillator**.
- This oscillator produces a periodic signal at the **desired ultrasonic frequency**.  
- For instance, an oscillator running at **40 kHz** will generate the electrical signal required to produce a **40 kHz ultrasonic wave**.
- 
At its output node, we observe a high-frequency signal (e.g., a 40 kHz square wave).

##### <span style="color:rgb(71, 215, 140)">3. Gating the Oscillation (Burst Generation)</span>

| Circuit                              | Signal                               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251121103103.png]] | ![[Pasted image 20251121103125.png]] |

Next, we use **logic gates**, in particular an **AND gate**, to ensure that the oscillation is applied to the transmitter **only during the enable interval**.

- The AND gate receives:
  - the **enable signal**, and 
  - the **oscillator output**.
- Its output is:
  - zero (no drive) when the enable signal is low,  
  - a copy of the oscillator waveform when the enable signal is high.

In this way, the transmitter receives a **burst** of oscillating voltage only during the enable time, as shown by a finite-duration high-frequency signal. This burst produces the corresponding burst of ultrasound.


##### <span style="color:rgb(71, 215, 140)">4. Circuit: Driver Stage</span>

| Circuit                              | Signal                               |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251121103103.png]] | ![[Pasted image 20251121103125.png]] |
Finally, we have the **driver circuit**, which interfaces the logic-level signal with the **piezoelectric transducer**.

- The driver replicates the oscillating waveform as a **square wave**.
- It provides this waveform with **opposite polarity** on the two terminals of the piezoelectric element:
  - one terminal sees the signal,
  - the other sees the inverted version (180° phase shift).

This differential drive effectively doubles the peak-to-peak voltage across the piezoelectric material, improving the efficiency of ultrasound generation.

#### <span style="color:rgb(2, 141, 192)">Distance Measurement Ultrasound Rx Circuit - More detail</span>

Now, let us move to the **receiving circuitry**.  The receiving stage is essentially a **standard non-inverting amplifier** used to amplify the voltage generated by the piezoelectric sensor.
![[Pasted image 20251121103710.png|400]]

##### <span style="color:rgb(71, 215, 140)">1. Input Connection and DC Blocking</span>

![[Pasted image 20251121104416.png|400]]
The piezoelectric receiver is connected to the **non-inverting input** of the operational amplifier. Before the signal reaches the amplifier, it passes through a pair of capacitors that act as **AC-coupling (DC-blocking) elements**.  These capacitors remove any DC component from the sensor signal, ensuring that only the AC ultrasound signal is amplified.

##### <span style="color:rgb(71, 215, 140)">2. DC Operating Point (Gain = 1 for DC)</span>

Because this circuit uses a **single-supply operational amplifier**, we need to bias the amplifier at **mid-supply** to allow the output to swing properly around a central value.

![[Pasted image 20251121104522.png|400]]
- A voltage divider (100 kΩ / 100 kΩ) generates **VDD/2**,
- This bias voltage is applied to both the non-inverting and inverting inputs (for DC only),
- The feedback network includes a capacitor, so at DC the capacitor behaves as an open circuit.

In this DC condition:

- No current flows through the feedback resistor ($R_F$),    
- The voltage at the inverting input equals the voltage at the non-inverting input,
- Therefore the **DC gain is 1**, placing the amplifier output at **VDD/2**.

This ensures the output remains centered in the linear operating region of the op-amp.
##### <span style="color:rgb(71, 215, 140)">3. AC Gain (Amplification of the Ultrasonic Signal)</span>

When an AC signal arrives from the piezoelectric sensor, the capacitors now behave approximately as **short circuits** at the ultrasonic frequency.

![[Pasted image 20251121104714.png|400]]

In this case, the amplifier behaves like a **standard non-inverting stage**, whose gain is:
$$A_{AC} = 1 + \frac{R_F}{R_{IN}}  $$
Given:
- ( $R_F = 100 \text{kΩ}$)
- ( $R_{IN} = 1 \text{kΩ}$ )

We obtain: 
$$A_{AC} = 1 + \frac{100,000}{1,000} = 101  $$

Thus, the AC ultrasonic signal is amplified by a factor of **101**, while the DC bias remains unchanged at unity gain.

This configuration is simple but highly effective for reading out piezoelectric ultrasound receivers:

- **DC biasing** ensures proper operation under single-supply conditions,
- **AC gain** provides strong amplification of the received ultrasonic burst.
 
### <span style="color:rgb(161, 40, 226)">Other Operation Modes</span>

Ultrasonic sensors can also operate in alternative modes, particularly for **measuring displacement**.  In this case, the measurement relies on the **Doppler effect**.

#### <span style="color:rgb(2, 141, 192)">1. Displacement Measurement Using the Doppler Effect</span>

According to the Doppler principle, when a sound source and an object move relative to one another, the frequency perceived by the object changes:

![[Pasted image 20251121105503.png|700]]
- If the object is **approaching** the source, it perceives a **higher** sound frequency.
- If the object is **moving away**, it perceives a **lower** frequency.
    
The same effect occurs in the **reflected (backscattered) sound**:

- If the object is moving closer to the sensor, the reflected signal will exhibit an **increased frequency**.
- If it moves away, the reflected frequency decreases.
    

Therefore, the **received frequency varies over time** depending on the movement of the target. For example, if the object oscillates around a central position, the output signal will show a frequency modulation: sometimes slightly higher, sometimes slightly lower than the original transmitted frequency.

This frequency variation can be processed to determine the **velocity** and **displacement** of the moving object.
#### <span style="color:rgb(2, 141, 192)">2. Measuring Medium Density Through Direct Propagation Time</span>

Another operating mode consists of measuring the **direct propagation time** of ultrasound through a medium. This technique is useful for estimating the **density** or **composition** of a substance.

The principle is based on the fact that:
![[Pasted image 20251121105528.png|600]]

- The **speed of sound** in a medium, $c$, **decreases** as the medium’s **density increases**.

In this setup, the **source** and the **receiver** are positioned on **opposite sides** of the medium. The distance between them is fixed.  
The measured **time of flight** between the transmitted pulse and the received pulse therefore depends **only** on the sound velocity ccc, not on distance (which is known and constant).

Since:
$$c = \frac{d}{\text{TOF}}$$

and $c$ is a function of the medium’s density, the sensor can be used to **identify or estimate the type of medium** located between the transmitter and receiver.

### <span style="color:rgb(161, 40, 226)">Applications of Ultrasound Sensors</span>

![[Pasted image 20251121105857.png]]
Ultrasonic sensors have a wide range of practical applications.  In proximity sensing, they are commonly used in **parking systems** to detect whether parking slots are occupied or free.  

![[Pasted image 20251121105912.png]]
For **distance measurement**, ultrasonic sensors are widely implemented in **automotive rear-sonar systems**, where they provide not only a binary indication of an obstacle but also a measurement proportional to the actual distance. This allows the vehicle to inform the driver with a continuous, distance-dependent warning.

![[Pasted image 20251121105925.png]]
As mentioned earlier, ultrasonic devices can also be employed to measure **displacement** or **direct propagation time**, enabling more advanced sensing applications.  For example, they play a fundamental role in **flow meters**, which measure the velocity of liquids flowing through a pipe. In these systems, the Doppler effect is exploited: the frequency of the received ultrasonic wave increases as the flow speed rises. The faster the fluid flows, the larger the frequency shift observed by the sensor.

## <span style="color:rgb(239, 179, 1)">Optical Sensors</span>

Let us now move on to **optical sensors**. As you will notice, they share many analogies with acoustic sensors; however, the key difference lies in the **propagation speed** of the signal. Light travels orders of magnitude faster than sound, which profoundly affects the sensor’s operating principles and performance.
![[Pasted image 20251121112455.png|300]]

Optical sensors can also operate as **proximity sensors**, and—similarly to ultrasound systems—they require a **transmitter** and a **receiver**.  Typically, the transmitter is an **infrared LED** or an **infrared laser diode**. Infrared is preferred because it is **invisible to the human eye**, avoiding visual disturbance.  
The receiver is most often a **photodiode**, which converts the incident light into an electrical current.

![[Pasted image 20251121112513.png|300]]
One major advantage of optical proximity sensors is that they are **immune to electromagnetic interference**, unlike capacitive or inductive proximity sensors, which can be affected by external electromagnetic fields.

However, when designing optical sensors, it is crucial to ensure **immunity to ambient light**, since sunlight or artificial lighting can interfere with photodiode readings. In the next slides, we will discuss methods to achieve this immunity.

Another important benefit of optical techniques is that they can achieve **greater sensing ranges**, both compared to capacitive/inductive sensors and often even compared to acoustic proximity sensors.

There are two main configurations for optical proximity sensing:

### <span style="color:rgb(161, 40, 226)">1. Transmission Configuration</span>

Here, the **transmitter and receiver are placed on opposite sides** of the monitored area.

![[Pasted image 20251121112541.png|400]]

- If no object is present, the emitted light reaches the receiver.
- If an object intervenes, it blocks the beam, and the receiver detects the interruption.

### <span style="color:rgb(161, 40, 226)">2. Reflection (Diffuse) Configuration</span>

In this configuration, the **transmitter and receiver are placed on the same side**.

![[Pasted image 20251121112610.png|300]]

- If no object is present, the emitted light travels forward and does not return to the receiver.
- If an object is in proximity, it **backscatters** part of the light toward the receiver, which detects its presence.
    
These two setups cover most proximity-sensing applications in industrial and consumer systems.


### <span style="color:rgb(161, 40, 226)">Three Main Setups</span>

Optical sensors can be implemented in three main setups: **True Beam**, **Retroreflective**, and **Diffuse**. Let’s analyze each of them in detail.

#### <span style="color:rgb(2, 141, 192)">1. True Beam Setup  </span>

![[Pasted image 20251121113205.png]]
In the True Beam setup, the emitter and the receiver are placed on opposite sides of the target. The presence of a target interrupts the light beam, preventing it from reaching the receiver. This configuration is very robust and precise, allowing detection of very small objects, especially when using focused lasers. It also supports long detection distances, up to tens of meters, and in some cases even up to 100 meters.

The main drawback of this setup is practical: the emitter and receiver need to be installed on opposite sides of the target area, which can be inconvenient in many applications.

#### <span style="color:rgb(2, 141, 192)">2. Retroreflective Setup  </span>

![[Pasted image 20251121113242.png]]

In the retroreflective setup, both the emitter and receiver are placed on the same side. A retroreflective material is positioned opposite the sensor to reflect the light back to the receiver. This setup behaves similarly to the True Beam setup, but it avoids the need to supply power to two separate locations because the source and detector are co-located.

One limitation is that highly reflective targets may return part of the light directly to the receiver, which can be mistaken for the reflection from the retroreflector. To mitigate this, polarization filtering can be used. Certain reflectors are designed to return light with a specific polarization, and the receiver detects only that polarized light, avoiding interference from reflections off the target. The polarization of light refers to the orientation of the electric field vibration in the propagating electromagnetic wave.

#### <span style="color:rgb(2, 141, 192)">3. Diffuse Setup </span>
![[Pasted image 20251121113319.png]]

The diffuse setup is the most widely used configuration. In this case, the target itself reflects or backscatters light to the sensor. The sensor detects the presence of the object when it receives the reflected light.

Unlike the previous setups, here the detection depends on the reflectivity of the target material. High-reflectivity materials may produce a strong signal at shorter distances, while low-reflectivity materials can be detected from farther away.

This setup is especially practical when a fixed reflector or opposite side is not feasible. A common example is a smartphone proximity sensor that turns off the display when you bring the phone close to your face. In such cases, the emitter and receiver must be in the same device, and the target (your head) itself reflects the light.

### <span style="color:rgb(161, 40, 226)">How to Implement An Optical Proximity Sensor?</span>

To implement an optical proximity sensor, the basic components are:
![[Pasted image 20251121113604.png|400]]

1. **Light Source** – Usually an LED or a laser that emits the light.
2. **Photodiode** – Acts as the receiver to detect reflected or backscattered light.
    
A key challenge is **making the sensor immune to ambient light**. For example, a smartphone must detect the light reflected from your head and ignore sunlight, lamps, or other background sources.



The solution is **modulated light**. The LED is driven with a modulated signal, typically a square wave at a high frequency (tens of kilohertz). This allows the sensor to distinguish between the emitted light and slowly varying ambient light.

The signal flow works like this:
![[Pasted image 20251121113718.png|500]]

1. **LED Driver** – Usually a transconductance amplifier that forces the desired current into the LED, generating modulated light.
2. **Photodiode** – Detects the light reflected from the target. The current it produces is proportional to the received light intensity.
3. **Transimpedance Amplifier (TIA)** – Converts the photodiode current into a voltage signal that can be further processed.
4. **High-Pass Filter** – Filters out DC and slow-varying components, passing only the modulated signal corresponding to the LED frequency. This removes interference from ambient light.
5. **Analog-to-Digital Converter (ADC)** – Digitizes the filtered signal so it can be read by a microcontroller or other digital system via standard protocols such as I²C or SPI.
    
By using this combination of modulation, filtering, and amplification, the sensor can reliably detect proximity while ignoring external light sources.


### <span style="color:rgb(161, 40, 226)">Optical distance measurement using time-of-flight (ToF):</span>  

When measuring **distance** with optical sensors, we exploit the **time of flight** of light, instead of sound as in acoustic sensors.  

***Basic principle:***
1. **Transmitter:** Typically a laser is used because it can generate very short light pulses.  
2. **Propagation:** The pulse travels to the target and is partially backscattered in all directions.  
3. **Receiver:** A photodiode or a single-photon avalanche diode (SPAD) detects the returning light.  
4. **Time Measurement:** The **time delay** between emission and detection, \(\Delta t\), is measured using a **time-to-digital converter (TDC)**.  

![[Pasted image 20251121114115.png|400]]

***Distance Calculation:***
The distance \(d\) is calculated as:
$$d = \frac{c \cdot \Delta t}{2}$$
- $(c)$ is the speed of light, approximately ($3 \times 10^8 \, \text{m/s}$).  
- The division by 2 accounts for the round-trip of the light pulse.  

***Resolution Considerations:***
- Because light is extremely fast, $(\Delta t)$ must be measured with very high precision.  
- For example, a time resolution of 300 picoseconds corresponds to a distance resolution of about **5 cm**.  
- Compared to acoustic sensors, which can reach **micrometer resolution**, optical ToF sensors typically achieve **centimeter-level resolution**.  

**Key Takeaways:**
- Optical ToF is excellent for longer ranges and high-speed measurements.  
- However, it is limited in precision compared to acoustic time-of-flight methods due to the extremely high speed of light.  

#### <span style="color:rgb(2, 141, 192)">Working Sensor - Time-correlated single photon counting (TCSPC)</span>
In optical time-of-flight measurements, the receiver can be a **photodiode** or, more commonly, a **single-photon avalanche diode (SPAD)**.

##### <span style="color:rgb(71, 215, 140)">Why not just a photodiode?</span>
- A photodiode detects many photons simultaneously and reproduces the pulse shape of the returning light.
- This works well if the returning pulse is strong, which happens at short distances or with highly reflective targets.
- However, for **long distances** or **low-reflectivity targets**, the pulse is heavily attenuated. You may receive **only one photon or even none per pulse**.
- Increasing the laser intensity is often limited due to **safety regulations**, especially for infrared lasers.
    
**The solution: Single-Photon Avalanche Diode (SPAD)**

- A SPAD can detect **even a single photon**.
- Because a single measurement may not detect any photons, the laser pulse must be **repeated many times**.
    
##### <span style="color:rgb(71, 215, 140)">How it works:</span>
![[Pasted image 20251121114829.png|400]]
1. Fire a laser pulse.
    - Measurement 1: no photon detected.
    - Measurement 2: one photon detected at some time.
    - Measurement 3: another photon detected at a different time, and so on.
2. After many repetitions, you can build a **histogram of photon arrival times**.
3. This histogram reconstructs the **shape of the original laser pulse**, because the probability of detecting a photon is higher when the pulse is stronger.
    
**Distance extraction:**

- You can apply a **threshold** to the histogram to detect the pulse arrival time.
- Alternatively, you can compute the **centroid of the distribution** to achieve **better precision**.

##### <span style="color:rgb(71, 215, 140)">Advantages and disadvantages:</span>

- **Advantages:**
    - Can detect very weak signals.
    - Works for long distances or low-reflectivity objects.
    - No need for powerful laser pulses.
        
- **Disadvantages:**
    - Requires many repetitions of the laser pulse.
    - Needs a high-frequency laser to acquire sufficient data quickly.

This method is known as **time-correlated single photon counting (TCSPC)** and is widely used in high-precision distance sensing applications.

#### <span style="color:rgb(161, 40, 226)">Example and Applications</span>

So, an example of application of time-of-flight optical sensors is what we call **LiDAR**, which stands for **Light Detection and Ranging**. Sometimes it is also called **Laser Imaging Detection and Ranging**. The idea is to reconstruct a **three-dimensional environment** using a sensor that measures distances very precisely.

![[Pasted image 20251121115409.png|300]]

For instance, imagine a **drone flying over an area of interest**. The LiDAR sensor emits laser pulses toward the ground, and these pulses are reflected back by the objects in the environment. The sensor measures the **time it takes for the light to travel to the object and back**, and from this time-of-flight, it calculates the distance of each point.

In many visualizations, the color of the points does not represent the actual color of the object. Instead, it represents distance. For example, in some visualizations, **blue can represent points that are closer to the drone**, and **orange can represent points that are farther away**. In this way, you can see a 3D map of the environment, where the depth information is encoded in color.
#### <span style="color:rgb(2, 141, 192)">TOF sensor Chip</span>

![[Pasted image 20251121115500.png|500]]

Now, let’s consider a **time-of-flight sensor chip**. In these chips, you have the **LED or laser driver**, which generates the light pulses, and a **sensor array**, for example, a **SPAD array** (Single Photon Avalanche Diode array), which can detect even single photons. This is very important, because in some cases, the reflected light is very weak, especially if the target is far away or has a low reflectivity.

The advantage of using this kind of sensor, compared to standard amplitude-based proximity sensors, is that we measure **actual distance** rather than relying on how strong the reflected signal is. Standard sensors might fail to detect very dark objects because the reflected signal is too weak. With a time-of-flight sensor, the measurement depends on the **time delay**, so you can detect objects reliably regardless of their surface reflectivity.

Practical examples of these sensors include:

- **Enhanced proximity sensors**: These are used in situations where you want to detect the presence of an object reliably, even if it has very low reflectivity.
- **Smartphones**: For example, in the front camera, a time-of-flight sensor can be used to measure the distance to the subject and **automatically adjust the focus**.
- **Public washroom sinks**: The sensor detects hands and activates the water tap automatically.
- **Automotive applications**: In autonomous or assisted driving, LiDAR sensors reconstruct the environment in front of the vehicle. They detect other cars, pedestrians, or obstacles. This is extremely useful for navigation and safety.
    

Finally, time-of-flight principles are also applied in **optical encoders**, which we will study in a bit. These encoders allow us to measure **linear or angular displacement** with high precision.


## <span style="color:rgb(239, 179, 1)">Proximity / Distance Sensors Comparison</span>

![[Pasted image 20251121115713.png]]

So, we have studied **capacitive sensors, inductive sensors, acoustic sensors, and optical sensors**.  

Let’s start with **capacitive sensors**. These sensors typically have the **shortest sensing range**. They are able to detect objects only if they are in **close proximity**, usually **just a few centimeters at most**. Their main advantage is the **high sensitivity to non-metallic materials**, but of course, the short range is a limitation.  

Then, we have **acoustic sensors**. These sensors can detect objects at **intermediate ranges**, typically **1, 2, or 3 meters**. Acoustic sensors work by sending ultrasound waves and measuring either the **time of flight** or **amplitude variations**. Their advantage is that they can cover **longer distances than capacitive sensors**, but the resolution is not as high.  

Next, **optical sensors**. These sensors can reach **much higher distances** than the previous ones. For example, **optical proximity sensors** can reach tens of meters, around **50 meters**, while time-of-flight systems like **LiDAR** can measure distances even in the **order of kilometers**. Optical sensors are very useful for **long-range detection**, but one thing to keep in mind is that their **resolution is generally lower than acoustic sensors** when measuring very small displacements.  

Finally, **inductive sensors**. These sensors are **particularly suited for detecting metallic objects**. They work by generating eddy currents in the metal, which influences the oscillator in the sensor. Their range is usually short to medium, similar to capacitive sensors, but they are very robust for **metal detection**.  

So, in summary:  

- **Capacitive sensors** → short range, non-metallic materials, very sensitive.  
- **Inductive sensors** → short/medium range, metallic materials, robust detection.
- **Acoustic sensors** → medium range (meters), non-contact, good resolution.  
- **Optical sensors** → long range (tens of meters to kilometers), less precise than acoustic, very flexible, especially for time-of-flight measurements like LiDAR.  

The choice of the sensor **depends on the application**, the **required sensing range**, and the **type of material you want to detect**.  
# <span style="color:rgb(223, 109, 109)"></span><span style="color:rgb(223, 109, 109)">Encoders</span>

So, let’s now move to **encoders**. Encoders form an entire family of sensors that are used to measure **displacement**, but they differ significantly from the displacement sensors we have studied so far—such as potentiometers or capacitive and inductive displacement sensors. The key difference is that **encoders provide a digital output directly**. This means they do **not** require triggers or analog-to-digital converters to interpret their signal. The encoder itself already outputs digital information.

We can classify displacement encoders into two main groups:

- **Rotary encoders**, which respond to rotational motion, and
- **Linear encoders**, which respond to linear displacement.
    
Both rotary and linear encoders can be implemented in two different architectures: **incremental** or **absolute**.

### <span style="color:rgb(161, 40, 226)">Incremental Encoder</span>

In an **incremental encoder**, the sensor generates a sequence of digital pulses as the shaft or slider moves. These pulses do not directly tell you the absolute position; instead, they tell you how much the position changes. For this reason, incremental encoders are typically used to measure **rotation speed** or **relative displacement**. You simply count the number of pulses per unit time or per revolution.

### <span style="color:rgb(161, 40, 226)">Absolute Encoder</span>

Instead, in an **absolute encoder**, the output at every position is a **unique digital word**—a multi-bit value. This means that at any moment you can read the encoder and know exactly in which position it is, without needing to know the previous positions. So absolute encoders give you the **true, absolute position** of the sensor.

Encoders can be implemented using **optical** or **magnetic** technologies.

- Optical encoders are preferred when a **very high resolution** is required, because light-based detection allows extremely fine position measurement.
- Magnetic encoders, on the other hand, are more robust and reliable in **harsh environments**, where dust, oil, vibration, or temperature variations would compromise optical components.

## <span style="color:rgb(239, 179, 1)">Optical Encoders</span>

Let us begin with **optical encoders**.

| ![[Pasted image 20251121132100.png]] | ![[Pasted image 20251121132109.png]] |
| ------------------------------------ | ------------------------------------ |
Optical encoders consist of a **glass disc** (for rotary encoders) or a **glass strip** (for linear encoders). On the surface of this disc or strip, a **pattern of opaque and transparent lines** is deposited. These lines play a fundamental role: they either allow an optical beam to pass through or they block it.

To operate, this type of sensor requires at least **one LED** on one side of the disc or strip, and a **photodiode** on the opposite side. The LED emits a beam of light. Whenever the transparent regions of the disc align with the LED and the photodiode, the light reaches the photodiode. Whenever an opaque line is in the way, the light is blocked. Therefore, as the disc or strip moves, the photodiode outputs a sequence of light/no-light signals, which are converted into digital pulses.

![[Pasted image 20251121132239.png]]
In **incremental encoders**, the disc usually contains **one or several equally spaced tracks** of lines. The encoder only produces a series of pulses, and these pulses correspond to the displacement.  
In contrast, in **absolute encoders**, the disc contains **multiple concentric tracks**, each representing a bit of a digital word. At any given position, all tracks together form a multi-bit code that corresponds to the absolute position of the sensor.

Let us examine incremental encoders more closely.

Incremental encoders generate a certain number of pulses as the disc or strip moves. These pulses can be used, for example, to measure the **speed of rotation** (in the case of rotary encoders) or the **linear displacement** (in the case of linear encoders).

There are two typical types of output in incremental encoders:
![[Pasted image 20251121132333.png]]

1. **Single-channel output**  
   In this case, the encoder provides only one square wave. The frequency of this wave depends on how fast the encoder is moving. However, with only one channel, it is impossible to determine the **direction** of the motion. You can measure how fast it is moving, but not whether it is moving forward or backward.

![[Pasted image 20251121132402.png]]

2. **Quadrature output**  
   To also obtain directional information, two channels are used: **channel A** and **channel B**. These channels are shifted in phase by 90 degrees (in quadrature).  
   This phase shift allows the system to determine the direction:  
   - If A leads B, the encoder is rotating (or moving) in one direction, for example clockwise.  
   - If B leads A, the encoder is rotating in the opposite direction, for example counterclockwise.

This same principle applies to linear encoders, where the direction would correspond to motion toward the right or toward the left.
![[Pasted image 20251121132455.png]]

In addition to channels A and B, many incremental encoders also include a **marker** (often called the index or Z signal). This marker provides a pulse once per revolution (for rotary encoders) or at a specific reference position (for linear encoders).  This index pulse serves as a known **zero position**. Once this reference has been detected, the system can count all subsequent pulses to compute the exact position relative to that zero.

![[Pasted image 20251121132742.png]]
In an **absolute encoder**, unlike an incremental encoder, you do **not** need to count pulses to determine the current position. The reason is that the position is **directly encoded** by the pattern of bits defined on the disc (or strip).  
Each angular position corresponds to a unique combination of bits, and this combination can be read at any moment.

In the example shown, the encoder produces **four bits**. This means the disc has **four concentric tracks**, and therefore you need **four photodiodes**, one for each track. Each photodiode detects whether light has passed through its corresponding track.  
So, for a given position:

- If the light is blocked for a particular track, the corresponding bit is **0**.
- If the light passes through and reaches the photodiode, the corresponding bit is **1**.
    
For instance, if the disc is in a specific angular position where the inner two tracks are opaque and the outer two tracks are transparent, the resulting code would be 0 0 1 1. This code uniquely identifies that angular position.

The position information can be encoded using **binary code** or **Gray code**.
![[Pasted image 20251121132756.png|200]]

Let us compare them:

1. **Binary code**  
    In binary, the code for each position follows the standard binary numbering. For example:
    
    - 0 = 000
    - 1 = 001
    - 2 = 010  
        Here, when you go from position 1 (001) to position 2 (010), two bits change simultaneously.
        
2. **Gray code**  
    Gray code also uses only 0s and 1s, but with an important constraint: **only one bit changes between two consecutive positions**.  
    Using the same example:
    
    - 0 = 000 (same as binary)
    - 1 = 001 (same as binary)
    - 2 = 011 (different from binary 010)  
        In this transition from 001 to 011, only a single bit changes.
        

The reason Gray code is preferred in many encoders is technological. When the disc rotates, the photodiodes might not detect all bit transitions at the exact same instant if several bits are changing at once. In binary code, a multi-bit transition could cause momentary “wrong” readings. Gray code avoids this because **only one bit transitions at a time**, reducing reading errors during movement.

Additionally, from a manufacturing perspective, it is easier to design and mask the disc using Gray code, because the transitions between neighbouring positions require less stringent alignment precision.

## <span style="color:rgb(239, 179, 1)">Magnetic Encoder</span>


Another type of encoder that we can use is the **magnetic encoder**. Magnetic encoders are often preferred in environments where optical encoders might be affected by dust, dirt, or vibration, because they are more robust.
![[Pasted image 20251121133109.png]]

There are two main types of magnetic encoders. The first type is the **variable reluctance sensor**.  

In a **variable reluctance sensor**:  
- The rotating element is typically a **metallic gear** or a toothed wheel.  
- The sensor detects changes in **magnetic reluctance** caused by the movement of the teeth. As the metallic teeth pass near the sensor, they alter the path of the magnetic flux.  
- This change in magnetic flux induces a voltage in a coil, which generates a **digital pulse** for each tooth.  
- By counting these pulses, the sensor can measure the **rotational speed** of the gear.  

Variable reluctance sensors are generally **incremental**, meaning they produce pulses proportional to rotation, but they do not provide the absolute position of the gear. They are widely used in **automotive applications**, such as measuring the speed of crankshafts or wheels.

### <span style="color:rgb(161, 40, 226)">Magnetic Reluctance</span>

Before analyzing the working principle of the sensor itself, it is important to review the concept of **magnetic reluctance**.

Magnetic reluctance in a magnetic circuit is analogous to **resistance in an electrical circuit**. In particular, we can write:
$$\mathcal{R} = \frac{F}{\Phi}  $$

Where:

- $(\mathcal{R})$ is the magnetic reluctance,
- (F) is the **magneto-motive force (MMF)**, and
- $(\Phi)$ is the **magnetic flux**.
    
The **magneto-motive force** (F) is the line integral of the magnetic field intensity $(H)$, while the flux $(\Phi)$ is the area integral of the magnetic flux density $(B)$.

### <span style="color:rgb(161, 40, 226)">Variable Reluctance Working Principle</span>

![[Pasted image 20251121133609.png]]

Now, imagine we have a **rotating ferrous gear** and a **permanent magnet** generating a constant MMF. As the gear rotates:


![[Pasted image 20251121133701.png]]

- When a tooth is in proximity (left) to the sensor, the magnetic flux lines concentrate in the tooth, producing a **high flux**.
- When the sensor is between two teeth (right), the flux decreases because the path of least reluctance is interrupted.

![[Pasted image 20251121133609.png]]
Since the magneto-motive force (F) is constant, these variations in flux ($\Phi$) correspond to changes in **magnetic reluctance**.

We can place a **coil** near this system to take advantage of **Faraday’s Law**. The law tells us that a time-varying flux ($\Phi$) through a coil induces a voltage (V) across the coil:
$$V = -N \frac{d\Phi}{dt}$$

Where (N) is the number of turns in the coil. Therefore, as the gear rotates, the induced voltage across the coil changes, and this voltage can be measured to determine the rotation speed or position of the gear.

Instead of using a permanent magnet, we can also generate a **fixed magnetic field with the coil itself**:
![[Pasted image 20251121134014.png|300]]

- By providing a **DC current** to the coil, a magnetic field (B) is generated perpendicular to the coil section.
- The rotating gear changes the **reluctance** of the magnetic path, altering the flux through the coil.
- Again, these variations in flux induce a voltage that can be measured to monitor the rotation.

In summary, **variable reluctance sensors detect changes in magnetic flux caused by a rotating ferrous element**, and by measuring the induced voltage in the coil, we can infer rotational motion.

### <span style="color:rgb(161, 40, 226)">Magnetic Wheel Encoders</span>

Another way to implement a **magnetic encoder** is to use a **magnetic wheel**.  

![[Pasted image 20251121134248.png]]

In this configuration, the wheel can carry a **single permanent magnet**, and we place **two Hall effect sensors** nearby to detect the magnetic field generated by the magnet.  

If the two Hall sensors are placed with a **90-degree phase difference**, we obtain a **quadrature incremental encoder**. Why? Because:  
- As the wheel rotates, each Hall sensor detects the magnetic field at slightly different times due to their phase shift.  
- This phase difference allows us to determine **not only the number of rotations** (like a simple incremental encoder) but also the **direction of rotation**, just like with quadrature optical encoders.  

![[Pasted image 20251121134321.png]]
Another possibility is to use **many permanent magnets** arranged around the wheel.  

- In this case, a single Hall sensor can be used to produce a **single-channel output**, which generates pulses as each magnet passes by the sensor.  
- This setup works as a **standard incremental encoder** and allows measuring the **rotation speed** with high precision.  

With a **single magnet**, you can measure the **average rotational speed** or the **frequency of rotation** over a full turn. With **multiple magnets**, you can measure the rotational speed more precisely, even for **subsections of a revolution**, which increases the temporal resolution of your measurement.  
	
In summary, magnetic encoders using Hall sensors are versatile and can provide either incremental information or directional speed information depending on the number of magnets and the sensor configuration.  

### <span style="color:rgb(161, 40, 226)">Applications</span>

**How to use magnetic encoders:**

Magnetic encoders are particularly useful as **non-contact sensors**, which means they do not require mechanical contact to measure motion. This makes them **very reliable**, even in **harsh environments** where dust, dirt, or vibration could affect traditional sensors.

One common application is the **variable reluctance sensor**, which can measure the **rotation speed of gears or wheels**. For example:

- **Motors:** Magnetic encoders can measure the rotational speed, which is useful for **ABS systems** in cars.
- **High-precision positioning:** They can measure the rotation of gears with **high accuracy**, useful in robotics or industrial machines.
- **Human-machine interfaces:** They can be used to detect precise rotations or positions in control knobs, joysticks, or other input devices.
    
In general, magnetic encoders provide **robust, precise, and reliable measurements** for both rotational and linear applications, complementing optical or other displacement sensors depending on the environment and required resolution.