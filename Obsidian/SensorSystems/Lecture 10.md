
20/11/2025
***

Hello everybody, the topic of today is microphones. We will start introducing the sound field quantities and then we will introduce the fundamentals of microphones. Then we will discuss two different types of microphone capsules, in particular the dynamic and the condenser microphones. And we will conclude speaking about the phantom power. 

# <span style="color:rgb(223, 109, 109)">Microphone</span>

A **microphone** is a sensor designed to detect **sound**, which is a mechanical vibration that propagates through a medium. Sound is an **audible mechanical wave** characterized by variations of **pressure** and **particle displacement** within that medium.

## <span style="color:rgb(239, 179, 1)">Sound Field</span>

Sound waves are **longitudinal**, meaning the movement of the particles in the medium occurs **parallel** to the direction in which the wave travels. These waves can propagate in **gases** and **liquids**.

Mechanical longitudinal waves are also known as:
![[Pasted image 20251203113910.png|500]]
- **Compressional waves**, due to alternating regions of **compression** (higher density and pressure) and **rarefaction** (lower density and pressure).
- **Pressure waves**, as they cause fluctuations—both increases and decreases—in pressure over time.
    
In summary, sound travels through a medium forming continuous cycles of **compression** and **rarefaction**, and microphones are the devices capable of detecting and converting these pressure variations into electrical signals.

Below is a **clear, structured and well-written** version of the next section of your notes. The scientific meaning remains unchanged, but the explanation is more organized and easier to follow.

### <span style="color:rgb(161, 40, 226)">Sound Field Quantities</span>

To better understand how a microphone senses sound, we need to examine the main physical quantities that characterize a sound field.
#### <span style="color:rgb(2, 141, 192)">Particle Distribution and Wave Propagation</span>
![[Pasted image 20251203115230.png]]

In an undisturbed medium, particles are **evenly distributed**.  When a sound wave travels through the medium, these particles begin to oscillate around their equilibrium positions. This motion creates alternating regions of:

- **Compression** — particles are pushed closer together.
- **Rarefaction** — particles move farther apart.

#### <span style="color:rgb(2, 141, 192)">Particle Displacement<br></span>
If we observe the motion of a single particle over time:

![[Pasted image 20251203115325.png]]
- At the center of a **compression zone**, the particle displacement is **zero**.
- At the center of a **rarefaction zone**, the displacement is also **zero**.
    
Between these two points, the displacement follows a **sinusoidal pattern**.

#### <span style="color:rgb(2, 141, 192)">Pressure Variation</span>

While displacement reaches zero at the centers of compression and rarefaction, **pressure behaves differently**:

- **Pressure is maximum** at the center of a compression zone.
- **Pressure is minimum** at the center of a rarefaction zone.
    
Therefore, pressure and displacement are shifted relative to each other in the sound wave.

#### <span style="color:rgb(2, 141, 192)">Particle Velocity</span>

Particle velocity is defined as the **time derivative of particle displacement**.  
This means:
![[Pasted image 20251203115603.png]]
![[Pasted image 20251203115807.png]]
- Velocity is **maximum** when displacement crosses zero with a **positive** slope.
- Velocity is **minimum** when displacement crosses zero with a **negative** slope.

#### <span style="color:rgb(2, 141, 192)">Pressure Gradient</span>

The **pressure gradient** is another key quantity, especially relevant for specific microphone designs.  

![[Pasted image 20251203115959.png]]

It is defined as:

> The difference in pressure between two points in the medium.  
> Mathematically, it corresponds to the **derivative of pressure**.

Because of this relationship:

- The pressure gradient crosses **zero** at points where **pressure reaches a maximum or minimum**, i.e., at the centers of compression and rarefaction.
## <span style="color:rgb(239, 179, 1)">Relationship Between Sound Field Quantities</span>

To establish relationships among the main sound-field variables, we begin with the expression for particle displacement.

### <span style="color:rgb(161, 40, 226)">Particle Displacement and Velocity</span>

Let the **particle displacement** be:
$$\xi(t) = \xi \cdot \sin(\omega t)$$

where **ξ** is the **amplitude of displacement**.  The **particle velocity** is the **time derivative** of displacement:
$$v(t) = \frac{d\xi(t)}{dt} = \xi \omega \cos(\omega t)$$
Thus, the **velocity amplitude** is:
$$v = \omega \xi$$
### <span style="color:rgb(161, 40, 226)">Pressure and Specific Acoustic Impedance</span>

The **pressure amplitude** is related to particle velocity by:
$$p = Z \cdot v$$
where **Z** is the **specific acoustic impedance**, defined as:
$$Z = \rho C$$
with **ρ** being the density of the medium and **C** the speed of sound.  
At around **20°C in air**, $( Z \approx 413 \, \text{Pa·s/m})$. Since ($v = \omega \xi$), pressure can also be written as:
$$p = \omega Z \xi$$

This relation is crucial because **microphones may respond to displacement, velocity, or pressure**, resulting in **different frequency responses**.

### <span style="color:rgb(161, 40, 226)">Angular Frequency and Sound Speed</span>

Angular frequency is defined as:
$$\omega = 2\pi f$$
and sound speed as:
$$C = \lambda f$$
It is important not to confuse these two with **particle velocity**, which is simply the oscillatory motion of each particle around equilibrium.  Instead, **sound speed** is the **wave propagation velocity** through the medium.

Typical values:

| Medium     | Sound Speed |
| ---------- | ----------- |
| Air (20°C) | ~340 m/s    |
| Water      | ~1500 m/s   |

### <span style="color:rgb(161, 40, 226)">Sound Intensity</span>

Another key parameter is **sound intensity**, which relates to perceived loudness. It is defined as:
$$I = \frac{P}{A}$$
and can also be expressed using field quantities as:
$$I = p \cdot v = \frac{p^2}{z} = zv^2=z\xi^2\omega^2$$
By substituting known relations, intensity may also be written entirely in terms of **pressure**, **velocity**, or **displacement**, depending on the application.

# <span style="color:rgb(223, 109, 109)">Microphones</span>

Now, after fundamentals, let's properly start with microphones

Microphones can be grouped into two main families:

1. **Pressure microphones**
2. **Pressure-gradient microphones**

### <span style="color:rgb(161, 40, 226)">Pressure Microphones</span>

![[Pasted image 20251208100605.png]]
Pressure microphones (also called **pressure transducers**) respond to the **absolute pressure amplitude** of the incoming sound wave. A key characteristic of this type is its **omnidirectional response**, meaning:

> The microphone’s sensitivity does not depend on the incident angle of the sound wave.

To describe microphone sensitivity, we define the **Transmission Factor (TF)**:
$$\text{TF} = \frac{V_\text{out}}{P_\text{in}}$$

