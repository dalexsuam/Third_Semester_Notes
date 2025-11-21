
12/11/20225
***

![[Pasted image 20251112083506.png]]

we start with this...

we came up with this relationship... p2tk2tRSK1p1


![[Pasted image 20251112085328.png]]

This is an important topic issue..(a bit bef)


the projection of the point in space I2=FP1 

selected in camera two (2) p2tFP1=0

![[Pasted image 20251112090312.png]]

previous slide

![[Pasted image 20251112090339.png]]

Let's see how we do it

![[Pasted image 20251112090635.png]]

when I start writing down...

![[Pasted image 20251112090838.png]]

In reality


![[Pasted image 20251112091136.png]]
as you read here

![[Pasted image 20251112091043.png]]
now, it is important to know

![[Pasted image 20251112091325.png]]

and I will still work on the essential matrix 

![[Pasted image 20251112093242.png]]

the last problem



***
We now start again with our learning on the on the eticholoma geometry for the calibration of a stereo camera system with a configuration of unknown control points. Okay?  
  

In there.  
  

And I'd like to recall the basic concepts that we already expressed last week concerning this topic. So first, the only rational way of introducing...  
  

Procedure to calibrate the stereo camera system for motion analogies with a configuration of unknown control points is only to get rid of the manual procedure for localization of the control points. points for calibration in the case of the conventional method. Why this? Because this procedure is prone to errors.  
  

It will never be possible to measure with high precision the localization, the position of the control points of calibration. And these errors that come into play during the manual procedure are particularly critical because you don't don't know where they are and they do influence the accuracy with which you are able to able to estimate the calibration parameters in the conventional method.  
  

And therefore.  
  

The resulting distortions, partial distortion of the calibrated volume will lead to a decreased accuracy of the way in which I am able to reconstruct in 3D the points of interest, for example, the markers placed on the human body.  
  

The riskiness of anatomical landmarks of my patient, of my subject during the motion analysis.  
  

I want to do. You will experience this by yourself because you will commit errors in your practical project for measuring the points position and this will in turn result or participate in decreasing the accuracy that you will have in your calibrated knowledge. Decrease the accuracy with which you will be able to reconstruct in 3D some of the points or most of the points placed on your subject and manually digitizing this is fun for the automatic system in a fancy laboratory for motion analysis.  
  

But in order to get rid of this one procedure, we have to pay a price. And we start to understand that, and it is important to recall what are the basic differences, also practical differences, between a procedure.  
  

Let's say a conventional procedure for calibration with no control points and an unconventional procedure for calibration with unknown control points. the first.  
  

The price, if you wish, or difference, if you wish, is that in the case of the epipolar geometry-based calibration with unknown control points, we need to work with at least a couple of cameras.  
  

So there is no more the possibility to calibrate one camera singularly.  
  

Separated by the others.  
  

Because the geometrical constraints that we need to take into consideration in this case is a planar constraints that tells us that the center of perspective the optical centers of the two cameras, the point in space that the two cameras are watching, are seeing, and the projection of this point in space of the two camera image planes and image planes, they all belong to a single plane that is called epipolar plane. Okay.  
  

In the conventional telemetry procedure, the geometrical constraints was the collinearity between the pointing space, its projection on the image plane, and the camera of the perception. And it was a geometrical constraint.  
  

Present within one single camera. Here, the geometrical constraint involves the two cameras, or the more cameras that we want to calibrate in our configuration, in our experiment, as you know.  
  

This implies a major critical point in the new procedure.  
  

That is the correspondence of points seen by the two cameras.  
  

From now on, we can need to take into consideration the fact that when I will show.  
  

The camera system, one point in space.  
  

And we have to be really sure that the two projections, that these points generate on the two image planes, are identified as the projection. projection of the same point in space. That is, that if we already understood that in order to calibrate the stereo camera system, I will have to show to the camera system a lot of points in whatever positions. unknown positions the important critical factor here is that for any point shown to the camera systems i will need to identify the correspondence of the related project this single point generates from the camera in each case and due to the fact that i will show maybe multiple points per frame camera to the camera edge to the camera system.  
  

Problem of correspondence search becomes critical because here if i make an error so i identify wrongly the the projection of the point on one camera and on the other camera then i will make a mess then i will make an error which will be very transparent which will be not identifiable easily and that we in turn complicate a lot.  
  

The possibility that I'm able to extract meaningfully the parameters of the fundamental matrix and therefore all the extrinsic and intrinsic parameters that I want to extract from the fundamental matrix. Okay.  
  

So if you have to talk to a laboratory technician that asks you what are the advantages and disadvantages of the epipolar geometry-based calibration with the no control points with respect to the conventional method, This is a a very critical factor. So you will have to have a robust algorithm for projection classification and corresponding search in the image planes of the two cameras, or multiple cameras that you want to use. This is really very critical. And it has a set of implications. We will see at the end that I will show to the system frame by frame not a lot of points.  
  

I will keep the number of points that I need to show to the camera system frame by frame to the minimum number possible, minimum number required to do the job.  
  

That's because the higher is the number of markers that are shooting the system frame by frame, the higher would be the complications in order to solve the problem of progress from the insertion in a robust way, which is an absolute requirement for the things we're doing.  
  

To do it. First problem, problem, first issue. Second issue, we needed in order to obtain the basic relationships of the bipolar geometry involving the fundamental matrix and today we will start to do this, we needed to include to introduce a very important simplification that is that we will be able to calibrate we consider two cameras.  
  

Minimum number of cameras that we need to work with.  
  

We need to calibrate one camera with respect to the other.  
  

So there will not be existing from the starting point of the procedure a laboratory reference frame with respect to which we are calibrating the camera system. This was true in the conventional method because when I take the measurements of the positions of the control points in space, I will refer this measurement manually to whatever laboratory reference frame with respect to which I am calculating the cameras and with respect to which I will reconstruct in 3D the points on my subject. This is implicit in the procedure of the calibration, okay? So when you will be listing the real and don't coordinates of your control points in a file that you need to feed this file to the calibration algorithm in the conventional way, well these positions.  
  

