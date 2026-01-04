
***
Date:24/09/2025


# <span style="color:rgb(223, 109, 109)">Requirements - Noise Artifacts</span>
![[Pasted image 20250924084206.png]]

# <span style="color:rgb(223, 109, 109)">Measurement artifacts in surface EMG</span>

![[Pasted image 20250924084215.png|500]]

When using **surface electrodes during movement**, the recorded signal can be contaminated by **measurement artifacts**, i.e. signals that do **not reflect true muscle activity**.

## <span style="color:rgb(239, 179, 1)">Main sources of artifacts</span>
1. **Electrode–electrolyte–skin movement**
    - Motion changes the **double-layer capacitance** at the electrode–skin interface
    - This mainly affects **polarizable electrodes** (strong capacitive behavior)
    - Results in low-frequency noise that can mimic muscle activity
    - **Mitigation**: stabilize electrodes and use **ideally non-polarizable electrodes** (e.g. Ag–AgCl), which behave mostly resistively
        
2. **Electrolyte–tissue displacement**
    - Movement of gel or tissue under the electrode alters the interface properties
    - Produces additional low-frequency artifacts
        
3. **Temperature variations**
    - Changes the **half-cell potential** (via the Nernst equation)
    - Differences in electrode temperature cause slow voltage drifts
        
4. **Sweating / electrolyte concentration changes**
    - Alters the **chemical activity** of the electrolyte
    - Leads to slow potential variations unrelated to muscle activation
### <span style="color:rgb(161, 40, 226)">Key characteristics</span>

- Artifacts are mainly **low-frequency**
- They **superimpose** on the true EMG signal and can distort interpretation

### <span style="color:rgb(161, 40, 226)">Practical takeaway</span>

To reduce measurement artifacts:
- Use **Ag–AgCl (non-polarizable) electrodes**
- Ensure **good fixation** and minimal electrode motion
- Control **temperature** and **skin preparation**
- Be cautious when interpreting low-frequency components during movement

## <span style="color:rgb(239, 179, 1)">Requirements for EMG signal conditioning</span>

When designing the **front-end electronics**, you must account for both **signal levels** and **noise sources** at the electrode–skin interface.

![[Pasted image 20260102090129.png|500]]
### <span style="color:rgb(161, 40, 226)">1. Electrode–skin impedance<br></span>
- Contact impedance (resistive + capacitive) typically in the range:
    - **~10 kΩ to 1 MΩ**
- ⇒ The amplifier must have **very high input impedance** to avoid signal attenuation and distortion.
### <span style="color:rgb(161, 40, 226)">2. Half-cell (electrode) potential</span>

- Ag–AgCl electrodes generate a **half-cell potential up to ~200 mV**, variable over time.
- This is **much larger than the EMG signal** (µV–mV).
- **Solution**:
    - Use **differential recording**
    - Common half-cell potentials are largely **cancelled** at the amplifier input.
### <span style="color:rgb(161, 40, 226)">3. Thermal (Johnson) noise</span>

- Intrinsic noise from resistive elements at the interface:    
$$V_{\text{th,RMS}} = \sqrt{4kTRB}$$
where:
- $k$: Boltzmann constant
- $T$: temperature
- $R$: resistance
- $B$: bandwidth
    
**Example**:
- $R = 10\,k\Omega$, $T = 303\,K$, $B = 200\,Hz$
- $V_{\text{th}} \approx 0.18\,\mu V$
    
**How to reduce it**:
- Reduce **bandwidth** of the EMG amplifier
- Reduce **effective resistance** (good skin prep, good electrodes)

### <span style="color:rgb(161, 40, 226)">4. Ionic exchange noise</span>

- Due to **random ionic movements** at the electrode–tissue interface
- Often **comparable to or larger than thermal noise**
- Cannot be eliminated, only **minimized** with:
    - Stable electrodes
    - Non-polarizable materials (Ag–AgCl)
    - Good mechanical fixation
### <span style="color:rgb(161, 40, 226)">5. Expected EMG signal amplitude</span>

- **From noise level (µV)** up to:
    - **5–6 mV** for surface EMG on large muscles
        
- ⇒ The system must:
    - Detect **very small signals**
    - Avoid saturation from DC offsets and half-cell potentials

