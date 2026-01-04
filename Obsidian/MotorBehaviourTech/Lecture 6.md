
Date: 03/10/2025
***

#### <span style="color:rgb(2, 141, 192)">Floating vs grounded in critical situations</span>
**In critical (medical) situations, we prefer a _floating system_**, not directly grounded at the patient side.
- The **patient side is floating** → minimizes leakage currents through the body
- The **device side can be grounded** → for safety and EMC compliance
- Isolation ensures that **any leakage current is independent** of other grounds
    
The key rule is:  
⚠️ **Avoid strong interdependencies between different grounds**, because voltage differences between grounds can drive unwanted currents.
#### <span style="color:rgb(2, 141, 192)">Why grounding / earthing? (same thing)</span>

Yes — **grounding (US)** = **earthing (UK)**

Purpose:
- Provide a **reference potential**
- Safely **drain fault and leakage currents**
- Reduce EMI and stabilize measurements
    
But in medical systems:
- Ground ≠ patient reference
- Patient must be **isolated from earth**
##### <span style="color:rgb(2, 141, 192)">Environmental model and current loops</span>
![[Pasted image 20260102143854.png|450]]

In the environmental model:
- The body is assumed **isopotential**
- There are **stray capacitances** between:
    - body ↔ mains
    - cables ↔ mains
    - device ↔ ground
        
Because of these:
- **Common-mode currents** (your yellow/green path) can flow
- If **different grounds have different potentials**, a **current loop** forms
- This loop:
    - injects noise
    - can create safety risks
    - must be safely discharged through controlled paths

### <span style="color:rgb(161, 40, 226)">Noise reduction III - Linear filtering</span>

![[Pasted image 20251002162844.png]]

**Purpose of linear filtering**

1. **Increase SNR** by removing noise outside the signal band
2. **Anti-aliasing**: remove high-frequency noise _before sampling_ to satisfy the **Shannon–Nyquist theorem**
    
Key idea:  
==The sampling frequency must be **> 2 × (maximum frequency of signal + noise)**, not just the signal.  Otherwise, **wideband noise folds into the signal band** (aliasing) and **cannot be removed after sampling**.==

#### <span style="color:rgb(2, 141, 192)">Basic requirements for linear filtering</span>

**Frequency content of both signal and noise must be known**  
**Signal and noise spectra should be weakly overlapped (ideally separated)**

If signal and noise overlap strongly:
- Filtering will remove **noise AND part of the signal**
- SNR improvement becomes limited or impossible
    
#### <span style="color:rgb(2, 141, 192)">Example: Surface EMG</span>

- Useful EMG bandwidth: **~10–15 Hz up to 250–500 Hz**
    
- Typical filtering:
    - **High-pass filter** → removes motion artifacts & baseline drift (<10 Hz)
    - **Low-pass filter** → removes high-frequency noise
    - **Notch filter (50/60 Hz)** → removes power-line interference
    - **Anti-aliasing low-pass filter** → before ADC
    

![[Pasted image 20251002165018.png]]

To give an intuitive example, suppose we have a **10 Hz sinusoidal signal** and a **50 Hz sinusoidal noise**. The measured signal is simply the **sum of the two**.  
If we look at its **frequency spectrum**, we clearly see:

- a peak at **10 Hz** (the signal),
- a smaller peak at **50 Hz** (the noise).
    
Since these two components are **well separated in frequency**, it is easy to design a filter that removes the 50 Hz noise while preserving the 10 Hz signal.

However, this is a **very ideal and rare case**. In real situations, the spectra of signal and noise **partially overlap**. When this happens, filtering becomes a trade-off:  
you must choose a cutoff frequency that **reduces noise** without **removing too much useful signal**.

#### <span style="color:rgb(2, 141, 192)">Why filtering should be applied as early as possible in the signal chain</span>

![[Pasted image 20251002165604.png|400]]
All the signal-processing concepts discussed so far assume that **both the signal and the processing blocks are linear**. Under this hypothesis, the order of blocks (amplification, filtering, processing) does not matter: exchanging blocks leads to the same result.

However, **real systems are not perfectly linear**. In particular, **amplifiers exhibit nonlinearities**, the most important one being **saturation**. Even though negative feedback reduces nonlinear effects by forcing the amplifier to operate in a limited gain range, some nonlinearity always remains.

Because of this, **the order of the processing blocks matters**.

![[Pasted image 20251002165943.png|500]]

Consider:

- A useful signal with an amplitude of **10 mV** and frequency around **10 Hz**
- A noise component that is a **DC offset of 100 mV (0 Hz)**
    
Since signal and noise are well separated in frequency, a **high-pass filter** can easily remove the DC noise.

Now compare two possible processing chains:

##### <span style="color:rgb(71, 215, 140)">Case 1 – <b>Filter first, then amplify (GOOD choice)</b></span>

1. The signal + noise amplitude is within **±110 mV**
2. The high-pass filter removes the DC noise
3. The remaining signal (±10 mV) is then amplified (e.g. ×10)
4. Output: **clean signal**, no distortion
    
The amplifier always works in its **linear region**, so the signal is preserved.

##### <span style="color:rgb(71, 215, 140)">Case 2 – <b>Amplify first, then filter (BAD choice)</b></span>

1. The signal + noise is amplified first
2. The large DC component pushes the amplifier into **saturation** (e.g. ±10 V supply limits)
3. The output becomes **clipped**
4. Filtering afterward cannot recover the original signal

Once saturation occurs, **information is permanently lost**. No filter can reconstruct the signal from a clipped waveform.

##### <span style="color:rgb(71, 215, 140)">Key takeaway</span>

- **Linear systems** → blocks can be exchanged freely
- **Nonlinear systems** → block order matters
    
Because amplifiers are nonlinear, **noise must be removed as early as possible**, ideally **before high gain is applied**.

> **Apply filtering as close as possible to the input of the measurement chain.**