These coordinates of the control points will be expressed with respect to a laboratory reference frame. You will know where it is and you will have also the freedom to choose where it is, so where is the origin, and how this reference.  
  

Because you will be deciding.  
  

This part by assigning the specific coordinates of your configuration of control points known in space and expressed with respect to this laboratory reference frame. okay so.  
  

If you want to, for example, have the right axis of your reference frame pointing upwards, you will be free to do that.  
  

Or you want the right axis to point upwards, for example, to be coinciding with the reference frame of the open seam human. muscle skeletal model, you have the freedom to decide where to put and how to orient your laboratory reference frame with respect to which you are calibrating your cameras, camera, because in the conventional method you can do it camera by camera.  
  

Which will be the reference frame in which you will express the 3D coordinates of your subjects.  
  

In the epipolar geometry calibration, based calibration than non-controlled. was you lose this freedom you are not able to decide you will be forced to calibrate one camera with respect to the else so you will have to choose which is the camera that is your basis this camera will have as a consequence of this choice the fact that the extrinsic parameters of this camera will be zero so the rotational matrix will be an identity matrix.  
  

The translational vector will be zero.  
  

And all the other cameras will be calibrated in terms of extrinsic calibration with respect to this first camera.  
  

So you will find an estimate through the procedure that we will see today, the extrinsic parameter of TV camera two with respect to TV camera one, and support and so on, okay? This is done in order to simplify the situation, reduce the number of parameters that I am forced to estimate because we will discover that we are entering in a rather complicated journey in terms of numerical stability. Okay?  
  

So the less I can... parameters that I need to compute.  
  

The better it is, or the more simple is the procedure, the higher is the probability that I will find a solution. Okay?  
  

By introducing this simplification and expressing, sorry, the consequence of this simplification I mentioned already at the other time, is that at the end of the procedure, when we have all my calibration parameters extracted, I will have everything... expressed with respect to the lab, to the reference frame that is solid to camera one, which is in whatever position in my lab. And this is, in most of the cases, unacceptable. So I will need to come up, and we'll see how we can do that.  
  

A small calibration procedure. It will not be a real calibration procedure. It will be a mapping procedure, a procedure for the estimation of the mapping of the foundational matrix in order to bring them to map the reference frame of the stereo camera system that is belonging to the camera number one into a new.  
  

More useful, more handy.  
  

Laboratory reference frame, for example, the one that is working with the force platform that you have or with any other device that you might have in your laboratory reference, in your laboratory. And so the price of this simplification.  
  

To calibrate one camera with respect to the other.  
  

Calibrate the cameras with respect to one single camera, is that that we will have to introduce in our procedure, an additional mapping procedure. or mapping estimation procedure, that will be a manual procedure that will require the definition of a small configuration of few control points whose position I will need to measure manually.  
  

And so if the rationale of the calibration with unknown control points was to get rid of manual procedures for the measuring the position of control points in space.  
  

We at the end will have the need to do it much more simple because the number of points that we will need for this estimation of the mapping of the processional matrix will be very small, at least three, we will use maybe four or five, so this makes things much more simple, but still.  
  

We still have to do a small calibration or mapping procedure requiring the manual measurement of a very simple configuration of control points.  
  

So no more agreed position in different positions, no more hundreds of points needed to be measured manually, but a small configuration of points measured manually would still have to be required. We'll come back at the end and we will recall everything. Okay.  
  

Now by introducing this simplification and by expressing the planarity constraint.  
  

We came up with this relationship that links the projection, the projections of a single point in space on the two camera image plane with a set of matrices.  
  

Where K2 is the intrinsic matrix of camera 2. It contains the intrinsic parameter. We remember what they are, this intrinsic parameter, the focal length, and the...  
  

Coordinates of the principal points.  
  

K1 is the intrinsic matrix of camera 1 and.  
  

R is the rotational matrix expressing the orientation of the camera. of camera 2 with respect to camera 1 and S is the skew symmetric matrix containing the translational component, the translational vector of camera 2 with respect to camera 1. So the product of R and S are the extrinsic parameters of containing the extrinsic parameters of camera 2 with respect to camera 1. This is only to say...  
  

That when we make this formulation more compact by putting the two intrinsic parameters matrices and the extrinsic parameters matrices in a unique matrix that would be our fundamental matrix.  
  

We know by construction.  
  

Because of the procedure that we have followed, that in this fundamental matrix F.  
  

I will have somehow what I need.  
  

That are the intrinsic parameters of the two cameras and the extrinsic parameters of camera 2 with respect to camera 1. And I will need just to try to find a way to extract these parameters from the fundamental matrix. Not an easy procedure as we will discover.  
  

So the product RNS, that is the explicit expression of matrices containing the extrinsic parameters of.  
  

Camera 2 with respect to Camera 1 is called the essential matrix.  
  

And let's say the product of the essential matrix with the two internal parameter matrices takes the name of the fundamental matrix. So if we find a way to extract the intrinsic parameters of the two cameras. then I will be able to make explicit the extension matrix. And from the extension matrix, working on the extension matrix, I will be able to extract the parameters.  
  

Now let's see. what is this only blessed fundamental matrix let me just underline that the two projections here p2 and p1 are the projections of one single point in space so the correspondence is there okay it's implicit in this formulation so we need to know the characteristics of the fundamental matrix.  
  

It contains a lot of stuff.  
  

It contains what we need, what we are interested in. But it is a simple matrix. It is a three by three matrix.  
  

Nine elements.  
  

Seven degrees of freedom.  
  

Because seven independent parameters.  
  

Because the determinant of F is zero. So the rank of the matrix is 2 and not 3 and.  
  

The scale factor, as we hear, is not an issue.  
  

What does this mean? This is an important topic, issue.  
  

That represents the second simplification. of the whole procedure when we show to the camera system the cloud of points of unknown coordinates in space that we will need to show to the camera system in order to calibrate the situation well the system doesn't know anything about space about about the space about the measurement.  
  

But the real measure is this. We are not providing our algorithm with any information related to the real dimensions of the space.  
  

As we will see, the cloud of points using the so-called magic wand.  
  

The magic wand will be typically, and we will discover why, will contain... typically three markers.  
  