### <span style="color:rgb(2, 141, 192)">Key design takeaways<br></span>
- High **input impedance** amplifier
- **Differential acquisition** to cancel half-cell potentials
- **Bandwidth limitation** to reduce thermal noise
- Stable, **non-polarizable electrodes**
- Front-end designed for **µV to mV signals**

## <span style="color:rgb(239, 179, 1)">Overpotentials at the electrode–electrolyte interface</span>

![[Pasted image 20250924085845.png|500]]
Up to now, we discussed the **half-cell potential at equilibrium** $E_0$​, measured when **no current flows**.  However, **real measurements always involve some current**, even if very small (input bias currents, leakage, motion-induced currents, etc.).

When **current flows**, the electrode is no longer at equilibrium, and the electrode potential shifts from its standard value:
$$E_0 \;\longrightarrow\; E_c$$
This shift is called **overpotential**.

### <span style="color:rgb(161, 40, 226)">1. Ohmic overpotential</span>

- Caused by the **finite resistance of the electrolyte and interface**
- Proportional to:
    - the **current**
    - the **electrolyte resistance**
- Similar to a voltage drop across a resistor:
$$\eta_{\text{ohmic}} \approx R_{\text{electrolyte}} \cdot I$$
- Not always perfectly linear due to interface effects
- **Purely electrical**, not chemical
📌 This is why high electrode impedance + current flow is dangerous for small biosignals.
### <span style="color:rgb(161, 40, 226)">2. Concentration overpotential</span>
- Caused by **changes in ion concentration** near the electrode surface
- When current flows:
    - ions are **consumed or produced**
    - diffusion cannot immediately restore equilibrium
- Leads to:
    - local depletion or accumulation of ions
    - change in electrode potential
- **Not an ohmic effect**, but a **mass-transport limitation**

📌 Strongly affected by:
- sweating
- gel drying
- poor electrolyte contact
### <span style="color:rgb(161, 40, 226)">3. Activation overpotential</span>

- Due to the **kinetics of the redox reaction**
- Current flow makes one reaction direction (oxidation or reduction) dominate
- Requires extra energy to:
    - initiate
    - sustain the reaction
- Depends on:
    - availability of ions
    - electrode material
    - reaction asymmetry
📌 This is why **electrode material matters** (Ag–AgCl behaves much better than polarizable electrodes).

# <span style="color:rgb(223, 109, 109)">Performances</span>
![[Pasted image 20260102091249.png]]

Here the key idea is **spatial filtering**, and it mainly depends on **electrode size and geometry**.

![[Pasted image 20260102095650.png]]

An electrode can be considered an **isopotential surface**: the potential is the same over its whole area. Because of this, any electrical activity reaching the electrode from the body is **summed** before being sent to the amplifier. If several current sources inside the muscle (for example, different muscle fibers or motor units) contribute currents $I_a, I_b, I_c$​, the electrode does not distinguish them individually. What is measured is a single current $I_u$​, which is simply the **sum** of all these contributions.
![[Pasted image 20260102095701.png]]
Now, electrode **size** plays a crucial role. A **large electrode** collects currents from a wider area of tissue, so more sources contribute to the sum. The immediate effect is that the **overall amplitude increases**, because many currents are added together. However, this comes at a cost: **fine details are lost**. Peaks or rapid variations that would be visible if a single source were measured tend to cancel or smooth out when many sources are summed.

A **small electrode**, instead, samples a smaller region of tissue. Fewer current sources contribute, so the signal amplitude is lower, but the electrode preserves **more local information**. In other words, it offers better **spatial selectivity**, making it easier to detect details related to individual fibers or small groups of fibers.

![[Pasted image 20260102095748.png|400]]

This effect can also be understood in terms of **spatial frequency**. High spatial frequencies correspond to rapid variations of electrical activity across space (fine details). Large electrodes act like a **low-pass spatial filter**: they attenuate high spatial frequencies and keep only slow, broad variations. When you look at the spatial power spectrum, the summed signal shows energy concentrated at **low spatial frequencies**, while the higher-frequency components present in the individual currents are strongly reduced or lost.

In summary:

- **Large electrodes** → higher signal amplitude, lower spatial resolution, loss of detail.
- **Small electrodes** → lower amplitude, higher spatial resolution, better detail.
    
