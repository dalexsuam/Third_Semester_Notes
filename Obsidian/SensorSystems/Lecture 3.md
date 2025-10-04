
Date: 02/10/2025

---

# <span style="color:rgb(223, 109, 109)">Image Sensors</span> 

There are two types of technologies:
* Charge Coupled Device (CCD)
* CMOS active pixel image sensor

# <span style="color:rgb(223, 109, 109)">Charge Coupled Device (CCD)</span> 
![[Pasted image 20251002223920.png]]
The figure below shows the cross-section of a single pixel in a CCD (Charge-Coupled Device) sensor.

| ![[Pasted image 20251002224012.png]] | You see it is a p-n junction with its corresponding depletion region. |
| ------------------------------------ | --------------------------------------------------------------------- |
The main difference from a normal photodiode is that, in a CCD, there is an **insulating layer** between the n-region and the electrodes. Each pixel usually has **three electrodes** that help control the charges inside the pixel.
![[Pasted image 20251002224742.png]]

When light (a photon) enters the depletion region:

- It creates an **electron–hole pair**.
- Because the p–n junction is **reverse biased**, the electron and hole move in opposite directions.
- The **electron** is trapped under the electrode (in a “potential well”).
- The **hole** goes to the p-side and disappears into the substrate.

As more photons are absorbed, more electrons get collected under the electrode. This stored charge is the **signal** of the pixel. Later, the charges are shifted from one pixel to the next until they reach the output of the CCD, where the image is read.


| ![[Pasted image 20251002224935.png]] | ![[Pasted image 20251002230039.png]] |
| ------------------------------------ | ------------------------------------ |

Just like in a normal photodiode, when the junction is in **reverse bias**, the light generates **electron–hole pairs**:

- The **electrons** move toward the n-region
- The **holes** move toward the p-region.

However, in a CCD pixel there is an important difference: the **insulating layer**. Because of this insulator, the electrons cannot move freely to the contact. Instead, they are stopped and trapped at the edge of the n-region, just below the electrodes.

From an electrical point of view, we can model a CCD pixel as a **photodiode in series with a capacitor**:

- The **photodiode** represents the light-sensitive p–n junction.
- The **capacitor** represents the insulating layer that prevents the electrons from going directly to the contact.

When light generates a **photocurrent**, this current is **integrated by the capacitor**, meaning that the electrons accumulate over time under the electrode, forming a potential well.

If we bias only the **central electrode** (out of the three), then all the charges produced will be collected **under this central electrode**, ready to be transferred in the readout phase.

## <span style="color:rgb(239, 179, 1)">CCDs Technologies</span>

CCDs are fabricated using dedicated **silicon imaging processes**. The starting point is a **p-doped silicon wafer**, on top of which an **n-type dopant layer** is added. Above this, a layer of **silicon dioxide** is deposited to serve as the insulator, and finally **polysilicon electrodes** are patterned to apply the reverse bias and control charge movement.

The typical thickness of a silicon wafer substrate is around **625 µm**. Depending on how light enters the sensor, two main CCD technologies are used: **front-side illuminated (FSI)** and **back-side illuminated (BSI)**.