Okay, placed at different distances one another or known distances one another. This would be L1, this would be L2, none, okay? This will be the configuration of the magic wand, and there will be some reasons why.  
  

But for the moment, when I will wave this magic wand in front of the cameras, this system has no idea of the distance. between the markers that I'm showing has no clue of the way in which the space is in front of the cameras because we are not providing numbers.  
  

We're not providing any information on this.  
  

So the quantity of which I am interested, for example, the extrinsic parameters, let's take the most easy of these ones, that is the baseline. So the distance between the optical center... center of camera one with respect to the optical center of camera two. The translational component of camera two with respect to camera one. This distance is unknown. Also in terms of scaling.  
  

The cameras could be so close that this translational vector is in the order of microns.  
  

Or of millimeters. Or of meters. Or of decameters. Or of kilometers.  
  

This information Formation of skating is not not present.  
  

Is not provided to the system. That is that the system will be able just to establish proportions.  
  

But these proportions will be unknown in terms of the real scaling that they have in the physical world. We are not providing any information regarding the physical world in which these proportions these constraints are valid. And so we need a scale factor.  
  

We need this information. We will need to provide this information at a certain point. And we just need a known distance between the control points that we are showing to the system in order to solve this situation, to solve this singularity.  
  

And in fact.  
  

One of these two distances will be used as a scale factor to recover the right physical world information, reality if you wish.  
  

Applied to all the calibration parameters that I will extract from the fundamental parameters.  
  

Second simplification, the whole calibration is performed independently from the physical world information. So in Italian I would say, a meno di un fattore di scala.  
  

Word in English regardless the scale factor regardless the scale so we need to provide that's the solution any information regarding the scaling in order to restore or the reality of our camera system, which is embedded in the real world, in the physical world, okay?  
  

So one of these two distance is gone, is used.  
  

And in terms of the fundamental matrix characteristics, this represents, let's say, a dependency, okay? So the independent parameters of the fundamental matrix only seven.  
  

Thank you.  
  

If we know the fundamental matrix.  
  

Now we have to forget the geometrical constraints in the real world, start to think in terms of the epipolar geometry. So the fundamental matrix is exactly what we need in order to calculate the important parameters of the epipolar geometry.  
  

The coordinates of the epipoles.  
  

We know what they are.  
  

The equations of the epipolar lines.  
  

They will be expressed exactly using the fundamental matrix. So the product of the projection of the point.  
  

1, that is the projection of the point in space of camera 1, re-multiplied by the fundamental matrix.  
  

Is the equation of the epipolar line on the image plane of the second camera.  
  

And vice versa.  
  

If we are using the transpose matrix.  
  

Okay? So if this is the fundamental relationship, P2, F, P1.  
  

If we are using the transpose of the fundamental matrix, it will become P1.  
  

F transpose P2.  
  

I can go from one camera to the other by simply transposing the fundamental matrix.  
  

And if we look at the expression of the equations of the two polar lines, the fundamental relationship that we have written can also be interpreted as the fact that the distance...  
  

Of a point on one tip if there is one point selected on camera 2 we need that the epipolar lines.  
  

This the distance between the epipolar line generated by this point selection on camera two so the people are lying on camera one and the distance of the corresponding point on camera one.  
  

From the epipolar line generated on camera one needs to be zero.  
  

This is the geometrical interpretation of the basic relationship that we have here.  
  

I select the point on camera image plane two.  
  

I generate an epipolar line on camera image plane one.  
  

The distance between the corresponding point of the selected point on camera two in camera one and the epipolar line generated by the selection of point on camera image plane two needs to be zero.  
  

Okay, so the point on camera one corresponding of point to point on camera two needs to lay, to be on the epipolar line in camera one generated by the selection of the point on camera two.  
  

And if I transpose the matrix, the fundamental matrix, it holds also the contrary.  
  

Okay? That's the geometrical interpretation, epipolar geometric interpretation of this basic relationship that we have written as a function of the fundamental matrix.  
  

Okay?  
  

Then, okay, there are some considerations related to the AP pulse and stuff like that. Okay, we lie. We know that if we are able to estimate this fundamental matrix.  
  

We have everything at hand.  
  

We can master the parameters of the epipolar geometry by drawing epipolar lines, finding the epipoles, rotating all the stuff. We have everything we need to move around. and to master the epipolar geometry that are evident in this previous slide somewhere here, these are the epipoles these are the epipolar lines and so forth and plus we know that if we are able to estimate the F in F we will be able to search somehow to extract then we know that the extrinsic . these parameters are there so our first problem is destination let's see how we do it.  
  

I mean, we will keep things very easy, but we need to make some assumptions also, because as I told you, the algebraic simulation is pretty complex. So we'll make some passages in which we need to make a sort of act of faith.  
  

The matrix, the fundamental matrix is estimated by implementing a system of equations.  
  

Where the equations are the basic relationship that we have written. Linking the projection of the same point in space with the two cameras to the fundamental matrix. Nothing more, nothing less.  
  

So we show to the camera system at least eight points quinto We introduce the homogeneous coordinates, that's why the method is called the eight-point algorithm. We need to show to the camera system at least eight points, eight different points in space with unknown coordinates. generating eight equations that I'm able to write down, the basic relationships there.  
  

And I write a system of equation that I need to solve in order to find the independent elements of the F that will be.  
  

Because of the homogeneous coordinates, only eight explicitly with respect to nine.  
  

In reality, I will show to the system in order to obtain an estimation of the fundamental...  
  

And much higher number of points in space.  
  

It's highly redundant number of control points with unknown coordinates in such a way that my system of equation that I need to solve becomes huge.  
  

Becomes a system of equation made up by thousands of equations. These are the numbers. I will show at least 10.  
  

1,000, 12,000, 15,000 of points to the camera system, which is easy to do because these systems are pretty fast. Now they are maybe 70 hertz.  
  

So.  
  

I can show easily, I can get easily to this high number of control points displayed to the camera system in the matter of some tens of seconds.  
  

By waving the magic wand in front of the camera system, trying to store that as much as I can. the volume that I want to calibrate reaching easily in less than one minute a very high number of the four sets this redundancy brings in numerical instability okay and we'll see how I mean just we need to normalize in order to show what the protein group is from but let's see.  
  