This trade-off between amplitude and spatial selectivity is fundamental when choosing electrode size and positioning for EMG and other electrophysiological recordings.


# <span style="color:rgb(223, 109, 109)">Electromyograph</span>

Up to this point, the picture is basically complete on the **signal side**: how the EMG signal is generated inside the muscle, how it propagates through tissues, and how it can be distorted by the skin, the electrolyte, and the electrode–electrolyte interface. We have also seen that the **electrodes themselves are not neutral**, because electrochemical (redox) reactions introduce contact potentials, impedance, noise, and low-frequency artifacts.

![[Pasted image 20250924091206.png]]

## <span style="color:rgb(239, 179, 1)">EMG Acquisition System</span>

![[Pasted image 20250924091216.png]]

The electromyograph starts at the **electrodes**, which are placed on or in the target muscle. 

| Stage                                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| EMG Electrodes<br><br>![[Pasted image 20260102101026.png\|500]]<br>  | Their **position and spacing** determine the working volume: a larger distance or surface electrode collects activity from many fibers (larger amplitude, less selectivity), while closer or depth electrodes collect activity from fewer fibers (smaller amplitude, higher selectivity). This choice directly affects the **signal amplitude and bandwidth**, and therefore drives the design of the EMG system.                                                                                                                                                                                                                                                                             |
| Reference Electrodes<br>![[Pasted image 20260102101200.png\|500]]    | Along with the active electrodes, a **reference electrode** is always required. In monopolar recordings (typically with depth electrodes), the signal is measured with respect to a distant, electrically inactive site to preserve the true shape of the action potential. In bipolar recordings (common in surface EMG), the reference electrode is still necessary to provide a return path for the **input bias currents** of the amplifier. Without this path, the amplifier inputs would float and saturate, making proper measurement impossible.                                                                                                                                      |
| Differential Amplifier (INA)<br>![[Pasted image 20260102101255.png]] | The signals from the electrodes are fed into a **differential amplifier**, usually an **instrumentation amplifier**. This type of amplifier has a very high input impedance, so it does not load the electrodes, and a very high **common-mode rejection ratio (CMRR)**. High CMRR is essential because the useful EMG signal is a small differential voltage, while unwanted signals such as half-cell potentials, motion artifacts, and power-line interference often appear equally on both electrodes as common-mode signals.                                                                                                                                                             |
| BW-Shaping Filters<br>![[Pasted image 20260102101337.png]]           | After amplification, the signal passes through **bandwidth-shaping filters**. Low-frequency components are removed to suppress motion artifacts, electrode drift, and overpotentials, while high-frequency components are removed to limit electronic noise. The chosen bandwidth depends on whether the recording is surface EMG or intramuscular EMG, but in all cases the goal is to maximize the signal-to-noise ratio while preserving physiological information.                                                                                                                                                                                                                        |
| ![[Pasted image 20260102101412.png\|2000]]                           | A critical block of the electromyograph is the **isolation barrier** between the patient-connected circuitry and the part of the system connected to the electrical mains. This isolation is mandatory for patient safety and prevents dangerous currents from reaching the body. Isolation is needed both for the **power supply** and for the **signal path**. Power isolation is commonly achieved using a DC–DC converter with galvanic isolation, typically based on a transformer. Signal isolation can be achieved with transformers or optocouplers; in the latter case, the signal is usually digitized and transmitted as a sequence of bits using light (LED–photodiode coupling). |


![[Pasted image 20260102101516.png|300]]

Once safely isolated, the signal is either converted to digital form (if not already done) using an **analog-to-digital converter**, and then sent to the processing unit. At this stage, additional inputs—such as force sensors, joint angle sensors, or other kinematic measurements—can be synchronized with the EMG signal. Finally, the data are stored, visualized, and processed on a computer for analysis, interpretation, and clinical or biomechanical assessment.

In summary, an electromyograph consists of electrodes with a reference, a high-CMRR differential amplifier, carefully designed filtering, strict electrical isolation for safety, analog-to-digital conversion, and digital processing. Each block exists to preserve a very small biological signal while rejecting noise, interference, and risk to the patient

## <span style="color:rgb(239, 179, 1)">EMG Signal Recap - Key features</span>

![[Pasted image 20250924092552.png|500]]

At a very high level, electromyographs are designed around a few **key performance requirements**, mainly driven by the nature of EMG signals and the way they are generated and recorded.