| Front-side illuminated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Back-side Iluminated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![[Pasted image 20251002231539.png]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | ![[Pasted image 20251002231603.png]]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| CCDs are fabricated using dedicated silicon imaging processes. The starting point is a p-doped silicon wafer, on top of which an n-type dopant layer is added. Above this, a layer of silicon dioxide is deposited to serve as the insulator, and finally polysilicon electrodes are patterned to apply the reverse bias and control charge movement.<br><br>The typical thickness of a silicon wafer substrate is around 625 µm. Depending on how light enters the sensor, two main CCD technologies are used: front-side illuminated (FSI) and back-side illuminated (BSI). | - Here, the **wafer is flipped**, and photons enter from the **bottom side** of the silicon.<br>    <br>- To prevent photons from being absorbed before reaching the depletion region, the substrate must be **thinned from ~625 µm down to ~15 µm**.<br>    <br>- This thinning process is technologically complex and relatively expensive.<br>    <br><br>Despite the extra cost, BSI offers significant advantages:<br><br>1. **Better contact integration** — since the top surface is now free, it can be used for **metalization** or even bonded to another wafer for **readout or signal processing**.<br>    <br>2. **Improved sensitivity** — the light-facing surface (the thinned bottom side) is **flat and uniform**, which makes **anti-reflective coatings** much more effective.<br>    <br>3. As a result, **BSI CCDs** achieve higher sensitivity and are preferred in **high-performance imaging applications**. |
![[Pasted image 20251002232838.png]]


In the **top view** of a CCD sensor, each red square represents a single pixel. On top of each pixel, we can see the **three electrodes** that play a key role in controlling charge distribution:

- During light integration, **only one electrode is biased (active)**, while the other two remain unbiased.
- This ensures that the charges generated by incoming light stay confined within the pixel and do not move into neighboring pixels along the same column.
    

For the separation between pixels in the **same row**, **channel stops** are used. These are highly **p-doped regions** that form reverse-biased p–n junctions between adjacent pixels. These junctions act as barriers, preventing the charges from spreading laterally to neighboring pixels.

![[Pasted image 20251002232900.png]]
In the **side view**, we can observe:

- The **p–n junction**, where light is absorbed and electron–hole pairs are generated.
- The **channel stops** (in orange), which confine the charges horizontally. 
- The **insulating layer** and the **electrodes** on top, which create and control the potential wells where electrons are stored.


# <span style="color:rgb(239, 179, 1)">CCD Readout</span>

![[Pasted image 20251003104049.png]]

In a CCD camera, each pixel stores charge generated by incident light. To **read out the image**, the charges are transferred across the pixel array until they reach a single **output amplifier**, typically located in one corner of the sensor.

The process works as follows:

1. Charges are shifted **vertically** from one pixel to the next, row by row.
2. When they reach the **last auxiliary row**, the charges are then shifted **horizontally** into the **readout register**.
3. Finally, the register passes the charges sequentially to the **output amplifier**, which converts them into a measurable voltage.
    

This mechanism is often compared to a **“bucket brigade”**.


![[Pasted image 20251003111655.png]]
Think of **pixels as buckets** and **light as raindrops**. During the **integration phase** (image acquisition), each pixel “bucket” fills up with water (electrons) from the light. During **readout**, the buckets are passed along in a controlled sequence:

* In the analogy, buckets move **horizontally** from one person to the next.
* In the CCD sensor, the charges are first shifted **vertically**, row by row.

Once a full column reaches the bottom (in the real sensor) , its contents are shifted **horizontally** into the readout register, and finally emptied into the **measuring container** (the operational amplifier).

**Now, the role of the electrodes**

During image acquisition:

- **One electrode is biased (active)**, creating a **potential well** that collects and stores the electrons.
- The **two adjacent electrodes remain unbiased**, creating **potential barriers** that prevent electrons from leaking into neighboring pixels.

During charge transfer:

* The biasing of the electrodes is changed step by step, so the potential well “moves,” allowing the electrons to flow from one pixel to the next in a controlled manner.
- This process ensures that charges are transferred with minimal loss or mixing, preserving the integrity of the image.


---
The transfer of charge in a CCD is controlled by the **electrodes (ϕ1, ϕ2, ϕ3)**. By biasing them in sequence, potential wells are created and removed, which allows the electrons to move step by step from one electrode to the next.

### <span style="font-weight:bold; color:rgb(161, 40, 226)">Readout - Step 1:</span> 
![[Pasted image 20251003212918.png]]
Only **ϕ3** is biased (positive). Electrons are collected and stored below this electrode.**ϕ1 and ϕ2** are at the same potential as the substrate → they act as barriers and do not collect charge.

### <span style="color:rgb(161, 40, 226)">Readout - Step 2</span>:

![[Pasted image 20251003212946.png]]
Now **ϕ2** is also biased.- The charge is shared between **ϕ2 and ϕ3**.  **ϕ1** remains unbiased to prevent mixing with the neighboring pixel on the left.

### <span style="color:rgb(161, 40, 226)">Readout - Step 3</span>:
![[Pasted image 20251003213034.png]]
**ϕ3** is switched off, **ϕ2** stays biased. The charge is now fully transferred under **ϕ2** → one step of shifting has been achieved.
### <span style="color:rgb(161, 40, 226)">Readout - Step 4</span>:

![[Pasted image 20251003213126.png]]
**ϕ1** is biased, so the charge is shared between **ϕ2 and ϕ1**. **ϕ3** stays off to maintain separation from the next pixel.

### <span style="color:rgb(161, 40, 226)">Readout - Step 5</span>:

![[Pasted image 20251003213212.png]]

Only **ϕ1** remains biased. The charge is now completely stored under **ϕ1**, completing another shift. 
### <span style="color:rgb(161, 40, 226)">Readout - Step 6</span>:

![[Pasted image 20251003213457.png]]

ϕ3 is biased again, so the charge is shared between ϕ1 and ϕ3. The sequence then repeats from Step 1, and the charge has effectively been shifted one full pixel down (vertical transfer).

By repeating these steps, the charge is moved row by row until it reaches the **readout register**.  
From there, a similar process shifts the charge **horizontally** toward the **output amplifier**, where it is converted into a voltage.

# <span style="color:rgb(239, 179, 1)">CCD Performance</span> 

When analyzing the performance of a CCD, we can look at several aspects of the signal flow: **charge generation, charge collection, charge transfer, and charge readout**.  To quantify these, different **figures of merit** are used, such as **quantum efficiency, well capacity, noise, dark current,** etc.

### <span style="color:rgb(161, 40, 226)">Charge Generation: Quantum efficiency</span>

$$
QE = \frac{\# \space Detected \space photons}{\# \space Incident \space photons}
$$

One of the most important parameters is the **quantum efficiency (QE)**. This is defined as the ratio between the number of detected electrons and the number of photons that actually hit the sensor. In other words, it tells us the probability that each photon will generate a measurable electron–hole pair.
    
![[Pasted image 20251004093857.png]]
For CCDs made from silicon, the quantum efficiency is significant in the visible range and extends into the near-infrared, roughly from 350 nanometers up to about 1000 or 1100 nanometers. In some advanced CCD technologies, the quantum efficiency in the visible range can even exceed 80 percent, which means that more than four out of five photons are successfully converted into electrons.

However, not all incident photons are detected, because some are lost in three main ways: **reflection, absorption, and transmission**.

1. **Reflection**
    -Reflection happens because of the refractive index mismatch between silicon and air. To reduce this loss, an anti-reflection coating is applied on top of the wafer. This coating has an intermediate refractive index, which minimizes the probability that a photon will bounce off the surface instead of entering the silicon.
        
2. **Absorption**
    Absorption losses occur when a photon is absorbed before it reaches the depletion region, for example in the electrodes, the insulating layer, or the shallow surface layers of silicon. This problem is especially relevant in front-side illuminated sensors, where light has to pass through the electrodes before reaching the active region. Back-side illuminated CCDs solve this issue by thinning the substrate to about 15 micrometers, so that photons can reach the depletion region from the back without being absorbed prematurely.
        
3. **Transmission**
    Transmission losses happen when a photon passes through the detector without being absorbed at all. This is common at the extremes of the spectrum: at very short wavelengths, photons may be absorbed too close to the surface to contribute to charge collection, while at very long wavelengths, the photon energy may be too low to cross the bandgap of silicon and therefore no electron–hole pair is created.

### <span style="color:rgb(161, 40, 226)">Charge Generation: Pixel uniformity</span>

Even if the average quantum efficiency is high, not all pixels behave exactly the same. Small variations in the fabrication process can cause differences in charge generation from pixel to pixel. These variations may come from slight changes in the thickness of the oxide layer or the electrodes, differences in electrode area, variations in doping concentration, or small mismatches in the applied voltages.
![[Pasted image 20251004094806.png]]
The result of these variations is what we call **fixed-pattern noise**. If the camera is illuminated uniformly, instead of producing a perfectly flat image, some pixels will appear brighter and others darker. Fortunately, this effect is not random but fixed, because it is determined by the manufacturing process. This means it can be corrected. The calibration method, known as **flat-fielding**, involves taking an image under uniform illumination and using it as a reference. Manufacturers usually provide this reference image, which allows the user to compensate for pixel-to-pixel variations during normal operation.

## <span style="color:rgb(161, 40, 226)">Charge Generation: Dark current</span>

Another important limitation comes from **dark current**, which is the generation of electrons not by incoming photons, but by thermal energy. In silicon, thermal agitation can occasionally give an electron enough energy to jump from the valence band into the conduction band, creating an electron–hole pair. This effect is especially strong at the interface between silicon and silicon dioxide, that is, between the n-doped region and the insulating layer.
![[Pasted image 20251004094946.png]]
Dark current is strongly dependent on temperature. At room temperature or around 0 degrees Celsius, a pixel can accumulate on the order of a thousand electrons per second due to thermal generation alone. This quickly overwhelms the signal in low-light imaging. However, if the sensor is cooled down to very low temperatures, for example to –80 or –100 degrees Celsius, the thermal generation drops drastically, down to only a few tens of electrons per pixel per hour.

For this reason, CCD cameras that are used in scientific research, astronomy, or other highly sensitive applications are often equipped with cooling systems. By lowering the temperature of the detector, the dark current can be minimized, allowing long exposure times without introducing significant noise.

### <span style="color:rgb(161, 40, 226)">Charge Collection: Well capacity</span>

The **well capacity** is defined as the maximum charge that can be stored inside a pixel. A typical order of magnitude is about **10 electrons per μm²**, which corresponds to several hundred thousand electrons per pixel, depending on the pixel size.

#### Example Calculation
Let’s consider the following example:

- Reverse voltage: $V_{cell} = 5V$ 
- Pixel size: $5 μm×5 μm$
- Oxide capacitance per unit area: $\frac{C_{ox}}{A} = 35 \, nF/cm^2$

The charge per unit area can be computed as:

$$\frac{Q}{A} = \frac{C_{ox}}{A} \cdot V_{cell}$$

Substituting the values:

$$\frac{Q}{A} = 35 \, \frac{nF}{cm^2} \cdot 5 \, V \approx 175 \, \frac{nC}{cm^2}$$

If we express this in electrons per $μm²:$

$$\frac{Q}{A} \approx 11,000 \, \frac{e}{\mu m^2}$$

Now, considering the total pixel area:

$$A = 5 \, \mu m \times 5 \, \mu m = 25 \, \mu m^2$$

The maximum number of electrons that can be collected in one pixel is:

$$Q \approx 11,000 \cdot 25 \approx 300,000 \, e^-$$
So, in this case, the well capacity is roughly **300,000 electrons per pixel**.

#### What happens if we exceed the well capacity?

If the integration time is too long and the number of collected electrons approaches the maximum capacity, two effects appear:

1. **Saturation (non-linearity):**
    
    - When we reach about **80% of the well capacity**, the response of the pixel becomes **non-linear**.
    - This happens because the accumulated charge modifies the potential well itself: the increasing voltage across the capacitance reduces the effective electric field at the p–n junction, which decreases the collection efficiency.
        
2. **Blooming (overflow):**
![[Pasted image 20251004105857.png]]
    - At **100% capacity**, the pixel is saturated and additional electrons cannot be stored.
    - These excess charges start to **overflow** into neighboring pixels.
    - This phenomenon is known as **blooming**, and it produces characteristic image artifacts, such as the bright streaks often seen around saturated stars in astronomical images.
    - Importantly, the charge typically overflows **vertically** (within the same column) rather than horizontally (across rows).
        - This is because vertical transfer is only weakly confined.
        - In contrast, horizontal transfer is blocked by **n-doped channel stops**, which act as strong barriers to lateral charge diffusion.

![[Pasted image 20251004105911.png]]

Thus, blooming appears as **vertical streaks** in the image rather than a spread in all directions.

### <span style="color:rgb(161, 40, 226)">Charge transfer: Efficiency/Inefficiency</span> 

![[Pasted image 20251004111324.png]]

When we read out a CCD, the stored charge must be transferred from pixel to pixel until it reaches the output amplifier. The **Charge Transfer Efficiency (CTE)** measures how well this transfer happens.

- **CTE** is the **probability that an electron is successfully transferred** from one pixel to the next.
- Typical values are very high, such as **0.999** or even **0.999999**.

![[Pasted image 20251004111415.png]]
Since these numbers are so close to 1, it is more practical to define instead the **Charge Transfer Inefficiency (CTI):**

$$CTI = 1 - CTE$$

This is the **fraction of electrons lost during each transfer**, usually between $10^{-6}$ and $10^{-4}$

#### Why are electrons lost?

Not all electrons make it to the next pixel because some are **trapped** in defects of the p–n junction or at the silicon/oxide interface. These traps can hold electrons temporarily and release them later, creating smearing or tails in the image.


#### Example: Accumulated Inefficiency

Let’s see what happens in a real CCD.
- Suppose we have a CCD with **12 million pixels** (about $3500 \times 3500$).
- Assume a CTE of **0.99999**.
![[Pasted image 20251004110452.png]]
- The **worst-case pixel** is the one in the corner farthest from the readout node.
    
    - To reach the output, its charge must be transferred about **7000 times** (≈3500 vertical + 3500 horizontal shifts).

The total transfer efficiency for that pixel is:

$$CTE_{TOT} = (0.99999)^{7000}$$

So the total inefficiency is:

$$CTI_{TOT} = 1 - (0.99999^{7000}) \approx 6.7\%$$

That means this pixel loses almost **7% of its charge** before reaching the output!

#### Effect on the Image

![[Pasted image 20251004111826.png]]

| Good CTE                             | Poor CTE                             |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251004111756.png]] | ![[Pasted image 20251004111805.png]] |