where:
- $V_\text{out}$​ = output voltage of the microphone
- $P_\text{in}$ = acoustic pressure at the microphone
Thus, **TF directly represents the microphone's sensitivity**.

### <span style="color:rgb(161, 40, 226)">Pressure-Gradient Microphones</span>

Pressure-gradient microphones operate differently. Instead of responding to absolute pressure, they respond to the **pressure gradient**, i.e., the **difference in pressure between two points**—commonly referred to as Point A and Point B.
![[Pasted image 20251208100634.png]]

Because they measure a pressure difference rather than absolute pressure, these microphones exhibit **directional behavior**.

Their sensitivity pattern typically forms a **Figure-8** (or **bidirectional**) response:

- The **maximum sensitivity** occurs at **0°**, when the sound arrives **orthogonally to the diaphragm**.
- The **sensitivity drops to zero** at **90°**, when the sound wave is **parallel to the diaphragm**.
    
### <span style="color:rgb(161, 40, 226)">Combined Patterns</span>

![[Pasted image 20251208100656.png]]

By combining pressure and pressure-gradient principles, various **directional polar patterns** can be achieved. Examples include:
- **Cardioid**
- **Super-cardioid**
- **Hyper-cardioid**
- **Sub-cardioid**

These patterns will be discussed later in the lesson.

## <span style="color:rgb(239, 179, 1)">Pressure Transducers</span>

![[Pasted image 20251208100826.png]]
Pressure transducers are microphones in which **only the front side of the diaphragm is exposed to the incoming sound field**. Because of this configuration, the diaphragm experiences pressure variations directly, without reference to a second point.
### <span style="color:rgb(161, 40, 226)">Directional Independence</span>

Since the microphone measures **absolute pressure**, its response does **not depend on the direction** of the incoming wave. Whether the sound arrives:
- **orthogonally** to the diaphragm,
- **parallel** to it,
- or at **any intermediate angle**,

the **pressure amplitude detected remains the same**. Therefore, the output voltage of a pressure microphone is **angle-independent**, resulting in an **omnidirectional response**.

### <span style="color:rgb(161, 40, 226)">Frequency Independence</span>

Another key property of pressure microphones is that their output is **independent of the frequency** of the sound wave. The microphone reacts only to **pressure amplitude**, not to how quickly the pressure oscillates.

- If frequency changes, the **waveform of the output voltage changes** accordingly,
- but its **amplitude remains unchanged**, provided the incoming sound pressure amplitude is constant.
    
This means that the **output is proportional solely to sound pressure amplitude**, making the behavior simple, predictable, and stable across frequencies.

## <span style="color:rgb(239, 179, 1)">Pressure Gradient Microphone</span>

![[Pasted image 20251208101324.png|500]]
Pressure-gradient microphones operate using **two sensing points**, commonly referred to as **Point A** and **Point B**. The output voltage is therefore proportional to the **difference in pressure** between these two points:

$$V_\text{out} \propto P_A - P_B = \Delta P$$
Because they measure pressure _difference_ rather than absolute pressure, their behavior is strongly influenced by the **direction of arrival** of the sound wave.
### <span style="color:rgb(161, 40, 226)">Dependence on Incident Angle</span>

Consider three incoming directions:

#### <span style="color:rgb(2, 141, 192)">Sound at 0° (Perpendicular to the diaphragm)</span>
![[Pasted image 20251208101412.png]]
The two sensing points experience **different pressures**, producing a measurable pressure difference:
$$\Delta P > 0$$
This corresponds to **maximum sensitivity**.

#### <span style="color:rgb(2, 141, 192)">Sound at 90° (Parallel to the diaphragm)</span>

![[Pasted image 20251208101501.png|]]
Both sensing points lie within the same pressure region (compression or rarefaction), so:

$$\Delta P = 0 \quad \Rightarrow \quad V_\text{out} = 0$$
Sensitivity at this angle is **zero**.

#### <span style="color:rgb(2, 141, 192)">Sound at any intermediate angle</span>
![[Pasted image 20251208101543.png]]
Each point receives a _different but not equal_ pressure.  Therefore:

$$0 < \Delta P < \Delta P_{(0^\circ)}$$
Sensitivity is neither maximum nor zero, resulting in an **intermediate response**.

This behavior produces a **Figure-8 polar pattern**, with:
- **Max sensitivity at 0° and 180°**
- **Zero sensitivity at 90° and 270°**

### <span style="color:rgb(161, 40, 226)">Frequency Dependence</span>

![[Pasted image 20251208101654.png]]
Unlike pressure microphones, pressure-gradient microphones are also affected by **sound frequency**.

For a fixed distance between Points A and B:

- At **low frequencies**, the wavelength is long → the pressure difference $\Delta P$ is small.
- At **higher frequencies**, the pressure variation between A and B increases → $\Delta P$ becomes larger.

Thus, the microphone's output grows with frequency.

### <span style="color:rgb(161, 40, 226)">Directional Characteristic</span>

As mentioned earlier, pressure-gradient microphones exhibit a **directional response**, typically a **Figure-8 pattern**. This polar behavior can be expressed analytically.
#### <span style="color:rgb(2, 141, 192)">Mathematical Description</span>

The **transmission factor** $TF(\theta)$ can be written as:
$$TF(\theta) = TF_0 \cdot \cos(\theta)$$

where:
- $TF_0$​ = sensitivity (transmission factor) at $0^\circ$
- $\theta$ = angle of incidence of the sound wave

![[Pasted image 20251208102420.png|300]]

This equation correctly predicts the microphone's directional behavior:
- At **$\theta = 0^\circ$** → $cos(0^\circ) = 1$ → $TF = TF_0$ → **maximum sensitivity**
- At **$\theta = 90^\circ$** → $\cos(90^\circ)$ = 0 → $TF = 0$ → **no sensitivity**
- At **$\theta = 180^\circ$** → $\cos(180^\circ) = -1$→ $TF = -TF_0$


When the sound arrives from $180^\circ$, the magnitude of the output is the same as at $0^\circ$, but the **sign is inverted**.  This means the microphone's output voltage is **180° out of phase** with the original pressure wave.

So:
- **0° incidence → output in phase with input**
- **180° incidence → output with same amplitude but opposite phase**

Graphically:

| Sound Direction | Output Voltage                 |
| --------------- | ------------------------------ |
| $0^\circ$       | Same phase as pressure         |
| $180^\circ$     | Same amplitude, opposite phase |


## <span style="color:rgb(239, 179, 1)">Cardioid and Mixed Directional Characteristics</span>

There are situations where neither an omnidirectional microphone nor a pure figure-8 microphone is ideal. For example, in a presentation environment with **one speaker and an audience**, we want:

- **high sensitivity at 0°** (the speaker)
- **low or zero sensitivity at 180°** (the audience and room noise behind the mic)
    