How do we solve the system of equations? I will solve the system of equations trying to find the elements of the fundamental matrix by minimizing it, by this square method of minimization. And the main function that I need to minimize.  
  

Is exactly.  
  

It is a non-linear manufacturing as expressed here, has many different possibilities, but the concept is I want to minimize exactly the message. that is described by the basic relationship that we have written so that for any point selected on camera 2 i will have an epipolar line on camera 1 and the distance of the corresponding point of p2 on camera 1 p1 with respect to the epipolar line will be zero that's what is expressed here that's exactly what i want to minimize if at the end i will find in the right way the f.  
  

This unique F will respect this constraint will respect the fact that for every point that I select on camera 2 I will have an epipolar line on camera 1 and the corresponding point on camera 1 on camera 2 will be lined on the epipolar line and there will be only one F for the whole set Thank you. control points that I have shown to my camera system.  
  

So only eight parameters to be shown to be estimated. Right? It seems easy.  
  

It is not from the numerical standpoint.  
  

Because when I started writing down the matrix of this system of equations, this is simply an example. But look at the numbers.  
  

I have a high variability there. there in this matrix that I need to solve. So I have a range, a wide range of values in the matrix that I need to move there if you wish to solve the system of equations. So the numerical instability is an issue, and there is the possibility.  
  

As Hartley preconditioned, Hartley is a guy who invented more or less this method.  
  

Together with others.  
  

That recommend.  
  

Thank you. A normalization procedure in order to improve the effects or to decrease the effects of the numerical instability in the procedure, in the estimation of the parameters of the image.  
  

Matrix therefore. It requires the introduction of a matrix which has as members and elements calculated as a function of the mean and of the standard deviation of the range of values. that I find in my matrix A here of the values of points so that I normalize the f.  
  

Reducing the range, if you wish, of values that I see in this example.  
  

But implying the fact that at the end of the estimation procedure, I will have to denormalize the f in order to obtain the real denormalized values of the elements of f. For us.  
  

We need to remember that the estimation of the elements of f is not trivial.  
  

It requires the implementation of a redundant system of equations suffering from numerical instabilities, thus requiring a normalization procedure followed by a denormalization procedure at the end of the estimation of the values of the elements of f.  
  

In reality.  
  

The algorithm that is running when you do a calibration procedure with unknown control points estimates the elements of.  
  

F by seeing their value in the proposition. which is the numerical net to solve the least square minimization that we highlighted just in the previous slide. OK.  
  

So you build the system of equations in homogeneous coordinates.  
  

And you try and find the unknowns, which are the nine elements of F.  
  

It can be demonstrated that the elements of F are the.  
  

As we hear, the components of the column of V, of the matrix V.  
  

Corresponding to the smallest eigenvalues.  
  

Eigenvalue contained in the matrix D.  
  

This is the algebraic or numerical solution by means of singular value decomposition of the expression of the least square minimization problem sure in the previous slide.  
  

Practically speaking, if we would implement, if we should implement on our laptops a net point algorithm for the estimation of the matrix F, we need to introduce the homogeneous coordinates, write the... system of equation and express it in the form a multiplied by x equals to zero it's just a manipulation of the basic formulation the basic relationship of the apicolar geometry and so.  
  

The system of equations by singular value decomposition, obtaining the unknown vector x, which are the nine elements of f, as the eigenvector associated to the smallest eigenvalue in the singular value decomposition matrix, still containing the eigenvalues.  
  

Plus an eventual normalization followed by denormalization at the end of the procedure to stabilize the numerical instability which is intrinsic in the formulation of the system of equations due to the wide range of values that the elements of the matrix A of the system of equations can assume.  
  

Okay?  
  

Now, it is important to know that if I do things wrong, I do not normalize, for example, or if the distribution of points that I've shown to the camera system is wrong.  
  

Is somehow wrong or partial. For example, I have concentrated all the points only in the small portion of the image that is very wrong. And we know it also from the conventional method of calibration that we need to distribute the control. points for calibration in such a way that they cover as much as possible our image.  
  

I will always come up to a formulation of F.  
  

But this F will hardly interpret the geometrical proportions and the planar constraints that should be valid there.  
  

So we need to keep a very high attention on the way in which we distribute the configuration of control points with a known coordinates in the field of view of the camera in such a way that the elements of F that I will record... that I will obtain.  
  

Do represent really the link between any projections of any point in space that the cameras make.  
  

In the future, let's say, the future utilization of the camera. If the points are only there, then this relationship will be valid only for points in that part of the field of view of the camera. And nothing will not be valid, it will not be valid in other areas of the field of view of the camera.  
  

So if the laboratory technician asks you why or let me give me some guidelines on how to show to the camera system the cloud of control points of unknown coordinates that need to be displayed to my camera system in order to obtain a successful calibration, you will have to recommend this laboratory technician to pay attention in distributing proper the configuration of the control points in the uniformly more or less in the whole field of view of the two cameras that you have in front of you. Which is another logistics or practical constraint right because if you do things wrong as you do as you do it if you if you define the configuration of control points with no coordinates in a very small portion of the field of view then you will have a If.  
  

It will come up with a fundamental matrix which will be valid only on a small area of your field of view of your two cameras.  
  

So typically the systems, the commercial system.  
  

Propose a feedback, a visual feedback to the operator during the weighting procedure in order to let the operator understand the way in which he is showing.  
  

The configuration of control points more or less uniformly more or less valid in terms of coverage with the control points configuration of the whole field of view of the two cameras or of the multiple cameras that you need to calibrate. Because two cameras is the simplest case for the practical purpose. Think of calibrating 16 cameras in a laboratory of motion analysis. and then you have to dance in the whole working volume, waving. in your magic wand, okay? And you will need a feedback from the system telling you, okay, that's the way in which you have covered the field of view of camera 1, of camera 2, of camera 14, of camera 16.  
  

Okay? That's a crucial factor together with the fact that in any frame of 16 cameras, you need to establish the correspondence between the projections of the points.  
  

Not trivial. if I would have only one mark. marker on my magic wand and I assume that I don't have phantom markers there because I checked everything okay then the correspondence search is trivial but we know and discovered already that we need at least two.  
  

