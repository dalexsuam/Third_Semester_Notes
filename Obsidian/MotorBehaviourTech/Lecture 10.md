
Date: 21/10/2025
***
# <span style="color:rgb(223, 109, 109)">3D Localization</span>
## <span style="color:rgb(239, 179, 1)">A bit of History</span>

![[Pasted image 20251016184953.png]]
![[Pasted image 20251016185332.png]]

![[Pasted image 20251016185349.png]]

![[Pasted image 20251016185412.png]]

![[Pasted image 20251016185916.png]]

***
# <span style="color:rgb(223, 109, 109)">Optical measurements for human motion analysis</span>

We are now moving to the **final part of the course**, which focuses on **optical measurement systems**.

- Optical methods are the **most accurate techniques** for analyzing **human motion and motor behavior**.
- They allow **higher measurement precision and performance** compared to other sensing approaches.
    
### <span style="color:rgb(161, 40, 226)"></span><span style="color:rgb(161, 40, 226)">Image processing and spatial localization</span>
![[Pasted image 20251021131449.png]]
Optical motion analysis is based on:

- **Image processing**, and
- **Localization of points in space**.
    
The key mathematical tool enabling this is the **perspective transformation**.

## <span style="color:rgb(239, 179, 1)">Image space vs. Euclidean space</span>
![[Pasted image 20251021132949.png]]

- The camera acquires information in the **image space** (the camera sensor plane).
- Our goal is to express measurements in a **Euclidean (3D) reference frame**, also called the **global reference frame**.
- To do this, we must model how **3D points are projected onto the 2D image plane**.
    
This model must account for:
- perspective effects,
- changes in apparent size due to distance,
- camera geometry and orientation.
    
### <span style="color:rgb(161, 40, 226)">Multiple viewpoints and triangulation</span>

A single camera is not sufficient to recover depth information reliably.

- Measurements are taken from **at least two different points of view**.
- This approach is known as **triangulation**.
    
By combining:
- multiple observations of the same point, and
- known camera positions and orientations,
    
it is possible to estimate the **3D position of points in space**.

### <span style="color:rgb(161, 40, 226)">Key idea</span>

**Multiple synchronized observations from different viewpoints enable accurate 3D reconstruction through triangulation**, which is the foundation of optical motion capture systems


![[Pasted image 20251021133309.png]]
The cameras used in our system perform a _central projection_, similar to what we observe in this image of a narrow street between trees, where all projection rays converge toward a single center of projection. Now we should define how this projection landmarks into the object space are projected on the image space

## <span style="color:rgb(239, 179, 1)">Object space, image space, and the need for a projection model</span>

![[Pasted image 20251021133659.png|400]]
Up to now, we know that we have an **object in space**—the _object space_—and a surface on which the image is formed. Historically, this surface was photographic **film**, because early cameras used chemical film instead of solid-state sensors. For our purposes, however, we can simply treat it as a **plane**, called the **image plane**.

The key question is:  
**How can points in object space be projected onto this image plane in a meaningful way?**

### <span style="color:rgb(161, 40, 226)">What happens without an optical system?</span>

If we simply expose the image plane to the scene, without any optical constraint, we cannot correctly measure the position of points in object space.
![[Pasted image 20251021133928.png|300]]
Consider a simple experiment:

1. Turn on a torch (flashlight).
2. Shine it onto a white wall.
    

What do you see?

You see a **uniformly illuminated surface**, essentially a gray or bright region. You do **not** see an image of the object itself.

Why does this happen?
![[Pasted image 20251021134233.png|500]]
Every point on the wall receives light coming from **many different points in object space**. There is no unique correspondence between:

- a point in object space, and
- a point on the image plane.
    
In other words, there is **no optical system** enforcing a one-to-one relationship. The image plane is just being illuminated.

For example, if I stand in front of a wall under uniform lighting, my image does not appear on the wall. The wall is illuminated, but there is no mapping between the tip of my finger and any specific point on the wall.

This means the system is **not objective**.

### <span style="color:rgb(161, 40, 226)">Introducing an objective system: the pinhole experiment</span>

Now let us modify the experiment.
![[Pasted image 20251021134345.png|400]]
Take a sheet of paper and pierce a **small hole** in the center. Place this sheet close to the wall.

What happens now?