- With a **good CTE**, the charge packets remain compact, and the image has **high contrast**: illuminated pixels look bright against a dark background.
    
- With a **poor CTE**, some of the charge leaks into neighboring pixels during the transfers.
    
    - This produces **tails or smearing** along the columns, where bright pixels “leak” into darker ones.
    - As a result, instead of sharp white spots on a black background, the image looks **washed out or gray**, with reduced contrast.
        

This explains why **CTE is a critical parameter** for CCD performance, especially in applications like astronomy, where faint sources must be separated from a dark background.

### <span style="color:rgb(161, 40, 226)">Charge Transfer: Dark columns </span> 

![[Pasted image 20251004112516.png]]
One common type of defect in CCDs is the appearance of **dark columns**. This happens when certain pixels contain **traps** that completely block the vertical transfer of charge. Once the charge is interrupted at a pixel, the entire column below it appears **black**, because no charge can continue to propagate downward.

In practice, almost every CCD has some dark columns. However, these do not usually appear in the final image delivered by the camera. Before release, each CCD is carefully **characterized**, and the affected columns are corrected by **interpolation**: the counts of the neighboring pixels in the same row are averaged and used to replace the dark column.

### <span style="color:rgb(161, 40, 226)">Other Types of Defects</span>

![[Pasted image 20251004112658.png]]
Besides dark columns, there are other defects that can occur:

1. **Bright Columns**
    - These are the opposite problem: instead of blocking charge, certain defects cause a **continuous leakage of electrons** during transfer.
    - As a result, the column appears **bright**, forming a visible vertical streak in the image.
    - Again, these are corrected by processing, averaging adjacent pixel values to smooth out the artifact.
        
2. **Hot Spots**
    
    - Some pixels show a **much higher dark current** than average.
    - These “hot pixels” generate extra electrons even without light, appearing as **bright spots** in dark frames.
    - Clusters of hot spots can also occur, degrading image quality.
    - In rare cases, the dark current can become so high that the pixel behaves almost like a **tiny LED**, emitting light.
    - The emitted light can then be detected by the **neighboring pixels**, producing a bright spot with a **halo** effect around it in the image.


## <span style="color:rgb(239, 179, 1)">Readout Noise</span> 

One of the main noise sources in a CCD camera is the **amplifier noise** that appears during the readout process.

To reduce this contribution, we can **narrow the bandwidth** of the preamplifier. A smaller bandwidth allows the output signal to settle more accurately, reducing fluctuations and hence the noise level. However, this comes at a cost: reducing bandwidth also means we must **slow down the readout speed**, since more time is required for each pixel to be read with a stable voltage at the output.

### <span style="color:rgb(161, 40, 226)">Trade-off: Noise vs. Speed</span>

![[Pasted image 20251004113601.png]]

If we look at the typical graph of readout noise versus sampling frequency:
- At **low sampling frequencies** 1e+05, the readout noise can be as low as **2–3 electrons RMS**, which is excellent performance.
- As the **sampling frequency increases**, the noise rises because the amplifier has less time to stabilize before the pixel value is sampled.
    

For example:

- At a sampling frequency of **500 kHz**, the equivalent readout noise is about **4–5 electrons RMS**.
- The corresponding sampling time per pixel is:
$$T_s = \frac{1}{f_s} = \frac{1}{500 \, kHz} \approx 2 \, \mu s$$
#### Example: 12 Megapixel CCD

Now let’s compute the **total readout time** for a CCD with **12 million pixels**:
$$T_{readout} = T_s \cdot N_{pixels} = (2 \, \mu s) \cdot (12 \times 10^6) \approx 24 \, s$$

