
Date: 07/10/2025
***


![[Pasted image 20251002190154.png]]

One of the main goals in electromyographic signal processing is to **detect muscle activation**, also referred to as the **muscle activation pattern**. Muscles are normally activated following well-defined temporal patterns. For example, during walking, muscles activate and deactivate in a precise sequence. In pathological conditions, however, these patterns can be altered.

A typical pathological case is **spasticity**, where **agonist and antagonist muscles contract simultaneously**. Under normal conditions, agonists and antagonists do not contract at the same time, except in special voluntary situations, such as when increasing joint stiffness to prepare for an external impact. In clinical tests, such voluntary co-contractions are not expected. Therefore, if co-contraction between agonists and antagonists is observed during a standard task like walking, it is usually considered pathological.

From a visual point of view, muscle activation seems easy to identify by looking at the EMG signal. However, visual inspection is not sufficient for signal processing, because a data-processing system requires **quantitative and objective measurements**, not qualitative judgments.

In the example shown, several muscles are recorded during a **repetitive movement such as walking**. The sinusoidal-like signal represents the knee displacement over time, starting from a resting position and returning to the same position at the end of the movement cycle. The first group of muscles shown are **knee extensors**, while the following muscles are **knee flexors**. In a healthy subject, these two muscle groups should not be active at the same time. Overlapping activation would indicate an abnormal motor pattern, such as spasticity or impaired neuromuscular coordination following injury.

The red boxes represent the **periods of muscle activation and inactivity** derived from the EMG signals during walking. These activation intervals are often identified by visual inspection, by marking the beginning and the end of each burst. While this approach is intuitive, it introduces **subjectivity**, especially when determining the exact onset and offset of muscle activity.

For this reason, there is a strong need for **automatic activation detection methods**. Such methods allow the onset and termination of muscle activity to be defined in an objective, reproducible, and quantitative way, which is essential for clinical evaluation and comparison across subjects and sessions.

### <span style="color:rgb(161, 40, 226)">Is the muscle ON or OFF? Muscle activation pattern</span>

![[Pasted image 20260102230937.png|400]]
One of the most common applications of electromyography (EMG) is the analysis of the **ON/OFF timing of muscle activation during the gait cycle**. This representation provides a clear overview of the neuromuscular activation pattern during walking and is widely used to compare **normal gait** with **pathological gait**, such as in cases of spasticity.

The gait cycle is conventionally divided into several phases, including **Loading Response (LR)**, **Midstance (MSt)**, **Terminal Stance (TSt)**, **Pre-Swing (PSw)**, **Initial Swing (ISw)**, **Mid-Swing (MSw)**, and **Terminal Swing (TSw)**. For each of these phases, muscles can be classified as either **active (ON)** or **inactive (OFF)**.

By representing muscle activity as a sequence of ON and OFF states across the gait phases, it becomes possible to visually and quantitatively assess whether muscles are activated at the correct times. Abnormal activation patterns, such as prolonged activation or co-contraction between agonist and antagonist muscles, are strong indicators of neuromuscular disorders.

![[Pasted image 20260102230955.png|400]]
To obtain this type of graph, the EMG signal must be **processed to detect the onset and offset of muscle activation**. This typically involves signal preprocessing (filtering and rectification), followed by an automatic detection method that converts the continuous EMG signal into a binary ON/OFF representation. The resulting activation pattern can then be aligned with the gait cycle phases to produce the final timing diagram.

## <span style="color:rgb(239, 179, 1)">EMG processing for muscle activation pattern detection</span>

To obtain numerical information from an EMG signal and extract the muscle activation pattern, a simple and widely used signal-processing chain is applied.
![[Pasted image 20260102231029.png]]

The first step is **band-pass filtering**, typically between **10 and 250 Hz** for surface EMG. This filter isolates the useful EMG frequency band and removes out-of-band noise, such as low-frequency motion artifacts and high-frequency electrical interference.

The second step is **full-wave rectification**. EMG signals are bipolar, meaning they contain both positive and negative values. Rectification consists of taking the absolute value of the signal, so that all negative peaks are mirrored into the positive side. After this step, the signal represents the overall amplitude of muscle activity more clearly.

