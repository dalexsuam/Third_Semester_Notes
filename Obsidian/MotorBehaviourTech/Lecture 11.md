
28/10/2025
***
# <span style="color:rgb(223, 109, 109)">Assumptions for Good Image Formation</span>

To obtain **accurate and well-focused images**, certain assumptions are made in the **camera model**. When these assumptions do not hold, **errors called aberrations** may occur.

> **Note:** Aberrations are mainly caused by lenses.  
> **Pinhole cameras** (without lenses) do not exhibit these lens-induced aberrations.

![[Pasted image 20251021144505.png|500]]
## <span style="color:rgb(239, 179, 1)">Main Assumptions</span>

1. **Single intersection of rays**
    - All rays from an **object point** intersect at a **single point** (the **perspective center** or **camera center**)
    - Result: Image is **well-focused**, with no blur
2. **Planarity of image points**
    - All image points lie on a **single plane** (the **image plane**)
    - Result: Perfect geometric alignment
3. **Straight-line projection**
    - Rays from object points to image points are **straight lines**
4. **Orthogonal axes**
    - The coordinate axes of the camera reference frame are **orthogonal**
5. **Single focal length**
    - Only **one focal length** is used, leading to a **unique image scale $M$**
        
### <span style="color:rgb(161, 40, 226)">Consequences of Violating Assumptions</span>

- When assumptions are not satisfied, **image imperfections occur**, including:
    - **Lens distortions**
    - **Aberrations**
    - **Misalignment of projected points**
- These imperfections often require **special processing**, such as **distortion correction**.
    
### <span style="color:rgb(161, 40, 226)">Practical Note</span>

- Aberrations are especially important in applications where the **precise position of points in the image** matters (e.g., photogrammetry, aerial surveys).
- Grids observed on the image plane are **projections of regular object-space grids**, and deviations from regularity indicate the presence of aberrations.

# <span style="color:rgb(223, 109, 109)">Aberrations (Lens Errors)<br></span>
**Aberrations** are **deviations from the ideal mapping** caused by lenses. They occur when a real lens **does not perfectly follow the pinhole camera assumptions**, leading to image imperfections.
![[Pasted image 20251021144518.png|500]]
## <span style="color:rgb(239, 179, 1)">Main Types of Aberrations<br></span>
1. **Distortion**
    - Geometric deviation where straight lines in object space appear curved in the image.
    - Example: barrel or pincushion distortion.
2. **Spherical Aberration**
    - Rays passing through the edges of a spherical lens focus at different points than rays near the center.
    - Result: Image blur.
3. **Chromatic Aberration**
    - Different wavelengths (colors) of light are focused at different points.
    - Result: Color fringing around edges.
4. **Astigmatism**
    - A point object is imaged as a line or ellipse instead of a point due to uneven focusing along different axes.
5. **Comatic Aberration (Coma)**
    - Off-axis point sources appear as comet-shaped blurs instead of points.
6. **Vignetting**
    - Image brightness decreases toward the edges of the image.
        

> **Note:** Pinhole cameras **do not exhibit lens aberrations**, because they have no lens. Aberrations are relevant when **using real lenses**.


## <span style="color:rgb(239, 179, 1)">Distortion (Lens Aberration)</span>

**Distortion** is one of the **most important aberrations** for many applications, because it **displaces the positions of points on the 2D image plane**.

### <span style="color:rgb(161, 40, 226)">How Distortion Works</span>
![[Pasted image 20251021144809.png|500]]
- Consider a **regular grid** of perfect squares in object space.
- After projection through a lens, the grid **no longer appears as perfect squares** — the shapes are **distorted**.
- This displacement affects **point positions**, which can lead to **incorrect 3D reconstructions** if not corrected.
    
### <span style="color:rgb(161, 40, 226)">Common Types of Distortion</span>

1. **Barrel Distortion**
    - Image magnification **decreases with distance from the center**.
    - Straight lines appear **curved outward**.
2. **Pincushion Distortion**
    - Image magnification **increases with distance from the center**.
    - Straight lines appear **curved inward**.
3. **Mustache Distortion**
    - A combination of barrel and pincushion distortion.
    - Produces a **wavy distortion** pattern.
        
> **Important:** If a point is displaced in the 2D image due to distortion, its **reconstruction in 3D space will be incorrect**.

### <span style="color:rgb(161, 40, 226)">Practical Implication</span>
![[Pasted image 20251021144828.png|500]]
- **Distortion correction** is necessary **before retro-projecting points into space**.
- This ensures **accurate measurements** and **precise 3D reconstruction**.

# <span style="color:rgb(223, 109, 109)">Measurements (Pinhole 'o' model): Homogeneous Coordinates</span>
![[Pasted image 20260105143854.png]]

We were exploring the model of the **pinhole camera**, and in particular how the **object space** is projected onto the **image space**. Let us continue with this topic.

This is the model that I have already shown you. We have the **camera center**, also called the **perspective center** ($C$), and a local reference frame defined by the axes ($X,Y, Z$). The ($Z$)-axis is orthogonal to the image plane. Any point in space ($P$) is projected onto its image point ($p$) on the sensor through the camera center.
![[Pasted image 20260105144014.png|400]]
We have seen that the sensor plane can be placed either **in front of** or **behind** the camera center. The only difference between these two configurations is a **change of sign in the coordinates** and a **vertical inversion of the image**. From a mathematical point of view, however, the two configurations are completely equivalent.
![[Pasted image 20260105143854.png]]
The projection of a point ($P$) in object space onto its corresponding point ($p$) on the image plane is performed through a **projection matrix**, which I am showing you here. In this matrix, the terms ($f$) represent the **focal length** of the optical system. As we have already seen, the focal length is directly related to the **field of view** of the camera: the longer the focal length, the narrower the field of view, and vice versa.
![[Pasted image 20260105144415.png]]
Since we are working with **homogeneous coordinates**, a point in space is represented by a four-dimensional vector $([X, Y, Z, 1]^T)$. One important property of homogeneous vectors is that multiplying the vector by any non-zero scalar ( $\lambda$ ) represents the same point in space. This property is fundamental for projective geometry.

When we apply the projection matrix to the 3D point, we obtain a vector in the image space with three components, but only **two of them are independent**, since the image lies on a plane. By dividing the resulting vector by the ( Z )-coordinate, we recover the actual image coordinates. This division does not change the point, because homogeneous vectors are defined up to a scale factor.

The overall projection from object space to image space can therefore be written using a matrix that contains the focal length terms. After multiplication, we obtain that the image coordinates are equal to:   
$$x = \frac{f X}{Z}, \quad y = \frac{f Y}{Z}  $$
This shows that the factor ( $\frac{f}{Z}$ ) acts as a **scaling factor** for the image coordinates. If the depth ($Z$) is fixed, changing the focal length directly changes the scale of the projected point. This result comes directly from the geometry of **similar triangles** in the pinhole camera model.

![[Pasted image 20260105143854.png]]
Here, I am showing a section of the object space in the ($XZ$)-plane. You can see that **all points in space that project onto the same image point ( p )** lie along a **single straight line** passing through the camera center ( C ). This means that, from a single image, we cannot determine the exact 3D position of a point: the point could be anywhere along that line.
![[Pasted image 20260105144415.png]]
As a consequence, the projection transformation **cannot be inverted** using a single camera alone. To recover the 3D position of points, we need additional information, such as measurements from **another camera** observing the same scene from a different viewpoint. This is the fundamental reason why **one camera is not sufficient** for three-dimensional reconstruction.

This is the basic transformation underlying image formation in the pinhole camera model.

## <span style="color:rgb(239, 179, 1)">Additional Aspects</span>

There are some additional aspects that we must take into account, which are related to the **real implementation of cameras**.

The first important aspect concerns the **position**, that is, the relationship between the **sensor reference frame** and the **principal point**. I remind you that the **principal point** is defined as the intersection of the optical axis (the $( Z )-axis$) with the image plane.
![[Pasted image 20260105145520.png]]
In practice, image sensors have their own **two-dimensional reference frame**, which may also be **rotated** with respect to the camera reference frame. In the example shown here, the sensor reference frame is **not rotated**, but its origin is **displaced** with respect to the principal point. In particular, the origin of the sensor reference frame is not located at the center of the image, but at one of the corners. It could also be located at a different corner, for example an upper corner.

This happens because sensors are typically **read out starting from one corner**, not from the center. The scanning process follows rows and columns beginning at that corner, which naturally defines the sensor’s coordinate system.