So, reading the full frame would take around **24 seconds**.

- The **advantage** is very low noise (only a few electrons), which is desirable for scientific imaging (e.g., astronomy or microscopy).    
- The **disadvantage** is the long readout time, which is clearly unacceptable for consumer devices like smartphones, where users expect images to be captured almost instantly.

#### Conclusion

The **choice of amplifier bandwidth** is a critical design decision. It defines a trade-off:

- **Low bandwidth → low noise but long readout times** (suitable for scientific applications).
- **High bandwidth → faster readout but higher noise** (suitable for consumer electronics).
    
This balance is what determines whether a CCD is optimized for research cameras or everyday devices.

### <span style="color:rgb(161, 40, 226)">Readout Circuit </span>
![[Pasted image 20251004115023.png]]
After the charges have been shifted row by row through the CCD array, they arrive at the **last auxiliary row**. From here, the signal is transferred to the **readout circuit**.

It is important to note that CCDs are fabricated in a **dedicated imaging technology**, which is optimized for light detection rather than for logic or analog processing. This means that while a CCD can integrate a few simple transistors within the wafer, it cannot accommodate **complex amplifiers** like those available in CMOS technology. For this reason, the **main amplification and analog signal conditioning** are usually performed by an **external circuit**, placed after the CCD output.

### <span style="color:rgb(161, 40, 226)">The reset transistor</span>
![[Pasted image 20251004114659.png]]
Inside the CCD, the **output stage** typically consists of a small number of transistors and a **readout capacitor** $C$. One of these transistors, called the **reset transistor**, plays a crucial role:

- After each pixel has been read, the reset transistor restores the readout capacitor to a reference voltage ($V_{DD}$​).
    
- When the charge packet from the last pixel in the auxiliary row is transferred, it shares its electrons with this capacitor. The result is a reduction of the capacitor voltage proportional to the charge carried by that pixel.
    

This voltage change is then measured by the external amplifier, providing the pixel intensity.

### <span style="color:rgb(161, 40, 226)">Reset Noise (kTC Noise)</span>
![[Pasted image 20251004114659.png]]

During the reset phase, the reset transistor operates in the **ohmic region**, which allows us to model it as a **resistor**. Like any resistor, it introduces **thermal noise**.

This thermal noise translates into fluctuations in the charge stored on the capacitor. The resulting uncertainty is called **reset noise** or **kTC noise**, because its RMS value depends on the thermal energy and the capacitance:
$$Q_{n,rms} = \sqrt{kT C}$$
#### Computation:

![[Pasted image 20251004122253.png]]
We consider the **reset transistor** of the CCD, which operates in its **ohmic region**. In this region, the transistor can be modeled as a **resistor**:
$$
R_{DS}=\frac{1}{2k(V_{GS}-V_{T})}
$$
Here, $k$ is a transistor constant, $V_{GS}$​ is the gate-source voltage, and $V_T$​ is the threshold voltage. We assume the transistor is in the ohmic region because we want the node it controls to be close to $V_{DD}$​. This implies that the voltage across the transistor ($V_{DS}$​) is small compared to the drive voltage applied.
![[Pasted image 20251004122303.png]]
The resistor $R_{DS}$ generates **thermal noise**, which can be represented by an equivalent current noise source with spectral density:
$$
S_I = \frac{4 k T}{R_{DS}}​
$$
To find the noise at the output (voltage across the capacitor), this current flows through $R_{DS}$, giving an output spectral density:

$$S_{V_\text{out}} = S_I \cdot R_{DS}^2 = 4 k T \cdot R_{DS}​
$$

![[Pasted image 20251004122317.png]]
For a single-pole RC circuit, the bandwidth is approximately:
$$\Delta f = \frac{1}{4 R_{DS} C}$$
Multiplying the spectral density by the bandwidth gives the **variance**, and taking the square root gives the **standard deviation of the voltage noise**:
$$\sigma_V = \sqrt{S_{V_\text{out}} \cdot \Delta f} = \sqrt{4 k T R_{DS} \cdot \frac{1}{4 R_{DS} C}} = \sqrt{\frac{k T}{C}}$$

- Thermal noise from the reset transistor appears at the CCD output.
- Voltage noise depends only on the capacitance: $\sigma_V = \sqrt{kT/C}$
- $\sigma_Q=\sqrt{KTC}$

The standard deviation of the noise in **charge** is $\sqrt{kTC}$ This noise comes from the **voltage fluctuations** across the output capacitance at the end of the **reset phase**. Ideally, at the end of the reset, the capacitance would be exactly charged to $V_{DD}$​. In reality, because of noise, the voltage will be slightly above or below $V_{DD} \pm \sigma _{Q}$​.

To reduce the effect of this noise, we **sample the voltage twice**: once **right after the reset**, and once **after the pixel has integrated the charge**. By taking the **difference between these two measurements**, we obtain the actual voltage corresponding to the charge stored in the pixel.

This technique is called **Correlated Double Sampling (CDS)**. It works by measuring the voltage across the capacitance **before and after charge transfer**, effectively removing the reset noise. Applying this for each pixel allows us to accurately determine the charge stored in each pixel.

## <span style="color:rgb(239, 179, 1)">Color Filtering</span> 

A **CCD sensor** is made of silicon, which can detect photons in the visible and near-infrared range. However, it has one limitation: **it cannot distinguish between wavelengths**. No matter the color of the photon (red, green, or blue), the absorption event always produces the same type of electron-hole pair.