If you look at the wall behind the sheet, you will see **an image**. Not just a dot—but a projection of the illuminated object.

If the light source has a circular shape, you see a circle.  If it has a triangular shape, you see a triangle.

Why does this happen?
![[Pasted image 20251021134355.png|400]]
The small hole acts as a **spatial constraint**:

- For each point in object space, only **one light ray** can pass through the hole and reach the image plane.
- All other rays are blocked by the paper.
    
This creates a **one-to-one correspondence** between:

- a point in object space, and
- a point on the image plane.
    
This is what we mean by an **objective system**.
### <span style="color:rgb(161, 40, 226)">Image inversion</span>

If you observe the projected image carefully, you will notice something interesting:

👉 **The image is upside down.**

For example:

- points at the top of the object appear at the bottom of the image,
- points on the left appear on the right.
    
This inversion occurs because all rays pass through a **single point** (the pinhole), causing the geometry of the projection to flip the image.

### <span style="color:rgb(161, 40, 226)">Key takeaway</span>

The presence of a single projection point—whether a **pinhole** or, in real cameras, a **lens system**—is essential to:

- enforce a unique mapping between object space and image space,
- allow meaningful position measurements,
- enable geometric models such as **perspective projection**.
    
This principle is the foundation of the **pinhole camera model**, which we will use to describe and analyze camera-based measurements.

## <span style="color:rgb(239, 179, 1)">The camera obscura principle</span>
![[Pasted image 20251021134828.png|500]]
This is the principle of the **camera obscura**, a device that projects images of the external world through a **small hole** onto an internal surface.

Historically, the camera obscura was used by artists to make accurate drawings of real scenes. For example, a scene outside a tent could be projected through a small opening onto a sheet of paper inside the tent. The artist could then trace the projected image to reproduce the real world with correct proportions and perspective.

This is conceptually very similar to what we want to achieve with a camera:  
**project the three-dimensional world onto a two-dimensional surface in a controlled and measurable way**.
### <span style="color:rgb(161, 40, 226)">Why must the camera be “obscura”?</span>

![[Pasted image 20251021134848.png|400]]
A key feature of the camera obscura is that the image is formed **inside a dark environment**. Why must it be dark?

The reason is related to the **amount of light** reaching the image plane.
Because the opening is very small:

- each point in the object space emits many light rays,    
- but only a **tiny fraction** of those rays can pass through the hole,
- the vast majority of the light is blocked by the barrier.

As a result, the projected image is **very dim** compared to the original scene.

This is why the interior of the camera obscura must be dark:  if there were additional light inside, it would overwhelm the weak projected image and make it difficult or impossible to see.

### <span style="color:rgb(161, 40, 226)">The fundamental trade-off</span>
![[Pasted image 20251021135146.png|500]]
The small hole is necessary to ensure:

- a **one-to-one correspondence** between object points and image points,
- sharp and geometrically accurate projections.
    
However, the same small hole causes:
- **low light intensity** on the image plane,
- a dark image that is hard to observe.
    
This introduces a fundamental trade-off:
- **small hole → sharp image, low brightness**
- **large hole → brighter image, but blurred projection**
    
### <span style="color:rgb(161, 40, 226)">A seemingly trivial solution—and its limitation</span>

A natural idea might be:

> “Why not simply make the hole larger?”

Indeed, increasing the hole size allows more light to pass through, making the image brighter.
However, this also allows **multiple rays from the same object point** to reach different points on the image plane, which destroys the one-to-one correspondence and causes **image blur**.

This is the problem that led to the development of **optical lenses**, which we will discuss next.
## <span style="color:rgb(239, 179, 1)">From camera obscura to modern cameras: the role of lenses</span>

Today, we no longer rely on the camera obscura principle for most imaging applications. Although some very low-cost or specialized sensors still use a **pinhole** instead of a lens, the practical solution to the brightness and sharpness problem is the use of a **lens**.

Now we will see **why lenses are used** and how a real camera is structured.

### <span style="color:rgb(161, 40, 226)">Main components of a real camera</span>
![[Pasted image 20251021135459.png|500]]
A modern camera consists of several key components arranged in sequence:

#### <span style="color:rgb(2, 141, 192)">1. Lens</span>

The camera starts with a **lens**, whose function is to collect light from the object space and focus it onto the image sensor.