This situation does not represent a major challenge. To account for this displacement, we simply need to **translate the coordinates** from the sensor reference frame to a reference frame centered at the principal point. This can be done very easily by adding a constant offset to the measured coordinates.
![[Pasted image 20260105145558.png]]
More specifically, we introduce the coordinates ($p_x$) and ($p_y$), which represent the position of the **principal point expressed in the sensor reference frame**. These values indicate how far the principal point is from the sensor origin along the horizontal and vertical directions.

Therefore, for any measured point on the sensor, we simply add the vector  
$$\mathbf{p} = \begin{bmatrix} p_x \ p_y \end{bmatrix}^T$$
to the sensor coordinates. This translation effectively moves the origin of the coordinate system from the sensor corner to the principal point, aligning the measurements with the camera model we have previously defined.

Then we basically have
$$(X,Y,Z)^T\rightarrow\left(\frac{fX}{Z}+p_x, \frac{fY}{Z}+p_y\right)^T
$$
Now we need to **place this translation vector within the projection chain**.

As you can see, it is straightforward to incorporate it directly into the **projection matrix**, which previously contained only the focal length. By doing so, we can include the coordinates of the **principal point expressed in the sensor reference frame**.

If you perform the matrix multiplication explicitly, you will see that it produces exactly the expected result. In particular, when you multiply the first row of the projection matrix by the 3D point vector, you obtain:    
$$f \frac{X}{Z} + p_x \frac{Z}{Z} = f \frac{X}{Z} + p_x$$
and similarly for the second coordinate. This confirms that the coordinates of the projected point are shifted by ($p_x$) and ($p_y$), which correspond to the position of the principal point on the sensor.

At this point, the projection model becomes slightly more complex, but also more realistic.

## <span style="color:rgb(239, 179, 1)">Compact matrix formulation</span>

Instead of writing all scalar equations explicitly, we can now express the projection in a **compact matrix form** using homogeneous coordinates.
![[Pasted image 20260105150937.png|300]]
The projected point ( $\tilde{\mathbf{p}}$ ) (a ( $3 \times 1$ ) vector in image space) can be written as:  
![[Pasted image 20260105150734.png|200]]
Here:

- ( $\lambda$) is a scalar factor introduced because we are working with **homogeneous coordinates** (any nonzero scalar multiple represents the same point),
- ( $\tilde{\mathbf{P}}$) is the point in 3D homogeneous coordinates,
- ( $\mathbf{I}$ ) is the ( $3 \times 3$ ) identity matrix,
- ( $\mathbf{0}$ ) is a zero vector,
- ( $\mathbf{K}$ ) is the **camera calibration matrix**, also called the **intrinsic matrix**.
![[Pasted image 20260105150826.png|400]]
![[Pasted image 20260105150855.png|200]]
The matrix ( $\mathbf{K}$ ) includes the intrinsic parameters of the camera, such as the focal length and the coordinates of the principal point. By multiplying ( $\mathbf{K}$ ) with the matrix ( $\mathbf{I} \mid \mathbf{0}$ ), we map a point from object space directly into image space.

### <span style="color:rgb(161, 40, 226)">Metric cameras and calibration</span>

When I previously showed you the example of a camera used for mapping landmarks, those devices were called **metric cameras**. They were designed so that the elements of the projection matrix—specifically, the intrinsic parameters contained in ( $\mathbf{K}$ )—were **known, fixed, and accurately measured**.

Because of this, users did not need to perform camera calibration: the camera was already calibrated by construction. This is the reason they are called _metric_ cameras.

In contrast, most general-purpose cameras do **not** have fixed intrinsic parameters. In particular:

- the **focal length** can vary due to zoom lenses,
- in older film cameras, even the position of the image center could change.
    
Today, film cameras are no longer used for measurement purposes. Modern cameras are all **solid-state sensors**, which means that the principal point coordinates ( $p_x$ ) and ( $p_y$ ) are fixed. However, the focal length ( $f$ ) may still vary depending on the lens configuration.

For this reason, **camera calibration is necessary** before performing any accurate measurement. If these intrinsic parameters are not measured correctly, the resulting 3D reconstruction or spatial measurement will contain systematic errors.

## <span style="color:rgb(239, 179, 1)">Introducing camera pose: rotation and translation</span>

Up to now, all the reference frames we have used were **coincident with the global reference frame**.
![[Pasted image 20260105145520.png]]
In the examples shown so far:

- the **sensor reference frame** was aligned with the **camera reference frame**,
- the camera axes were not rotated with respect to the global axes,
- and the 3D point in space, the camera center, and the image plane were all expressed in the **same coordinate system**.
    
This is a convenient assumption for introducing the projection model, but it is **not realistic** in practical measurement systems.

### <span style="color:rgb(161, 40, 226)">Multiple cameras and non-coincident reference frames</span>
![[Pasted image 20260105151933.png]]
In real applications—especially when using **two or more cameras**—each camera occupies a different position in space and has a different orientation.

If two cameras had exactly the same position and orientation, they would be coincident, and stereo reconstruction would be impossible. Therefore, at least one camera must be:

- **translated** with respect to the global reference frame,
- **rotated** with respect to the global axes.

As a result, each camera is characterized by:
- a **rotation matrix** ( $\mathbf{R}$ ),
- a **translation vector** ( $\mathbf{T}$ ).
    
These two quantities together define the **pose of the camera** in the global reference frame.

### <span style="color:rgb(161, 40, 226)">Coordinate transformation between global and camera frames</span>

Let:

- ( $\mathbf{P}_G = (X_G, Y_G, Z_G, 1)^T$ ) be a point expressed in the **global reference frame**,
- ( $\mathbf{P}_C = (X_C, Y_C, Z_C, 1)^T$ ) be the same point expressed in the **camera reference frame**.
    
The transformation from global coordinates to camera coordinates is given by a **rigid-body transformation**:  
![[Pasted image 20260105152542.png|500]]
Here:

- ( $\mathbf{R}$ ) is a ( $3 \times 3$ ) rotation matrix,
- ( $\mathbf{T}$ ) is a ( $3 \times 1$ ) translation vector representing the position of the camera center with respect to the global origin,
- the full matrix is a ( $4 \times 4$ ) homogeneous transformation matrix.
    

This matrix converts coordinates **from the global reference frame to the camera reference frame**.

---

### <span style="color:rgb(161, 40, 226)">Updated projection chain</span>

Because of this, the projection from 3D space to the image plane is **no longer a single-step operation**.

Instead, it consists of two consecutive transformations:

1. **Extrinsic transformation**  
    Converts a point from the global reference frame to the camera reference frame:  
    $$\mathbf{P}_G \rightarrow \mathbf{P}_C$$
2. **Intrinsic projection**  
    Projects the point from the camera reference frame onto the image plane using the camera calibration matrix ( $\mathbf{K}$ ):  
    $$\mathbf{P}_C \rightarrow \tilde{\mathbf{p}}$$
Putting everything together:  
$$\tilde{\mathbf{p}} = \lambda \mathbf{K}  [\mathbf{R} \mid \mathbf{T}]  \tilde{\mathbf{P}}_G  $$

This matrix:  
$$\mathbf{P} = \mathbf{K} [\mathbf{R} \mid \mathbf{T}]  $$
is called the **camera projection matrix**.

### <span style="color:rgb(161, 40, 226)">Key takeaway</span>

- ( $\mathbf{K}$ ) contains the **intrinsic parameters** (focal length, principal point, pixel scaling),
- ( $\mathbf{R}$ ) and ( $\mathbf{T}$ ) contain the **extrinsic parameters** (camera orientation and position),
- Accurate 3D reconstruction and triangulation require **both** intrinsic and extrinsic calibration.
    
## <span style="color:rgb(239, 179, 1)">Camera Projection with Rotation and Translation (Extrinsic + Intrinsic Parameters)</span>

![[Pasted image 20260105145520.png]]
Until now, we assumed that all reference frames coincided:
- the **global (world) reference frame**,
- the **camera reference frame**, and
- the **sensor (image) plane reference frame**.
    
In that simplified case, a 3D point was projected onto the image plane using only the **intrinsic calibration matrix** ( K ).

However, this situation is unrealistic in practice. As soon as we use **multiple cameras**, each camera:
![[Pasted image 20260105151933.png]]

- is located at a **different position** in space, and
- has a **different orientation** with respect to the global reference frame.
    