So, how do CCD cameras capture **color images**?

The solution is to place **color filters** on top of the sensor. The most common arrangement is called the **Bayer filter array**, which uses red, green, and blue (RGB) filters.

In the ***Bayer pattern***, pixels are grouped into **2×2 blocks** (“macropixels”):

- 1 pixel has a **red** filter,
- 1 pixel has a **blue** filter,
- 2 pixels have **green** filters.

The reason for doubling the green pixels is that the **human eye is more sensitive to green light**, so this arrangement produces images that look sharper and more natural to us.
![[Pasted image 20251004154031.png]]

Each pixel in the sensor only measures **one color component** (red, green, or blue). But to display a full image, we need all three color values for every pixel.

For example, consider a **green pixel**: it only records the green intensity, but has no direct information about red or blue. To recover those missing values, the camera uses the information from the **neighboring pixels**.

This process is done through a technique called **demosaicing**. Instead of simply averaging neighbors, the algorithm uses more advanced interpolation methods to estimate the missing colors as accurately as possible.

## <span style="color:rgb(239, 179, 1)">Types of CCD</span> 

CCD sensors can be built in different architectures, and the three most common ones are the **full frame**, the **frame transfer**, and the **interline transfer** CCDs.

### <span style="color:rgb(161, 40, 226)"><b>Full frame CCD </b></span> 
![[Pasted image 20251004161840.png]]
The entire chip is exposed to light, which means that all pixels collect the image at the same time. This setup has the advantage of being very efficient in terms of sensitivity, since every pixel is available for light collection. However, it comes with a major drawback: the readout process is very slow. If we want to achieve very low noise, down to the single-electron level, a megapixel sensor could take around 24 seconds to read out completely. During such a long readout, light can still reach the chip and distort the image. To prevent this, a mechanical shutter is required to block incoming light while the sensor is being read.

To overcome this limitation, the **frame transfer CCD** was developed. 

### <span style="color:rgb(161, 40, 226)">Frame transfer CCD</span>

![[Pasted image 20251004161858.png]]

In this design, the sensor is divided into two regions: an image array, which is exposed to light, and a storage array, which is completely covered. When an exposure is completed, the entire image is quickly shifted from the image array into the storage array through a vertical transfer. Since the storage array is shielded from light, it can then be read out at a slower pace while the image array is already free to start capturing the next exposure. This avoids the need for a mechanical shutter and allows for much faster operation compared to the full frame architecture.

An even faster approach is the **interline transfer CCD**. 

### <span style="color:rgb(161, 40, 226)">Interline transfer CCD</span>

![[Pasted image 20251004161934.png]]

Here, every other column of the array is covered, while the alternate columns are exposed to light. During image acquisition, light is integrated only on the exposed columns. At the end of the exposure, the charge collected is transferred very quickly into the adjacent covered columns, which are protected from light. From there, the charges are shifted out during readout, while the exposed columns are immediately available to start recording the next frame. This continuous availability makes interline transfer CCDs especially suited for video applications, where high frame rates are necessary. One trade-off of this method is that part of the array is covered, reducing the light-sensitive area.

---
In short, full frame CCDs offer the highest sensitivity but require a shutter and slow readout, frame transfer CCDs provide a good balance between sensitivity and speed by using a storage array, and interline transfer CCDs sacrifice some sensitivity in exchange for very high speed, making them ideal for video recording.

## <span style="color:rgb(239, 179, 1)">CCD Applications</span> 

![[Pasted image 20251004162522.png]]

In conclusion, CCDs are built using **dedicated technologies** specifically optimized for imaging. This makes them relatively expensive compared to other sensors, but also allows them to deliver outstanding performance. One of their main strengths is their **high quantum efficiency (QE)**, since the silicon wafers are carefully optimized for light detection. In fact, CCDs can reach or even exceed a QE of 80%.

They also achieve **very low dark currents**, especially when combined with cooling systems that lower the sensor temperature to –50 °C or even –100 °C. On top of this, CCDs can provide **extremely low readout noise** if the readout bandwidth is reduced and the image is read slowly, sometimes over tens of seconds.

Because of these characteristics, CCDs are not suitable for everyday consumer applications like smartphones, where low cost and fast operation are more important. Instead, they are widely used in **scientific and professional fields** where image quality is critical. Examples include digital research cameras, **microscopy**, **biological imaging**, and **astrophotography**, where they are used to capture galaxies and nebulae. Their high quantum efficiency in the near-infrared range also makes them valuable for **night vision** and **specialized photography applications** such as VLS testing.

In short, while CCDs are too specialized and costly for mass-market devices, they remain the **gold standard in scientific imaging** whenever maximum sensitivity, low noise, and precise light detection are required.

# <span style="color:rgb(223, 109, 109)">CMOS active pixel image sensor</span> 

![[Pasted image 20251004162804.png]]
In this case, the image sensor is fabricated using **standard CMOS technology**. This allows not only the integration of the **photosensitive area** inside each pixel, but also the necessary **transistors for the readout circuitry**.

Typically, the photosensitive area in each pixel is implemented with a **standard photodiode**, while the remaining part of the pixel is occupied by the transistors that handle the signal processing and readout. As a result, only about **30% of the pixel area** is actually light-sensitive, while the other **70% is taken up by the electronics**.

