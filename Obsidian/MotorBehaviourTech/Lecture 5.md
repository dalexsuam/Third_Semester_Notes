
Date: 25/09/2025
***

## <span style="color:rgb(239, 179, 1)">EMG Noise sources</span>

When recording an electromyographic (EMG) signal, several **noise and interference sources** affect the measurement. These noises can be classified in different ways depending on **where they originate** and **their frequency content**.

![[Pasted image 20250925163555.png]]
### <span style="color:rgb(161, 40, 226)">1. Noise before and after the measurement</span>

#### <span style="color:rgb(2, 141, 192)">Noise <b>before</b> the electrode measurement</span>
These disturbances exist **on the body itself**, before the signal crosses the electrode–skin interface:

- **Electromagnetic interference (EMI)**  
    The human body acts like an antenna and picks up environmental electromagnetic fields (e.g. 50/60 Hz mains, lamps, computers, mobile phones).
    
- **Physiological interference**  
    Signals generated inside the body but not related to the target muscle:
    - ECG (especially when measuring near the chest)
    - Activity of nearby muscles (cross-talk)
    - Nerve activity
        
These noises are often unavoidable and depend on electrode placement and anatomy.

#### <span style="color:rgb(2, 141, 192)">Noise <b>at the electrode interface</b></span>

The **electrode–skin impedance** plays a critical role:

- It is **variable**, depending on:
    - Temperature
    - Ionic activity in the electrolyte
    - Skin condition
- Variations in impedance introduce noise and distortions exactly at the measurement boundary.
    
#### <span style="color:rgb(2, 141, 192)">Noise <b>after</b> the measurement</span>

Once the signal has crossed the electrodes, additional interferences appear:

- **Stray capacitive currents**  
    Cables act as antennas and couple capacitively with surrounding electrical devices.
    
- **Movement-related noise**  
    When the patient or cables move:    
    - Cable position changes
    - Parasitic capacitances change
    - Induced noise varies over time
        
- **Loop-induced magnetic interference**  
    The wires from electrodes to amplifier form a loop:
    - A changing magnetic field induces a voltage (Faraday’s law)
    - Loop area and orientation change with movement → variable noise
        

![[Pasted image 20250925164840.png|400]]

### <span style="color:rgb(161, 40, 226)">2. Frequency-based classification</span>

#### <span style="color:rgb(2, 141, 192)">Low-frequency noise</span>

Typically affects the **baseline** of the EMG signal:
- Amplifier DC offset and thermal drift
- Skin temperature fluctuations
- Electrode impedance variations
- Movement artifacts (0–10 Hz, differential)
- Power-line interference (50 Hz in Europe, 60 Hz elsewhere – common mode)
    
#### <span style="color:rgb(2, 141, 192)">High-frequency noise</span>

Overlaps with or exceeds the EMG bandwidth:

- Nerve action potentials
- Activity of other muscles
- Radio broadcasts
- Computers, mobile phones
- Fluorescent and energy-saving lamps

### <span style="color:rgb(161, 40, 226)">3. Exogenous vs. endogenous noise</span>

#### <span style="color:rgb(2, 141, 192)">Exogenous noise (external to the body)</span>

- Skin–electrode interface noise
- Movement artifacts (0–10 Hz, differential)
- Coupling with electric and magnetic fields  
    → Usually **common mode** if electrodes are close together
#### <span style="color:rgb(2, 141, 192)">Endogenous noise (generated inside the body)</span>

- ECG
- Other muscles
- Nerve activity
    
These signals are often **common mode** if electrodes are far from the noise source, but can become **differential** if electrodes are close to the source (e.g. ECG when recording on the chest).

### <span style="color:rgb(161, 40, 226)">4. Why this classification matters</span>

Understanding noise origin and type is essential to:

- Design **proper filtering** (low-pass, high-pass, notch)
- Choose **electrode size and spacing**
- Maximize **CMRR** using differential amplifiers
- Improve overall **signal-to-noise ratio (SNR)**
    
### <span style="color:rgb(161, 40, 226)">One-sentence takeaway</span>

> EMG noise arises from physiological sources, electrode interfaces, and environmental coupling, and it must be managed through electrode design, differential amplification, high CMRR, filtering, and electrical isolation.

### <span style="color:rgb(161, 40, 226)">Example of Noisy EMG signal</span>