Unlike a pinhole, a lens allows many light rays from the same object point to be properly redirected so that they converge onto a single point on the sensor. This makes the image both **bright and sharp**.
#### <span style="color:rgb(2, 141, 192)">2. Aperture (f-stop)</span>

The first “shutter” is the **aperture**, also known as the **f-stop**. Its role is to control the **amount of light** entering the camera:

- opening the aperture allows more light to pass,
- closing the aperture reduces the number of incoming light rays.
    
In this sense, the aperture replaces the pinhole of the camera obscura, but with adjustable size and much better optical performance.

#### <span style="color:rgb(2, 141, 192)">3. Exposure shutter</span>

The second shutter controls the **exposure time**, that is, how long the sensor is exposed to light.
Imaging means storing light information—either on film (in older cameras) or in electronic form (in modern sensors). Both film and electronic sensors **integrate light over time**.

This means:
- the longer the exposure time,
- the more photons reach the sensor,
- and the brighter the resulting image becomes.

Therefore, brightness can be increased either by:

- allowing more light in (aperture),
- or by waiting longer (exposure time).
    
Modern electronic cameras allow these two parameters to be controlled **independently**, unlike older mechanical systems.
#### <span style="color:rgb(2, 141, 192)">4. Image sensor</span>

After the shutters, light reaches the **image sensor**.

The two main sensor technologies are:
- **CCD (Charge-Coupled Device)**,
- **CMOS (Complementary Metal-Oxide Semiconductor)**.

Both convert incoming light into electrical signals, which represent the image.
#### <span style="color:rgb(2, 141, 192)">5. Processing and post-processing</span>

Finally, the electrical signals produced by the sensor are:
- digitized,
- processed,
- and post-processed.

This includes operations such as filtering, enhancement, geometric correction, and—relevant for us—**point localization and measurement in space**.

#### <span style="color:rgb(2, 141, 192)">Summary</span><br>
The imaging chain in a real camera can be summarized as:

**Lens → Aperture → Exposure control → Sensor → Signal processing**

This is the path we will follow next, starting from the optical principles of lenses and moving toward how camera images can be used for **accurate spatial measurements** in human motion analysis.

### <span style="color:rgb(161, 40, 226)">The pinhole camera model</span>

![[Pasted image 20251021135658.png|600]]
The first optical element we introduced is the **lens**.  
The **pinhole** can be considered a special case of a lens with an aperture that is **practically zero**.

The term **aperture** refers to how much light is allowed to pass through the lens (or, in this limiting case, through the pinhole). With a pinhole, only a very small fraction of the incoming light reaches the image plane.

#### <span style="color:rgb(2, 141, 192)">Geometric model of the pinhole camera</span>

The pinhole camera is modeled as follows:

- An **object space**, containing points in 3D space.
- A single **infinitesimal pinhole**, acting as the optical center.
- An **image (or view) plane**, placed behind the pinhole.

In this model, each point in the object space is connected to a corresponding point on the image plane by a straight line passing through the pinhole. This establishes a **collinearity condition** between:

1. the 3D point in space,    
2. the pinhole (optical center),
3. the projected point on the image plane.
    
This is the fundamental assumption of the pinhole camera model.

#### <span style="color:rgb(2, 141, 192)">Image inversion</span>

An important consequence of this geometry is that the image formed on the image plane is **inverted**:

- points that are high in the object space appear low on the image plane,
- points on the left appear on the right, and vice versa.
    

Although this inversion is usually corrected in practical camera systems (either optically or digitally), it is intrinsic to the ideal pinhole camera model and must always be kept in mind when developing the mathematical formulation of perspective projection.

### <span style="color:rgb(161, 40, 226)">Effect of increasing the pinhole size</span>
![[Pasted image 20251021135803.png|400]]
Let us return to the pinhole experiment and imagine **increasing the size of the hole** in the sheet of paper.

What happens?
The image becomes **blurred**.
#### <span style="color:rgb(2, 141, 192)">Why does blurring occur?</span>
![[Pasted image 20251021135541.png|500]]
With an **infinitesimal pinhole**, each point in the object space ideally corresponds to **a single light ray** reaching the image plane. As a result, a point in the object space is mapped to a single point in the image plane, producing a **sharp image**.