To achieve this, we use the **cardioid characteristic**, whose polar shape resembles a heart and offers:

- **Maximum TF at 0°**
- **Zero sensitivity at 180°**
    
### <span style="color:rgb(161, 40, 226)">Obtaining the Cardioid Pattern</span>

The cardioid can be created by combining:
1. **Omnidirectional response:**
    $TF_{\text{omni}} = TF_0$
    (constant at all angles)
2. **Figure-8 response (pressure-gradient):**
    $TF_{\text{fig8}} = TF_0 \cos(\theta)$

By summing these two contributions with equal weight, we obtain the cardioid response:

![[Pasted image 20251208103722.png]]
$$TF(\theta) = TF_0 (1 + \cos\theta)$$

### <span style="color:rgb(161, 40, 226)">Evaluating the Cardioid Pattern</span>

| Angle       | Cos(θ) | TF(θ) = TF₀(1 + cosθ) | Result              |
| ----------- | ------ | --------------------- | ------------------- |
| $0^\circ$   | 1      | $TF = 2TF_0$          | Maximum sensitivity |
| $90^\circ$  | 0      | $TF = TF_0$​          | **−6 dB** vs 0°     |
| $180^\circ$ | −1     | $TF = 0$              | No sensitivity      |

Because the output at 90° is **half of the 0° value**, we get a **6 dB attenuation**.  
At 180° the output is zero → **infinite attenuation**. This makes cardioid microphones ideal for reinforcing speech or signals coming from the front while rejecting sound from behind.

### <span style="color:rgb(161, 40, 226)">Other Mixed Directional Patterns</span>

By modifying the weight of the omnidirectional and figure-8 components instead of using them equally, we can generate other directional patterns:
- **Subcardioid**
- **Supercardioid**
- **Hypercardioid**

These patterns differ in how much they attenuate sound at **90°** and **180°**, offering finer control depending on application needs.

### <span style="color:rgb(161, 40, 226)">Typical Attenuation Characteristics</span>

![[Pasted image 20251208104019.png]]
_Each pattern is formed by a different weighted sum of omnidirectional and figure-8 responses._

 ***
## <span style="color:rgb(239, 179, 1)">Understanding the frequency response of pressure-gradient microphones</span>

To study how the **transmission factor varies with frequency** in a pressure-gradient microphone, we first consider a **simplified condition**:  
a **plane sound field**.

### <span style="color:rgb(161, 40, 226)">What is a plane sound field?</span>

A plane field is an _ideal acoustic field_ in which the **sound pressure amplitude is the same at every point**, meaning that there is no attenuation of the wave as it propagates. Under this assumption, the pressure difference measured by the two sensing points of the microphone—points **A** and **B**—depends **only on the phase difference** of the wave between those points.

So, in a plane field:
$$\Delta p \propto \text{phase difference between A and B}$$

Since phase difference increases with frequency, the **output of a pressure-gradient microphone also increases with frequency**.

### <span style="color:rgb(161, 40, 226)">Why does output increase with frequency?</span>

At low frequencies, the wavelength is large. The two sensing points (separated by a fixed distance) experience almost the same pressure — so the pressure difference is small → small output. As frequency increases, wavelength decreases, so the **phase difference between A and B grows**. Therefore, the measured pressure difference increases, and so does the microphone output (transmission factor).

However, this increase does **not continue indefinitely**.

### <span style="color:rgb(161, 40, 226)">The transition frequency — ft<br></span>
Each microphone has a **transition frequency**, noted $f_t$
- For **frequencies below $f_t$**:  
    Increasing frequency → larger phase difference → larger output.
- At **$f = f_t$**:  
    The two sensors are separated by **half a wavelength**:
    $d_{AB} = \frac{\lambda}{2}$​
    
    This is the condition for **maximum output**, because the pressure at one point matches a wave crest and at the other a trough — the maximum possible difference.
    
- For **frequencies above $f_t$​**:  
    The output **starts to decrease**, even if the frequency increases.
    
### <span style="color:rgb(161, 40, 226)">Why does output decrease above ft?</span>

![[Pasted image 20251208105910.png]]
When the wavelength becomes **shorter than twice the spacing** between A and B, the phase difference exceeds 180°, and the pressure contributions begin to cancel. The microphone can no longer extract a greater differential signal, so its sensitivity rolls off.

Graphically, the transmission factor vs. frequency curve rises until $f_t$​, peaks, then declines.
### <span style="color:rgb(161, 40, 226)">Visual explanation using the diagram</span>

To better understand how the transmission factor depends on frequency in a **pressure-gradient microphone**, we can refer to the drawing showing the two sensing points **A** and **B**, separated by a fixed distance.
![[Pasted image 20251208110526.png]]
#### <span style="color:rgb(2, 141, 192)">Low-frequency case<br></span>
When the sound frequency is low, the wavelength is very large compared to the distance **AB**.  As a result, the **pressure at A and B is nearly the same**, and the pressure difference $\Delta p$.

On the graph (Δp versus frequency), this corresponds to the **left-hand, low-frequency region**:  small $\Delta p$, small output, small transmission factor.

#### <span style="color:rgb(2, 141, 192)">Increasing frequency — Δp grows</span>

If we **increase the frequency**, the wavelength becomes smaller, so the **phase difference between A and B increases**.  This leads to a **larger pressure difference**, and therefore a **larger output**. On the graph, we move upward along the rising part of the curve.
#### <span style="color:rgb(2, 141, 192)">After the transition frequency — output begins to fall</span>

Once we exceed the **transition frequency** $f_t$​, the situation changes. At $f_t$​ the distance **AB** corresponds to **half a wavelength**:

$AB = \frac{\lambda}{2}$​

This is the condition of **maximum measurable pressure difference**, because A corresponds to a peak while B corresponds to a trough (or vice-versa). However, **if we increase frequency beyond this point**, the wavelength becomes _too small_, and the microphone is no longer able to measure a maximum difference. The Δp begins to decrease, and this is reflected by the descending part of the curve.

This is what your third case in the drawing represents.
#### <span style="color:rgb(2, 141, 192)">Zeros of the transmission function</span>

The pressure difference becomes **exactly zero** when the spacing **AB equals one full wavelength**:
$$AB = \lambda$$
In that condition, both sensing elements measure the _same_ point of the wave — only one period apart — so:

$$\Delta p = 0 \quad \Rightarrow \quad TF = 0$$
These **zeros repeat** every time the spacing equals an integer multiple of the wavelength:
$$AB = k\lambda \quad (k = 1,2,3...)$$

meaning the microphone becomes blind to those frequencies.

#### <span style="color:rgb(2, 141, 192)">Practical operating range</span>