Because we need the scaling factor.  
  

So at least two are in every frame of every camera that I'm calibrating contemporarily because I need also the time synchronization between the cameras to establish the correlations.  
  

And we will discover then that we need at least another one for solving the last of our problems.  
  

Now.  
  

Let's suppose that we succeeded to estimate properly the elements of the fundamental matrix F.  
  

Now we can do whatever we want. For example, we can draw the epipolar lines, know where the epipoles are, everything. We must have the epipoles.  
  

Polar geometry there. We know that exists only one F for the whole set of calculation points that we have shown to the camera. A unique fundamental matrix that link every projection.  
  

Every couple of projections of any of the points that I've shown to the camera.  
  

And we know that inside the f we can find what we need.  
  

We can find the f.  
  

Theoretically speaking, the f, the principal points, the intrinsic parameters of the two cameras, which would be different for camera 1 and camera 2.  
  

And the calibration parameters, the extreme calibration parameters of camera 2 with respect to camera 1. We need to try to find them.  
  

Now.  
  

We need to make another very important simplification here.  
  

That will have a lot of practical implications.  
  

First.  
  

We are in the super ideal condition. This was true from the very beginning. but it is even more true here that we have no skew.  
  

So we have only one F per camera.  
  

Okay, we don't have pixels which are not perfectly square. We have perfectly square. square and a perfect rectangular or better said even better square image plane sensor. So we don't have an fx and fy in one single camera. We have one single f per camera. F1, f2. And this was a minor, minor simplification.  
  

The major simplification is that we need to assume that we know where the principal point is. need to have the coordinates of the principal point known for both cameras. That is to say, there is no way to extract from the fundamental matrix the coordinates of the principal points of the two cameras.  
  

And this is a major simplification. It is as if we have started the journey to extract the calibration parameters from the cloud points of unknown coordinates. And now we are half of the way and we discover that... two important parameters that are if you wish, four because there are four coordinates two for each of the principal points we cannot obtain and not only we cannot obtain we need to assume assume we know them. Because in order to extract the focal length from the fundamental matrix of the two cameras, we need to introduce the position of the supposed or known position of the principal point of the two cameras.  
  

It's a nice joke, okay?  
  

But that's the way it is. So the solution is either.  
  

I calibrate the principal point before a priori on the, let's say.  
  

In my laboratory.  
  

I can perform a sort of intrinsic calibration procedure to estimate at least the position of the principal point.  
  

Or I will need to come up with a more complex method in order to estimate the principal point and we will see what it is.  
  

In the first case.  
  

I can do an a priori calibration of the intrinsic parameters of the camera at least focused on the principal point if and only if I have fixed optics on my cameras because if I change the focal length by measuring the optics not only change the focal length, but I also change inevitably the position of the principal quad, because the two parameters, principal quad position and focal length, are intrinsically connected.  
  

So we will work on the idea that we want to calibrate in this way a general purpose motion analysis system with variable optics. We cannot accept to keep the optics fixed and to come up with a solution of this limitation by an apriorism and apriori calibration.  
  

Now, it is also important to say that in many situations, I'm thinking for example the optical tracking system which are used in surgical rooms, radiation oncology, these are systems...  
  

That do have a fixed optics.  
  

Because we don't want to change them.  
  

Because we need to have them always calibrated regardless of the way you move your camera system during the surgery. These are other problems. But that's to say that there exists indeed an application situation in which having fixed optics is not a problem.  
  

It is something that you need to have for other reasons. And the other reasons are the possibility to move the cameras inside the surgical room or inside your...  
  

Measurement volume according to the idea that you want to keep always a line of sight between the cameras and the markers in your field of view in complex environments.  
  

So in some cases it is not a scandal to think of fixed optics camera systems that would ease a lot this limitation because it will pave the way of the possibility of an a priori calibration for the estimation. of the position of the principal point and of the focal length also before going to be used in these systems. And in fact, typically these systems come pre-calibrated. So you open the box.  
  

You have your camera system embedded in a unique envelope with optics that you don't even see.  
  

With a fixed position of one camera with respect to the.  
  

This system of cameras is pre-calibrated so you put it on a tripod you switch it on you place a marker on the table and you have the 3d reconstruction of this marker expressed with respect to a reference system mounted on the two camera system envelope maybe one of the two cameras or in the middle of the two cameras and these camera systems are calibrated exactly in this way but with fixed optics a priori calculated in terms of this very handy okay the commercial system the ndi the polar ndi polar system they do come out on the market pre-calibrated so you don't need to do anything else then maybe map the reference system that you don't want to have solid to the camera system with respect to a laboratory reference system that you want to use and you spend like 12 000 euros.  
  

We want to calibrate the general part of the functional analysis system. So we want to...  
  

We cannot accept that we don't know and we cannot extract the principal point from the fundamental.  
  

Let's say for the moment we accept this limitation, then we will find a way to get rid of this limitation. For the moment.  
  

That is for the extraction from the fundamental matrix, the value of the focal length of the two cameras.  
  

We accept the idea that we know the position of the please.  
  

And also that's why in this K here.  
  

These two coordinates are placed to zero.  
  

We have already solved the issue related to the knowledge. of the principal function. The fact that we assume that we know it, it allows us to express the intrinsic parameter matrix with a 0, 0 in the last column, because we know where it is. centered the whole geometry in such a way that the principal point are exactly in the middle in the center of the theoretical position ideal position of the principal point.  
  

Now here there is one of these act of faith, maybe the only one that we have in order to proceed.  
  

There is a way to transform to rotate let's say the complex our stereo matrix system that was that we're playing around in order to obtain a lot.  
  

Alignment of the epipoles with respect to the camera mounted regular space in order to further simplify the geometry here and obtain an expression of the fundamental matrix in the form that you see here.  
  

It is a geometrical transformation that is the absolute comic interpretation. We are not going into details there. I will upload the Hartley and the Fouchera paper for those of you who are interested in reading this stuff.  
  

We are not really interested in the details here.  
  

We know that by introducing the two simplifications that are there, no skew.  
  