When the pinhole is enlarged:
- multiple light rays originating from the **same object point** can pass through the opening,
- these rays reach **different locations** on the image plane.
    
As a consequence, a single point in object space is no longer mapped to a single point, but to a **small region** (typically a disk or ellipse) on the image plane.

This region is known as the **blur spot** (or point spread). The larger the pinhole, the larger this blur region becomes.
#### <span style="color:rgb(2, 141, 192)">Trade-off between brightness and sharpness</span>

This leads to a fundamental trade-off:
- **Small pinhole**
    - very sharp image
    - very low brightness (dark image)
- **Large pinhole**
    - brighter image
    - loss of objectivity due to blurring
    
Therefore, we need to find a **compromise** between image brightness and image sharpness. In real cameras, this compromise is achieved using **lenses**, which allow more light to enter while maintaining a sharp image.
#### <span style="color:rgb(2, 141, 192)">Towards geometric measurement</span>

We now move toward understanding how to **measure positions** using this projection model.
We consider the **pinhole camera geometry**, where:
- the pinhole is also called the **perspective center**,
- the image plane (sensor or view plane) is placed at a fixed distance from the pinhole,
- a point in object space is projected onto the image plane through straight-line rays passing through the pinhole.
#### <span style="color:rgb(2, 141, 192)">Similar triangles and perspective projection</span>
![[Pasted image 20260104211144.png]]
From the geometry, it is immediately clear that two triangles are formed:
- one between the object point, the pinhole, and the image plane,
- another between the object point, the pinhole, and the reference plane in object space.
    
These two triangles are **similar**, differing only by a **scale factor**. This similarity relationship is the key to deriving the **perspective projection equations**, which allow us to relate 3D coordinates in object space to 2D coordinates in image space.

### <span style="color:rgb(161, 40, 226)">Integration time and motion blur</span>

Let us return to our experiment.

We said that a **very small pinhole** allows only a limited amount of light to reach the image plane. One way to compensate for this lack of light is to **increase the integration time** of the sensor.

If we wait longer, more photons reach the sensor. Each photon generates electrons, and the accumulated electrons produce a **brighter image**. From a purely photometric point of view, this strategy works well.

#### <span style="color:rgb(2, 141, 192)">The problem with moving objects</span>
![[Pasted image 20251021140515.png|500]]
However, this solution works **only if the object is perfectly still**.

In most practical measurement scenarios—especially in human motion analysis—the object is **moving**. During a long integration time:

- a point in object space does not remain fixed,
- its projection moves across different positions on the image plane.
    
As a result, instead of accumulating light at a single pixel, the sensor accumulates light along a **trajectory**. This produces a **blurred image**, not because of optics, but because of motion.

This phenomenon is known as **motion blur** (or _photomotion blur_), and it occurs whether:
- the object moves,
- or the camera itself moves.
    
#### <span style="color:rgb(2, 141, 192)">Short exposure as a solution</span>

To reduce motion blur, the **integration time must be short**.
With a short exposure:

- the object moves very little during the acquisition,
- each point is projected onto approximately the same pixel,
- motion-induced blurring becomes negligible.
    
However, shortening the exposure time reduces the amount of collected light, making the image **darker**.
#### <span style="color:rgb(2, 141, 192)">Fundamental trade-off</span>

We are therefore faced with another fundamental trade-off:

- **Long integration time**  
    → brighter image, but motion blur if the object moves
- **Short integration time**  
    → sharp image for moving objects, but less light
    
This trade-off between **light intensity** and **motion speed** is one of the central constraints in optical measurement systems.

The use of **lenses**, larger apertures, and more sensitive sensors is precisely aimed at relaxing this trade-off by allowing enough light to be collected even with short exposure times.

### <span style="color:rgb(161, 40, 226)">From the pinhole camera to the lens-based camera</span>

Recall that this is the **basic model of the pinhole camera**. In this configuration, there is **no lens**—only a small hole, as in the classical _camera obscura_ examples shown earlier.

Now consider the same geometry **with the introduction of a lens**.

If we focus only on the **center of the lens**, the geometry is identical to the pinhole model:  
the two triangles formed by the object point, the projection center, and the image plane are the same as in the pinhole camera. In other words, a point in object space is projected through the center of the lens onto the image plane exactly as it would be through a pinhole.