Because of this non-monotonic response, **pressure-gradient microphones are typically used only in the first region**, the _green zone_ of your plot — that is, for frequencies **below the transition frequency**, where the response is smooth and rising. For example, if this microphone has its transition frequency around **8 kHz**, then it is suitable for sound detection **up to approximately that range**.

As a reminder, the useful audible band extends roughly from:

$$20 \,\text{Hz} \rightarrow 20 \,\text{kHz}$$

so a microphone with $$f_t \approx 8 \,\text{kHz}$$performs very well for most speech-related applications.

## <span style="color:rgb(239, 179, 1)">Spherical Sound Field and Its Effect on Pressure-Gradient Microphones</span>
![[Pasted image 20251211095956.png|300]]
In a **realistic acoustic environment**, sound rarely behaves like an ideal plane wave.  Instead, it radiates outward from a **point source**, forming a **spherical sound field**.  In such a field, the sound pressure **decreases with distance** from the source.

This attenuation follows a well-known law:

$$I \propto \frac{1}{r^2}$$
where r is the distance from the source.  Therefore, the **pressure** measured at a point farther from the source will be **lower** than the pressure measured closer to it.

### <span style="color:rgb(161, 40, 226)">Two Contributions to the Measured Δp</span>
![[Pasted image 20251211101801.png|300]]
If we place the two sensing elements of a pressure-gradient microphone, **A** and **B**, in a spherical sound field, the total pressure difference $\Delta p$ between them arises from **two separate physical effects**:

#### <span style="color:rgb(2, 141, 192)">1. Phase-related Δp (frequency dependent)</span>

Just as in a plane sound field, A and B detect the wave with a **phase difference**.  
This phase difference creates a $\Delta p$ that **increases with frequency**, because higher frequencies have shorter wavelengths.

This effect dominates at **high frequencies**.

#### <span style="color:rgb(2, 141, 192)">2. Distance-related Δp (frequency independent)</span>

In a spherical field, pressure also decreases with distance.  If A is closer to the source than B, it measures a **higher pressure**, regardless of the frequency.  
This creates an additional Δp caused purely by the **1/r² attenuation**, not by phase.

- This effect is **significant at short distances** (steep slope of the 1/r² curve).
- It becomes **negligible at large distances**, where the curve flattens.
Thus:
$$\Delta p_{\text{total}} = \Delta p_{\text{phase}}(f) + \Delta p_{\text{distance}}$$

### <span style="color:rgb(161, 40, 226)">When Each Component Dominates</span>
![[Pasted image 20251211101930.png]]
#### <span style="color:rgb(2, 141, 192)">At high frequencies</span>
- Phase-related Δp is large.
- Distance-related Δp becomes irrelevant.
- So the microphone output is almost **independent of distance** from the source.
#### <span style="color:rgb(2, 141, 192)">At low frequencies</span>
- Phase-related Δp is small (low-frequency waves have large wavelengths → small phase differences).
- Therefore, the distance-related Δp becomes important **only when the microphone is close to the source**.
    

If the microphone is far away:
- Phase-related Δp is small
- Distance-related Δp is small
- → Total Δp is small
    
If the microphone is close:
- Phase-related Δp is still small
- **But** distance-related Δp becomes large
- → Total Δp increases significantly
    
### <span style="color:rgb(161, 40, 226)">Practical Consequence: Low-Frequency Boost (“Proximity Effect”)</span>

This explains the common audio phenomenon known as the **proximity effect**:
#### <span style="color:rgb(2, 141, 192)">When you bring a directional microphone close to your mouth</span>:

- High frequencies stay almost unchanged  
    (phase-related Δp dominates and is distance-independent)
- **Low frequencies increase sharply**  
    (because distance-related Δp becomes large at small r)
    
This produces the well-known **low-frequency boost** when a singer or speaker moves the microphone very close to their mouth.

## <span style="color:rgb(239, 179, 1)">Low-Frequency Boost Expressed by an Equation</span>

The phenomenon we previously described intuitively—the **low-frequency boost** (or proximity effect)—can also be expressed mathematically.

The ratio between:
- $e_8$​: the output voltage of a **pressure-gradient (figure-8) microphone**, and
- $e_0$​: the output voltage of an **omnidirectional microphone** with the same transmission factor at 0°
is given by:
$$\frac{e_8}{e_0} = \frac{1}{\cos \alpha}$$

where the angle $\alpha$ depends on the **wavelength** $\lambda$, the **distance** r from the sound source, and therefore on the **frequency**.

In practice:
$$\tan \alpha = \frac{\lambda}{2\pi r} = \frac{54.14}{f \cdot r}$$
This leads to the final expression:
$$\frac{e_8}{e_0} = \sqrt{1+\left( \frac{54.14}{f \cdot r} \right)^2 }$$

- **$e_8$** – output of a figure-8 (pressure gradient) microphone
- **$e_0$​** – output of an omnidirectional microphone
- **$r$** – distance between the microphone and the sound source (meters)
- **$\lambda$** – wavelength of the sound (meters)
- $f$ – frequency of the sound (Hz)

### <span style="color:rgb(161, 40, 226)">Interpreting the Equation</span>

####  <span style="color:rgb(2, 141, 192)">High frequencies OR large distances → No boost</span>

If $f$ is large, or if $r$ is large:
$$\frac{54.14}{f \cdot r} \ll 1$$
so the term inside the square root is:
$$\approx \sqrt{1 + 0} = 1$$
This means:
$$e_8 \approx e_0$$
**→ No proximity effect.**  
The figure-8 microphone behaves almost like the omnidirectional one.

#### <span style="color:rgb(2, 141, 192)">Low frequencies AND short distances → Large boost</span>

If **frequency is low** AND **distance is short**, then:
$$\frac{54.14}{f \cdot r} \gg 1$$

and the ratio becomes:
$$\frac{e_8}{e_0} \gg 1$$

This means:

- The figure-8 microphone output becomes **much larger** than that of the omnidirectional microphone.
- The microphone **overemphasizes low-frequency components** when placed close to the source.
    
This is exactly the **low-frequency boost** (or **proximity effect**) that vocalists deliberately use to get a warmer, bass-rich sound when singing very close to the microphone.

### <span style="color:rgb(161, 40, 226)">Summary</span>

- The ratio $e_8 / e_0$​ describes how much stronger the figure-8 microphone output is relative to an omnidirectional microphone at the same location.
- The ratio increases only when **two conditions** are satisfied:  
    **(1) low frequency** and **(2) small distance from the source**.
- At high frequencies or long distances, the boost is negligible because the distance-related pressure difference becomes extremely small.
- At low frequencies and short distances, the boost becomes significant because the distance-related pressure difference dominates over the (small) phase difference.

# <span style="color:rgb(223, 109, 109)">Implementation of Omnidirectional, Figure-8, and Cardioid Microphones</span>

## <span style="color:rgb(239, 179, 1)">Omnidirectional vs. Figure-8 Microphones (Summary)</span>