This:
- Prevents amplifier saturation
- Limits nonlinear distortion
- Avoids generation of harmonics
- Preserves signal integrity
- Improves overall SNR
#### <span style="color:rgb(2, 141, 192)">EMG signal spectrum and mains interference</span>

![[Pasted image 20251002170256.png|600]]
A **surface EMG signal** has a **wide frequency spectrum**, typically ranging from **a few hertz up to 300–400 Hz**, depending on:

- the muscle,
- electrode placement,
- and the experimental setup.
    
This frequency band represents the **useful physiological information** we want to measure. 

In a real acquisition, the EMG spectrum is **not clean**. Superimposed on the signal, we observe **narrow spectral peaks** at: **50 Hz** (mains frequency in Europe), **150 Hz**, **250 Hz**, **350 Hz**, **450 Hz**, etc. These peaks are caused by **power-line interference**.

The presence of **multiple peaks at integer multiples of 50 Hz** is a clear indication of **nonlinearities** in the system.

- A **purely linear system** would only show a peak at **50 Hz**    
- **Nonlinear components** (e.g., amplifiers, electrode interfaces) generate **harmonics**
- In this case, only **odd harmonics** appear (50, 150, 250, …), which indicates an **odd nonlinearity**
    
This happens because nonlinear systems effectively **multiply signals**, creating new frequency components.

##### <span style="color:rgb(71, 215, 140)">Two filtering situations</span>

1. **Frequencies outside the EMG band (easy case)**

If the useful EMG content ends at, say, **350 Hz**, then:

- Everything above that frequency is mostly **noise**    
- A **low-pass filter** placed at the upper limit can remove a large amount of noise without affecting the signal
    
This is the **ideal filtering scenario**.

2. **Overlap between signal and noise (hard case)**

The mains harmonics (50 Hz, 150 Hz, etc.) lie **inside the EMG frequency band**.
This creates a **spectral overlap**:
- We cannot remove these frequencies with a standard band-pass filter
- Removing them entirely would also remove part of the EMG signal

 **Solution: Notch filters**
![[Pasted image 20251002170933.png|600]]
To remove these specific disturbances, we use **notch filters**.
A **notch filter**:
- Passes almost all frequencies unchanged
- Strongly attenuates **only one narrow frequency band**

Example:
- Gain ≈ 1 up to **49 Hz**
- Gain ≈ 0 at **50 Hz**
- Gain ≈ 1 again at **51 Hz**
    
These filters can be designed to be **very narrow**, so they:
- Remove mains interference
- Minimize distortion of the EMG signal
    
In practice, multiple notch filters may be used:

- One at **50 Hz**
- Others at **150 Hz, 250 Hz**, etc., if needed
    
We reduce the thickness of the Notch by means of the Q parameter.

#### <span style="color:rgb(2, 141, 192)">Typical frequency ranges in EMG and required filtering</span>

To understand **which frequencies must be filtered out** and **which must be preserved** in electromyography, we usually refer to standard bandwidth recommendations. These depend on **electrode type** and **application**.

![[Pasted image 20251002171308.png|700]]

**Low-frequency filtering (high-pass filter)**

In almost all EMG systems, a **high-pass filter between 10 and 20 Hz** is required.
Its purpose is to remove **low-frequency artifacts**, mainly caused by:

- electrode–skin interface variations,
- electrolyte displacement,    
- motion of the electrodes relative to the skin,
- baseline drift.
    
These disturbances typically occur **below 10 Hz**, so a high-pass filter in this range effectively cleans the signal without affecting the physiological EMG content.

**High-frequency content and low-pass filtering**

**Surface EMG (sEMG)**. For **surface electrodes**, the useful EMG frequency content usually extends up to:

- **400–500 Hz** for standard applications,
- up to **~1000 Hz** for specific analyses (e.g. signal decomposition).
    
Surface EMG naturally has a **limited bandwidth** because the biological tissues between the muscle fibers and the electrodes act as a **spatial low-pass filter**, attenuating high-frequency components.

As a result, the required low-pass cutoff is **relatively low**.

***
Intramuscular / wire / needle electrodes. For **wire or needle electrodes**, the situation is different:

- The electrodes are placed **very close to individual muscle fibers**
- The detected signals originate from **single fibers or small groups of fibers**
    

Because of this:

- There is **much less spatial filtering**
- The EMG signal contains **significant high-frequency components**
- The bandwidth often extends well beyond **1 kHz**
    
Therefore, **higher low-pass cutoff frequencies** are required compared to surface EMG.

 **Summary**
- **High-pass filter (10–20 Hz)**  
    → Removes motion artifacts and baseline drift
- **Low-pass filter (depends on electrode type)**
    - Surface EMG: typically **400–500 Hz**, up to **1000 Hz** in special cases
    - Wire/needle EMG: **much higher bandwidth** required    
- Surface EMG has lower high-frequency content due to **tissue-induced spatial low-pass filtering**
- Intramuscular EMG preserves higher frequencies because electrodes are **close to the signal source**
### Key takeaway

> **Filtering choices in EMG are dictated by physiology, electrode type, and application—not by electronics alone.**


## <span style="color:rgb(239, 179, 1)">Analog Filters</span>

To satisfy the **Shannon–Nyquist theorem**, signals **must be band-limited before sampling**.  
Since sampling happens after the analog front-end, this limitation **must be done with analog filters**, not digital ones.

In EMG systems, the **most critical filter is usually the low-pass filter**, because:

- the **high-pass filter** (to remove motion artifacts and DC drift) is relatively easy to design,    
- the **low-pass filter** must strongly attenuate high-frequency noise **without distorting the signal**.

### <span style="color:rgb(161, 40, 226)">Key filter design requirements</span>

When designing or choosing a filter, several competing requirements must be balanced:
#### <span style="color:rgb(2, 141, 192)">1. Transition band</span>

