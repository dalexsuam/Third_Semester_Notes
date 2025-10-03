
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