### <span style="color:rgb(161, 40, 226)">Omnidirectional Microphones</span>

- Only the **front face** of the diaphragm is exposed to sound.
- They measure **absolute pressure at a single point**, not a pressure difference.
- Sensitivity is **independent of angle**.
    
### <span style="color:rgb(161, 40, 226)">Figure-8 (Pressure-Gradient) Microphones</span>

- Both the **front** and the **rear** faces of the diaphragm are exposed.
- They measure the **pressure difference** between two points (A and B) located at the diaphragm’s two sides.
- The spacing between A and B is approximately the **thickness of the diaphragm**
- The response is **directional**, with a **figure-8 pattern**.
    
## <span style="color:rgb(239, 179, 1)">How to Implement a Cardioid Microphone</span>
![[Pasted image 20251211104423.png|200]]
A **cardioid characteristic** is obtained by combining:

- an _omnidirectional_ response, and
- a _figure-8_ response.

Since the cardioid pattern is algebraically the **sum** of these two characteristics, we can implement it using three possible approaches.

### <span style="color:rgb(161, 40, 226)">Method 1: Summing Two Separate Capsules (Omni + Figure-8)</span>

- Use **two physical microphone capsules**:
    - one omnidirectional capsule
    - one figure-8 capsule
        
- Electrically sum their outputs:
    - **Analog summation** (e.g., using an amplifier that adds two voltages)
    - or **digital summation** after A/D conversion.
    
This reproduces the equation:

$$\text{Cardioid} = \text{Omni} + \text{Figure-8}$$
### <span style="color:rgb(161, 40, 226)">Method 2: A Single Diaphragm Partially Exposed to Sound</span>

- The diaphragm is designed so that:
    - **one part** is exposed _only_ to the front (omni-like behavior),
    - the **other part** is exposed to the front and rear (figure-8-like behavior).
        
- The resulting vibration is an **intermediate response** between omni and figure-8.
- The output becomes similar to a cardioid pattern.

This is a **mechanical way** to mix the two behaviors within a single physical structure.

### <span style="color:rgb(161, 40, 226)">Method 3: Using an Acoustic Delay Element Behind the Diaphragm</span>

This is a **more advanced and common practical implementation**.
#### <span style="color:rgb(2, 141, 192)">Concept</span>

A cardioid response is produced by creating controlled **phase differences** between the sound arriving at the front and rear sides of the diaphragm.

To do this, the microphone includes:
- a **rear acoustic cavity**, and
- an **acoustic delay element** (a labyrinth or resistive acoustic path).
    
This delay determines how sound reaches the rear face of the diaphragm.
#### <span style="color:rgb(2, 141, 192)">How It Works</span>

Assume sound arrives at three angles
##### <span style="color:rgb(71, 215, 140)">1. Sound arriving at 0° (front incidence)</span>

![[Pasted image 20251211104306.png|300]]
- The front face is reached at time **t₀**.
- The rear face is reached after:
    - traveling the external distance **s**, plus
    - traveling through the acoustic delay path of length **L**.
- Total delay to the rear:
    $T_s + T_L$
- **Large phase difference → large pressure difference → maximum sensitivity.**
    
##### <span style="color:rgb(71, 215, 140)">2. Sound arriving at 90° (side incidence)</span>
![[Pasted image 20251211104326.png|200]]
- The front face is reached at time **t₀**.
- The rear face is reached only through the delay element.
- Delay to rear:
    $T_L$
- This delay is **smaller** than at 0°, so the pressure difference is smaller.
- **Sensitivity is reduced**, matching the cardioid shape.

##### <span style="color:rgb(71, 215, 140)">3. Sound arriving at 180° (rear incidence)</span>
![[Pasted image 20251211104348.png|200]]
- The rear face is reached first (after time $T_L$​).
- The front face is reached after time $T_S$​.
- If the microphone is designed with:
    $T_S = T_L$​
- Then the sound reaches **front and rear simultaneously**.
- Their pressures cancel out.
- Result:
    $\text{Sensitivity} = 0 \quad \text{at } 180^\circ$
- This gives the cardioid microphone its **null** at the rear.

#### <span style="color:rgb(2, 141, 192)">Summary of the Acoustic-Delay Method</span>

- The **maximum phase difference** occurs at 0°.
- The **half phase difference** occurs at 90°.
- The **phase difference becomes zero** at 180° (by design).
    
This engineered pattern produces the **classic cardioid polar shape**.


##### <span style="color:rgb(2, 141, 192)">Explanation of the Transition Frequency in Cardioid Microphones</span>
![[Pasted image 20251211104822.png]]
In a cardioid (pressure-gradient + pressure) microphone, the sound wave reaches the diaphragm from two sides:

- **Front side**
- **Rear side**, after going through an acoustic path and a delay network
    
Because the rear sound must travel through ducts or openings, the wave that reaches the **back** of the diaphragm is **delayed** with respect to the wave that reaches the **front**.  Let’s call the total delay:
$$t_\text{delay} = t_S + t_L$$
where:
- $t_S$ = delay due to the sound path
- $t_L$​ = delay due to the internal low-pass/acoustic network

The microphone’s output is proportional to the _difference_ between:

- the pressure arriving at the front    
- the pressure arriving at the back (delayed)
    
So the output signal is:
$$\text{Output}(t) = P_\text{front}(t) - P_\text{rear}(t - t_\text{delay})$$
![[Pasted image 20251211104822.png]]
This difference depends on how “out of phase” the two waves are at a given frequency.

At low frequencies:
- The period $T$ of the wave is very long.
- The delay $t_S + t_L$​ is very small compared to the period.

So the front and back pressures are almost the same → very small difference.  
Thus, **low frequencies produce small output**.

When frequency increases:
- The period becomes shorter.
- The fixed delay $t_S + t_L$​ corresponds to a larger phase shift.
    
This makes the two waveforms more different, so the output increases.

The _maximum possible_ difference occurs when the wave at the back is exactly **half a period** behind the wave at the front.

Why?

Because:
- When the front side pressure is at its _maximum_,  
    the rear side pressure is at its _minimum_.
- Subtracting them gives the **largest possible output**.
    

Half a period means:
$$\frac{T}{2} = t_S + t_L2$$
Since the frequency is:
$$f = \frac{1}{T}​$$
Replacing:
$$\frac{1}{2f} = t_S + t_L$$
Solving for $f$:
$$f_\text{transition} = \frac{1}{2 (t_S + t_L)}$$
This is the **transition frequency**: the frequency at which the microphone gives its _maximum_ output.

## <span style="color:rgb(239, 179, 1)">How Microphone Size Affects Sound Propagation and Causes Distortion</span>