![[Pasted image 20251004163340.png]]

This ratio is referred to as the **fill factor**, defined as the fraction of the pixel area that is photosensitive. In CMOS active pixel sensors, the fill factor is therefore quite low, around 30%. This reduced fill factor negatively affects the detector’s efficiency, since a large portion of the incoming photons (those that hit the transistor area) do not contribute to the signal.

To mitigate this problem, CMOS sensors make use of **microlenses** placed on top of the wafer. Each microlens is aligned with a pixel and concentrates the incoming light onto the photosensitive area. With this approach, the **effective fill factor** can be increased to nearly **100%**, making the sensor much more efficient.

As in CCDs, CMOS sensors also require **color filters**—such as the Bayer filter array—to distinguish between different wavelengths and reconstruct color images.

## <span style="color:rgb(239, 179, 1)"> Readout electronics</span>

![[Pasted image 20251004164519.png]]
In a CMOS active pixel sensor, each pixel contains not only the **photodiode**, but also several **transistors** that handle resetting and readout. During the **acquisition phase**, the photodiode—which is a **reverse-biased diode**—integrates the photocurrent onto a capacitance. This capacitance isn’t a physical component, but rather represents the combined capacitance of the photodiode junction and the parasitic capacitances of the transistors (for example, gate-drain-source capacitances of the reset transistor).

![[Pasted image 20251004164635.png]]
A second transistor, often called **M2**, is configured as a **buffer**. Its purpose is to transfer the voltage across this capacitance to the **column bus**, which is shared by all pixels in the same column. Because multiple pixels connect to the same bus, a **row selector** is needed to choose which pixel’s voltage is placed on the column bus at any given time.

After a pixel is read out, the **reset transistor** is switched on to restore the voltage across the capacitance to $V_{DD}$​, preparing the pixel for the next acquisition. During the subsequent exposure, the photocurrent flowing through the photodiode gradually decreases this voltage, reflecting the amount of light captured.

At the end of the column, the signal is passed to a **column amplifier**, which boosts the voltage for readout. This is an important distinction from CCD sensors: in CCDs, the **charge-to-voltage conversion** happens outside the pixel array and requires transferring the charge across the sensor. In CMOS sensors, this conversion is performed **directly within each pixel**, so there is no need for large-scale charge transfer. Instead, the readout simply involves scanning the rows and reading the voltages along the shared column bus.

## <span style="color:rgb(239, 179, 1)">Noise sources</span>

The **in-pixel circuitry** of CMOS sensors introduces several sources of noise. Similar to CCDs, CMOS sensors also exhibit **fixed pattern noise (FPN)**. This noise arises from variations in photodiode efficiency between different pixels, as well as mismatches in the readout circuitry. Because fixed pattern noise is **constant and reproducible**, it can be corrected using a calibration process called **flat-field correction**.

Another source of noise in CMOS sensors is **reset noise**. Just like in CCDs, we need to reset the storage capacitance in each pixel after readout. Since CMOS sensors perform the **charge-to-voltage conversion directly in the pixel**, the reset noise is expressed as a voltage:
$$\sigma_v = \sqrt{\frac{kT}{C}}​$$

The calculation is the same as for CCDs, but the difference is that in CMOS sensors, this noise originates **inside each pixel**, whereas in CCDs it is mainly introduced by the readout circuit.

Additional noise sources in CMOS sensors include the **column amplifiers**, which can contribute their own electronic noise. CMOS transistors also generate **1/f noise**, a type of noise that increases at low frequencies. Finally, the photodiode itself introduces **shot noise**, which is related to the statistical nature of photon detection and can also be seen as thermal noise associated with the photodiode’s equivalent resistance.

## <span style="color:rgb(239, 179, 1)">CMOS Sensor General Structure</span>
![[Pasted image 20251004173340.png]]

A **CMOS image sensor** consists of more than just the array of pixels. At the center of the chip, we have the **active pixel array**. On top of each pixel, there are **Bayer mosaic filters** to separate light into red, green, and blue components, enabling color imaging.

Surrounding the pixel array, a large portion of the chip is dedicated to **peripheral electronics**. This includes **column amplifiers** that boost the signal from each column, as well as **analog-to-digital converters (ADCs)** that digitize the pixel voltages directly on the chip. Once the information is digital, additional **on-chip processing** can be performed, such as image correction or noise reduction.

The sensor also contains electronics to **generate clocks and control signals**, which coordinate the timing of readout, analog processing, ADC operation, and digital processing. After processing, the sensor includes **digital interfaces** to transmit the data in standard protocols. In modern cameras, this is often done via **MIPI Camera Serial Interface (CSI)**, which is a high-speed serial protocol, or sometimes via **Digital Video Port (parallel CMOS interface)**.

Finally, the chip is surrounded by a **pad ring**, which provides the bonding pads used to connect the CMOS sensor to the camera system for power, control, and data readout.

## <span style="color:rgb(239, 179, 1)">CMOS sensor functional blocks</span> 

![[Pasted image 20251004174210.png]]
This is an example of a **block diagram of a CMOS camera**. At the center, we have the **active pixel array** with a VGA resolution, meaning roughly 640 × 480 pixels. In practice, there are often a few extra pixels that are **shielded or covered**; these are used to compensate for **dark current** and improve image quality.