Therefore, we must explicitly account for **camera rotation and translation**.
### <span style="color:rgb(161, 40, 226)">Camera Pose: Rotation and Translation<br></span>
Each camera is characterized by:

- a **rotation matrix** ($\mathbf{R}$ ), describing the orientation of the camera reference frame with respect to the global reference frame;
- a **translation vector** ( $\mathbf{C}$ ), representing the position of the **camera center** in global coordinates.

These parameters are called the **extrinsic parameters** of the camera.

From the slide:

- ( $\mathbf{R}$ ): rotation between camera and global reference frames
- ( $\mathbf{C}$ ): camera origin position in the global frame
- ( $\mathbf{R}, \mathbf{C}$ ) are included in the transformation matrix ( $\mathbf{H}$ )


### <span style="color:rgb(161, 40, 226)">From Global Coordinates to Camera Coordinates</span>

Let:
- ( ${}^{g}\tilde{\mathbf{P}}$ ) be a 3D point expressed in **global homogeneous coordinates**,
- ( ${}^{c}\tilde{\mathbf{P}}$ ) be the same point expressed in the **camera reference frame**.

The transformation from global to camera coordinates is obtained using the **inverse of the camera-to-global transformation**.

If the camera-to-global transform is defined by ( $(\mathbf{R}, \mathbf{C})$ ), then the **global-to-camera transform** is:
$$  
{}^{c}\tilde{\mathbf{P}}=
\begin{bmatrix}  
\mathbf{R}^T & -\mathbf{R}^T \mathbf{C} \\  
\mathbf{0}^T & 1  
\end{bmatrix}  
{}^{g}\tilde{\mathbf{P}}  
$$
This matrix contains:
- ( $\mathbf{R}^T$ ): inverse rotation,
- ( $-\mathbf{R}^T \mathbf{C}$ ): translation expressed in the camera frame.

### <span style="color:rgb(161, 40, 226)">Projection onto the Image Plane</span>

Once the point is expressed in the **camera reference frame**, we can apply the **pinhole projection model**.

Using homogeneous coordinates, the image point ( $\tilde{\mathbf{p}}$ ) is given by:


$$\tilde{\mathbf{p}}=

\lambda  \mathbf{K}  
\begin{bmatrix}  
\mathbf{I} & \mathbf{0}  
\end{bmatrix}  
{}^{c}\tilde{\mathbf{P}}  
$$
Substituting the global-to-camera transformation:
$$\tilde{\mathbf{p}}=

\lambda  \mathbf{K}  
\begin{bmatrix}  
\mathbf{I} & \mathbf{0}  
\end{bmatrix}  
\begin{bmatrix}  
\mathbf{R}^T & -\mathbf{R}^T \mathbf{C}  
\end{bmatrix}  
{}^{g}\tilde{\mathbf{P}}  $$
Since only the first three rows are needed for projection, this simplifies to:
$$\tilde{\mathbf{p}}=

\lambda \mathbf{K}  
\mathbf{R}^T  
\begin{bmatrix}  
\mathbf{I} & -\mathbf{C}  
\end{bmatrix}  
{}^{g}\tilde{\mathbf{P}}  $$

### <span style="color:rgb(161, 40, 226)">The Complete Camera Projection Matrix</span>

We now define the **full camera projection matrix**:

$$\mathbf{M}=
\lambda \mathbf{K}  
\mathbf{R}^T  
\begin{bmatrix}  
\mathbf{I} & -\mathbf{C}
\end{bmatrix}
=
\lambda  \mathbf{K}\mathbf{H}  $$

where:
- ( $\mathbf{K}$ ) contains the **intrinsic parameters**:  
    $$\mathbf{K} =  
    \begin{bmatrix}  
    f & 0 & p_x \\
    0 & f & p_y \\ 
    0 & 0 & 1  
    \end{bmatrix}$$
    
-  $$\mathbf{H} = \mathbf{R}^T [ \mathbf{I} \mid -\mathbf{C}]$$contains the **extrinsic parameters**.

The final projection equation becomes:
  
$$\tilde{\mathbf{p}} = \mathbf{M} {}^{g}\tilde{\mathbf{P}} $$

### <span style="color:rgb(161, 40, 226)">Degrees of Freedom Interpretation (from the slide)</span>
![[Pasted image 20260105154858.png|500]]
- **Intrinsic parameters (3 DOF)**:
    - focal length ( f ),
    - principal point ( $(p_x, p_y)$ ).
- **Extrinsic parameters (6 DOF)**:
    - rotation ( $\mathbf{R}$ ) (3 DOF),
    - translation ( $\mathbf{C}$ ) (3 DOF).
        
➡️ The **general pinhole camera** therefore has **9 degrees of freedom**.

### <span style="color:rgb(161, 40, 226)">Key Takeaway</span>

The camera projection is fully described by:

- **Intrinsic parameters** (how the camera forms images),
- **Extrinsic parameters** (where the camera is and how it is oriented).
    
All of this information is compactly encoded in the **camera projection matrix** ( \mathbf{M} ), which maps a 3D point in the world directly onto the 2D image plane.


## <span style="color:rgb(239, 179, 1)">Non-Square Pixels and the Intrinsic Matrix</span> ( K )

Let us now look again at the **intrinsic calibration matrix** ( $\mathbf{K}$ ).

Up to now, we assumed that the camera had:
- a **single focal length** ($f$),
- a **principal point** ( $(p_x, p_y)$ ),
- and square pixels.

With this assumption, the intrinsic matrix was:

$$\mathbf{K} =  
\begin{bmatrix}  
f & 0 & p_x \\  
0 & f & p_y \\  
0 & 0 & 1  
\end{bmatrix}$$
This corresponds to **3 degrees of freedom** for the intrinsic parameters.

### <span style="color:rgb(161, 40, 226)">Why Two Focal Lengths?</span>

In reality, this assumption is not always valid.

Historically, in **film cameras**, the film could shrink differently along the horizontal and vertical directions, producing **different scalings along the (x) and (y) axes**.

Nowadays, with **solid-state sensors (CCD/CMOS)**:

- pixels may still have **different physical sizes** in the horizontal and vertical directions,
- but this difference is **fixed, known, and specified** in the sensor datasheet.
    
If the pixel size in the (x)-direction is different from the pixel size in the (y)-direction, then the same physical focal length produces **different effective focal lengths** when expressed in pixel units.

To account for this, we replace the single focal length ( f ) with **two different focal lengths**:
- ($\alpha_x$) along the (x)-axis,
- ($\alpha_y$) along the (y)-axis.
    
These parameters compensate for the non-square pixels and ensure that the **same viewing angle** is preserved in both directions.
### <span style="color:rgb(161, 40, 226)">Intrinsic Matrix with Non-Square Pixels</span>

The intrinsic matrix becomes:

$$\mathbf{K} =  
\begin{bmatrix}  
\alpha_x & 0 & p_x \\  
0 & \alpha_y & p_y \\  
0 & 0 & 1  
\end{bmatrix} $$

This introduces:
- ( $\alpha_x$ ): focal length along (x),
- ( $\alpha_y$ ): focal length along (y),
- ( $p_x, p_y$ ): coordinates of the principal point.
    
So the **intrinsic parameters now have 4 degrees of freedom** instead of 3.

### <span style="color:rgb(161, 40, 226)">Total Degrees of Freedom of the Camera Model</span>

Let us now count all the unknowns in the **complete pinhole camera model**.
#### <span style="color:rgb(2, 141, 192)">Intrinsic parameters (4 DOF)</span>

- ( $\alpha_x$ ),
- ( $\alpha_y$ ),
- ( $p_x$ ),
- ( $p_y$ ).
    
#### <span style="color:rgb(2, 141, 192)">Extrinsic parameters (6 DOF)</span>

- Rotation matrix ( $\mathbf{R}$ ): **3 DOF**
    - although ( $\mathbf{R}$ ) is a ($3 \times 3$) matrix, it depends only on **three independent parameters** (e.g. roll, pitch, yaw),
- Translation vector ( $\mathbf{C}$ ): **3 DOF**.

### <span style="color:rgb(161, 40, 226)">Final Camera Projection Matrix</span>

The full camera projection matrix is:

$$\mathbf{M} = \lambda \mathbf{K}\mathbf{R}^T  
\begin{bmatrix}  
\mathbf{I} & -\mathbf{C}  
\end{bmatrix}  $$
or equivalently:

$$\tilde{\mathbf{p}} = \mathbf{M}  \tilde{\mathbf{P}}  $$
### <span style="color:rgb(161, 40, 226)">Final Count</span>
![[Pasted image 20251021150941.png|400]]

- Intrinsic parameters: **4 DOF**
- Extrinsic parameters: **6 DOF**
    

$$\boxed{\text{Total DOF} = 10}  $$

This corresponds exactly to the **general pinhole camera model with non-square pixels**, as shown in the slide.


## <span style="color:rgb(239, 179, 1)">Skew Factor and Final Degrees of Freedom of the Camera Model</span>

There is **one additional intrinsic parameter** that we have not considered so far: the **skew factor**, usually denoted by ( s ).
![[Pasted image 20251021151011.png|400]]
### <span style="color:rgb(161, 40, 226)">What is the skew factor?<br></span>
The skew factor accounts for **non-orthogonality between the image axes** of the sensor reference frame. In other words, it models the case where the (x) and (y) axes of the image plane are **not perpendicular**.

This effect is mainly a **legacy of film-based cameras**:
- photographic films could **shrink or deform non-uniformly** during development,
- this deformation could introduce a **shearing effect**,
- as a result, the image axes would no longer be perfectly orthogonal.

### <span style="color:rgb(161, 40, 226)">Intrinsic Matrix Including Skew</span>

When the skew factor is included, the intrinsic matrix becomes:
$$\mathbf{K} =  
\begin{bmatrix}  
\alpha_x & s & p_x \\
0 & \alpha_y & p_y \\ 
0 & 0 & 1  
\end{bmatrix}$$

Where:
- ( $\alpha_x, \alpha_y$ ): effective focal lengths (possibly different due to non-square pixels),
- ( $p_x, p_y$ ): principal point coordinates,
- ( $s$ ): skew factor.
### <span style="color:rgb(161, 40, 226)">Skew in Modern Cameras</span>

With **modern solid-state sensors (CCD/CMOS)**:
- pixel grids are manufactured with **high precision**,    
- the image axes are **always orthogonal**,
- therefore, the skew factor is **zero** in practice.
    
So, for real cameras today:  
$$s = 0$$
### <span style="color:rgb(161, 40, 226)">Degrees of Freedom: Formal vs Practical</span>

If we count **all possible parameters**, the full pinhole camera model has:

#### <span style="color:rgb(2, 141, 192)">Intrinsic parameters (5 DOF)</span>
- ($\alpha_x$)
- ($\alpha_y$)
- ($p_x$)
- ($p_y$)
- ($s$)
#### <span style="color:rgb(2, 141, 192)">Extrinsic parameters (6 DOF)</span>

- Rotation ( $\mathbf{R}$ ): 3 DOF
- Translation ( $\mathbf{C}$ ): 3 DOF
$$\boxed{\text{Total formal DOF} = 11}$$
### <span style="color:rgb(161, 40, 226)">Practical Reduction of DOF</span>

In practice:
- the **skew factor (s) is zero**,
- pixel sizes in ($x$) and ($y$) are **fixed and known**,
- film shrinkage effects do **not exist** anymore.
    
Therefore, although the camera model **formally has 11 degrees of freedom**, **only 9 are effectively unknown and need to be estimated** in real-world calibration problems.


## <span style="color:rgb(239, 179, 1)">Summary of the Camera Projection Pipeline</span>
![[Pasted image 20251021151135.png|600]]
 We start with a point in the **object space (3D)**, expressed in a **global reference frame**.
- **Global → Camera transformation (H)**
    
    - Each camera has its own **position and orientation** in space.
    - These are described by:
        - Rotation matrix **R** (3 DOF)
        - Camera center **C** (translation, 3 DOF)
    - Together they form the **extrinsic transformation matrix H**, which maps points from the **global frame to the camera reference frame**.
        
- **Ideal projection (K): 3D → 2D**

    - The point in the camera reference frame is projected onto the **camera (image) plane** using the **intrinsic matrix K**.
    - This step models an **ideal pinhole camera** and performs a **perspective projection** from 3D to 2D.
    - This operation is **not invertible**:
        - from a 2D image point, we cannot recover the original 3D point,
        - only a **ray (infinite set of 3D points)** passing through the camera center.
            
- **Camera plane → Linear sensor (2D)**
    
    - The projected point is mapped onto an **ideal (linear) sensor**.
    - This sensor is a **mathematical abstraction**, assuming perfect geometry and no distortions.
    - At this stage, we are fully in **2D coordinates**.
        
- **Linear sensor → Real sensor (2D)**
    
    - Real cameras deviate from the ideal linear model.
    - **Lens-induced effects** introduce distortions such as:
        - blur,
        - radial and tangential distortions,
        - slight displacement of projected points.
    - These effects cause points to be measured in positions that differ from the ideal projection.
        
- **Final measurement**
    
    - On the **real sensor**, we finally measure the **2D coordinates** of image points.
    - These measurements are the ones used for:
        - motion analysis,
        - 3D reconstruction (with multiple cameras),
        - calibration and correction procedures.

### <span style="color:rgb(161, 40, 226)">Compact Formula Reminder</span>

- Overall projection:
$$\tilde{p} = \mathbf{M}\,\tilde{P}, \quad \mathbf{M} = \lambda\,\mathbf{K}\mathbf{R}^T [\,\mathbf{I} \mid -\mathbf{C}\,] = \mathbf{K}\mathbf{H}$$

## <span style="color:rgb(239, 179, 1)">Intrinsic and Extrinsic Parameters</span>

![[Pasted image 20251021151239.png|500]]
### <span style="color:rgb(161, 40, 226)">Extrinsic (External) Parameters</span>

- Extrinsic parameters describe the **pose of the camera in the global reference frame**.
- They consist of **6 Degrees of Freedom (DoF)**:
    - **3 rotation parameters** (e.g. roll, pitch, yaw → matrix **R**)
    - **3 translation parameters** (camera position → vector **C** or **T**)
        
- These parameters:
    - change **every time the camera is moved or rotated**,
    - must be re-estimated if the camera position changes.
        
- Practical implication:
    - If a camera is accidentally moved (e.g. someone hits it during acquisition),  
        **R and T must be recalibrated**.
    - This is critical in multi-camera measurement systems.

### <span style="color:rgb(161, 40, 226)">Intrinsic (Internal) Parameters</span>
- Intrinsic parameters describe the **internal geometry of the camera system**.
- They include:
    - focal length(s),
    - principal point coordinates (**pₓ, pᵧ**),
    - skew factor (usually zero in modern sensors),
    - pixel scaling (αₓ, αᵧ if pixels are not square).
- These parameters characterize the **camera assembly**, not its position in space.
- In principle:
    - Intrinsics are **constant over time and space** once calibrated.
- In practice:
    - They **change if the focal length changes** (e.g. zoom lenses),
    - They may change if the camera is damaged (e.g. dropped).
  
### <span style="color:rgb(161, 40, 226)">Practical Interpretation</span>

- **Extrinsics** answer the question:  
    _“Where is the camera, and how is it oriented in the world?”_
- **Intrinsics** answer the question:  
    _“How does this camera project 3D points onto the sensor?”_
- With:
    - **fixed camera + fixed lens** → intrinsics can be trusted once calibrated,
    - **movable camera or zoom lens** → calibration must be repeated.
        
## <span style="color:rgb(239, 179, 1)">Lens Distortion and Image Rectification</span>

The last transformation we have introduced is the one from the **ideal (linear) sensor** to the **real sensor**.  
This transformation accounts for **nonlinear effects**, mainly caused by **lens distortions**.
![[Pasted image 20251028141130.png|600]]
- In an ideal pinhole camera, these nonlinearities would not appear.
- However, real cameras use **lenses**, and therefore lens aberrations must be taken into account.
    
### <span style="color:rgb(161, 40, 226)">Effect of Lens Distortion</span>

- A typical effect of lens distortion is that **straight lines appear curved** in the image.
- In the example shown, the keyboard appears bent, even though it is actually straight.
- This means that:
    - a point that should lie at a certain image coordinate is **displaced**,
    - parallel lines in the scene are no longer parallel in the image.
### <span style="color:rgb(161, 40, 226)">Why Distortion Must Be Corrected</span>

- When distortion is present, the measured 2D coordinates of image points are **not their true projections**.
- This displacement introduces **errors in 3D reconstruction**, because:
    - the back-projection rays do not intersect at the correct spatial location.