![[Pasted image 20260102211106.png]]
The **transition band** is the frequency region between:
- the cutoff frequency (e.g. −3 dB),
- and the frequency where the desired attenuation is reached.
    
An _ideal_ filter would have a vertical transition (rectangular response), but this **does not exist in practice**.

- Wide transition band → easier to build, less selective
- Narrow transition band → better noise rejection, harder to build
    
#### <span style="color:rgb(2, 141, 192)">2. Amplitude distortion (ripple)</span>

![[Pasted image 20260102211119.png]]
Filters may introduce **ripples**, meaning that different frequencies in the passband are amplified differently.

- Flat passband → minimal amplitude distortion
- Rippled passband → signal shape distortion
    
#### <span style="color:rgb(2, 141, 192)">3. Phase distortion (very important)</span>
Any real signal can be decomposed into sinusoids.  
A linear system affects each sinusoid by:

- changing its **amplitude**    
- adding a **phase shift**
    

If the **phase response is linear with frequency**, then:

- all sinusoids are delayed by the same amount of time,
- the signal shape is preserved,
- this constant delay is called **group delay** (measured in seconds).
    
If the phase is **non-linear**:

- different frequency components are delayed differently,
- the reconstructed signal is **distorted in time**,
- this is especially harmful for EMG waveform analysis.
    

### <span style="color:rgb(161, 40, 226)">Common analog low-pass filter families</span>

#### <span style="color:rgb(2, 141, 192)">1. Butterworth filter</span>

![[Pasted image 20260102211207.png|200]]
- **Monotonic and flat passband**    
- No ripple
    
- **Good phase linearity**
- Wider transition band
    

✅ Very good when **signal shape preservation** matters  
❌ Less selective in frequency

#### <span style="color:rgb(2, 141, 192)">2. Chebyshev filters</span>

![[Pasted image 20260102211248.png|200]]

**Type I**

- Ripple in the **passband**
- Steeper transition band than Butterworth
    
**Type II**

![[Pasted image 20260102211315.png|200]]
- Flat passband
- Ripple in the **stopband**
    
❌ Worse phase linearity than Butterworth  
⚠️ Some amplitude distortion

### 3. Elliptic (Cauer) filter

![[Pasted image 20260102211344.png|200]]
- Ripple in **both passband and stopband**
- **Very sharp transition band** (closest to ideal)
    

✅ Excellent frequency selectivity  
❌ Strong amplitude ripple  
❌ Very poor phase linearity  
❌ More sensitive to component tolerances

#### <span style="color:rgb(2, 141, 192)">Poles and zeros</span>

- Butterworth and Chebyshev: **only poles**
- Elliptic: **poles and zeros**
    
Having zeros makes the filter:

- more selective,
- but harder to design,
- more sensitive to component tolerances,
- especially problematic when poles and zeros nearly cancel.
### <span style="color:rgb(161, 40, 226)">Practical trade-off</span>

- If you need **very sharp frequency separation** (e.g. 50 Hz vs 55 Hz), elliptic filters are effective.
- If you care about **signal morphology and timing** (as in EMG), Butterworth filters are often preferred.
- There is **no perfect filter**: every design is a compromise between
    - selectivity,
    - amplitude distortion,
    - phase distortion,
    - implementation complexity.
        

### <span style="color:rgb(161, 40, 226)">Analog vs digital filters</span>

Digital filters generally:
- offer **better performance and flexibility**,
- allow precise control of amplitude and phase,
- are easier to redesign.
    
However:
- **they cannot replace analog filters before sampling**,
- analog filtering is mandatory for **anti-aliasing**.

### <span style="color:rgb(161, 40, 226)">Butterworth filter: magnitude response</span>

The **Butterworth filter** is characterized by a **maximally flat and monotonic magnitude response** in the passband.  
This means:

- no ripple in the passband,
- smooth attenuation beyond the cutoff frequency.

![[Pasted image 20260102213818.png|200]]
If we look at the **squared magnitude** of the transfer function

$$  
\left|\frac{V_\text{out}}{V_\text{in}}\right|^2  
$$
its frequency response has a characteristic shape:

- ( $f_c$ ) is the **cutoff frequency**
- ( $n$ ) is the **order of the filter**
    
A key property of Butterworth filters is that **independently of the order ( n )**:

$$\left|\frac{V_\text{out}}{V_\text{in}}\right|^2 = \frac{1}{2}  
\quad \text{at} \quad f = f_c  $$
This corresponds to:
- **−3 dB in amplitude (gain)**
- **−6 dB in power**
    
Therefore, **all Butterworth filters cross −3 dB exactly at the cutoff frequency**, regardless of their order.

The **order (n)** of the Butterworth filter does **not change**:
- the −3 dB point at ( $f_c$ ),
    
but it **does change**:
- the **steepness of the transition band**.
    
Higher-order Butterworth filters:
- attenuate faster beyond ( $f_c$),
- but preserve a flat passband and smooth phase behavior.
    
#### <span style="color:rgb(2, 141, 192)">Passive vs active implementation</span>

##### <span style="color:rgb(71, 215, 140)">Passive low-pass filters</span>

![[Pasted image 20260102214156.png]]
A **second-order passive low-pass filter** requires:

- **one capacitor**
- **one inductor**
    
This is because:
- capacitors store energy as **electric charge**,
- inductors store energy as **magnetic current**,
- these two storage mechanisms are phase-shifted with respect to each other.
    

However, inductors present several practical problems:
- they generate **magnetic fields**,
- they are bulky,
- they have **large tolerances** (often ±10% or worse),
- their parasitics affect accuracy.
    

As a result:

- the actual cutoff frequency may differ from the design value,
- the filter may only approximate a Butterworth response.
    
This limitation applies not only to Butterworth filters, but also to **Chebyshev and elliptic passive filters**.


#### <span style="color:rgb(2, 141, 192)">Active Butterworth filters (Sallen–Key topology)</span>