First is **signal amplitude**. EMG signals can be extremely small, starting close to the noise floor (tens of microvolts), and reaching a few millivolts during normal voluntary contractions. Typical surface EMG amplitudes range from about **100 µV up to 5 mV**. Even higher values, up to **10–15 mV**, can occur during **electrically stimulated muscle activity**, where many fibers fire synchronously. In this case, there is little cancellation between motor unit action potentials, so the amplitudes reinforce each other—similar to what happens in cardiac signals.

Second is **bandwidth**, which depends strongly on the type of electrodes and the application.  
For **neurophysiological EMG** using depth (needle or fine-wire) electrodes, the system must capture very fast action potentials from individual motor units. These signals are short in time and therefore rich in high-frequency content, requiring a bandwidth on the order of **10 Hz up to 10 kHz**.  
For **kinesiological EMG** using surface electrodes, the recorded signal is the interference pattern of many motor units. This signal is slower and smoother, so a much narrower bandwidth is sufficient, typically **10 Hz up to 250–500 Hz**.

A third crucial requirement is **rejection of common-mode noise**. EMG electrodes pick up large unwanted signals that appear equally on both inputs, such as power-line interference, motion-related artifacts, and electrode half-cell potentials. Since the useful EMG is a small differential signal, the front-end amplifier must have a **very high common-mode rejection ratio (CMRR)**, typically in the range of **90 to 120 dB**, to prevent these disturbances from overwhelming the physiological signal.

In short, an EMG device must handle a **wide dynamic range of amplitudes**, provide the **appropriate bandwidth** depending on surface or depth recordings, and offer **excellent common-mode noise rejection** to reliably extract muscle activity from a noisy biological and electrical environment.

## <span style="color:rgb(239, 179, 1)">Electromyograph Characterisation</span>

Another important characteristic of an electromyograph is the **number of channels**. So far, we have reasoned as if we were recording a single EMG signal, but in practice you often want to measure **several muscles at the same time**, or even several locations on the same muscle.

![[Pasted image 20250924093003.png|400]]

In simple clinical or experimental setups, an EMG system may have **1 to 4 channels**, each one connected to a pair of electrodes (plus a reference). In more advanced applications, especially **high-density EMG**, the number of channels can increase dramatically, reaching **64, 128, or even more** electrodes distributed over the muscle surface.

From a system-design point of view, increasing the number of channels does not just mean “adding more electrodes.” Each channel must have its **own complete front-end**. This front-end includes:

- the **input stage**, connected to the differential electrodes and the reference electrode,
- an **amplification and filtering block**, with adjustable gain and bandwidth to match the type of EMG being recorded,
- an **A/D converter**, which digitizes the conditioned signal.

Only after these steps do all channels **merge into a common data-processing block**, where signals are synchronized, stored, analyzed, and possibly combined with other measurements (such as kinematics or force).

In other words, a multichannel EMG system is essentially many single-channel EMG systems running in parallel, sharing the same processing, storage, and user interface. This parallel structure is what allows simultaneous, spatially rich measurements of muscle activity, especially in high-density EMG applications.


## <span style="color:rgb(239, 179, 1)">Monopolar vs Differential EMG Amplifiers (Summary)</span>

**Monopolar configuration**

![[Pasted image 20260102102618.png|300]]

- Used mainly in **neurological EMG** and **depth electrodes**.
- One **active electrode** is placed on the active tissue; the **reference** is placed far away in an electrically inactive area (almost constant potential).
- Measures the signal **with respect to the reference**.
- **Large working volume**: collects signals from a wide tissue region (see the distance between inverting and non inverting input).
- **No common-mode noise rejection** → environmental and physiological noise are amplified together with the EMG signal.

**Differential (bipolar) configuration**

![[Pasted image 20260102102640.png|300]]
- Used mainly in **kinesiological (surface) EMG**.
- Two electrodes are placed on the **active tissue**, plus a distant reference.
- The EMG signal is the **difference between the two electrode potentials (A − B)**.
- **Common-mode noise is rejected** thanks to subtraction (high CMRR).
- **Smaller working volume**, which depends on:
    - electrode **size**
    - **distance** between electrodes
    - tissue attenuation
- **Closer electrodes → smaller working volume → more selective signal**.
    