Surrounding the array, there are electronics to **select the rows** during readout. CMOS sensors can also implement **correlated double sampling (CDS)**, which helps mitigate **reset noise**. In CDS, the voltage across the storage capacitance is measured both **after the reset** and **after light integration**, and the difference gives the true signal.

In simpler CMOS designs, there is often a **single amplifier** that reads out the pixels, along with **multiplexers or registers** to connect different columns to the amplifier. The amplified analog signal is then converted to digital by an **ADC**. After that, **digital image processing** can be performed on-chip, and the data is finally transmitted through a **standard camera interface**.

More advanced cameras aiming for **higher frame rates** often use **one amplifier and one ADC per column**, allowing all columns to be read out simultaneously. This greatly speeds up the readout process and increases the camera’s overall frame rate.

## <span style="color:rgb(239, 179, 1)">Active Window</span> 

![[Pasted image 20251004175049.png]]

One of the advantages of CMOS pixel sensors is that we can **speed up the readout** by reducing the number of pixels we read. This is a major difference compared to CCD cameras, where **all pixels must participate in the charge transfer**, so you cannot selectively read only part of the array. In CMOS sensors, since **charge-to-voltage conversion occurs within each pixel**, we can choose to read only a **subset of pixels**.

For example, we can select a **window of interest** on the sensor. By reading only this smaller region, we reduce the total number of pixels processed, which increases the **frame rate**. This is commonly used in smartphones: when capturing a still image, the full sensor is used, but for video, only a subset of pixels is read to maintain higher frame rates.
![[Pasted image 20251004175105.png]]

Another approach is **window subsampling**, which allows us to read fewer pixels while keeping the same field of view. However, subsampling must be done carefully to avoid losing important information. In particular, the **Bayer filter array** on top of the sensor requires that groups of four pixels (covering red, green, and blue filters) are read together. Skipping pixels arbitrarily could lead to missing color information or creating artifacts in the image.

## <span style="color:rgb(239, 179, 1)">Readout modes</span>

There are two main methods for capturing an image with a CMOS sensor: **rolling shutter** and **global shutter**.

| Rolling Shutter                      | Global Shutter                       |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251004175939.png]] | ![[Pasted image 20251004180005.png]] |
|                                      |                                      |

### <span style="color:rgb(161, 40, 226)"><b>Rolling shutter</b></span>

The sensor reads and resets the pixels **one row at a time**. When the first row finishes its readout, it begins a new acquisition, then the second row is read and reset, and so on until the last row. This means that the **exposure is not simultaneous across the sensor**—the first row starts capturing light earlier than the following rows. For static scenes, this is not a problem. However, for fast-moving objects, this can create **artifacts**, such as skewed or stretched images, because different rows capture the scene at slightly different times.

### <span style="font-weight:bold; color:rgb(161, 40, 226)">Global shutter</span>

In contrast, a **global shutter** exposes **all pixels at the same time**. The entire array integrates light simultaneously, and then the readout happens afterward. The main disadvantage is that the readout can take longer, potentially introducing some dead time between frames. The major advantage, however, is that **all pixels are perfectly synchronized**, so fast-moving objects are captured without any distortion or artifacts.


## <span style="color:rgb(239, 179, 1)">CMOS APS applications</span>
![[Pasted image 20251004180226.png]]
As we have seen, **CMOS active pixel sensors** are widely used in **high-volume imaging applications**, such as smartphones, webcams, and machine vision systems. They are also suitable for **niche applications** that require very small sensor sizes, like **endoscopy pill cameras**. Additionally, CMOS sensors are sometimes used in **digital reflex cameras**, where their compact design, low power consumption, and integrated electronics offer practical advantages.

# <span style="color:rgb(223, 109, 109)">CCD vs CMOS APS</span> 

![[Pasted image 20251004181155.png]]
A brief comparison between **CCD** and **CMOS sensors** highlights their differences in **fabrication technology and design philosophy**.

**CCDs** are made using **custom, dedicated imaging technology**, while **CMOS sensors** are produced with **standard CMOS processes**, which are more cost-effective. Because CMOS sensors use standard technology, it is possible to integrate electronics directly **inside each pixel**, including the **charge-to-voltage conversion**, whereas in CCDs this conversion occurs **after the charge has been transferred** across the sensor.


![[Pasted image 20251004181214.png]]

The advantage of dedicated CCD technology is **higher sensor performance**. CCDs generally have **higher photodetection efficiency**, which extends into the near-infrared, **lower dark current**, and **lower noise**, because almost the entire pixel area is dedicated to light capture. This also results in **higher fill factor** and more uniform images with less fixed pattern noise.

On the other hand, CMOS sensors excel in **flexibility and speed**. Because charge-to-voltage conversion occurs inside each pixel, CMOS sensors allow for **faster readout**, selective readout of a **window of interest**, and **direct digital output**. They also require fewer external electronics, enabling **lower-power systems** and simpler PCB designs.

From a **cost perspective**, CCDs are expensive due to their customized fabrication and are generally used in **specialized, high-performance applications**, such as scientific imaging, microscopy, or astrophotography. CMOS sensors, by contrast, are **less expensive** and can be produced in **large volumes** for consumer applications like smartphones, webcams, and machine vision.


![[Pasted image 20251004181227.png]]

If you compare the external electronics required, a CCD sensor typically needs **almost all supporting circuitry**—amplifiers, ADCs, and control logic—outside the chip, leading to more complex PCBs. CMOS sensors, however, integrate most of these functions on-chip, resulting in **cleaner and more compact system designs**.