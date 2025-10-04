
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

<span style="color:rgb(239, 179, 1)">CCD Performance</span> 

Now, we´re going to discuss the CCD performance in terms of some characteristics:
Charge generation, charge collection, charge transfer, charge readout...And in order to quantify the performance, weĺl use differente figures of merit as Quantum efficiency, well capacity, noise, etc...

Charge generation: Quantum efficiency

It is define by the ratio of the detected photons between the number of incident photons. It represents the probability that the photoelectron will be generated for each incident photon. Here we have an example of a QE% of different CCD cameras which are implemented in different technoogies, in particular you see that we have a significant quantum efficiency in the visible range up to the near-infrared so from 350nm up to 1000, 1100nm more or less because CCD are publicated with silicon waveforms, so photodiodes are limited in this visible near infrared branch.

FOr some technologies we might reach in the visible range a very high QE in the order of even exceeding 80% tHE Mechacnism for which main enter the photon collection are mainly three: REflection, absorption and transmission.

REflection: it is because the difference between refractive indexes between the silicon and the medium in which the light is travel (The air), in order to mitigate it we can use antireflection coating, putting at the top of the wafer an antireflecting coating which are materials which a refractive index in between the air and the silicon and this will avoid or reduce the probability of reflecting  photons

Absorption: Absorption bef the photon can reach the depletion region, in the polysilicon electrodes or insulator or n region bef reaching the depletion region from the front sided dominated technologies, from the back-side illuminated we have the absorption in the thinnest substrate bef reaching the depleted region

TRansmission: happens when the photon pass through the detector withotu being absorbed, it happens for shorter wavelenghts, photons which have higher energy, they can be absorpebd before reaching the depletion region, instead the transmission typically happen for higher wavelenghts cos this photons has a energy lower than the energy gap of the silicon that can´t produce the electron-hole pair

Charge GEneration: pixel uniformity

In a CCD camera we can have some differences in the ability to generate charge when a photon is absorbed from pixel to pixel mainly due to process variations between different pixels of the same image, for instance, differences of the thickness of the oxide or the electrodes, or the area of the electrodes or doping concentration or in the biasing voltage in different electrodes of the array.

IN particular this non unifomity forms the so called fixed pattern noise. If you illuminate your imager with an uniform light over the entire array what you´d obtain is a raw image as the one displayed which is not a flat image which would be expected from a uniform light but some pxels are darker than other and we create this fixed pattern noise. Unfortunately it is fixed cos it is caused by process variations mainly and so it can be calibrated, and fro the calibration 21:30