Once the signal is rectified, it is still highly variable and difficult to analyze directly. Therefore, a **low-pass filtering** step is applied, typically with a cutoff frequency between **5 and 10 Hz**. This operation extracts the signal envelope, producing a smooth, low-frequency waveform that represents the muscle activation level over time. This envelope makes it easy to define thresholds to detect when muscle activity starts (onset) and ends (offset).

Instead of a simple low-pass filter, the smoothing step can also be performed using a **moving average (MA)** or a **root mean square (RMS)** computation over a time window, usually between **50 and 100 ms**. Both approaches produce a similar envelope. When RMS is used, rectification is not required, because squaring the signal inherently removes negative values.

After these processing steps, the resulting signal is smooth and strictly positive, allowing reliable threshold-based detection of muscle activation and deactivation.

### <span style="color:rgb(161, 40, 226)">Half-wave and full-wave rectification<br></span>
![[Pasted image 20251007131642.png|500]]

Rectification can be implemented either digitally or using analog components, and the principle is slightly different in the two cases.

When rectification is performed **digitally**, directly on sampled data, the operation is very simple and can be described mathematically.

For **half-wave rectification**, only the positive samples of the signal are kept:

- if the sample value $x(i)>0$, then $y(i)=x(i)$
- if $x(i) \le 0$, then $y(i)=0$
    
For **full-wave rectification**, both positive and negative samples are mapped to positive values:

- if $x(i)>0$, then $y(i)=x(i)$
- if $x(i) \le 0$, then $y(i)=−x(i)$
    
In other words, full-wave rectification is equivalent to taking the absolute value of the signal.

When rectification is implemented **in the analog domain**, using components such as diodes and operational amplifiers, the result depends on the circuit configuration. Different diode arrangements allow either half-wave or full-wave rectification, but the underlying goal remains the same: converting a bipolar signal into a unipolar one.

The expressions above describe the **digital implementation**, applied after the signal has been sampled.

### <span style="color:rgb(161, 40, 226)">Spectral Paradox</span>

![[Pasted image 20251007131830.png]]
Consider the following situation:  

you first filter an EMG signal using a **high-pass filter at 10 Hz** (for example, a band-pass filter from 10 to 250 Hz), and then you apply a **high-order low-pass filter at 5 Hz**.

A naïve expectation would be that the output is almost zero, because the signal components below 10 Hz have already been removed, and the low-pass filter at 5 Hz should not pass anything.

![[Pasted image 20251007132231.png|400]]
However, this is **not** what actually happens. Instead, we observe a non-zero output signal (as shown by the black trace in the figure).

This apparent contradiction is known as the **spectral paradox**.
![[Pasted image 20260102231932.png|300]]
The reason lies in the **rectification process**.  Full-wave rectification is a **non-linear operation**. Before rectification, the EMG signal can be represented as a sum of sinusoids at different frequencies. When each sinusoidal component passes through the full-wave rectifier, the output is no longer a single sinusoid at the original frequency.

As a consequence:

- New frequency components are generated, starting from the **second harmonic**
- A **DC component** appears in the spectrum, even though it had been previously removed by the high-pass filter

Because of this spectral transformation introduced by rectification, low-frequency components reappear in the signal. These components can then pass through the low-pass filter at 5 Hz, producing a non-zero output.

This explains why the final signal is not null, despite the apparent incompatibility between the filter cut-off frequencies.

### <span style="color:rgb(161, 40, 226)">Signal Processing</span>

![[Pasted image 20251007132604.png]]

These are examples used to evaluate the **reliability of EMG signal processing**, starting from the **rectified signal** and applying **low-pass filtering** in different ways.

Different filtering methods are compared:

- Moving Average (MA)
- Root Mean Square (RMS)
- Low-pass Butterworth filter
    
For each method, some parameters are computed and compared to check how **consistent** they are across methods and with respect to the original signal. The main parameters considered are:

- **Area**
- **Mean value**
- **Peak (maximum value)**
    
From the results, we observe the following:

- The **area** of the signal is very similar when using the Moving Average and the Butterworth filter. The RMS gives a value that is close, but not identical.
- The **mean value** is almost the same for all methods, with only small differences, especially when using RMS.
- The **peak value**, instead, changes significantly from one method to another and appears almost random.
    