![[Pasted image 20250925165705.png]]

A typical example of **movement artifacts** in EMG is the **baseline shift**. During repetitive muscle activity (for example walking), the **true EMG signal** should oscillate around a stable baseline. However, when **movement artifacts** are present—such as **electrode–skin or electrode–electrolyte displacement** caused by body motion—the recorded signal shows a **slowly varying baseline**.

This baseline drift:
- Appears as **low-frequency components** (usually **below 10 Hz**)
- Is not related to real muscle activation
- Causes the signal baseline to move up and down over time
    
The unstable baseline is mainly due to:
- Motion of the patient
- Motion of the skin relative to the electrode
- Changes in electrode impedance during movement

Since movement artifacts are **low-frequency (LF) noise**, they can be **effectively reduced or removed using high-pass filtering**, without significantly affecting the useful EMG signal.

## <span style="color:rgb(239, 179, 1)">Noise Reduction Techniques</span>
### <span style="color:rgb(161, 40, 226)">Noise reduction techniques I – <b>Hardware design</b></span>

![[Pasted image 20260102111610.png|400]]
Many EMG noise sources can be reduced **already at the hardware level** by proper system design:

- **Reduce cable loop area**
    - Use **short cables**
    - Keep wires **close together** and **twisted**
    - Twisting helps cancel magnetic-field–induced noise because the magnetic flux affects adjacent loops in opposite directions
        
- **Use shielded cables**
    - A shielded cable has a **conductive sleeve** around the signal wires
    - The shield is kept at a constant potential (often ground or reference), reducing **capacitive coupling** with external electric fields
    - This strongly reduces electromagnetic interference (EMI)
        
- **Proper electrode–skin coupling**
    - Ensure **good adhesion** of electrodes to minimize motion artifacts
    - Use appropriate skin preparation and gel
        
- **Correct electrode placement**
    - Avoid placing electrodes **too close to the heart** to reduce ECG crosstalk
    - Avoid nearby active muscles if they are not the target
    - Choose a suitable **inter-electrode distance** for the desired working volume
        
- **Stable wiring and fixation**
    - Prevent cable movement relative to the body to reduce motion-induced noise
        

> ⚠️ **Important note**: EMG signals can be contaminated by **cardiac activity (ECG)**, typically visible as low-frequency components (~1 Hz). Correct and stable electrode placement is essential to minimize this crosstalk.


### <span style="color:rgb(161, 40, 226)">Noise reduction techniques II – Signal pre-processing optimization (additional devices)</span>

This second group of techniques acts **after the signal is picked up by the electrodes**, at the **input stage of the EMG acquisition system**. The goal is to **prevent common-mode noise from being converted into differential noise**, which cannot be removed later.

![[Pasted image 20250925170212.png]]
#### <span style="color:rgb(2, 141, 192)">1. High input impedance</span>
![[Pasted image 20260102142545.png]]
- EMG electrodes have **time-varying impedances** (temperature, sweat, motion).
- If the amplifier input impedance is **not very high**, small impedance differences between electrodes:
    - convert **common-mode voltage** into a **fake differential voltage**
    - this fake differential noise **cannot be canceled**, even with a differential amplifier.

**Solution**
![[Pasted image 20260102142601.png]]
- Use amplifiers with **very high input impedance**:
    - Resistive: $10^7$ to $10^{12}\,\Omega$
    - Capacitive: a few pF
- This minimizes current flow and **reduces impedance asymmetry effects**.

#### <span style="color:rgb(2, 141, 192)">2. Differential input stage with very high CMRR</span>

- EMG is measured as **V2 − V1**, not absolute voltage.
- Environmental noise (50–60 Hz, EMI) appears mostly as **common-mode voltage**.
    
**Instrumentation amplifier (INA)**
- High **differential gain** (≈ 60–80 dB)
- Very low **common-mode gain**
- **CMRR up to 100–120 dB**
- High input impedance on both inputs
👉 This strongly suppresses common-mode noise **before amplification**.

#### <span style="color:rgb(2, 141, 192)">3. Effect of unbalanced impedances (why high input impedance matters)</span>

![[Pasted image 20250925174227.png|500]]


Even with a perfect differential amplifier:
- If:
    - electrode impedances are unequal    
    - or amplifier input impedances are unequal