#### <span style="color:rgb(2, 141, 192)">Role of a converging lens</span>

![[Pasted image 20260104211956.png]]
However, a **converging lens** has an additional and crucial property.

Consider another ray coming from the same object point. When this ray passes through the lens, it is **refracted**, meaning that its direction is changed. The lens bends this ray so that it converges to **the same point on the image plane** as the ray passing through the lens center.

This is not limited to just two rays.  
**All rays** coming from the object point and passing through different points of the lens are refracted in such a way that they converge onto a **single image point**.

The consequences are fundamental:
- A **single point in object space** is mapped to a **single point on the image plane** → **sharp image**
- Many rays contribute to the same point → **high illumination**
    
Thus, compared to the pinhole camera, the lens-based camera provides **much more light** while preserving sharpness.
#### <span style="color:rgb(2, 141, 192)">A key difference with respect to the pinhole camera</span>

However, there is an important difference between these two systems.

In the **pinhole camera**, if you move the image plane along the optical axis (the (z)-axis):
- the image becomes larger or smaller,
- but it remains **in focus**.
    
The distance between the pinhole and the image plane acts only as a **scaling factor**. The object is always sharp, regardless of where the image plane is placed.

#### <span style="color:rgb(2, 141, 192)">Focus in a lens-based camera</span>
![[Pasted image 20260104212025.png]]
This is **not true** when a lens is used.

If you move the image plane closer to or farther from the lens, you will notice that the refracted rays no longer converge to the same point. Instead, they intersect the image plane at **different locations**.

As a result:
- a single point in object space is projected as a **bright but extended spot**,
- the image becomes **blurred**.
    
This blur occurs because the image plane is no longer located at the correct position where the rays converge.

#### <span style="color:rgb(2, 141, 192)">Focal plane and focusing</span>

The plane where rays from a point converge to a single image point is called the **focal plane**, and its position depends on the **focal length** (or optical power) of the lens.

When you **focus a camera**, you are physically moving the image plane (or equivalently the lens) forward or backward so that the sensor lies exactly on this focal plane.
#### <span style="color:rgb(2, 141, 192)">Summary: pinhole vs lens</span>

- **Pinhole camera**
    - No need for focusing
    - Always in focus
    - Very low light efficiency
- **Lens-based camera**
    - Requires focusing
    - Only one plane is perfectly in focus
    - High light efficiency
        
By introducing a lens, we gain brightness and sharpness—but we lose the very convenient property of being **always in focus**.

### <span style="color:rgb(161, 40, 226)">Focal length and the thin lens equation<br></span>
![[Pasted image 20251021141808.png]]
The **focal length** ( f ) is defined through the following relationship, known as the **thin lens equation**  
$$\frac{1}{\zeta_0} + \frac{1}{\zeta_1} = \frac{1}{f}$$
This equation describes how to correctly place the **image sensor** so that it lies on the **focus plane** of the lens system.
- ($\zeta_0$) is the distance from the object to the lens
- ($\zeta_1$) is the distance from the lens to the image plane (sensor)
- ($f$) is a characteristic property of the lens, called the **focal length**
    
#### <span style="color:rgb(2, 141, 192)">Physical meaning of the focal length</span>

The focal length can be defined as the **distance from the lens to the image plane where parallel rays converge**.