This happens because the EMG signal is **stochastic**. The peak value is strongly affected by factors such as:

- Cancellation between positive and negative contributions
- Changes in electrode position relative to the muscle during movement
    
For this reason, the **peak should not be used** as a reliable indicator to extract information from the EMG signal.

In contrast, parameters such as **area** and **mean** are much more consistent across different filtering methods and are therefore **reliable descriptors** of the EMG signal.

In summary:
- **Area and mean** are reliable and consistent parameters
- **Peak value is unreliable** and should be avoided
- RMS can be used, but it introduces a scaling effect compared to linear filters, which must be taken into account

![[Pasted image 20251007133141.png|600]]

The **moving average** is a very simple operation. You take **m samples**, average them, and use that value to produce **one output point**.

This means that **each output sample depends on m input samples**. To compute one output value, the filter needs the **current sample plus the previous m − 1 samples**, because the summation includes samples taken at earlier time instants.

In other words, the filter must first collect **m samples** before it can produce a valid output. The factor **1/m** simply represents the averaging operation.

![[Pasted image 20251007133810.png]]

If you use this formula, you need **past samples** to compute the current output $y_i$​. The output is placed at the **end of the window**, so the computation introduces a **phase lag**. In practice, the result is delayed by about **$M/2$** samples.

If instead you place the output **at the center of the window**, the reconstructed point depends on **both past and future samples**. In this case, the summation is **symmetric**, and the filter is **zero-phase** (no phase shift).

This is possible only when the **future samples are available**, which is not feasible in real-time processing. However, when working with **recorded (offline) signals**, future samples are known, so this approach is perfectly acceptable. As before, a few samples at the beginning and end of the signal are lost because the window must be fully filled.

So:

- **End-aligned window → phase lag**
- **Centered window → in-phase (zero phase)**


![[Pasted image 20251007134221.png]]

The original signal already contains noise.  When using a moving average (MA) filter, the **number of points in the window matters**. For example, with an **11-point window** or a **51-point window**, some **data loss** occurs at the beginning and the end of the signal. The **larger the window**, the **greater the data loss**.

In general:
- **More points → more smoothing**
- **More points → less detail preserved**
    
Now, looking at the **frequency behavior of the moving average filter**:

In the example, the original signal (top left) is a **square wave with strong noise**.

- With an **11-point moving average**, the output still looks similar to the input signal, but the **noise is only partially reduced**.
- With a **51-point moving average**, the noise is **strongly reduced**, but the signal becomes **over-smoothed**.
    
So, increasing the window size improves noise reduction, but at the cost of **losing signal details**. The result is a **cleaner but less accurate representation** of the original signal due to the stronger low-pass filtering effect.

#### <span style="color:rgb(2, 141, 192)">How to compute the cutoff frequency of the MA filter?</span>
![[Pasted image 20260103102038.png]]

The moving average filter has a well-defined transfer function $H(f)$, and its behavior strongly depends on the **number of points M** in the averaging window. In particular, the value of $M$ determines the **cutoff frequency** of the filter.
![[Pasted image 20260103102444.png|200]]
When the number of points is small, for example **3 points**, the cutoff frequency is relatively high. This means that the filter removes only very high-frequency components and leaves much of the signal unchanged. As M increases, the cutoff frequency moves toward lower frequencies, so the filter becomes more selective and behaves as a stronger low-pass filter.

![[Pasted image 20260103102530.png|400]]
An important characteristic of the moving average filter is that, after the magnitude response reaches zero, it **oscillates (bounces)**. These oscillations correspond to sidelobes in the frequency response. As the number of points increases, two things happen:  the sidelobes become **smaller**, and the decay of $H(f)$ becomes **faster**, meaning that the response crosses the $-3\,\text{dB}$ line more sharply.

The cutoff frequency can be estimated using an **approximate formula**, which expresses the cutoff as a **fraction of the sampling frequency**, not as an absolute frequency. This approximation becomes quite accurate when $M \ge 3$, and improves further as $M$ increases. Using this formula, you can correctly predict how the cutoff frequency shifts when you change the window length.