Knowledge of the principal point, there is a way to express the fundamental matrix in such a way that we are able to obtain an expression of the.  
  

F, the focal length of the two cameras as a function of the elements of this new expression ...of the fundamental matrix that is done exactly to obtain an analytical formulation of the focal length of camera 1 and camera 2 from the elements of the fundamental matrix. I need to have... the epipose here, these are the coordinates of the epipose of the camera one, the camera two and the camera one. These are scalars, so numbers.  
  

And it is possible to demonstrate that we can obtain a photo. formulation and algebraic formulation of the focal lengths of the two cameras from this simplified formulation of the fundamental matrix F in the frame of the absolute conic interpretation.  
  

For us.  
  

We introduced the simplification, we are able to extract algebrically the values of the focal lengths. that that's square there, it is important to notice that. So in order to obtain the real value of the focal length, plus or minus the scale factor.  
  

We need to extract the root, the square root of the values that we obtained with this formulation.  
  

So we need that these two numbers are positive.  
  

If I made something wrong.  
  

If I made concentrate my control points only in a very small portion of the field of view, if I don't have resolved properly the numerical instability for the calculation of f, it can happen that these two values, or one of the two, are negative.  
  

In that case, the focal length means that the focal length is an irrational number, it's a complex number.  
  

This is not acceptable. This means that I made errors or I have not mastered properly the numerical problems in the estimation of the elements of f and I need to do stuff again.  
  

So that is to say, it may happen.  
  

Due to the problems that are intrinsically in this formulation of the calibration, that things go wrong.  
  

And that I need to redo the calibration. To me, personally, it happened many times that the algorithm at the end tells me, no.  
  

Sorry.  
  

Because it finds negative values of the focal length. So there's something wrong. We did something wrong.  
  

We didn't provide properly the information that I needed in order to obtain a meaningful solution of the problem, in terms at least of the focal length.  
  

Let's go on.  
  

If we assume and we need to assume that we know the principal point then by extracting the focal lengths and let's suppose they are positive numbers so I can calculate the square root I solve the problem of the related to the intrinsic parameters now I need to concentrate on the extrinsic parameters of camera 2 with respect to camera 1 and these are only the only extrinsic parameter that I need to solve because of the initial simplification. I can include camera two on camera one, okay? And I will still work on the essential matrix. So if I know now the K1 and K2.  
  

I can make the essential matrix explicit.  
  

I know the value of the elements of the essential matrix because I can incorporate the two Ks from the fundamental matrix in order to make, highlight the real element elements of only the essential matrix, which by definition is the matrix that contains the exclusive parameters of camera two and camera one, and I perform a new singular value decomposition.  
  

And I will extract from the singular value decomposition matrices, u, w, and t that you see here, all the parameters that I need.  
  

T.  
  

That is the baseline, that is the translational vector.  
  

The position of the optical center of camera 2 with respect to camera 1, the position vector, it's only three scalars.  
  

The three components of the position vector of camera optical center 2 with respect to camera optical center 1 which is the origin of everything by definition by because of the simplification that is made is.  
  

The eigenvector associated to the smallest eigenvalue in the singular value No.  
  

You see here it is a t equals minus v3, v3 because it is the smallest eigenvalue.  
  

Or the eigenvector associated to the smallest eigenvalue, but also it is possible t equals plus v3.  
  

Two cases that we need to choose from.  
  

And there is an expression of the rotational matrix here that is a combination of these three matrices. The two matrices coming up from the... singular value decomposition u and v plus a service matrix if you wish z that has the expression that as you see here that is only needed to make things work in terms of matrix algebra.  
  

Algebra okay and here again i have two possible cases in terms of combination of these matrix products that interprets 180 degree rotations with one case with respect to the other so i have two choices negative value of the baseline positive value of the baseline and 180 degrees so whether the cameras are looking at you or I'm looking at you.  
  

And we don't know.  
  

We need to find here the right combination of the expression of the translational vector t and of of the expression of the rotational matrix are in such a way that the real scenario that we have in our lab is respected, okay? That I'm not pretending that the camera are pointing at you, but I've shown the points here.  
  

And that the two cameras are one on the right of the other, or one on the left of the other.  
  

This is simple to be done, because we always have a subset of control. control points for testing that will be tested exactly in terms of their relative position when reconstructed in 3D according to the calibration parameters that now I have in such a way that I know if I have made the right choices. So if the points that I reconstruct in 3D are in the position that I expect given the real scenario in which I have performed my calibration procedure.  
  

Any question guys? We still have to solve another, the last problem, right? Is everything clear? So let me summarize for you the basic concepts here, right? So.  
  

We start from the basic relationship.  
  

Of every polar field. P2 transpose multiplied by F multiplied by P1 equals 0. We need to know what is the geometrical interpretation of this equation.  
  

And the geometrical interpretation of this equation is... is that if I select a point that is exquisitely embedded in the epipolar geometry, that is the geometry that is underlying the method that we are exploring.  
  

The geometrical interpretation is that this equation expresses the fact that if I select a point on camera 2.  
  

Image plane, I will give rise to an epipolar line as a function of fundamental matrix on the camera image plane one and the point corresponding the point two on point one on camera one need to lay on the a people that's the geometrical I need to know some of the characteristics of s.  
  

And I need to recall that in F I have everything I need, the intrinsic parameters and the extrinsic parameters of camera 2 with respect to camera 1.  
  

How do I establish, how do I estimate the elements of camera F?  
  

Problems, numerical instability, solution, normalization and denormalization.  
  

Real case, I'm not using eight points, I'm using thousands of points. How do I formulate the system of equations? A multiplied by X equals 0.  
  

X is the unknown coordinates, the nine elements of the fundamental matrix. Because if I remove that, I don't care. I will just estimate the whole number, the whole nine elements of F, regardless if the F has only seven independent parameters.  
  

And how I formulate what is the expression of the form, from the shape of the matrix A, which is the .  
  

Stable one.  
  

Once I have the F.  
  

I need to solve the problem to extract, I mean, I can do whatever I want in terms of mastering the polar geometry, I draw whatever I want to draw there.  
  