When we discussed the cardioid microphone, we saw that the _geometry_ of the microphone can influence how the sound reaches the front and the rear of the diaphragm.  This leads to an important general principle:

### <span style="color:rgb(161, 40, 226)">A microphone affects sound propagation only when its size is comparable to the wavelength</span>

Sound waves have different wavelengths depending on their frequency:
- **Low-frequency sounds** → very long wavelengths (meters)
- **High-frequency sounds** → short wavelengths (centimeters or millimeters)
    
A microphone begins to **disturb** or **scatter** the sound wave when its size is on the same order of magnitude as the sound wavelength.

So:

- If the microphone is **much smaller** than the wavelength → the sound propagates around it almost undisturbed.
- If the microphone’s size becomes **comparable to λ**, or even **larger** → it begins to block, reflect, bend, or shadow the wave, which introduces **distortion** in its directional characteristics.
    

### <span style="color:rgb(161, 40, 226)">Wavelengths in the audible range (practical example)</span>

Humans hear roughly from **20 Hz to 20 kHz**, although adults usually hear less than 20 kHz.  Let’s look at some example wavelengths:

|Frequency|Approx. Wavelength|Comment|
|---|---|---|
|32 Hz|~10 m|Very long — almost impossible for a microphone to perturb|
|320 Hz|~1 m|Still far larger than any microphone|
|3 kHz|~10 cm|Now wavelengths are small enough that microphone size matters|
|16 kHz|~2.1 cm|Very small — many microphones are not negligible in size|

**Rule of thumb:**  
If the microphone dimensions in all directions are **< 6 mm**, then it will not significantly disturb sound in the audible range.  
If it is **> 6 mm**, then at high frequencies the microphone becomes “big” relative to the wavelength → distortion begins.
### <span style="color:rgb(161, 40, 226)">What kind of distortion appears?</span>

![[Pasted image 20251211105730.png|400]]
To illustrate this, imagine an **omnidirectional microphone**, which should ideally respond the same in every direction (a perfect circle in a polar plot).

If the microphone is physically large:

- When sound arrives from the front (0°), it hits the diaphragm directly → _no distortion_.
- But when sound arrives from behind (180°) or from the sides, it must **interact with the microphone body** before reaching the diaphragm.
    
This interaction—reflection, diffraction, shadowing—creates **frequency-dependent distortion**.


At **low frequencies** (long wavelengths):
- The microphone is “tiny” compared to λ
- The sound flows around it smoothly
- The directional pattern stays almost perfectly circular
    
At **higher frequencies** (short wavelengths):

- The microphone becomes “big” compared to λ
- Sound cannot bend easily around it
- The body of the microphone blocks or reflects part of the wave
- The polar pattern becomes increasingly distorted
    
In the example you referenced (from a real microphone datasheet):
- Up to ~1 kHz → the polar pattern is still a perfect circle (no distortion).
- As frequency increases to 8–16 kHz → wavelength becomes comparable to the microphone size.
- The worst distortion occurs at **16 kHz**, where the wavelength is only about **2 cm**.
- The polar pattern shows strong irregularities at all angles except 0°, because only the front receives the sound directly.
    
###  <span style="color:rgb(161, 40, 226)">Summary</span>

- Microphone size matters when it becomes comparable to the wavelength of the sound.
- Low frequencies (long λ) are not affected by microphone size.
- High frequencies (short λ) are affected, causing directional distortion.
- Distortion is strongest at angles where the microphone body obstructs or reflects the incoming wave.
- This is why miniature microphones (≤ 6 mm) are preferred for accurate high-frequency response.

# <span style="color:rgb(223, 109, 109)">How Microphones Are Implemented and How Their Frequency Response Is Determined<br></span>
To understand how real microphones behave, we need to look at two aspects:
1. **What physical quantity they measure** (pressure or pressure gradient)
2. **What type of sensing element (capsule) they use**
    

These two factors, together with the **mechanics of the diaphragm**, determine the _overall frequency response_ of the microphone.

## <span style="color:rgb(239, 179, 1)">Types of Sensing Elements (Microphone Capsules)</span>

Microphones can be built using different physical sensing principles:

### <span style="color:rgb(161, 40, 226)">A. Condenser (capacitive) microphones</span>
- One plate of the capacitor is fixed.
- The other plate is the membrane (the diaphragm).
- Sound pressure moves the diaphragm and changes the capacitance.
- This change is converted into a voltage.
### <span style="color:rgb(161, 40, 226)">B. MEMS microphones</span>
- These are essentially condenser microphones implemented at micrometer scale using MEMS processes.
- Same working principle as A, just miniaturized.
### <span style="color:rgb(161, 40, 226)">C. Dynamic microphones</span>
- Work by **electromagnetic induction** (Faraday’s law).
- The diaphragm is attached to a coil that moves in a magnetic field.
- Motion of the coil induces a voltage proportional to the _velocity_ of the diaphragm.
### <span style="color:rgb(161, 40, 226)">D. Piezoelectric microphones</span>
- Sound pressure deforms a piezoelectric material.
- The material produces charge proportional to the deformation.
- Similar to pressure sensors in general.
### <span style="color:rgb(161, 40, 226)">E. Carbon microphones</span>
- Resistive microphones based on variable resistance of carbon granules.
- Poor linearity, noise, and low performance → rarely used.

## <span style="color:rgb(239, 179, 1)">What do the capsules actually measure?</span>

This distinction is fundamental.
### <span style="color:rgb(161, 40, 226)">Condenser capsule</span>
Output ∝ **displacement** of diaphragm
$$\xi \propto \frac{p}{\omega Z}$$
![[Pasted image 20251211111303.png]]
- At higher frequencies (larger ω), displacement decreases.
- So the output **decreases with frequency**.

### <span style="color:rgb(161, 40, 226)">Dynamic capsule</span>
![[Pasted image 20251211111334.png]]
Output ∝ **velocity** of diaphragm
$$v \propto \frac{p}{Z}$$
- No dependence on frequency.
- So the output is **flat with frequency**.

This difference will matter later when we combine with pressure vs pressure-gradient microphones.

### <span style="color:rgb(161, 40, 226)">Pressure vs Pressure-Gradient Microphones</span>

#### <span style="color:rgb(2, 141, 192)">Pressure microphones</span>
![[Pasted image 20251211111431.png]]
- Output depends only on absolute pressure at one point.
- Their **transmission factor is independent of frequency** → flat response.
#### <span style="color:rgb(2, 141, 192)">Pressure-gradient microphones</span>
![[Pasted image 20251211111437.png]]
- Output depends on **difference** between pressures at two points.
- Output ∝ frequency (at least up to the transition frequency).
- So the response **increases with frequency**.

### <span style="color:rgb(161, 40, 226)">Combining the capsule physics with the microphone type</span>

So far we know:

|Microphone type|Frequency response|
|---|---|
|Pressure|Flat|
|Pressure-gradient|Increasing (up to transition)|
|Condenser capsule|Decreasing|
|Dynamic capsule|Flat|

If we combine these _as they are_, some combinations naturally give a good flat response, others do not.

For example:
- **Pressure + dynamic capsule → flat × flat = flat** (good)
- **Pressure-gradient + condenser → increasing × decreasing = flat** (also good)
    

But the other combinations are not naturally flat.

This is why we need a third “degree of freedom”: **microphone mechanics**.
### <span style="color:rgb(161, 40, 226)">The role of microphone mechanics</span>

The diaphragm is a mechanical system with a **resonance frequency $f_R$​**.
- **Below resonance** → mechanical sensitivity **increases** with frequency
- **At resonance** → peak in the response
- **Above resonance** → sensitivity **decreases**
    
By choosing _where_ the resonance is placed relative to the operating band, we obtain three mechanical tuning strategies:

#### <span style="color:rgb(2, 141, 192)">A. High-frequency-tuned mechanics</span>
![[Pasted image 20251211111655.png]]
- Resonance at high frequencies
- In the audible band, the response is **increasing** with frequency
    
#### <span style="color:rgb(2, 141, 192)">B. Low-frequency-tuned mechanics</span>
![[Pasted image 20251211111721.png]]
- Resonance at low frequencies
- In the audible band, the response is **decreasing** with frequency
#### <span style="color:rgb(2, 141, 192)">C. Mid-band-tuned mechanics</span>
![[Pasted image 20251211111736.png]]
- Resonance inside or near the useful band
- Damped so the curve is as flat as possible

So mechanical tuning provides a slope (increasing or decreasing) that can be used to compensate the capsule response and the microphone topology (pressure or pressure-gradient).

### <span style="color:rgb(161, 40, 226)">Putting everything together: all combinations</span>

You now have **three factors**:
1. Microphone type
    - Pressure → flat
    - Pressure-gradient → increasing
2. Capsule type
    - Condenser → decreasing
    - Dynamic → flat
3. Mechanical tuning
    - High-frequency-tuned → increasing
    - Low-frequency-tuned → decreasing
    - Mid-band-tuned → flat
        

To obtain an overall **flat frequency response**, we combine them appropriately. Here is the summary table in words:
#### <span style="color:rgb(2, 141, 192)">A. Pressure microphones</span>
![[Pasted image 20251211111850.png]]
##### 1. With dynamic capsule (flat × flat)
→ Use mid-band tuned mechanics (to keep it flat)
##### 2. With condenser capsule (flat × decreasing)
→ Use **high-frequency tuned** mechanics (increasing) to compensate
#### <span style="color:rgb(2, 141, 192)">B. Pressure-gradient microphones</span>
![[Pasted image 20251211112042.png]]
##### 1. With dynamic capsule (increasing × flat)
→ Use **low-frequency tuned** mechanics (decreasing) to compensate
##### 2. With condenser capsule (increasing × decreasing)
→ The two effects already cancel  
→ Use **mid-band tuned** mechanics to maintain flatness

The table essentially shows that with proper mechanical design, **any capsule type** can be used to build:

- pressure microphones
- pressure-gradient microphones
    

and still achieve a flat frequency response — as long as the mechanical tuning is chosen carefully.

# <span style="color:rgb(223, 109, 109)"><b>Dynamic Microphones: Two Implementations</b></span>

Dynamic microphones work by **electromagnetic induction**:  sound moves a conductor in a magnetic field → the magnetic flux changes → a voltage is induced (Faraday–Neumann–Lenz law).

There are two main ways to physically implement this:
1. **Moving-coil microphone**
2. **Ribbon microphone**
    
Both are velocity-sensitive devices (output ∝ vibration velocity), but the mechanical implementation is quite different.

## <span style="color:rgb(239, 179, 1)">Moving-Coil Microphone</span>

### <span style="color:rgb(161, 40, 226)">Structure</span>
![[Pasted image 20251211113134.png|300]]
A moving-coil microphone contains:
- **Diaphragm** (flexible membrane, usually light plastic)
- **Voice coil** (thin wire wound into a coil, attached rigidly to the diaphragm)
- **Permanent magnet** with a precisely shaped magnetic gap
- **Pole pieces** that direct the magnetic field into the gap

`Sound → moves diaphragm → moves coil → cuts magnetic field → induces voltage`

The **magnet is fixed**; the **coil moves** together with the diaphragm.

### <span style="color:rgb(161, 40, 226)">How induction occurs</span>

The magnetic field in the gap has a strong, focused geometry.  
As the coil moves back and forth:

- the **amount of magnetic flux** passing through the loops changes
- this produces an induced voltage
    
$$V_{\text{out}} \propto \frac{d\Phi}{dt} \propto \text{velocity of the diaphragm}$$
This is why dynamic microphones are **velocity microphones**.

- If only **front side** of the diaphragm is exposed → **pressure microphone**
- If **both sides** are exposed → **pressure-gradient microphone**
    
The capsule type does not determine the polar pattern — the **acoustic design** does.

## <span style="color:rgb(239, 179, 1)">Mechanical tuning and resonance</span>

Moving-coil microphones typically have a **relatively heavy diaphragm–coil assembly**, which makes the diaphragm’s **resonance pronounced** and **hard to damp**.

But for a good microphone you want the frequency response to be as flat as possible.  Since damping the main resonance is difficult, manufacturers use a trick:

###  <span style="color:rgb(161, 40, 226)">Multiple resonant cavities</span>
![[Pasted image 20251211113339.png|300]]
The acoustic structure (holes, chambers, ducts) is designed so that:

- each cavity has its own resonance at a different frequency
- the individual resonances overlap
- the peaks and dips partially cancel each other
    
Result → the **overall frequency response becomes much flatter**.

This is the characteristic design strategy behind moving-coil microphones.


## <span style="color:rgb(239, 179, 1)">Ribbon Microphone</span>

### <span style="color:rgb(161, 40, 226)">Structure</span>

In a ribbon microphone:
![[Pasted image 20251211113434.png|300]]
- The “diaphragm” is a **very thin aluminium ribbon** (a few micrometers thick).
- It is suspended between the poles of a **strong permanent magnet**.
    
- The ribbon itself acts as both:
    - the **moving conductor**, and
    - the **coil** of the transducer  
        (the electrical terminals are connected at the ends of the ribbon).
        
The magnetic field is uniform and runs perpendicular to the ribbon.

### <span style="color:rgb(161, 40, 226)">How induction occurs</span>

As sound arrives, the ribbon vibrates back and forth:
- its motion changes the **area** of the loop formed by the ribbon
- → this changes the magnetic flux
    
$$V_{\text{out}} \propto \frac{d\Phi}{dt} \propto \text{velocity of the ribbon}$$
Again, the microphone is a **velocity transducer**.