![[Pasted image 20260103102530.png|400]]
Regarding the sidelobes, their number is related to the window length: approximately **M−2** sidelobes appear in the frequency response. For example, with a 3-point moving average, only one sidelobe is visible, while for an 11-point filter many more sidelobes are theoretically present, even if not all are clearly visible in practice.

Looking at specific examples helps clarify this behavior. With a **3-point moving average**, the $-3\,\text{dB}$ cutoff occurs at a high normalized frequency, the transition band is very wide, and attenuation in the stopband is poor. Increasing the window to **11 points** lowers the cutoff frequency and reduces the ripple in the stopband. With **31 points**, the cutoff frequency is even lower, and the ripple in the stopband becomes very small. Since the frequency axis is normalized up to **0.5** (half the sampling frequency, i.e. the Nyquist frequency), the frequency response is symmetric around this point.

In summary, increasing the number of points in a moving average filter lowers the cutoff frequency, sharpens the transition band, and reduces sidelobes, but at the cost of stronger smoothing and loss of temporal detail.

![[Pasted image 20260103104740.png]]

Another way to filter and smooth the EMG signal is to use the **RMS (Root Mean Square)** value. The RMS is defined as the square root of the mean of the squared signal values over a given window. In practice, you take a set of (n) samples, square each sample, compute their average, and then take the square root of that average.

To understand what this means, consider a simple sinusoidal signal. When you square a sinusoid, its frequency is effectively doubled and the signal becomes entirely positive. If you then compute the mean of this squared signal, you obtain a value equal to one half of the squared amplitude. Taking the square root of this result brings you to approximately 0.7 times the original amplitude. This is the well-known RMS value of a sinusoid.

For signals other than pure sinusoids, such as EMG signals, the RMS must be computed numerically using the sampled data within the selected time window. The same formula applies: square the samples, average them, and take the square root.

An important advantage of the RMS approach is that it can be applied **directly to the raw signal**. Since the signal is squared as part of the computation, all values automatically become positive. This means that **explicit rectification is not required**, unlike in the moving average approach. The RMS operation itself inherently performs the rectification and smoothing in a single step.

### <span style="color:rgb(161, 40, 226)">Data Normalisation</span>

After pre-processing the EMG signal with smoothing techniques such as a low-pass filter, moving average, RMS, or a Butterworth filter, the next essential step is **normalization**. Normalization is required to make EMG data comparable, either across repeated trials of the same subject or between different subjects.

![[Pasted image 20251007135237.png]]


Raw EMG amplitudes cannot be directly compared because they depend on many factors that are not physiological, such as electrode placement, skin impedance, subcutaneous fat, and amplifier settings. For this reason, without normalization, reproducibility is poor.

The most widely used and reliable normalization method is based on the **Maximum Voluntary Contraction (MVC)**. MVC is a reference value obtained during a calibration phase in which the subject is asked to perform a **maximal isometric contraction** of the muscle under investigation. In theory, this contraction represents 100% of the subject’s voluntary muscle activation capacity.

![[Pasted image 20251007135554.png]]

It is important to clarify that, although we call it MVC, what we actually measure is the **electrical activity associated with the MVC**, not the mechanical force itself. The EMG signal reflects neural activation and muscle fiber recruitment, not force directly, so normalization is performed on the electrical signal.

Once the MVC has been recorded, all subsequent EMG measurements are expressed as a percentage of this reference value. In practice, the processed EMG amplitude is divided by the MVC value and multiplied by 100. This allows different contractions to be interpreted as a percentage of maximal activation.

$$x(t)=\frac{V_{EMG}}{MVC} \cdot100$$

By normalizing EMG data to MVC, it becomes possible to:

- Compare repeated measurements from the same subject across time or sessions
- Compare muscle activation levels between different subjects
- Reduce variability due to electrode placement and individual anatomical differences
    
In this sense, MVC normalization acts as a **calibration step**, rescaling the electrical activity of the muscle into a meaningful and reproducible reference framework.

![[Pasted image 20251007135712.png]]

#### <span style="color:rgb(2, 141, 192)">Maximum Voluntary Contraction (MVC) normalization</span>