I need to concentrate on the problem of extracting the intrinsic and the intrinsic parameters from F. The intrinsic parameters are extracted only in terms of the two focal lengths with no skew of the two cameras. So one number for camera one, one number for camera two. for camera two.  
  

I obtain this extraction if and only if I assume to know the position of the principal point for camera one and camera two.  
  

That has a side of implications there.  
  

That is the problem that we need still to solve.  
  

And I know that there is a formulation that allows us to express the fundamental matrix as a function of the epipolar coordinates, the comments of the two. two epipoles and a matrix of scalars in such a way that I can obtain the analytical expression of f1 and f2 as a function of the epipoles coordinates and these scalars.  
  

The formulation that gives us the square number, the squared value of f1 and f2 that I need to obtain with a square root for having the right estimation of f1 and f2.  
  

So I need that the numbers that I obtained from this simple relationship are positive. It can happen they are negative.  
  

This allows forces to redo the acquisitions of the points.  
  

And let's remember that the F needs then to be scaled according to the scale factor that is something that we need to introduce in the procedure because there is no a priori knowledge of the physical world in which everything is taking place.  
  

So it can be in the scale of meters or of nanometers. The proportions are there.  
  

Everything could be valid even if we are moving in a microscopic or in a macroscopic world. So we need to have at hand a scale factor that restores the physics of the real world in which the calibration takes place.  
  

Then...  
  

We have the K1 and K2 in this way, and from the K1 and K2 I can make explicit the essential matrix and obtain by singular value decomposition the rotational component and the translational component of the extrinsic parameters of camera 2 with respect to camera 1.  
  

And in this case we have multiple choices.  
  

Camera 2 on the right or on the left with respect to camera 1.  
  

Camera points in front or in the rear of the camera. So the orientation of the camera. camera system can be 180 degrees variable. And I need to choose the right solution, the right combination of solutions. It will be trivial because it will come out from the last problem that we need to solve having available... available a cloud of testing points in order to test what is the choice that is the right one in terms of extrinsic parameters of the particles.  
  

These are the basic concepts that you need to recall in this work. Let's face the last problem.  
  

The last problem is related to the extraction.  
  

Of the principle. I told you there are cases in which this is not needed because we have fixed optics, we want to calibrate a general purpose motion analysis system in our lab, so we need to solve this problem.  
  

The last simplification is the most critical one. It was, I know where they are. I don't really know where they are.  
  

What is the solution? The solution is to apply large-scale optimization algorithms.  
  

These kind of optimization algorithms that are not only iterative, but are...  
  

Structured in such a way that they explore widely the space of the solutions of the product in order to minimize the risk to fall into a local minima of the space of the solutions and not be able to move from this local minima thus.  
  

Spitting out the wrong solution of the product.  
  

One example of this large state of humanization algorithms are the so-called genetic algorithms it is only one possibility but we will explore this one the idea of the genetic algorithms is to perform a set of calibrations.  
  

According to initial set of assumptions of the position of the principal point and have available a method to rank the quality of these calibrations.  
  

So the idea is, okay, let's do like this.  
  

Let's start by generating a set of assumptions of the position of the principal points in the two cameras.  
  

The first assumption is, in both cameras, it is in the center. of the camera image plane.  
  

But then I say, if this is the camera image plane of camera one.  
  

It may be in the center, then this is the first assumption. The second assumption is I start moving around. the assumption of the principal point position generating.  
  

200 assumptions 300 assumptions of the position of the principal point many and the same for camera 2 so I generate 200 for camera 1 200 for camera 2 so I have a lot of different combinations possible.  
  

Of the stereometric system. Okay?  
  

Camera 1, first assumption, can go together with all the camera 2 assumptions.  
  

I get a very high number very quickly. This...  
  

This is the first generation of assumptions in the architecture of my genetic algorithm.  
  

It is a first generation. It is a primordial animal generation.  
  

200 billion years, a million years ago.  
  

What do i do for every for each of the assumptions i perform the calibration i have my cloud of points stored shown and stored by the system i do the calibration so when i get to i i let's say i do the calculation of the matrix f which will always be only one time and then when I need to extract the F.  
  

I use one assumption of it. many that i have generated in my first generation of the genetic algorithm i take out the 2f i take out the extrinsic parameters and i have one calibration parameter set for each assumption if i have four thousands assumptions as combinations of the assumptions made for camera one and camera two i have four thousand set of calibration parameters.  
  

I need now to rank.  
  

The quality of these calibration parameters that is the quality of the assumptions that underlies the calculation of each of these calibration parameters.  
  

How do I do that?  
  

I extract from the whole cloud of points that I've shown to the system a subset of points that I will not use to estimate the fundamental matrix. So these are points that... did not participate in the estimation of the parameters of the fundamental matrix. So these are independent points.  
  

And I use these points as testing points.  
  

Of course, I have to select these testing points uniformly from the cloud of points that I've shown to my new system. So it is not that if this is the field of view of the camera and these are the points that I've shown to the camera, I think make as the testing points this one.  
  

Okay, I would be really stupid.  
  

I need to extract them uniformly from the whole field of view of the camera.  
  

Okay.  
  

Respecting the correspondence between camera one and camera two.  
  

So I will have like 80% of the points that I have shown to my system that are used to estimate F.  
  

And 20% of the points uniformly extracted from the whole configuration of points that will be used for as testing points.  
  

So that for each calibration, I try to reconstruct in 3D.  
  

These testing points.  
  

I do have all what I need to reconstruct in 3D, because I have all the set of camera parameters. I'm reconstructing in 3D these points, these testing points, and I need to extract some metrics in order to...  
  

Estimate the level of accuracy of this reconstruction that will be linked to the accuracy of the estimation of the calibration parameters that will be linked to the accuracy of the assumption of the principal points that I need.  
  

Okay?  
  

So I need some metrics on the 3D reconstruction. We have two metrics that we use. The first one is the 3D reconstruction error.  
  

Now when we do the reconstruction in 3D.  
  

You know that.  
  

I have the line from camera 1 on which I know that that will be the point in space.  
  

I have the other line from camera two linking the center of perspective, the projection of the points on the camera image plane, and on which same line I need that the point in space needs to be.  
  

Intersection of the two lines, that is the point in space.  
  