- As a result, the reconstructed point in space is wrong, even if all other camera parameters are correct.
    
### <span style="color:rgb(161, 40, 226)">Image Rectification (Distortion Correction)</span>

- The first required step is **image rectification**:
    - transform the distorted (real) image into an **undistorted (ideal) image**.
- After rectification:
    - straight lines become straight again
    - points are relocated to their correct positions in the image plane.
### <span style="color:rgb(161, 40, 226)">Position in the Projection Chain</span>

- Distortion correction is applied **after image acquisition**, at the sensor level.
- Once the image is rectified:
    - we can safely move backward along the projection chain,
    - from the sensor plane to the camera plane,
    - and finally back to the 3D point in object space.

## <span style="color:rgb(239, 179, 1)">How to Account for Lens Distortion in the Camera Model</span>

The projection matrix **M** models an **ideal pinhole camera**, meaning it maps a 3D point in space to a point on an **ideal (linear) image plane**.  However, in a real camera, the measured image coordinates are affected by **lens distortion**, so the projection produced by **M** is no longer sufficient.
![[Pasted image 20251028141139.png|500]]
### <span style="color:rgb(161, 40, 226)">Distorted vs. Undistorted Image Coordinates</span>

- What we **measure** on the real sensor are the **distorted coordinates**:
    - ( ($x_d, y_d$) )
- What the ideal camera model predicts are the **undistorted (linear) coordinates**:
    - ( ($x_u, y_u$) )
The relationship between them is modeled as:
- ( $x_d = x_u + \Delta x$ )
- ( $y_d = y_u + \Delta y$ )

where:
- ( $\Delta x, \Delta y$ ) are **distortion displacements**
- these displacements depend on:
    - a vector of **distortion parameters** ( $\mathbf{q}$ ),
    - and on the image point location itself.
### <span style="color:rgb(161, 40, 226)">Distortion as an Additive Nonlinear Term</span>

- Distortion is **not included inside the matrix M**.
- Instead, it is modeled as a **nonlinear correction applied in image space**.
- Conceptually, the full pipeline becomes:

1. Project 3D point using the ideal model:
    - ( $\mathbf{p}_u = M , \mathbf{P}$ )
2. Apply distortion:
    - ( $\mathbf{p}_d = \mathbf{p}_u + \Delta(\mathbf{p}_u, \mathbf{q})$ )

This separation is intentional:
- **M remains linear and projective**
- distortion is treated as a **post-projection nonlinear effect**
    
### <span style="color:rgb(161, 40, 226)">Example: Barrel Distortion</span>

- In barrel distortion:    
    - straight lines bend outward,
    - points farther from the image center are displaced more.
        
- The displacement ( ($\Delta x, \Delta y$) ) is typically modeled using:
    - radial terms (e.g. ( $r^2, r^4$ )),
    - sometimes tangential terms.

- These models usually require **2 or more parameters**, stored in the vector ( \mathbf{q} ).
    

### <span style="color:rgb(161, 40, 226)">The Apparent Paradox (and Why It Is Not a Problem)</span>

You correctly noticed a conceptual issue:

> The distortion correction depends on the _true_ (undistorted) point,  
> but the true point is exactly what we are trying to estimate.

This seems circular, but it is resolved as follows:

- We **start from the measured distorted coordinates** ( ($x_d, y_d$) ).
- Distortion models are constructed so that:
    - either the correction can be **applied iteratively**, or
    - the inverse mapping can be **approximated accurately**.
        
- In practice:
    - camera calibration estimates **both**:
        - the intrinsic/extrinsic parameters,
        - and the distortion parameters **simultaneously**,
    - using many known reference points (e.g. calibration patterns)

So even though:
- the correction depends on the point,
- and the point depends on the correction,

the problem is **well-posed** and solvable because:
- we have many observations,
- and the distortion model is constrained and smooth.
    

### <span style="color:rgb(161, 40, 226)">Key Takeaways</span>

- Distortion is **not embedded in the matrix M**.
- It is modeled as a **nonlinear displacement in image space**.
- The correction depends on:
    - distortion parameters,
    - image coordinates.
- The apparent circular dependency is resolved through:
    - calibration,
    - redundancy,
    - and iterative or closed-form correction methods.
        


![[Pasted image 20251028141159.png]]

> Lens distortion cannot be included in the intrinsic matrix **K** because it is a nonlinear, point-dependent effect; it must be modeled as an additional correction applied in image space after the linear projection.

## <span style="color:rgb(239, 179, 1)">Modelling Non-linear Errors and Calibration</span>
![[Pasted image 20251028141223.png|500]]
### <span style="color:rgb(161, 40, 226)">1. Black-box approach</span>

The black-box approach treats distortion as a **generic input–output mapping**, without explicitly modeling the physics behind it.  
A general approximator (for example, a polynomial fit, interpolation scheme, or learning-based model) is trained to map distorted image coordinates to corrected ones.

Conceptually, it works like a learned correspondence:
- given an observed (distorted) coordinate as input,
- it returns the corresponding corrected coordinate as output.
    
This is not exactly a lookup table, but it behaves similarly: the model “learns” how to correct distortions based solely on data, without any physical interpretation of the lens.


### <span style="color:rgb(161, 40, 226)">2. Physical (model-based) approach</span>

The physical approach explicitly models the **optical phenomena** that cause distortion.  
For lenses, this is well studied in the literature, and several analytical models exist.

We focus on a **simple and widely used model**: **radial (barrel) distortion**.

## <span style="color:rgb(239, 179, 1)">Radial (barrel) distortion model<br></span>![[Pasted image 20251028141240.png|500]]
Radial distortion depends on the **distance of a point from the optical center** (principal point) of the camera. This distance is called the **radius**, hence the term _radial_ distortion.

The distorted image coordinates (($x_d, y_d$)) are modeled as:

$$\begin{aligned}  
x_d &= x \left( 1 + q_1 r^2 + q_2 r^4 \right) \\  
y_d &= y \left( 1 + q_1 r^2 + q_2 r^4 \right)  
\end{aligned}$$

where:

- ($(x, y)$) are the **ideal (undistorted)** coordinates on the linear camera model,
- ($q_1, q_2$) are the **distortion parameters**,
- ($r$) is the **radial distance** from the principal point.

### <span style="color:rgb(161, 40, 226)">Definition of the radial distance</span>

The radius ($r$) is defined as:
$$r = \sqrt{(x - p_x)^2 + (y - p_y)^2}$$
where ($(p_x, p_y$)) is the **principal point** in the camera coordinate system.

### <span style="color:rgb(161, 40, 226)">Important conceptual issue</span>

The difficulty of this model is that:

- the distortion depends on ($r$),
- (r) depends on the **ideal coordinates** ($(x, y)$),
- but what we directly measure are the **distorted coordinates** ($(x_d, y_d)$).
    
This creates an **implicit problem**:  the correction depends on quantities that are not directly observable.

### <span style="color:rgb(161, 40, 226)">Practical consequence</span>

Because of this dependency:
- distortion correction is typically performed using **iterative methods**, or
- by estimating the distortion parameters ($(q_1, q_2)$) together with intrinsic parameters during **camera calibration**.
    
This is why distortion is treated as a **separate nonlinear correction step**, applied after the linear projection defined by (K), and not embedded inside the camera matrix itself.

> Radial distortion is modeled as a nonlinear, radius-dependent scaling of ideal image coordinates, where the radius is measured from the principal point and the distortion parameters must be estimated through calibration.

### <span style="color:rgb(161, 40, 226)">Iterative correction of radial (barrel) distortion</span>
![[Pasted image 20251028141306.png|500]]
- We consider **barrel distortion modeled up to fourth order**, with **two parameters**:
    
    - ( $q_1$ ) (second-order term)
    - ( $q_2$ ) (fourth-order term)
        
- The distortion model (shown here for the **x-coordinate**, y is analogous) is:  
$$    x_d = x \left(1 + q_1 r^2 + q_2 r^4\right)  $$
    where:
    - ($x_d$) is the **measured (distorted)** coordinate,
    - ($x$) is the **true (undistorted)** coordinate,
    - ($r = \sqrt{x^2 + y^2}$) is the distance from the principal point.
        

### <span style="color:rgb(161, 40, 226)">Why an iterative method is needed</span>