**Pros**
- Provides an **estimate of neuromuscular effort**, expressed as a percentage of maximum muscle activation
- Helps understand **at what capacity level** a muscle is working during a task
- Allows **comparison of EMG signals**:
    - within the same subject (repetitions, different days)
    - between different subjects
    - across different operators, if a standardized protocol is used
        
- Reduces variability due to:
    - electrode placement
    - individual anatomy
    - overall signal amplitude differences

**Cons**

- Applicable only to **healthy, cooperative, and trained subjects**
    - Not suitable for newborns or patients with severe neurological impairments
        
- True MVC is **difficult to obtain**:
    - requires strong motivation and correct execution
    - depends on the operator’s ability to guide and position the subject properly
        
- Possible observation of **supramaximal EMG during submaximal tasks**, due to:
    - muscular synergies
    - activation of neighboring muscles
    - incorrect or underestimated MVC
        
- MVC reflects **electrical activity**, not mechanical force, and remains an **estimate**, affected by:
    - signal stochasticity
    - muscle deformation
    - electrode displacement
    - cancellation effects

# <span style="color:rgb(223, 109, 109)">Parameters Estimate</span>


![[Pasted image 20251007140129.png]]
After pre-processing, we can now focus on the **estimation of diagnostic parameters** from the EMG signal. This represents the final step of the path we started earlier: from signal generation, to acquisition, to pre-processing, and now to parameter extraction. We will first consider **time-domain parameters**, and later move to **frequency-domain parameters**.

![[Pasted image 20251007142336.png]]

When estimating diagnostic parameters in the **time domain**, several important issues must be considered.

* First, EMG provides a **local measurement**, not a global one. The electrodes capture the activity of only a limited portion of the muscle. If a pathology affects only part of a muscle, the electrode may be placed either on the pathological area or on a healthy region, leading to very different measurements. This limitation is not always negative: in **neurological EMG**, for example, the goal is precisely to study the activity of a single fiber, a motor unit, or a small group of motor units. However, when the interest is the **overall muscle activity**, it is important to remember that the electrode’s working volume represents only a subset of the muscle.

* A second issue is that **motor unit activity depends strongly on electrode placement**. Changes in muscle shape during contraction modify the relative position between the muscle fibers and the electrodes. As a consequence, even if the physiological activity remains the same, the recorded EMG signal may change simply because the geometry has changed.

Another relevant problem is **crosstalk and limited isolation**. The EMG signal may include contributions from muscles that are not the primary target, especially when nearby muscles are close to the electrodes. This effect is particularly significant for **small muscles**, such as those in the neck, where it is difficult to isolate a single muscle. In contrast, for **large muscles**, such as knee extensors, crosstalk is usually less critical because the detection volume is more likely to remain within the target muscle.
## <span style="color:rgb(239, 179, 1)">Time Domain Parameters</span>

In the time domain, two commonly used parameters to estimate **muscular electrical activity** are the **mean value** and the **root mean square (RMS)** of the rectified EMG signal.

![[Pasted image 20260103130057.png]]

- The **mean value of the absolute signal** ($e_m$​) represents the average amplitude of the EMG over a time interval $T$. It is computed as the mean of the rectified signal.
- The **RMS value** ($e_{rms}$​) represents the square root of the mean of the squared signal over the same interval $T$. This parameter gives more weight to higher amplitudes.
    
Both parameters provide a **rough estimate of muscle activation** and are often used as indirect indicators of muscle force. However, this relationship is not exact.

There are important limitations to keep in mind:

- **Cancellation effects** can reduce the measured amplitude due to overlapping positive and negative motor unit action potentials.
- **Muscle shape variations** during contraction change the relative position of fibers and electrodes, affecting the measured signal.
    

For these reasons, mean and RMS values should be interpreted as **approximations of muscular effort**, not as precise measurements of force.
### <span style="color:rgb(161, 40, 226)">Zero-Crossing Point</span>

![[Pasted image 20260103130212.png|400]]
When using **depth electrodes** to detect **motor unit action potentials (MUAPs)**, time-domain parameters related to signal frequency become particularly useful.

One widely used parameter is the **zero crossing count**.

Zero crossings represent the number of times the EMG signal changes sign (from positive to negative or vice versa). To avoid counting noise, a zero crossing is typically counted **only if the signal (or its derivative) exceeds a predefined threshold**, usually in the range of **10–100 µV**.