**Key idea**
- Monopolar: larger volume, more signal but more noise.
- Differential: smaller volume, better spatial selectivity and noise rejection.


## <span style="color:rgb(239, 179, 1)">Why differential amplifiers reduce noise (and why CMRR matters)</span>

In surface EMG, electrodes are usually placed **a few centimeters apart**.
* ***Larger electrodes and larger distance** → larger working volume  
    → higher signal amplitude, but **less detail** in the signal shape.
- **Smaller distance** → smaller working volume  
    → lower amplitude, but **better spatial selectivity**.

To improve signal quality, EMG systems use a **differential amplifier**.
### <span style="color:rgb(161, 40, 226)">Common-mode noise</span>

Common-mode noise is noise that reaches **both electrodes with the same value**.  
Typical sources are:

- power-line interference (50/60 Hz),
- environmental electromagnetic fields,
- motion-related artifacts.
    
For example, imagine:

- both electrodes receive **1 mV of noise** at the same time.

Since this noise is identical on both inputs, it is called **common-mode noise**.

### <span style="color:rgb(161, 40, 226)">Ideal differential amplifier (theoretical case)</span>
![[Pasted image 20260102103829.png]]
Each electrode measures:

- the **local EMG signal**, which is different at each electrode because the action potential propagates along the muscle,
- plus **noise**, which is (ideally) the same at both electrodes.
    
When the differential amplifier subtracts the two inputs:
- the **EMG signals do not cancel**, because they are different in time and amplitude,
- the **noise cancels out**, because it is identical on both electrodes.
![[Pasted image 20260102103917.png]]
In theory, this would completely remove common-mode noise.

### <span style="color:rgb(161, 40, 226)">Real differential amplifier (practical case)</span>

In reality, amplifiers are **not ideal**:

![[Pasted image 20260102103935.png]]

- they amplify the **difference between inputs** (differential gain, **Ad**),
- but they also amplify a **small fraction of the common-mode signal** (common-mode gain, **Ac**).
    
This means:
- common-mode noise is **strongly reduced**, but **not completely eliminated**,
- a small amount of noise always appears at the output.
### <span style="color:rgb(161, 40, 226)">Common-Mode Rejection Ratio (CMRR)</span>

The **CMRR** quantifies how good the amplifier is at rejecting common-mode noise.

It is defined as:
- the ratio between **differential gain (Ad)** and **common-mode gain (Ac)**.
    

Key points:

- **High CMRR → better noise rejection**
- **Low CMRR → more noise at the output**
    

Typical values:

- Standard instrumentation amplifiers: **90–120 dB**
- 120 dB corresponds to rejecting noise by a factor of **about one million**

### <span style="color:rgb(161, 40, 226)">Why high CMRR is essential in EMG</span>

- EMG signals are **very small** (microvolts to millivolts).    
- Common-mode noise can be **much larger** than the EMG signal.
- Without a **very high CMRR**, noise would dominate the measurement.

👉 That is why EMG amplifiers use **instrumentation amplifiers with extremely high CMRR**.

## <span style="color:rgb(239, 179, 1)">Instrumentational Amplifier (INA)</span>

![[Pasted image 20250924094307.png]]

At the core of an instrumentation amplifier there is a **differential amplifier** (the stage with $R_2$, $R_3$​, and the final op-amp).  
![[Pasted image 20260102104639.png]]

This stage subtracts the two input voltages, producing the EMG signal as a difference.

However, **by itself**, this differential amplifier has an important limitation:

- Its **input impedance is relatively low**, mainly determined by the resistor network.
- In EMG, electrode–skin impedance can vary significantly.
- This impedance mismatch **degrades the Common-Mode Rejection Ratio (CMRR)**, making noise rejection worse.
    
This is a serious problem because EMG signals are very small and highly sensitive to noise.

### <span style="color:rgb(161, 40, 226)">Role of the input buffer amplifiers</span>

![[Pasted image 20260102104655.png]]
To solve this, the instrumentation amplifier adds **two input amplifiers (buffers)** before the differential stage.

These input amplifiers:
- Have **extremely high input impedance** (on the order of $10^{12}\ \Omega$),
- Prevent loading of the electrodes,
- Isolate the electrode impedance variations from the differential stage,
- **Greatly improve the overall CMRR** of the system.
    