### <span style="color:rgb(161, 40, 226)">Why the raw output is extremely small</span>

Unlike the moving-coil microphone, which may have **dozens of coil turns**, the ribbon microphone has **basically one turn**.

→ The induced voltage is **very small** (millivolts or less).  
→ This would normally require a very low-noise amplifier.

But conventional transistor amplifiers introduce noise that could easily be **larger** than the signal itself.

Solution: **Step-up transformer**
![[Pasted image 20251211113531.png|400]]
Ribbon microphones almost always include a **step-up transformer**:

- Typical ratio ≈ **1:37**
- Input voltage = E from the ribbon
- Output voltage = $E \cdot 37$
    

The transformer:
- amplifies **without adding noise**
- matches the ribbon’s very low impedance to standard microphone preamps
- preserves a good signal-to-noise ratio
    
Without this transformer, ribbon microphones would be nearly unusable.



## <span style="color:rgb(239, 179, 1)">Condenser Microphones</span>

We are analyzing another important family of microphones, which are the condenser microphones. 
![[Pasted image 20251211114858.png|300]]
In a condenser microphone, there is a fixed black plate and a second plate, which is the diaphragm itself. When the diaphragm vibrates, it changes the distance between the two plates of the capacitor, causing a variation in the capacitance. In this type of microphone, the output depends on particle displacement, which results in a characteristic that decreases as frequency increases.
$$\xi = \frac{v}{\omega} = \frac{p}{\omega \cdot z}$$

### <span style="color:rgb(161, 40, 226)">DC bias</span>
![[Pasted image 20251211115012.png|400]]
Typically, capacitive microphones require a DC bias, a voltage that we provide to the microphone, which here is called ($E_0$). To understand the required voltage, we can examine the relationship between the output voltage, the DC bias, and the expected variations in capacitance.

First, the charge $(Q)$ on the capacitor can be considered almost constant if the operating frequencies are higher than the pole frequency of the circuit. This pole frequency is ($1 / (2 \pi R C_0)$), where ($C_0$) is the nominal capacitance and ($R$) is the resistance used to read out the capacitance variations. Typical values for ($C_0$) range from 20 to 100 picofarads. To ensure the charge remains approximately constant and the minimum operating frequency is around 20 Hz, a high resistance ($R$) is required.

Under these conditions, at steady state (without sound impinging on the capacitor), the charge ($Q_0$) equals the product of the capacitance and the voltage across it, ($C_0 \cdot E_0$). 
$$Q_0=C_0\cdot E_0$$
When pressure is applied to the diaphragm, the capacitance changes to 
$$C=C_0+c(t)$$

$c(t)$ varying over time due to diaphragm vibrations. The charge at this moment is $$Q = C \cdot (E_0 - V_{out})$$ where ($V_{out}$) is the voltage across the readout resistor.

If we assume the charge remains nearly constant
$$Q \approx Q_0$$we can solve the equation
$$C_0 \cdot E_0 = (C_0 + c(t)) \cdot (E_0 - V_{out})$$to find the relationship between the output voltage and the capacitance variation. The output voltage is therefore proportional to the DC bias and the ratio of capacitance variation to the nominal capacitance.

The typical variation in capacitance is very small, on the order of 1 picofarad or less. Consequently, to obtain a readable output voltage with a front-end circuit, the required DC bias would need to be very high, around 40 to 200 volts. This high voltage requirement poses a practical problem because standard sensor boards, powered by USB at 5 volts, cannot supply such high voltages.

### <span style="color:rgb(161, 40, 226)">Electret Microphone</span>

The solution is the electret microphone, which is the type used in common sensor boards. In an electret microphone, the fixed plate is made of a material like Teflon, which can accept and maintain a permanent electrical charge. The fixed plate is electron-bombarded to store the charge, so no external DC bias is needed. The diaphragm can be made from standard materials because the opposite charge naturally appears on the moving plate.
![[Pasted image 20251211115549.png|400]]

Electret microphones have a simpler readout circuit because no external voltage supply is required. Many electret microphones include a simple preamplifier, often just a transistor in a common-source configuration, with a resistor ($R_1$) at the output. 
![[Pasted image 20251211115636.png|400]]
Additional amplifiers can be added to further amplify the signal. A coupling capacitor is important in the circuit because the fixed charge on the plate creates a fixed voltage, which is present across the capacitance even though it is not supplied by the readout circuit.

## <span style="color:rgb(239, 179, 1)"></span><span style="color:rgb(239, 179, 1)">Phantom Power</span>

In most cases, you do not need to provide an external supply to a microphone. For example, an electret microphone does not require an external supply because the fixed plate is electron-bombarded and already maintains a permanent charge. Similarly, a dynamic microphone does not need external power because it already has a permanent magnet inside, and the voltage is generated by the motion of the coil in the magnetic field. In these cases, no supply is required.

However, standard capacitive microphones, unlike electret microphones, do require a high-voltage supply. To make audio equipment like mixers compatible with different types of microphones, it is convenient to provide a way to supply power only when needed while keeping the cabling simple.



| ![[Pasted image 20251211120123.png]] | ![[Pasted image 20251211120213.png]] |
| ------------------------------------ | ------------------------------------ |

Typically, XLR connectors are used, which consist of two signal wires plus a shielding. The two wires are balanced, meaning they have identical input and output impedance, and they serve a dual purpose. They carry the differential output signal from the microphone and, at the same time, can provide power if needed. The shield acts as the ground reference for the microphone, while the two balanced wires carry the differential signal. Phantom power works by providing an intermediate voltage, exactly at the average of the V+ and V− differential output, which is used to supply the microphone when necessary.



![[Pasted image 20251211120404.png]]
Here is a more detailed schematic of how phantom power and microphone connections work. On the microphone side, we have the microphone itself, which is always followed by a preamplifier. At the output of the preamplifier, there is a coil connected to a transformer, which generates the differential voltage for the output. The two terminals, typically colored blue and red, carry this differential voltage.

The secondary side of the transformer is divided into inductances, and the intermediate point between them is used to provide the supply voltage to the preamplifier. The signal is then transmitted through a balanced cable to the mixer. The microphone and the mixer are connected using XLR connectors.

At the mixer input, the differential signal is received and decoupled through a capacitor before being sent to the amplifier. This decoupling is important because you do not want to pass the high voltage that may be present at the intermediate point directly to the amplification stage. The intermediate voltage can be needed by the preamplifier or, in the case of a standard capacitive microphone, by the microphone itself.

This configuration allows the use of just two cables to carry both the differential output signal and the phantom power, which can supply the microphone or its internal preamplifier as needed.

*This is all for today and the course, good luck in your exam :) Bye!*![[il_570xN.4108208755_addp.avif|300]]