This parameter provides a **simple and effective approximation of the signal’s frequency content**:

- A **higher number of zero crossings** indicates higher frequency components.
- A **lower number of zero crossings** indicates lower frequency components.
    

Zero crossing analysis is especially useful in pathological conditions where the **frequency content of MUAPs is altered**, such as:

- **Muscular dystrophy**, where MUAPs often show higher frequency content
- **Acute neurogenic diseases**, where frequency characteristics may differ significantly from normal patterns
    
Overall, zero crossing count is a **computationally efficient feature** that helps characterize neuromuscular alterations in neurological EMG recordings.


### <span style="color:rgb(161, 40, 226)">Motor Unit Action Potential (MUAP) variation as a diagnostic method</span>
![[Pasted image 20260103130353.png]]
Variations in **motor unit action potentials (MUAPs)** provide important diagnostic information because they reflect changes in the **number and organization of muscle fibers within a motor unit**. These changes are typically caused by pathological processes affecting either the muscle fibers or the motor neurons.

Key pathological conditions include:

- **Degeneration of muscle fibers**  
    In myopathies such as **muscular dystrophy**, the number of fibers belonging to a motor unit is reduced. This typically results in **short-duration, low-amplitude MUAPs** and a **high count of motor unit activations**.
    
- **Initial degeneration of alpha motor neuron connections**  
    In **acute neuropathies** and diseases such as **amyotrophic lateral sclerosis (ALS)**, the loss of connections between alpha motor neurons and muscle fibers leads to altered MUAP morphology and firing behavior.
    
- **Reinnervation in chronic neuropathies**  
    In the chronic phase of neuropathies (e.g. **Guillain-Barré syndrome**, **alcoholic neuropathy**), surviving alpha motor neurons may reinnervate denervated fibers. This increases the **innervation ratio**, producing **larger and longer-duration MUAPs**.
    

Overall, analyzing MUAP variations allows clinicians to **differentiate between myopathic and neurogenic conditions** and to assess whether a neuropathy is in an acute or chronic stage.

## <span style="color:rgb(239, 179, 1)">Frequency Domain Parameters</span>
![[Pasted image 20251007143526.png]]

What you see on the plot is the **power spectral density (PSD)** of EMG:

- **x-axis:** frequency (Hz)
- **y-axis:** power (V²/Hz)
    

Because the EMG spectrum is **asymmetric and non-Gaussian**, we do **not** describe it with parametric models. Instead, we extract meaningful descriptors directly from the spectrum.

Here is what each labeled parameter means:

### <span style="color:rgb(161, 40, 226)">Peak power (or peak frequency)</span>  
This is the frequency at which the spectrum reaches its **maximum power**.  
It indicates where most of the EMG energy is concentrated, but it is **not very robust**, because it can be sensitive to noise and small variations.

### <span style="color:rgb(161, 40, 226)">Mean frequency</span>  
This is the **power-weighted average frequency** of the spectrum.  
It represents the “center of mass” of the spectral power distribution.  
Mean frequency is often used to study **muscle fatigue**, since it typically **shifts toward lower frequencies** as fatigue increases.

### <span style="color:rgb(161, 40, 226)">Median frequency</span>  
This is the frequency that **divides the total power into two equal halves**:

- 50% of the power is below it
- 50% is above it
    
Median frequency is **more robust than peak frequency** and is widely used in clinical and biomechanical EMG analysis, especially for fatigue assessment.

### <span style="color:rgb(161, 40, 226)">Total power</span>  
This corresponds to the **area under the power spectrum curve**.  
It reflects the overall electrical activity of the muscle and is related to signal amplitude, although it is still affected by cancellation and electrode placement.

**Why non-parametric parameters are used**

- The EMG spectrum is **not Gaussian**
- Mean, median, and total power do **not assume any model**
- They are more **stable and reproducible** than time-domain peak measures
    

In practice:

- **Mean and median frequency** → fatigue and neuromuscular changes
- **Total power** → overall muscle activation
- **Peak frequency** → descriptive, but less reliable diagnostically