then a **common-mode voltage $V_c$​** generates a **fake differential voltage**.

This means:
- Noise at 50–60 Hz leaks into the EMG band
- The problem is **structural**, not fixable by filtering
    
**Key idea**
> The more balanced the impedances and the higher the input impedance, the higher the effective CMRR.

#### <span style="color:rgb(2, 141, 192)">4. Negative feedback – Right Leg Drive (RLD) circuit</span>
![[Pasted image 20260102141806.png|200]]
- The body picks up large common-mode voltage from the environment.
- The RLD circuit:
    - senses the **common-mode voltage**
    - inverts it
    - feeds it back into the body via the **reference electrode**

**Effects**
- Strong reduction of common-mode voltage on the subject
- Improved CMRR
- Increased patient safety (current limited by resistors)
![[Pasted image 20260102141836.png|300]]
📌 Common in ECG and multichannel EMG systems.

#### <span style="color:rgb(2, 141, 192)">5. Ground or floating?</span>

![[Pasted image 20260102141940.png|300]]

- **Grounding the patient is risky**
- Standards (IEC 60601) recommend **floating applied parts** (BF class)
- Floating systems:
    - reduce leakage currents
    - reduce ground-loop noise
    - improve safety
**Alternative**

![[Pasted image 20260102142001.png|500]]
- Active cable shielding:
    - shield connected to common-mode voltage instead of ground
    - minimizes capacitive currents without grounding


![[Pasted image 20250925174710.png]]

#### <span style="color:rgb(2, 141, 192)">Example</span>

![[Pasted image 20250925175156.png]]

![[Pasted image 20250925182640.png]]

![[Pasted image 20250925182933.png]]



In EMG systems, electrodes are **directly connected to the patient** (applied parts, BF class).  
Therefore, the patient **must be electrically isolated from the power network (mains)** to:

- prevent **electric shock**    
- limit **leakage currents** to < 100 µA
- avoid ground loops and mains-related noise
    
Isolation must apply to:
1. **Power supply**
2. **Signal path**

##### <span style="color:rgb(71, 215, 140)">1. Magnetic isolation (transformers)</span>

- Uses **magnetic coupling** between primary and secondary coils
- **No direct electrical connection** (galvanic isolation)
- Can isolate **both signal and power**
- Very common in medical devices
⚠️ Transformers only work with **time-varying signals**  
→ DC signals must be **modulated** before isolation

##### <span style="color:rgb(71, 215, 140)">2. Optical / radio isolation</span>

- Signal converted into:
    - light (optocouplers, optical fiber)
    - RF signal
- Completely galvanically isolated
- Ideal when:
    - subject moves a lot
    - long distances are needed
⚠️ Requires **batteries** on the patient side

##### <span style="color:rgb(71, 215, 140)">3. Capacitive isolation</span>

- Signal transferred through **capacitors**
- Cheap solution
- Limited bandwidth and poorer noise immunity
- Rarely used in EMG
![[Pasted image 20250925183032.png|500]]
**Isolation amplifiers (e.g. AD210, AD202)**

An **isolation amplifier** integrates:
- modulation
- isolation barrier
- demodulation
    
All inside one certified medical component.

**Two-port structure**
- Input side (patient side): floating, isolated, low-voltage 
- Output side: connected to mains and data acquisition

**Why modulation is needed**

Transformers cannot pass DC:
$$\text{emf} = -\frac{d\Phi}{dt}$$
So:
- A **constant voltage gives zero output**
- The EMG signal must be **converted into a high-frequency signal**

##### <span style="color:rgb(71, 215, 140)">Frequency modulation (FM)</span>
![[Pasted image 20260102143434.png]]
- EMG signal $m(t)$ modulates a carrier:

$$f_i(t) = f_c + k_s$$
![[Pasted image 20260102143522.png]]

- Implemented with a **voltage-controlled oscillator (VCO)**
- Varicap diodes often used
    
High frequency advantages:
- Smaller transformer
- Lower parasitic effects
##### <span style="color:rgb(71, 215, 140)">Demodulation (PLL)</span>
![[Pasted image 20250925184000.png|600]]
On the output side:
- A **Phase-Locked Loop (PLL)** reconstructs the carrier
- The PLL:
    - locks to the modulated signal
    - extracts the low-frequency EMG signal
- High-frequency components are removed with a **low-pass filter**