In practice, this corresponds to rays coming from an object located at **infinite distance**. For example, if you image the Sun, which is extremely far from the Earth, the incoming rays can be considered parallel. These rays converge to a single point located exactly at a distance ( f ) from the lens. In the thin lens equation, when one of the distances goes to infinity (for example ( $\zeta_0 \to \infty$ ), the equation reduces to:
$$\frac{1}{\zeta_1} = \frac{1}{f}  $$
which means that the image plane must be placed at a distance equal to the focal length.

⚠️ **Important safety note:**  
Imaging the Sun without proper precautions is extremely dangerous. Concentrating all incoming solar radiation onto a single point can generate very high temperatures and may damage the sensor or even cause fires. This experiment should never be performed without appropriate protection.
#### <span style="color:rgb(2, 141, 192)">Lens power and diopters</span>

Another way to characterize a lens is through its **optical power**, which is measured in **diopters**.
The optical power ($D$) is defined as the reciprocal of the focal length:
$$D = \frac{1}{f}$$
where:
- ($f$) is expressed in **meters**
- ($D$) is expressed in **diopters**

Thus:
- a short focal length corresponds to a **high-power lens** 
- a long focal length corresponds to a **low-power lens**
    
This definition is widely used in optics and ophthalmology to quantify the focusing capability of lenses.

## <span style="color:rgb(239, 179, 1)">Practical implementation of lenses</span>
![[Pasted image 20251021141822.png|500]]
In practice, when using lenses, we aim to obtain images that are as **accurate and reliable** as possible for measurement purposes.

Up to this point, we have not considered **image distortion**. Ideally, a square object in the scene should appear as a square on the image plane. The image may be scaled or transformed (for example, a rectangle may become a parallelogram if the viewing geometry changes), but the fundamental geometry should remain consistent.

Once distortion is introduced, this ideal behavior no longer holds.
### <span style="color:rgb(161, 40, 226)">Desired image properties</span>

For accurate measurements, an image should satisfy several key requirements:

- **Sharpness**: The image must be in focus. Blur leads to errors in point localization.
- **Low distortion**: Geometric distortion should be minimized so that spatial measurements remain accurate.
- **High contrast**: Features must be clearly distinguishable from the background.
- **Correct color reproduction**: Colors should be faithfully represented (e.g., red objects appear red, blue objects appear blue).
### <span style="color:rgb(161, 40, 226)">Lens selection criteria</span>

When choosing a lens, several factors must be considered:
![[Pasted image 20251021141832.png|500]]
#### <span style="color:rgb(2, 141, 192)">Field of view (FOV)</span>

The **field of view** is the angular extent of the scene captured by the camera. It determines how much of the object space is visible.

- A **narrow field of view** allows you to observe a small portion of the scene with high detail.    
- A **wide field of view** allows you to observe a larger portion of the scene.
    

The required field of view strongly depends on the specific application.

#### <span style="color:rgb(2, 141, 192)">Light-gathering capability</span>

Another important factor is the **amount of available light** the lens can collect. This corresponds to how many photons reach the sensor and are converted into electrical signals (electrons). Lenses that transmit more light improve image quality, especially in low-light conditions.

#### <span style="color:rgb(2, 141, 192)">Cost</span>

Lens performance and cost are closely related. High-performance lenses that offer low distortion, high sharpness, and high light-gathering capability tend to be significantly more expensive.

### <span style="color:rgb(161, 40, 226)">Types of lenses</span>

Common lens types include:

- **Telephoto lenses**:  
    These have a very **narrow field of view** and are used to image distant objects with high detail.
- **Normal lenses**:  
    These provide a field of view similar to human vision and are often used as a reference.
- **Wide-angle lenses**:  
    These have a **large field of view**, allowing a large portion of the scene to be captured.
- **Fisheye lenses**:  
    These provide an **extremely wide field of view**, often with strong geometric distortion.
    
In general, as lens performance improves—particularly in terms of low distortion and high light sensitivity—the price increases significantly.

### <span style="color:rgb(161, 40, 226)">Example of Small Field of View</span>
![[Pasted image 20251021142703.png]]
This is the first example of a **small field of view**. A small field of view is obtained by using a **long focal length** lens.

The distance indicated here corresponds to the **focal length** of the lens, usually denoted by ( f ). When the focal length is large, the imaging plane “sees” the external world through a **small angular aperture**. As a result, the captured angle is narrow.

Because of this narrow angle, the light rays do not diverge significantly, and the resulting image appears **magnified**. Objects that may be located tens or even hundreds of meters away appear relatively close when imaged with a long focal length lens.

In this configuration:
- The **field of view is narrow**.
- **Geometric distortion is minimal**.
    
You can observe that straight structures, such as walls, maintain their right angles (approximately 90°), and **parallel lines in the real world remain parallel** in the image. This low level of distortion is a characteristic advantage of lenses with long focal lengths.

### <span style="color:rgb(161, 40, 226)">Large Field of View Example</span>
![[Pasted image 20251021142715.png]]
Conversely, if you are interested in a **large field of view**, typically in the range of **70 to 120 degrees**, you should use **wide-angle lenses**, which are characterized by a **very short focal length**.

This short focal length is indicated here and can be directly compared with the long focal length used in the previous example. With a long focal length, the camera is able to image objects that are very far away, but only within a **small angular range**. In contrast, when using a short focal length lens, the captured angle becomes **much wider**.

As the field of view increases, **geometric distortions** begin to appear. In the image, you can observe that walls which should ideally appear flat and straight instead show noticeable **curvature**. This effect is a typical consequence of wide-angle optics and becomes more pronounced as the focal length decreases.

## <span style="color:rgb(239, 179, 1)">Shutter</span>
![[Pasted image 20251021142729.png|500]]

As mentioned earlier, there are two different mechanisms often referred to as _shutters_. One of them is used to control **how much light reaches the sensor**. This is achieved, for example, by **movable blades** that increase or decrease the size of the pupil, known as the **aperture**.
![[Pasted image 20251021142739.png|500]]
The aperture is located in front of the lens. By closing the aperture, you reduce the amount of light coming from the external world, resulting in a **darker image**.

A natural question arises: _why reduce the light using the aperture instead of simply reducing the integration (exposure) time_, which would have a similar effect?

The reason is that closing the aperture **blocks the peripheral regions of the lens**. These peripheral areas are typically responsible for **optical distortions and aberrations**. By limiting light to the central part of the lens, the image quality improves.

Therefore, although the image becomes darker, it is **optically more accurate**, with reduced distortions and a representation that is closer to the true geometry of the observed scene.

### <span style="color:rgb(161, 40, 226)">Aperture and F-number</span>
![[Pasted image 20251021142751.png|500]]
The aperture is usually defined and specified using **F-numbers**. Typical values are **f/1, f/2.8, f/8, f/11, f/16**, and so on.

These numbers represent the **ratio between the focal length of the lens and the diameter of the entrance pupil**. In other words, the F-number is defined as:

$$f\text{-number} = \frac{\text{focal length}}{\text{aperture diameter}}$$

If you use a **very wide aperture** (small F-number), almost the entire lens is used. This results in **brighter images**, but also increases **optical distortions and aberrations**.

If you **close the aperture** (large F-number), less light reaches the sensor. The image becomes **darker**, but optical quality improves because distortions are reduced.

In addition, changing the aperture also affects the **depth of field**. While the **field of view** refers to the angular extent of the scene captured at a given distance, the **depth of field** describes the range of distances over which objects appear in acceptable focus.

### <span style="color:rgb(161, 40, 226)">Depth of Field</span>
![[Pasted image 20251021142804.png|500]]
Depth of field is a different concept from field of view. It refers to the range of distances from the camera within which objects appear **in focus**. Objects that are very close to the camera or very far away from it appear blurred, while objects that lie within a certain distance range—the so-called **depth of field**—are sharp.

When you **close the aperture** (that is, use a larger F-number), the **depth of field increases**. This can be understood intuitively: when the aperture becomes very small, approaching a pinhole, the focusing problem almost disappears, and objects at different distances all appear in focus.
![[Pasted image 20251021143451.png|500]]
This happens because, with a **pinhole camera**, there is no specific focal plane: the image remains in focus regardless of where the image plane is placed, and changing its position only affects the image scale.

With a **lens-based camera**, instead, there is a **specific focal plane** determined by the lens properties. Objects lying exactly on this plane are in perfect focus. As you move away from this plane, the image becomes progressively blurred. The distance between the nearest and farthest points that still appear acceptably sharp defines the **depth of field**.

## <span style="color:rgb(239, 179, 1)">Exposure Duration</span>
![[Pasted image 20251021143503.png|500]]
In the early days of photography, exposure was controlled in a very rudimentary way. 

![[Pasted image 20251021143531.png|400]]
Photographers simply covered the lens, removed the cover to take the picture, and then put it back on again—asking people to remain perfectly still during the process. This was, of course, the very beginning of photographic art.

Later, an important idea was introduced: instead of relying on ambient light, photographers used a **very powerful flash**, often based on burning magnesium. The cover was removed, but the environment was kept dark enough that no image was formed until the flash was fired. Since the flash produced an extremely intense light for a very short time, it effectively defined the exposure duration.

![[Pasted image 20251021143540.png|500]]

Today, we no longer use this method. Instead, exposure is controlled using **mechanical shutters** or **electronic shutters**.

A **mechanical shutter** consists of moving blades. These blades open very rapidly to reach the selected aperture (defined by the f-stop), remain open for the desired exposure time, and then close again very quickly. The opening and closing typically take only a few hundred microseconds, while the exposure time itself can range from about **1 millisecond up to several hundred milliseconds**, depending on how much light needs to be integrated on the sensor or film. This is the shutter mechanism that originally produced the characteristic “click” sound in cameras. In modern digital cameras, this sound is often simulated electronically, even though no mechanical movement may be present.

![[Pasted image 20251021143554.png|500]]
With **solid-state sensors**, such as CMOS or CCD sensors, exposure can also be controlled using an **electronic shutter**. In this case, the process works by first clearing all the electrical charge stored in the sensor, then integrating light for a precisely controlled time interval (which can be as short as a few hundred microseconds), and finally reading and storing the image. After that, the sensor is reset again to prepare for the next exposure. Since there are no moving parts, electronic shutters operate silently.

# <span style="color:rgb(223, 109, 109)">Measurements in the Pinhole Camera Model</span>

In this section, we focus on **measurements using the pinhole camera model**, ignoring lens effects.
![[Pasted image 20251021143908.png|500]]
## <span style="color:rgb(239, 179, 1)">Image Scale<br></span>
![[Pasted image 20251021143924.png|600]]
The **image scale** ($M$) describes how distances in **object space** correspond to distances in **image space**. It can be defined as the ratio of measurements between these two spaces:
$$M = \frac{\text{distance in image plane}}{\text{distance in object space}}$$
More specifically, $M$ depends primarily on the ratio of distances along the **Z-axis**:
$$M \propto \frac{Z_{\text{lower}}}{Z_{\text{upper}}}$$
- **$Z_{\text{upper}}$**: Distance from the camera to the reference plane in object space
- **$Z_{\text{lower}}$**: Distance in the plane being imaged
    
> The position of the plane in space directly determines the **scaling of the image**.

## <span style="color:rgb(239, 179, 1)">Historical Context</span>

- After **World War I**, large cameras were used for aerial surveys.
- These cameras were **mechanically precise**, allowing accurate measurement of **landmark positions** on the ground.
- Measurement involved using **mechanical systems** to determine positions of landmarks on **films or photographs** captured during the survey.

# <span style="color:rgb(223, 109, 109)">Camera Model and 3D-to-2D Mapping</span>

In this section, we describe how to **map the 3D world onto a 2D image** using a **central projection**.

## <span style="color:rgb(239, 179, 1)">Central Projection System</span>
![[Pasted image 20251021143936.png]]
A central projection system consists of:
1. A **camera reference frame** (fixed with the camera).
2. A **camera center** (also called the **perspective center**).
3. An **image plane** where 3D points are projected.
    
**Key principle**: All points from the object space, the corresponding point on the image plane, and the camera center are **collinear**.

- This **collinearity** is the foundation of the **pinhole camera model**.
- Let $P_0$ represent the **sensor reference frame** on the image plane relative to the global reference frame.
- The **principal axis** passes through the **origin of the image plane reference frame** and the **camera center**.
    
### <span style="color:rgb(161, 40, 226)">Projection of 3D Points</span>

A 3D point $(X, Y, Z)$ in object space is projected onto a 2D point $(X', Y')$ on the image plane:

$$(X, Y, Z) \quad \xrightarrow{\text{projection}} \quad (X', Y')$$

> **Important:** This transformation is **one-way**. You cannot uniquely reconstruct the original 3D point from a single 2D image because **all points along the line from the camera center through the projected point map to the same sensor point**.

### <span style="color:rgb(161, 40, 226)">Mathematical vs. Physical Model</span>

- In the **mathematical implementation**, the image plane can be placed **in front of the perspective center**, resulting in a non-upside-down image.
    
- In the **physical pinhole camera**, the plane is **behind the perspective center**, producing a physically buildable system where the image is typically upside-down.

| Model        | Plane Position     | Physical Implementation? | Image Orientation |
| ------------ | ------------------ | ------------------------ | ----------------- |
| Mathematical | In front of center | ❌ No                     | Not upside-down   |
| Physical     | Behind center      | ✅ Yes                    | Upside-down       |

Both models yield almost the same results; the main difference is **image orientation** and whether the system can be physically constructed.