![[Pasted image 20251007144831.png]]
![[Pasted image 20251007145314.png]]
### <span style="color:rgb(161, 40, 226)">Fiber recruitment and its effect on the estimation of conduction velocity (cv)</span>

Muscle force is modulated not only by firing rate, but also by **fiber recruitment**, that is, by activating different types of muscle fibers. Skeletal muscle is composed of a **mixture of fiber types**, each with distinct electrical and mechanical properties, and this directly affects EMG measurements, including the estimation of **muscle fiber conduction velocity (cv)**.

Muscles contain **fast and slow fibers**, which differ in size, metabolism, fatigue resistance, and spectral content of the EMG signal.  
Fast fibers (Type IIX) are large, pale or white in appearance, and capable of generating high force and rapid contractions. However, they fatigue quickly. When these fibers are recruited, their action potentials propagate faster along the membrane, producing **higher conduction velocities** and contributing **higher-frequency components** to the EMG spectrum.

Slow fibers (Type I) are smaller, red in color due to high myoglobin content, and are specialized for endurance and postural control. Their action potentials propagate more slowly, so they are associated with **lower conduction velocities** and **lower-frequency spectral components** in the EMG. These fibers are typically recruited first during low-force or sustained contractions.

Between these two extremes, there is a third group: **Type IIA fibers** (fast oxidative–glycolytic). These fibers have intermediate properties: they are faster and stronger than Type I fibers, more fatigue-resistant than Type IIX fibers, and contribute intermediate frequencies to the EMG spectrum.

As force increases, the nervous system progressively recruits fibers from **slow to fast** (Henneman’s size principle). As a consequence:

- The **average conduction velocity increases**
- The EMG spectrum shifts toward **higher frequencies**
    

Therefore, changes in estimated conduction velocity do not depend only on membrane properties or fatigue, but also on **which fiber populations are being recruited** at a given contraction level. This is a key point when interpreting cv measurements in both physiological and pathological conditions.

![[Pasted image 20251007144434.png]]
Here is the **same explanation in English**, summarized with bullet points and keeping the key context:

- The figure compares the **characteristics of muscle fiber types I, IIa, and IIx**.
    
- **Fatigue resistance**:
    - **Type I**: very high resistance to fatigue.
    - **Type IIa**: intermediate resistance.
    - **Type IIx**: very low resistance to fatigue.
        
- **Force production**:
    - **Type I**: low force.
    - **Type IIa**: intermediate force.
    - **Type IIx**: very high force.
        
- **Functional examples**:
    - **Type I**: long-duration, low-intensity activities (e.g., running 5–10 km, postural tasks).
    - **Type IIx**: short, near-maximal efforts (e.g., 100 m sprints, heavy lifting).
        
- **Energy source (fuel)**:
    - **Type I**: oxidative metabolism → mainly uses **fat**, requires oxygen.
    - **Type IIx**: glycolytic metabolism → mainly uses **glycogen**, with limited oxygen involvement.
        
- **Recovery characteristics**:
    - **Type I fibers** can sustain prolonged activity due to efficient metabolic cycles.
    - **Type IIx fibers** accumulate metabolites and require **1–2 days** to fully recover after intense exercise.
        
- This explains why excessive or very intense exercise leads to **delayed muscle recovery**.


![[Pasted image 20251007145632.png]]

- A spectrum with **positive skewness** shows a longer tail toward **higher frequencies**.
- **Kurtosis** describes how **narrow or wide the peak region** of the spectrum is:
    - Narrow, sharp peak → **high kurtosis**
    - Wide, flat peak → **low kurtosis**
- **Spectral median frequency** is used to estimate:
    - **Motor unit recruitment**
    - **Muscle fatigue**
    - **Possible pathological conditions**
- **Skewness and kurtosis** provide additional information by indicating whether the spectrum is:
    - More sensitive to **fatigue-related changes**
    - More affected by **pathological alterations**
- Together, these spectral parameters help characterize changes in muscle behavior beyond simple power or frequency measures.

==The more it is going to the left, the more is the muscle suffering because the lower the speed of conduction of the action potentials==
![[Pasted image 20251007145720.png]]

Median and median frequencies signal decrease during a task that induces fatigue

![[Pasted image 20251007145832.png]]