- The radius ($r$) depends on the **true coordinates** (($x, y$)),
- but we only **measure the distorted coordinates** (($x_d, y_d$)),
- therefore, the correction equation cannot be inverted analytically in a simple way.

### <span style="color:rgb(161, 40, 226)">Iterative procedure (idea)</span>
![[Pasted image 20251028141315.png|600]]
- Start from the measured distorted coordinates:
    
    - ($x_0 = x_d$), ($y_0 = y_d$)
        
- Compute the radius:  
    $r_0 = \sqrt{x_0^2 + y_0^2}$  

- Update the estimate:  
	$$x_{1} = \frac{x_d}{1 + q_1 r_0^2 + q_2 r_0^4}$$
    (same for $(y_1)$)
    
- Repeat:
    - use ($(x_1, y_1)$) to compute a new radius,
    - obtain ($(x_2, y_2)$),
    - and so on.
### <span style="color:rgb(161, 40, 226)">Convergence property</span>

- If the iteration reaches the **true undistorted coordinates** ($(x, y)$),
    - the distortion equation is exactly satisfied,
    - and all subsequent iterations will return the same values.
- This means the solution is a **fixed point** of the iteration.
### <span style="color:rgb(161, 40, 226)">Numerical example</span>
![[Pasted image 20251028141323.png|400]]
- Distortion parameters:
    - ($q_1 = 0.005$)
    - ($q_2 = 0.0005$)
        
- True (unknown) point:
    - $(x = 2), (y = 3)$
        
- Measured distorted coordinates:
    - $(x_d \approx 2.30)$
    - $(y_d \approx 3.45)$
        
- Iteration starting from ($(x_d, y_d)$):
    - values oscillate initially,
    - but after a few iterations,
    - they converge to the correct values (x = 2), (y = 3).
        
### <span style="color:rgb(161, 40, 226)">Final remark</span>

- This **iterative distortion correction** is:
    - simple,
    - effective,
    - widely used in camera calibration pipelines.
- Other correction methods exist, but this one clearly illustrates the principle.
    

# <span style="color:rgb(223, 109, 109)">Estimation of camera parameters: collinearity equations</span>

### <span style="color:rgb(161, 40, 226)">Goal<br></span>
- Estimate the **camera projection parameters** (camera matrix (M), intrinsics and extrinsics)
- Then use them to:
    - **reconstruct 3D points** from 2D image measurements
    - using **two or more cameras** (triangulation)

## <span style="color:rgb(239, 179, 1)">Collinearity principle</span>

- The **fundamental assumption** of the camera model is **collinearity**
    - The **3D point** (P)
    - The **camera center** (C)
    - The **image point** (p)  
        all lie on the **same straight line**.
This is exactly the geometric meaning of perspective projection.
## <span style="color:rgb(239, 179, 1)">Mathematical expression of collinearity</span>
![[Pasted image 20251028133319.png|500]]
The collinearity condition can be written as:  

$$\mathbf{P} - \mathbf{C} = \lambda  (\mathbf{p} - \mathbf{C})  $$

Where:
- ($\mathbf{P}$) = point in **object (world) space**
- ($\mathbf{p}$) = corresponding point in **image space**
- ($\mathbf{C}$) = **camera center**
- ($\lambda$) = scalar (due to homogeneous coordinates)

This equation states that the vectors ($(P - C)$) and ($(p - C)$) are **linearly dependent**, i.e. collinear.
## <span style="color:rgb(239, 179, 1)">Simplification: placing the camera at the origin</span>

- **Without loss of generality**, we can choose:  
	$\mathbf{C} = \mathbf{0}$
    
- This simplifies the equation to:   
    $\mathbf{P} = \lambda  \mathbf{p}$
This simplification is valid because:
- Any real camera position can later be recovered using **rotation and translation**
- The geometry of projection is preserved

## <span style="color:rgb(239, 179, 1)">Introducing camera orientation and position</span>

In practice:
- The camera is **not aligned** with the global reference frame
- The camera has:
    - a **rotation** (R)
    - a **translation** (T)

Thus, a point expressed in the **global reference frame** must be transformed into the **camera reference frame**.

This is done as:  
$$\mathbf{P}_{cam} = R \left( \mathbf{P}_{global} - \mathbf{C} \right)$$
Where:
- ($R$) = rotation matrix (3 DOF)
- ($\mathbf{C}$) = camera center in global coordinates

## <span style="color:rgb(239, 179, 1)">Meaning of the transformation</span>

- The transformation:  
    $$R(\mathbf{P} - \mathbf{C})  $$
    expresses the **same 3D point** as seen from the **camera coordinate system**

- Once the point is expressed in the camera frame:    
    - it can be projected onto the image plane
    - using the **intrinsic matrix** (K)
        
## <span style="color:rgb(239, 179, 1)">Summary of the idea so far</span>

1. **Collinearity condition**:
    - Camera center, 3D point, and image point are aligned
        
2. **Camera at the origin**:
    - Simplifies equations
    - Does not lose generality
        
3. **Real cameras**:
    - Require rotation (R) and translation (C)
    - Convert global coordinates → camera coordinates
        
4. **Next steps** (what comes after this):
    - Use collinearity equations to:
        - estimate camera parameters
        - reconstruct 3D points from multiple views


## <span style="color:rgb(239, 179, 1)">Expanding the collinearity equations</span>

We start from the **collinearity condition**, already expressed in the camera reference frame:
  
$$\mathbf{P}_{cam} = \lambda \mathbf{p}  $$

where:

- $(\mathbf{P}_{cam} = R(\mathbf{P} - \mathbf{C}))$
- ($R$) is the **rotation matrix**
- ($\mathbf{C} = (X_0, Y_0, Z_0)$) is the **camera center** in global coordinates
- ($\lambda$) is a scalar (homogeneous coordinates)

### <span style="color:rgb(161, 40, 226)">Writing the equation component by component</span>

Let the 3D point in the **global reference frame** be:  
$$\mathbf{P} = (X, Y, Z)$$

After translation and rotation, the point in the **camera reference frame** becomes:  
$$\begin{bmatrix}  
X_{cam} \\  
Y_{cam} \\  
Z_{cam}  
\end{bmatrix}

\begin{bmatrix}  
R_{11} & R_{12} & R_{13} \\  
R_{21} & R_{22} & R_{23} \\ 
R_{31} & R_{32} & R_{33}  
\end{bmatrix}  
\begin{bmatrix}  
X - X_0 \\  
Y - Y_0 \\  
Z - Z_0  
\end{bmatrix}  $$

This gives **three scalar equations**, one per row of the rotation matrix.

### <span style="color:rgb(161, 40, 226)">Projection onto the image plane</span>

On the image plane:
- All points lie on the **same plane**
- Therefore, the third coordinate is **not generic**
- It is fixed and equal to the **focal length** (f)
    
So the image point in homogeneous coordinates is:  
$$\mathbf{p} = (x, y, f)  $$
### <span style="color:rgb(161, 40, 226)">Introducing λ (scale factor)</span>
![[Pasted image 20251028133644.png]]
The projection equation is:  

$$\begin{cases}  
X_{cam} = \lambda x \\  
Y_{cam} = \lambda y \\  
Z_{cam} = \lambda f  
\end{cases} $$

From the **third equation**, we can compute (\lambda):

$$\lambda = \frac{f}{Z_{cam}}  $$
where:  
$$Z_{cam} = R_{31}(X - X_0) + R_{32}(Y - Y_0) + R_{33}(Z - Z_0)$$
This is why **λ is eliminated**: it is determined directly from the third equation.

### <span style="color:rgb(161, 40, 226)">Substituting λ into the first two equations</span>
![[Pasted image 20260105175210.png|500]]
Now substitute ($\lambda$) into the first two equations:
#### Equation for x
$$
x =  
f  
\frac{  
R_{11}(X - X_0) + R_{12}(Y - Y_0) + R_{13}(Z - Z_0)  
}{  
R_{31}(X - X_0) + R_{32}(Y - Y_0) + R_{33}(Z - Z_0)  
}  $$
#### Equation for y

$$y =  
f  
\frac{  
R_{21}(X - X_0) + R_{22}(Y - Y_0) + R_{23}(Z - Z_0)  
}{  
R_{31}(X - X_0) + R_{32}(Y - Y_0) + R_{33}(Z - Z_0)  
}$$  
#### Why only two equations?
- A 3D point has **three coordinates** ((X, Y, Z))
- Its projection onto the sensor lies on a **2D plane**
- Therefore, the image point has only **two coordinates** ((x, y))
This is why:
- We start with **three equations**
- One is used to compute (\lambda)
- The remaining **two equations** fully describe the projection