The two lines.  
  

They never intersect in reality. Theoretically they do.  
  

But we have inaccuracies, uncertainties, so that we always be, I never recall the word in English in this case, every year, they are .  
  

They do not encounter in space.  
  

So by the assumption is that the position of the point in space will be in the middle of the minimal segment representing the minimal distance between the two lines.  
  

The more wide, the more apart are the two lines.  
  

The bigger is the error. The bigger are the inaccuracies.  
  

If I'm doing things right, the two lines, they never intersect, but...  
  

The distance between the two is more.  
  

The bigger is the distance, the bigger is the 3D reconstruction error. That is, by definition, the size of the segment, the minimal distance between the two lines.  
  

The bigger is the 3D reconstruction error, the worse is the quality of the reconstruction.  
  

So when I reconstruct in 3D the testing points.  
  

I compile a vector, I fill a vector of the 3D reconstruction error that I have for the single calibration.  
  

Out for example the mean or the median value of this reconstruction error for calibration number one or calibration number two and so forth and so on so i have a first method for ranking each of the camera calibration that i have obtained as a function of each of the assumptions that i have made on the principal point of discussion.  
  

I need another one to obtain a more robust ranking of the calculations that is linked to the so-called expected features.  
  

Do I have anything that maybe... is an expected feature in the cloud of points that i've shown to my system yes if i have a third marker on the magic wand the distance that this marker has with with respect to marker number 2 and marker number 1 is a distance that I have not used as the scale factor, because I've used the one marker 1 and 2 as the scale factor. So I cannot use the same matrix, because I've already used it.  
  

So I need another one.  
  

Very powerful.  
  

That is the distance between marker 3 with respect to marker 2, for example.  
  

That is a very powerful expected feature because it can happen that even reconstructions with the let's say over threshold 3d reconstruction error is a good reconstruction and the quality of this reconstruction is confirmed by comparing the distance that i have between marker 3 and marker too theoretical with the real one that comes out from my freedom dimension of the construction.  
  

I put together the two in whatever combination I want and I have a unique matrix made by two matrix.  
  

One from the third dimension of the construction error, the other one from the expected feature feature of expect.  
  

That are used to make the ranking of the calibrations much more robust.  
  

So the question.  
  

Why do I have to have three markers on the magic wand?  
  

One for the scale factor, the other one for, or the other two if you wish, but one is because They're not independent. one another for the expected feature metric calculation when ranking the calibrations according to different assumptions of the principal points position in camera 1 and camera 2.  
  

Well, now the game is done. So I do my ranking.  
  

And I could do one thing. OK, let's take the best one, and the game is done.  
  

Now, I'm not doing a large optimization algorithm in this case. I'm restricting a lot here. the vision of the optimization algorithm i need to go forward because you have to keep in mind that the difference is between the different assumptions of the principal point position is is a sub pixel stuff there's very small variation.  
  

But even a small variation of the principal point has a huge effect on the focal length estimation and therefore also on the explicit parameters estimation of the camera 2 with respect to camera 1. So it's a very sensitive parameter.  
  

Even very small variation of the principal point may cause improvement or decrease of the accuracy of the 3D measurement.  
  

The assumptions that I make is that, okay, center then center plus 10 to the minus three pixels in the X direction.  
  

It's very small direction, very small variations. So I need to go forward. And I don't need only one generation of assumption.  
  

I need to...  
  

Switch and get into the future of ten millions years and give birth to a new generation of assumptions. The first generation was done randomly.  
  

Generation will be obtained by letting different results, different assumptions belonging to the first generation, mate on one another, mate coupling to one another. together good assumptions or bad assumptions or good assumptions with bad assumptions trying to mix stuff trying to mix the DNA's of good guys with bad guys in order to enlarge the vision if I would make only good assumptions the first ten for example the one with the ten the two with the five but I would have I am piloting, I am biasing the optimization algorithm towards one local solution.  
  

I want to keep the vision wide, so I will generate the second generation of assumptions in terms of positions of principal points in camera one and camera two by coupling good cases with good cases, bad cases with bad cases.  
  

And good cases with bad cases. cases generating in you can we reality there are there are criteria for these meetings okay so it's not the before and only you take the one you can try to do the one with the inverse sign there's a lot of possibility for generating the second generation from the first one the important thing to me is that I'm not considering only the good cases.  
  

I need to consider the good cases and also many of the bad cases and of the average cases in order to keep the vision of the optimization algorithm wider, larger.  
  

Because that's what I want to do.  
  

Because in this case, due to the fact that it is an impulse problem, it is very easy to fall into a local mean and stay there.  
  

But it will not be the optimal solution.  
  

So I generate the second generation.  
  

And I do the game again.  
  

Calibrate, ranking on the calibration, I still have thousands of cases, hundreds of cases.  
  

And I go on generation after generation.  
  

Till a situation in which the new generation.  
  

Or let's say the best case of the new generation, will not improve the quality on the matrix, the values of the matrix.  
  

With respect to the best case of the previous generation, when the improvement will be below a predefined threshold involving the two metrics that I've used.  
  

3D reconstruction error an expected feature, then I can stop.  
  

But this improvement will be very very small, the threshold is very very small, 10 to the minus whatever.  
  

Millimeters in terms of 3D reconstruction error. and the expected features like.  
  

10 to the minus 2, 10 to the minus 3 millimeters.  
  

Okay?  
  

Then I can stop. Typical numbers.  
  

Tens of generations, 20, 30, 40 generations until I get to the final criteria I spent, with respect to the final stopping criteria.  
  

Okay?  
  

So it takes some time.  
  

Nowadays with the power of the computers it takes some minutes, okay, or minutes let's say to have the calibration, to have the algorithm do the calibration. the f is calculated only once but the extraction of the proper calibration parameters the reconstruction and the calculation of the matrix takes time when you have to deal with the 21st.  
  

Of the points that is probably 2,000, 3,000 points.  
  

Okay, so it's a good numbers that the computer needs to do. So it takes time, but it is the only way to come up to a assumption of the principal point position that is meaningful and that allows you to have a system of cameras calibrated in a proper way in the general path was application of the motion analysis. I think we are done.  
  

Any questions?