To avoid inductors, Butterworth filters are commonly implemented as **active filters**, using:

- resistors,
- capacitors,
- an operational amplifier.
    
![[Pasted image 20260102214044.png|500]]
A very common structure is the **Sallen–Key second-order low-pass filter**.

In this configuration:

- the operational amplifier **emulates the behavior of an inductor**,
- energy storage is achieved using **only capacitors**,
- the circuit realizes a **second-order dynamic system**,  
    equivalent to an RLC passive filter.
    
The positive feedback around the capacitor creates the required phase behavior. The Sallen–Key configuration is **non-inverting**, and its gain is:
$$G = 1 + \frac{R_2'}{R_2}  
$$
This gain:

- affects the **quality factor (Q)** of the filter,
- must be carefully chosen to obtain the correct Butterworth response.

##### <span style="color:rgb(71, 215, 140)">Why active Butterworth filters are preferred in EMG systems</span>

- No inductors → compact and stable design
- Better control of cutoff frequency
- Flat passband → minimal signal amplitude distortion
- Better phase behavior than Chebyshev or elliptic filters
  
> A Butterworth filter always reaches −3 dB at the cutoff frequency, regardless of order.  
> Active implementations (like Sallen–Key) are preferred because they avoid inductors, improve accuracy, and preserve EMG signal integrity.


### <span style="color:rgb(161, 40, 226)">Why we focus on second-order filters</span>

Let’s start from **first-order filters**.

#### <span style="color:rgb(2, 141, 192)">First-order low-pass filter</span>

A **first-order Butterworth low-pass filter** is simply the classical **RC passive low-pass**:

- Time constant:  $$\tau = RC  $$
- Cutoff pulsation:  
    $$\omega_c = \frac{1}{\tau} = \frac{1}{RC} $$
Now an important observation:

> A **first-order Butterworth**, **first-order Chebyshev**, and **first-order elliptic filter** all have **exactly the same topology and component values**.

This happens because:
- with only one pole, there is **no freedom** to shape the response,
- differences between filter families only appear **from second order onward**.
    
That is why first-order filters are **not very interesting** from a design point of view.

#### <span style="color:rgb(2, 141, 192)">Building higher-order filters by cascading</span>

Higher-order filters are obtained by **cascading lower-order sections**:

- **1st order** → one RC cell
- **2nd order** → one second-order cell
- **3rd order** → one 1st-order + one 2nd-order
- **4th order** → two 2nd-order cells
- **5th order** → one 1st-order + two 2nd-order cells
- and so on…

⚠️ **Important warning**

If you want a **4th-order Butterworth filter**, you **cannot** simply cascade **two identical 2nd-order Butterworth filters**.

Why?

Each Butterworth filter has:

- **−3 dB at its cutoff frequency**
    
If you cascade two identical 2nd-order Butterworth sections:  
$$(-3\text{ dB}) + (-3\text{ dB}) = -6\text{ dB}  $$

So the resulting filter would **not** have the correct Butterworth response.

**Conclusion:**  For orders ≥ 2, **each second-order section must have different parameters**.

The **only section that remains identical** for all orders is the **first-order section**, used only in odd-order filters.

#### <span style="color:rgb(2, 141, 192)">General second-order transfer function</span>

To design a second-order Butterworth section, we start from the **canonical second-order transfer function**:
$$H(s) = \frac{\omega_n^2}{s^2 + 2\zeta \omega_n s + \omega_n^2}  $$

Where:
- ( $\omega_n$ ) = **natural (cutoff) pulsation**
- ( $\zeta$ ) = **damping factor**
    
These two parameters fully define:

- the **frequency response**,
- the **pole positions** in the complex (Gauss) plane,
- the filter’s transient and phase behavior.
    
#### <span style="color:rgb(2, 141, 192)">Sallen–Key second-order Butterworth filter</span>

In the **Sallen–Key active low-pass configuration**:
![[Pasted image 20260102215048.png|400]]
**Cutoff pulsation**
$$\omega_n = \frac{1}{RC}  $$

So the design is straightforward:

1. choose ( $\omega_n$ ) (cutoff frequency),
2. select either ( R ) or ( C ),
3. compute the remaining component.
This sets the **radius of the pole locations** in the complex plane.

**Damping factor and gain**

For the Sallen–Key topology, the damping factor is:
$$\zeta = \frac{3 - A_v}{2}  $$

where the amplifier gain is **non-inverting**:
$$A_v = 1 + \frac{R_2}{R_1} $$
So:
- the **gain directly controls the damping factor**,
- and therefore the **shape of the frequency response**.
    
#### <span style="color:rgb(2, 141, 192)">Why Butterworth polynomials matter</span>

The value of ( $\zeta$ ) **is not arbitrary**.

For a Butterworth filter:
- ( $\zeta$ ) is obtained from **Butterworth polynomials**,
- which depend only on the **filter order**.
    
These values:
- are available in tables,
- or can be computed analytically.
    
Once ( $\zeta$ ) is known:
1. compute the required gain ( $A_v$ ),
2. select ( $R_1$ ) and ( $R_2$ ),
3. the second-order Butterworth section is fully defined.
    
#### <span style="color:rgb(2, 141, 192)">Frequency response parameters</span>

Looking at the frequency response of the Sallen–Key cell, we see that it is fully determined by:

- **( $\omega_n$ )** → cutoff frequency
- **( $\zeta$ )** → damping / selectivity
    
These two parameters control:
- bandwidth,
- roll-off steepness,
- phase behavior.
    
### <span style="color:rgb(161, 40, 226)">Bode plot behavior of Butterworth filters (order 1–4)</span>

![[Pasted image 20251002174410.png|500]]

The figure shows the **Bode magnitude plots** of Butterworth low-pass filters of **order 1, 2, 3, and 4**.
Two fundamental properties characterize **all Butterworth filters**, regardless of order:

#### <span style="color:rgb(2, 141, 192)">1. −3 dB at the cutoff frequency</span>

For **any order**, all Butterworth filters:
- cross **−3 dB exactly at the cutoff frequency** ($f_c$ ),
- do so **without ripple** in the passband.
    
This is a defining property of the Butterworth family and one of the main reasons it is widely used in biomedical signal processing.
#### <span style="color:rgb(2, 141, 192)">2. Maximally flat passband</span>

Butterworth filters are called **maximally flat** because:
- At ( $f = 0$ ) (DC),
- the **maximum possible number of derivatives** of the magnitude response are zero.
    
More precisely:

- for an ( $n$ )-th order Butterworth filter,
- the first ( $2n - 1$ ) derivatives of ( $|H(j\omega)|^2$ ) at ( $\omega = 0$ ) are zero.
    

This means:
- the passband is **as flat as mathematically possible** for a filter of that order,
- no other filter of the same order can have a flatter passband.
    
Increasing the order **does not change passband flatness**, it only:
- increases the **slope of attenuation** in the stopband.
    
#### <span style="color:rgb(2, 141, 192)">Effect of filter order on attenuation slope</span>

Each pole contributes approximately **−20 dB/decade** to the roll-off.

So:

- 1st order → −20 dB/dec
- 2nd order → −40 dB/dec
- 3rd order → −60 dB/dec
- 4th order → −80 dB/dec
    
As the number of poles increases:
- the transition from passband to stopband becomes **steeper**,
- the cutoff frequency remains fixed at the −3 dB point.
This is clearly visible in the plots.

### <span style="color:rgb(161, 40, 226)">Butterworth polynomials and pole placement</span>

The Butterworth filter is defined by **Butterworth polynomials**, which form the **denominator** of the transfer function.
![[Pasted image 20260102220005.png|300]]
Key observations:

- the **constant term is always 1**,
- the coefficient of the ( $s$ ) term determines the **damping factor** ( $\zeta$ ).

In practice:
- the filter is first designed for a **unit-radius circle** in the complex (Gauss) plane,
- then scaled to the desired cutoff frequency using:  
    $$\omega_n = \frac{1}{RC}  $$
So:

- ( $\omega_n$ ) sets the cutoff frequency,
- the polynomial coefficients define ( $\zeta$ ).

For a **second-order section**:    
$$\zeta = \frac{\text{coefficient of } s}{2} $$
### <span style="color:rgb(161, 40, 226)">Even vs odd order filters</span>
![[Pasted image 20251002174501.png]]

- **Odd-order filters**:
    - contain one **first-order** section,
    - plus several **second-order** sections.
        
- **Even-order filters**:
    - are made entirely of **second-order sections**.
    
The first-order section:
- has no damping factor ( $\zeta$ ),
- only sets the cutoff frequency via ( RC ).
    
### <span style="color:rgb(161, 40, 226)">Critical point: fourth order ≠ two identical second orders</span>

A **fourth-order Butterworth filter is NOT obtained by cascading two identical second-order Butterworth filters**.

Why?

- Each second-order section must have a **different damping factor** ( $\zeta$ ),
- these values come from the **Butterworth polynomial of the chosen order**.
    
If you cascade two identical second-order Butterworth sections:

- the −3 dB point shifts,
- the frequency response is **no longer Butterworth**.
    

This is why:

- a 4th-order Butterworth filter uses **two different second-order cells**,
- each cell has its own ( $\zeta$ ) and therefore its own gain (in Sallen–Key form).
    

![[Pasted image 20251002174752.png|500]]
![[Pasted image 20251002175046.png|500]]
If we compare **Butterworth, Chebyshev, and Bessel filters**, the main difference is not really in the ultimate slope of attenuation, but in **where that slope starts** and **what happens to the signal phase**.

From a magnitude (gain) point of view, all three filters eventually show **parallel slopes** at high frequencies. This is because, for a given order, the asymptotic decay depends only on the number of poles (about −20 dB/decade per pole). As frequency increases, their behaviors become more and more similar. The real difference appears in the **transition region**, near the cutoff frequency.

* The **Chebyshev filter** reaches the same attenuation level **earlier in frequency** compared to Butterworth. In other words, for the same order, it has a **steeper transition band**, meaning it suppresses unwanted frequencies more aggressively. This improvement in selectivity comes at a cost: the Chebyshev filter introduces **ripples in the passband** and, more importantly, **strong phase distortion**. When looking at phase-related quantities, such as group delay, Chebyshev filters perform poorly, especially in the passband.

* The **Butterworth filter** represents a compromise. Its magnitude response is **maximally flat**, meaning there are no ripples in the passband, and the cutoff always occurs at −3 dB regardless of order. Its transition band is not as steep as Chebyshev, but not as poor as Bessel either. In terms of phase behavior, Butterworth filters are **not linear-phase**, but their group delay is relatively smooth and acceptable in many practical applications, including biomedical signals like EMG.

* The **Bessel filter**, on the other hand, performs worst in terms of magnitude selectivity. Its transition band is wide, and attenuation increases slowly with frequency. From a purely frequency-domain perspective, it may look “bad.” However, the reason to use a Bessel filter lies entirely in the **phase response**. The Bessel filter is designed to have an **almost constant group delay in the passband**, which means that all frequency components experience nearly the same time delay. This corresponds to an **approximately linear phase response**, so the waveform shape in the time domain is preserved as much as possible. This becomes clear when looking at the group delay, defined as the negative derivative of the phase with respect to angular frequency. If the group delay is constant, the phase varies linearly with frequency. Among the three filters, the Bessel filter has the flattest group delay, the Butterworth is reasonably close, and the Chebyshev shows large variations, leading to significant waveform distortion.

In summary, although all three filters converge to similar attenuation slopes at high frequencies, they serve different purposes. The **Butterworth filter** prioritizes amplitude flatness, the **Chebyshev filter** prioritizes steep attenuation, and the **Bessel filter** prioritizes minimal phase distortion and waveform fidelity..


![[Pasted image 20251002175312.png]]
Here we are looking at how the **poles of a Butterworth filter are placed in the complex (Gauss) plane**, and how this placement depends on the **order of the filter**.

For a Butterworth filter, all poles lie on a **circle of radius ωₙ** in the **left half-plane**. The left half-plane placement is mandatory for stability, so no poles ever appear on the right side. The exact value of the radius is not critical at the beginning, because after the design you can always rescale the filter to the desired cutoff frequency.

The difference between **even and odd order filters** is very clear.  If the order is **even**, all poles appear as **complex-conjugate pairs**, symmetrically placed with respect to the real axis.  
If the order is **odd**, there is always **one real pole** located on the negative real axis, plus the remaining poles arranged as complex-conjugate pairs. That real pole corresponds directly to the first-order cell in the circuit.

A very practical and intuitive design rule avoids using Butterworth polynomials altogether. You take the full circle, **360 degrees**, and divide it into **2n equal angular sectors**, where _n_ is the order of the filter. For example, for a third-order filter, you divide the circle into six equal parts. Then:

- For **odd orders**, one pole lies exactly on the negative real axis.
- For **even orders**, poles are placed symmetrically around the real axis, without any pole exactly on it.
    

Only the poles in the **left half-plane** are kept; the right half-plane poles are discarded.

Once the poles are positioned, the **damping factor ξ (zeta)** of each second-order cell can be obtained directly from geometry. For a given pole, ξ is simply the **cosine of the angle θ** between the pole and the negative real axis. For example, an angle of 45° gives ξ = √2/2, while 60° gives ξ = 1/2. This makes it very easy to compute the exact ξ values needed for each second-order section.

In short, the Butterworth pole placement is highly structured: the order defines how many poles there are, symmetry ensures stability and flatness, and a simple geometric rule lets you extract the damping factors without explicitly using Butterworth polynomials.

### <span style="color:rgb(161, 40, 226)">High Pass Filter</span>

![[Pasted image 20251002175722.png]]

Up to now we have only discussed **low-pass filters**—Butterworth, Bessel, and Chebyshev—but in EMG acquisition we also **need high-pass filters**, mainly to remove low-frequency components such as motion artifacts and slow baseline variations.

For the **Butterworth filter**, moving from a low-pass to a high-pass implementation is actually very straightforward. Conceptually, nothing changes in the “shape” of the filter: the **denominator of the transfer function remains the same**, meaning that the pole locations are unchanged. What changes is the **numerator**, which now introduces zeros at the origin.

From a circuit point of view, this transformation is done simply by **swapping resistors and capacitors** in the low-pass topology. Wherever you had a capacitor, you place a resistor, and wherever you had a resistor, you place a capacitor. The overall structure of the circuit remains the same, including the amplifier configuration and the gain expression.

Because of this swap, a second-order high-pass Butterworth filter will have **two zeros at zero frequency**, while keeping the same second-order denominator as the low-pass version. As a result, low frequencies are strongly attenuated, while higher frequencies pass through with the same Butterworth characteristics: maximally flat magnitude response and a −3 dB point at the cutoff frequency.

So, in practice, designing a high-pass Butterworth filter is not a new problem at all. You reuse the same design rules, the same damping factors, and the same gain calculations—only the **roles of resistors and capacitors are exchanged**, and the filter now suppresses low-frequency components instead of high-frequency ones.

### <span style="color:rgb(161, 40, 226)">A/D Resolution and sampling frequency</span>

Here we are looking at the **key characteristics of analog-to-digital (A/D) conversion**, especially as they apply to EMG signals.
![[Pasted image 20251002182154.png|600]]

First, there are **three main types of A/D converters**, ordered from fastest to slowest conversion speed: **Flash**, **Ramp (or integrating)**, and **SAR (Successive Approximation Register)**. Flash converters are extremely fast because they perform the conversion in a single step, but this comes at the cost of very high circuit complexity, power consumption, and price, and often with limited resolution. Ramp converters are simple but slow. SAR converters sit in between and are the most commonly used in biomedical and EMG systems because they offer a good compromise between **speed, accuracy, cost, and power consumption**.

In general, there is an important trade-off: **the higher the number of bits, the slower the converter** tends to be. Increasing resolution requires more precise comparisons and longer conversion time. For this reason, the design of the A/D stage usually starts from the **expected signal amplitude**. Typical A/D input ranges are ±5 V, ±10 V, or ±15 V. The EMG signal must therefore be **amplified and conditioned** so that it fully exploits this input range without clipping.

The **resolution** of an A/D converter depends on the number of bits NNN. The smallest voltage change that can be resolved—the **Least Significant Bit (LSB)**—is given by
$$V_{\text{LSB}} = \frac{V_{\text{range}}}{2^N}$$

where $V_{\text{range}}$​ is the full-scale input range of the converter. This value represents the quantization step of the A/D.

For proper EMG acquisition, the **LSB amplitude should be comparable to, or smaller than, the noise level** of the system. If the LSB is much larger than the noise, quantization error dominates and information is lost. In practice, **12 to 16-bit A/D converters are usually sufficient** for EMG signals. A useful rule of thumb is that the quantization signal-to-noise ratio increases by about **6 dB per bit**, so higher resolution directly improves measurement accuracy—up to the point where analog noise becomes the limiting factor.

![[Pasted image 20251002183220.png|600]]

Finally, the **sampling frequency** must satisfy the **Shannon–Nyquist theorem**. To correctly reconstruct a signal after A/D conversion, the sampling frequency fsf_sfs​ must be **greater than twice the maximum frequency content of the signal**:

$$f_s > 2 f_{\max}$$

Since EMG signals can contain frequency components up to several hundred hertz, the sampling rate must be chosen accordingly, usually with some margin to account for filter roll-off and non-idealities.

In summary, proper A/D design for EMG requires matching the **signal amplitude to the full input range**, choosing a **resolution that balances noise and speed**, selecting an appropriate **converter architecture**, and ensuring a **sampling rate that respects the Shannon–Nyquist criterion**.


# <span style="color:rgb(223, 109, 109)">Preprocessing</span>

Once the signal has been properly acquired—using all the techniques we discussed before, such as amplification, filtering, grounding, and A/D conversion—the next step is **signal processing**. The goal of this stage is to extract **diagnostic parameters** that are useful for identifying possible pathologies and for guiding treatment.

![[Pasted image 20251002183727.png]]
This is the path we started following a couple of weeks ago, and at this point we are at the **pre-processing stage**. Pre-processing is crucial because raw EMG signals are affected by many sources of variability and noise, and they are not immediately suitable for direct clinical interpretation.

![[Pasted image 20251002183800.png|700]]
It is useful to recall how the EMG signal is generated. Muscles have a **hierarchical structure**: small fibrils are grouped into muscle fibers, fibers are organized into motor units, and motor units form the muscle. Each muscle contraction is associated with an **electrical activity**, and this electrical activity is what ultimately triggers the mechanical contraction. What we measure with EMG—especially surface EMG—is therefore an indirect observation of this electrical activation.

The detected EMG signal typically looks like a **stochastic signal**. It is stochastic because, unless you are recording from a single muscle fiber, you are observing the combined activity of many motor units firing in a partially random and asynchronous way. As a result, you will **never obtain exactly the same signal in two different acquisitions**, even if the task and conditions are identical.

A typical surface EMG signal is characterized by **bursts of activity** during muscle contraction and an **almost zero-level signal** when the muscle is at rest. This burst-like, non-deterministic behavior is one of the defining features of EMG and is the main reason why careful pre-processing is needed before extracting meaningful features for diagnosis or analysis.



![[Pasted image 20251002183933.png]]

Essentially, two main effects shape the EMG signal and explain why it looks irregular and why its amplitude does not always reflect the true level of muscle activation.

The first effect is the **stochastic activation of motor units**. During a muscle contraction, the central nervous system does not recruit motor units in a perfectly synchronized or repeatable way. Even when the same motor units are involved, they are activated with **different timing (delays)** from one contraction to the next and even within the same contraction. Because of this variable recruitment and firing timing, the resulting EMG signal is **not repeatable**: two recordings under identical conditions will still look different.

The second effect is **cancellation**. With surface EMG, we are not recording the activity of a single motor unit, but the **interference signal**, which is the sum of the action potentials generated by many motor units at the same time. Since these action potentials can have different polarities and phases, it is very common that a positive peak from one motor unit overlaps in time with a negative peak from another. When this happens, their contributions partially or even completely cancel each other out. What the electrodes measure is the algebraic sum of all these contributions at each instant, so the recorded signal amplitude can be **smaller than the actual underlying activity**.

These two phenomena have a common origin: the **stochastic nature of motor unit activation, firing times, and propagation**. Because action potentials are added together in time, their summation does not always lead to a larger signal. In some cases, adding more action potentials can actually reduce the measured amplitude instead of increasing it. This leads to what is called **cancellation or underestimation of the EMG signal**, and it can also cause apparent shifts or distortions in the waveform.

For this reason, the raw EMG amplitude is not a straightforward measure of muscle activation, and careful pre-processing and feature extraction are needed to obtain reliable physiological or clinical information.

![[Pasted image 20251002184216.png]]
If we look at the **power spectrum of a surface EMG signal**, it has some very characteristic features that are quite different from what we would expect from an ideal or “textbook” signal.

First of all, the spectrum is **asymmetric**. Most of the useful frequency content lies roughly between **20–250 Hz**, and in many cases it can extend up to **400–500 Hz**, depending on the muscle, electrode type, and experimental setup. The **maximum power (the spectral peak)** is typically located somewhere between **50 and 80 Hz**, which can be considered the central region of the EMG spectrum.

At low frequencies, you always observe a **drop in spectral power below about 10–20 Hz**. This is not a physiological property of the muscle itself, but rather an **artifact introduced by signal conditioning**. In practice, EMG signals are always passed through a **high-pass filter** to remove low-frequency disturbances such as motion artifacts, electrode–skin impedance changes, and baseline drift. As a consequence, the spectrum is forced toward zero at very low frequencies, and this behavior is clearly visible in the power spectrum.

Another important point is that the EMG power spectrum is **not Gaussian**. It is clearly skewed, with a long tail toward higher frequencies. This non-Gaussian shape reflects the complex and stochastic nature of motor unit action potentials: different conduction velocities, different firing rates, and the summation and cancellation effects that occur when many motor units are active simultaneously.

Because of these properties, working in the **frequency domain**—and especially with the **power spectrum**—is often advantageous. The power spectrum is less sensitive to the exact timing of individual motor unit action potentials and to cancellation effects in the time domain. It allows us to identify meaningful features such as **peak frequency, mean frequency, or median frequency**, which are widely used in EMG analysis, for example to study muscle fatigue or changes in muscle activation patterns.

So, in summary, the EMG power spectrum is asymmetric, band-limited, shaped by high-pass filtering at low frequencies, and distinctly non-Gaussian—features that make spectral analysis particularly useful for EMG signal interpretation.


![[Pasted image 20251002184823.png]]

Because the **EMG power spectrum is clearly non-Gaussian and strongly asymmetric**, using **parametric statistics** is not appropriate.

Parametric statistics rely on the assumption that the data follow a known distribution, typically a **Gaussian (normal) distribution**. In that case, the distribution can be fully described by just two parameters: **mean** and **variance**. For a perfect Gaussian distribution, several statistical descriptors coincide or take fixed values: the **mean, median, and mode are identical**, and higher-order descriptors such as **skewness** (asymmetry) and **kurtosis** (peakedness) are both equal to zero.

This is not what happens with EMG spectra. The EMG power spectrum is **asymmetric**, with a long tail toward higher frequencies, so the **mean, median, and mode are different**. In addition, the skewness is non-zero and the kurtosis is not zero either, indicating a distribution that is both asymmetric and differently shaped compared to a Gaussian curve. As a consequence, the mean alone is not a reliable descriptor of the spectral content, and variance does not fully capture the dispersion of the data.

For this reason, EMG spectral analysis typically relies on **non-parametric approaches**. These methods do not assume any specific underlying distribution and instead use robust descriptors such as the **median frequency**, **percentile-based measures**, or other distribution-free estimators. These quantities are much more stable and meaningful when dealing with asymmetric, non-Gaussian data like EMG power spectra.

==So, the key point is that the statistical nature of the EMG signal itself dictates the choice of analysis tools: since the spectrum is not Gaussian, **non-parametric statistics are the correct and physically meaningful choice**.==

![[Pasted image 20251002185148.png]]

The **amplitude of the surface EMG signal does not depend only on the level of muscle activation**, but also very strongly on the **physical characteristics of the patient**. For example, the thickness of **subcutaneous fat**, skin properties, and tissue composition between the muscle and the electrodes act as a **spatial low-pass filter** and attenuate the signal. If one patient has a thicker fat layer than another, the EMG signal will be **more attenuated** before it reaches the electrodes, even if both patients are producing the **same muscle contraction force**.

Because of this, two patients performing the same task with the same level of activation can produce EMG signals with **very different amplitudes**. This variability is not due to differences in neural drive or muscle physiology, but simply to **volume conduction effects** and electrode–tissue coupling.

That is why **absolute EMG amplitude is not directly comparable across subjects** (and sometimes not even across different sessions in the same subject). In practice, this is the reason why EMG analysis often relies on:

- **Normalization procedures** (for example, to a maximum voluntary contraction, MVC), or
- **Frequency-domain features** (like median or mean frequency), which are much less affected by tissue thickness and amplitude scaling.

![[Pasted image 20251002185301.png]]

These are the main **drawbacks of surface EMG signal detection**.

First, there is the **cancellation effect**. When many motor unit action potentials are summed together, positive and negative phases can overlap in time and partially cancel each other. Because of this, the measured EMG amplitude is **smaller than the true underlying neural activity**. As a consequence, if you try to estimate the total number of active muscle fibers from the EMG signal, you will **systematically underestimate** it. This underestimation is intrinsic to surface EMG and cannot be completely avoided.

A second important limitation is **physiological crosstalk**. When two muscles are close to each other, the electrical activity generated by one muscle can be detected by the electrodes placed over the neighboring muscle. For example, one muscle alone would produce one EMG signal, and another nearby muscle would produce a different one, but what is actually measured is the **sum of both contributions**. From this combined signal, it is very difficult—often impossible—to separate the activity of the individual muscles. You cannot “turn off” one muscle to observe the other in isolation.

The only practical way to reduce crosstalk is through **electrode placement**: positioning the electrodes as far as possible from other active muscles and **reducing the detection volume** by placing the electrodes closer to each other. However, even with careful placement, crosstalk cannot be completely eliminated and must be accepted as a fundamental limitation of surface EMG.

![[Pasted image 20251002185416.png]]
Another important problem comes from **changes in muscle geometry during contraction**. When a muscle contracts, its shape and position change, and this also changes the **relative position between the electrodes and the muscle fibers** generating the signal. As a result, even if the level of neural activation were the same, the recorded EMG signal could vary simply because the electrodes are sensing a different portion of the muscle. For this reason, EMG is **not a reliable tool for accurately estimating muscle force**: when force changes, electrode position changes as well, and the measured signal does not depend only on force.

In addition to this, EMG recordings are affected by **external noise**. This includes low-frequency disturbances such as power-line interference, as well as higher-frequency noise coming from electromagnetic sources like broadcast systems, computers, and other electronic devices. Finally, there are also **internal noise sources**, such as noise generated at the electrode–skin interface and noise introduced by the amplifiers themselves. All these contributions further degrade the quality of the EMG signal and must be managed during acquisition and processing.

![[Pasted image 20251002185618.png]]

This figure shows a **typical EMG recording**. In theory, when the muscle is at rest, the signal should appear as a **thin, almost flat line**. Then, during contraction, we expect bursts of activity, followed again by flat segments during rest.

![[Pasted image 20260102230444.png|300]]
In practice, however, during the resting phases we often observe a **thick line instead of a thin one**. If we zoom in, we can see that this thickness is caused by a **50 Hz sinusoidal oscillation**, which corresponds to **power-line interference** (50–60 Hz hum). This noise is present even when the muscle is not active.

![[Pasted image 20260102230537.png|400]]
Another common issue is the **baseline offset**, which is a shift of the signal away from zero. This offset is mainly due to **DC offsets introduced by the amplifiers**. Fortunately, this problem is relatively easy to handle during signal processing.

In other cases, we observe **slow baseline shifts**, where the baseline moves up and down over time. These shifts are typically caused by **movement of the electrodes on the skin**, which changes the electrode–skin impedance and generates low-frequency artifacts.

![[Pasted image 20260102230523.png|300]]
Finally, the figure also shows **ECG artifacts**. These appear as large, sharp peaks superimposed on the EMG signal and are caused by the electrical activity of the heart, especially when electrodes are placed close to the chest. ECG artifacts are difficult to remove using filtering alone. Although the heart rate is around 1 Hz, the ECG waveform contains significant **high-frequency components**, so simply applying a high-pass or low-pass filter would distort the EMG signal as well.

For this reason, **filtering is not an effective solution for removing ECG artifacts**. The most reliable approach is to **place the electrodes farther away from the chest**, minimizing the contribution of cardiac activity to the recorded EMG signal.