This is exactly what we should expect physically and mathematically.

### <span style="color:rgb(161, 40, 226)">Sign of the focal length</span>

Sometimes you may see:
- (+f)
- or (-f)

This depends on:
- Whether the image plane is placed **in front of** or **behind** the perspective center
    
Both conventions are equivalent:
- The sign change only flips the image
- The geometry remains the same

## <span style="color:rgb(239, 179, 1)">Including the principal point offset (sensor coordinates)</span>
![[Pasted image 20251028134248.png|600]]
So far, ((x, y)) are coordinates in the **ideal camera reference frame**.
In real sensors:
- The origin is **not** at the principal point
- There is an offset (($p_x, p_y$))
Thus, the **measured pixel coordinates** are:
$$\begin{cases}  
x_m = x + p_x \\  
y_m = y + p_y  
\end{cases}  
$$
In the lecture notation:
- ($x_0 = p_x$)
- ($y_0 = p_y$)
    
This is simply a **translation** in the image plane.
### <span style="color:rgb(161, 40, 226)">Final interpretation</span>

These equations are the **collinearity equations**:

- They link:
    - 3D point coordinates (($X, Y, Z$))
    - camera pose (($R, C$))
    - camera intrinsics (($f, p_x, p_y$))
        
- They are the basis for:
    - **camera calibration**
    - **3D reconstruction**
    - **motion capture and optical measurement systems**
    

## <span style="color:rgb(239, 179, 1)">Iterative linearization for camera calibration</span>
![[Pasted image 20260105180228.png|500]]
We now introduce a **classical camera calibration method**, developed more than **30 years ago**, which is still conceptually important today.

As is common in engineering when dealing with **nonlinear problems**, the idea is to:

1. **Linearize** the nonlinear system around an initial guess that is assumed to be close to the correct solution
2. **Solve the linearized system**
3. Use the obtained solution as a **new estimate**
4. Repeat the process iteratively until convergence
    
Ideally, this procedure converges to a solution that is very close to the true camera parameters.

### <span style="color:rgb(161, 40, 226)">Implicit formulation of the collinearity equations</span>

To apply this approach, we rewrite the collinearity equations in **implicit form**.

Instead of writing:  
$$x = f(\mathbf{P}), \quad y = g(\mathbf{P})$$

we move all terms to one side and define:  
$$\mathbf{f}(\mathbf{p}) = \mathbf{0}  $$

That is, we search for the **zeros of a vector-valued function**.

Here:
- ($\mathbf{p}$) is the **parameter vector**
- ($\mathbf{f}(\mathbf{p})$) contains the two collinearity equations (one for (x), one for (y))
### <span style="color:rgb(161, 40, 226)">Parameter vector</span>

In this formulation, the camera model contains **9 parameters**:

- **3 rotation angles**: ($\omega, \phi, \kappa$)
- **3 translation parameters**: ($X_0, Y_0, Z_0$)
- **1 focal length**: ($f$)
- **2 principal point offsets**: ($x_0, y_0$)
Thus, the parameter vector is:  
$$\mathbf{p} =  
\begin{bmatrix}  
\omega & \phi & \kappa & X_0 & Y_0 & Z_0 & f & x_0 & y_0  
\end{bmatrix}^T $$
### <span style="color:rgb(161, 40, 226)">Multiple observations</span>
![[Pasted image 20251028134559.png|500]]
The index ($i$) denotes a **single measurement** (or observation).

Each observation consists of:

- A known **3D point** ($(X_i, Y_i, Z_i)$) in the global reference frame
- A measured **image point** ($(x_i, y_i)$) on the sensor
    
For each control point (i), we obtain **two equations** (one for ($x_i$), one for ($y_i$)).

### <span style="color:rgb(161, 40, 226)">Minimum number of control points</span>

To estimate the 9 unknown parameters
- Each control point provides **2 equations**
- Therefore, at least **5 control points** are required
    
This yields:  
$$5 \text{ points} \Rightarrow 10 \text{ equations} \Rightarrow 9 \text{ unknowns}  $$
The system is then solved using a **least-squares approach**.

If only **4 control points** are used:
- We obtain only **8 equations**
- This is **not sufficient** to estimate the 9 parameters

### <span style="color:rgb(161, 40, 226)">Geometric constraints on control points</span>

An important additional condition is that the control points:
- **Must not all lie on a single plane**

If all points are coplanar:
- A strong correlation appears between the **focal length** and the **translation along the Z-axis**
- The calibration becomes **ill-conditioned** and unreliable
    
For this reason:
- Control points should be **well distributed in 3D space**
- A volumetric arrangement leads to **more stable and accurate calibration results**

If you want, next I can:
- explain the **linearization step using Taylor expansion**
- derive the **Jacobian matrix**
- or show how this leads to the **classical photogrammetric calibration algorithm**

![[Pasted image 20251028134954.png]]
This is just a reminder that the elements ($r_{ij}$ ) of the rotation matrix ( $\mathbf{R}$ ) are **trigonometric functions** of the three rotation angles ( $\omega$ ), ( $\phi$ ), and ( $\kappa$ ).

These angles follow the **nautical or aeronautical convention**:

- **Roll (($\omega$))**: rotation around the longitudinal axis
- **Pitch (($\phi$))**: inclination around the lateral axis
- **Yaw (($\kappa$))**: rotation around the vertical axis
    
This convention is commonly used in photogrammetry, robotics, and aerospace applications.

### <span style="color:rgb(161, 40, 226)">Why is this important?<br></span>
This representation is important because, in order to **linearize the camera model**, we must compute **partial derivatives** of the projection equations.

The derivatives are taken with respect to the **rotation angles**:  
$$\omega,\ \phi,\ \kappa $$
and **not directly with respect to the elements of the rotation matrix**.

### <span style="color:rgb(161, 40, 226)">Key point</span>

The elements of the rotation matrix, such as ( $R_{11}, R_{12}, \ldots$ ), are **not independent parameters**.  Instead, each of them is a **function of the angles** ( $\omega, \phi, \kappa$ ).

For example:  
$$R_{11} = \cos\phi \cos\kappa $$

Therefore, when computing a derivative like:  $$
\frac{\partial R_{11}}{\partial \omega},\  
\frac{\partial R_{11}}{\partial \phi},\  
\frac{\partial R_{11}}{\partial \kappa}  $$
we are actually differentiating **trigonometric functions** of the rotation angles, not independent matrix entries.
### <span style="color:rgb(161, 40, 226)">Consequence for linearization</span>

When forming the Jacobian matrix for the linearized system:
- The partial derivatives must be computed **with respect to ($\omega, \phi, \kappa$)**
- The chain rule is applied, since each ( $r_{ij}$ ) depends on these angles
    
This is why the explicit trigonometric expressions of the rotation matrix are required before performing the linearization.

Here is a **clear, structured, and corrected English version** of your explanation, written in a way that fits well as lecture notes or a textbook-style summary, while preserving the original meaning.


***


![[Pasted image 20251028135605.png]]

When applying this method of **linearizing a nonlinear problem**, it is necessary to start from an **initial guess**. This initial estimate is usually obtained from rough measurements and serves as the starting point of an **iterative procedure**.