As a result:
- The EMG signal is preserved,
- Common-mode noise (e.g. power-line interference) is much more effectively rejected.
    
### <span style="color:rgb(161, 40, 226)">Why the reference electrode is necessary</span>

![[Pasted image 20260102104737.png]]
Because the input impedance is so high, the amplifier inputs are **not connected to ground**.

Operational amplifiers require **small bias currents** at their inputs to function correctly.  
Without a return path for these currents:

- the amplifier inputs would float,
- the amplifier could saturate.
    
The **reference electrode** provides this missing path:
- It allows bias currents to flow,
- The current loop is closed through the patient’s body, which has a reasonably low impedance,
- This stabilizes the amplifier operation.

So the reference electrode is **not optional** — it is essential for correct operation.

### <span style="color:rgb(161, 40, 226)">Main advantages of an instrumentation amplifier in EMG</span>

- **Very high input impedance** → minimal signal distortion
- **Much higher CMRR** → strong rejection of common-mode noise
- **Stable operation** thanks to the reference electrode


## <span style="color:rgb(239, 179, 1)">Electrical safety and standardization of EMG devices</span>

![[Pasted image 20260102105301.png]]

Electrical safety is a **critical requirement** for electromyographic devices because they are **powered medical devices** with parts in direct contact with the patient. Protection against **electrical shock** is therefore mandatory and regulated by international standards.

### Standardization bodies

Two main international organizations define safety standards:
- **IEC** (International Electrotechnical Commission)
- **ISO** (International Organization for Standardization)
    
Electrical medical devices are regulated mainly by **IEC 60601-1**, which defines **general safety requirements**. More specific standards exist for particular devices, including electromyography.

## <span style="color:rgb(161, 40, 226)">Electrical shock and its effects on the human body<br></span>
Electrical shock risk is related to the **current flowing through the body**, not voltage. Typical effects are:

- ~1 mA → perception / tingling
- ~15 mA → tetanic muscle contraction (dangerous)
- ~25 mA → respiratory paralysis
- 70–400 mA → ventricular fibrillation (life-threatening)
- > 2–10 A → severe burns
    

==For comparison, household safety switches trip at around **15 mA**, while medical devices must remain **far below perception levels**.==

## <span style="color:rgb(161, 40, 226)">Applied parts and device classification (IEC 60601-1)</span>
![[Pasted image 20260102105613.png]]

An **applied part (AP)** is any part of the device that comes into contact with the patient. Applied parts are classified according to risk:

- **Type B** (least stringent)
    - Non-conductive contact
    - Easily removable (e.g. pulse oximeter)
    - May be grounded
        
- **Type BF** (Body Floating)
    - Conductive contact with the patient
    - Medium/long-term contact
    - **Typical classification for EMG devices**
        
- **Type CF** (Cardiac Floating – most stringent)
    - Direct conductive contact with the heart
        

Type **BF and CF devices must be electrically floating**, meaning **no direct earth/ground connection**, because grounding may increase patient risk.

## <span style="color:rgb(239, 179, 1)">Leakage current and fault conditions</span>

IEC 60601-1 defines strict limits for **leakage currents**, both in:

- **Normal operation**
- **Single-fault condition** (the device must remain safe even if one fault occurs)
    
![[Pasted image 20260102105448.png]]
For **BF devices**, the maximum allowed leakage current to the patient is typically:

- **< 100 µA**, well below perception level

This ensures patient safety even in the presence of one internal failure.

## <span style="color:rgb(239, 179, 1)">How safety is achieved in EMG systems</span>

Patient protection is ensured by:

- **Galvanic isolation** of signal paths (optocouplers or transformers)
- **Isolated power supplies** (DC-DC converters or batteries)
- Avoiding grounding of patient-connected circuits
- Using **floating instrumentation**, which is safer than grounded systems
## <span style="color:rgb(239, 179, 1)">Key takeaways</span>

- EMG devices are **BF-type applied medical devices**
- Electrical safety is regulated by **IEC 60601-1**
- Patient leakage current must be **extremely low (<100 µA)**
- Devices must tolerate **single faults without danger**
- **Floating, isolated designs** are essential for patient safety
    
![[Pasted image 20250924100942.png]]



![[Pasted image 20250924101246.png]]

![[Pasted image 20250924101302.png]]