Let us denote this initial estimate of the parameter vector as ( \mathbf{P}' ).  
Around this point, the nonlinear equations are **linearized using a Taylor series expansion**, which is truncated at the **first-order term**. This is the practical approximation used in the algorithm.
### <span style="color:rgb(161, 40, 226)">Linearization using the Taylor series</span>

We consider the collinearity equations written in implicit form as:  
$$f_{i,j}(\mathbf{P}) = 0   $$
where:
- ( $i$ ) identifies the **control point**
- ( $j = 1, 2$ ) corresponds to the **two collinearity equations** (image (x) and (y))    

For example:
- ( $f_{1,1}$ ): first control point, first equation
- ( $f_{1,2}$ ): first control point, second equation
- ( $f_{2,1}$ ): second control point, first equation
- and so on, up to ( $f_{n,2}$ )
    

To estimate the camera parameters, the total number of equations must be **at least equal to the number of unknowns**, which in this case is 9.

Expanding the function around the initial estimate ( $\mathbf{P}'$ ), we obtain the first-order Taylor approximation:    
$$f(\mathbf{P}) \approx f(\mathbf{P}') +  
\sum_{k=1}^{9}  
\left.  
\frac{\partial f}{\partial P_k}  
\right|_{\mathbf{P}'}  
\Delta P_k  $$
where:  
$$\Delta P_k = P_k - P_k'$$

This means that the solution of the linearized problem provides the **correction vector** ( $\Delta \mathbf{P}$ ), which tells us how much the initial estimate must be updated.

### <span style="color:rgb(161, 40, 226)">Matrix formulation</span>

By writing all equations together, we obtain a linear system of the form:  
$$\mathbf{F}(\mathbf{P}') + \mathbf{J} , \Delta \mathbf{P} = \mathbf{0}  $$
where:

- ( $\mathbf{F}(\mathbf{P}')$ ) is a ( $2n \times 1$ ) vector containing the residuals computed from the measured image points
- ( $\mathbf{J}$ ) is the **Jacobian matrix** of partial derivatives, with dimensions ( $2n \times 9$ )
- ( $\Delta \mathbf{P}$ ) is the unknown correction vector of size ( $9 \times 1$ )
    
This formulation is dimensionally consistent and matches the structure of the problem.

### <span style="color:rgb(161, 40, 226)">Solving the system</span>

- If **exactly 9 equations** are used and the Jacobian matrix has **full rank**, the system can be solved directly by **matrix inversion**, yielding:  
    $$\Delta \mathbf{P}$$
    
- If **more than 9 equations** are available (which is strongly recommended), the system becomes **overdetermined** and is solved using the **least-squares approach**.
    
### <span style="color:rgb(161, 40, 226)">In this case, the solution is obtained using the <b>pseudo-inverse</b>:  </span>
$$\Delta \mathbf{P}

(\mathbf{J}^T \mathbf{J})^{-1} \mathbf{J}^T \mathbf{F} $$

This solution minimizes the **sum of the squared residuals**, meaning it provides the best estimate in the **least-squares sense**.
### Iterative refinement

Once ( $\Delta \mathbf{P}$ ) is computed, the parameter vector is updated:  
$$\mathbf{P}_{\text{new}} = \mathbf{P}' + \Delta \mathbf{P}  $$
This updated vector becomes the new initial estimate, and the entire process is repeated until convergence is reached.


![[Pasted image 20251028135551.png]]
The result of the linearized problem is the **correction vector** ( $\Delta \mathbf{P}$ ), which contains **nine elements**, corresponding to the nine camera parameters.

This vector ( $\Delta \mathbf{P}$ ) is the solution of the **linearized system around the current estimate** ( $\mathbf{P}'$ ). Its meaning is the following: if we update the parameter vector by moving from ( $\mathbf{P}'$ ) to  
$$\mathbf{P}' + \Delta \mathbf{P}$$
we should get **closer to the true solution** of the original nonlinear problem.

The word _should_ is important here, because convergence is not guaranteed if the initial guess is extremely far from the true solution. However, in practice, even if the initial estimate contains errors of several tens of percent, the method usually converges without problems.
### <span style="color:rgb(161, 40, 226)">Iterative update scheme</span>

The procedure is iterative and works as follows:
1. Start from an initial estimate ( $\mathbf{P}'_0$ )
2. Solve the linearized system and compute ( $\Delta \mathbf{P}_1$ )
3. Update the parameters:  
    $\mathbf{P}'_1 = \mathbf{P}'_0 + \Delta \mathbf{P}_1$
4. Linearize again around ( $\mathbf{P}'_1$ ) and compute a new correction ( $\Delta \mathbf{P}_2$ )
5. Repeat the process:  
    $\mathbf{P}'_{k+1} = \mathbf{P}'_k + \Delta \mathbf{P}_k$
    
This iterative refinement continues until convergence is reached.

### <span style="color:rgb(161, 40, 226)">Stopping criterion</span>

Convergence is typically detected when the correction vector ( \Delta \mathbf{P} ) becomes **very small** between two successive iterations. When this happens, it means that the solution has been reached and further updates only cause small oscillations around the optimum due to measurement noise.
Therefore, the algorithm stops when:  
$$| \Delta \mathbf{P} | < \varepsilon  $$
where ( $\varepsilon$ ) is a predefined threshold.


## <span style="color:rgb(223, 109, 109)">Triangulation: reconstructing a 3D point from multiple cameras</span>

A single camera cannot determine the 3D coordinates of a point in space. This is because a measured image point corresponds to **an infinite number of 3D points** lying along a straight line passing through:

- the **perspective center** ( $C$ ),
- the **image point** ( $p$ ),
- and the unknown **object point** ( $P$ ).
    
This line is called a **viewing ray**. Therefore, depth cannot be recovered from one camera alone.

## <span style="color:rgb(239, 179, 1)">Using two cameras: basic triangulation principle</span>

To recover the 3D position of a point, we use **at least two cameras**, for example the green and the yellow cameras shown in the figure.

Each camera is characterized by:

- **Extrinsic parameters**: rotation angles and translation (position of the camera in the global reference frame)    
- **Intrinsic parameters**: focal length, principal point coordinates ( $(p_x, p_y)$ )

All parameters are assumed to be **known from calibration**.
![[Pasted image 20251021151303.png]]
## <span style="color:rgb(239, 179, 1)">Construction of viewing rays<br></span>
For each camera:
1. The measured image point defines a direction in space.
2. Knowing the camera calibration, we can construct a **3D straight line**:
    - passing through the camera’s perspective center,
    - directed according to the projection of the image point.
    
Thus, for the same physical point in space, we obtain **two viewing rays**, one from each camera.


## <span style="color:rgb(239, 179, 1)">Ideal case: intersection of rays</span>

If:
- both cameras are perfectly calibrated,
- and there is no measurement noise,
    
then the two rays **intersect exactly** at the true 3D point.
However, in practice, due to noise and calibration errors, the two rays **do not intersect**.

## <span style="color:rgb(239, 179, 1)">Why the rays do not intersect (algebraic view)</span>

Each ray can be written in parametric form:  
$$\mathbf{L}_1(\lambda_1), \quad \mathbf{L}_2(\lambda_2)  $$

To force an intersection, we would require:  
$$\mathbf{L}_1(\lambda_1) = \mathbf{L}_2(\lambda_2) $$
This gives **three equations** (for ( x, y, z )) but only **two unknowns** (( $\lambda_1, \lambda_2$ )).  
In general, such a system **has no solution**.

## <span style="color:rgb(239, 179, 1)">First workaround: partial intersection (not optimal)</span>

One could enforce equality only on two coordinates (e.g. ( x ) and ( y )), ignoring the third.  
This produces a solution, but the remaining coordinate contains an error.

This approach is simple but **not optimal**.

## <span style="color:rgb(239, 179, 1)">Optimal solution: minimum-distance triangulation</span>
![[Pasted image 20251021151346.png]]
A better approach is to explicitly model the error.

We write:    
$$\mathbf{L}_1(\lambda_1) = \mathbf{L}_2(\lambda_2) +  
\begin{bmatrix}  
\delta x \  
\delta y \  
\delta z  
\end{bmatrix} $$

Now we have:
- **5 unknowns**: ( $\lambda_1, \lambda_2, \delta x, \delta y, \delta z$ )
- **3 equations** from coordinate matching
    

To close the system, we introduce **two additional equations** by minimizing the squared error:  
$$E = \delta x^2 + \delta y^2 + \delta z^2  $$

We impose:  
$$\frac{\partial E}{\partial \lambda_1} = 0, \quad  
\frac{\partial E}{\partial \lambda_2} = 0 $$

This results in a **5×5 system of equations**.
## <span style="color:rgb(239, 179, 1)">Geometric interpretation of the solution</span>

Solving this system gives:
- one point on the first ray,
- one point on the second ray,

such that the **distance between the two rays is minimal**.

These two points are the **closest points between the two viewing rays**.

## <span style="color:rgb(239, 179, 1)">Final 3D point estimate</span>

The reconstructed 3D point is obtained by:
- taking the midpoint of the segment connecting the two closest points.
    

This point minimizes the **sum of squared distances** and is therefore the **least-squares triangulation solution**.

## <span style="color:rgb(239, 179, 1)">Key takeaway</span>

- Triangulation requires **at least two calibrated cameras**
- Due to noise, rays do not intersect
- The correct solution is obtained by **minimizing the distance between rays**
- The result is a **least-squares estimate** of the 3D point position













