
19/11/2025
***
![[Pasted image 20251119083507.png]]
In particular we recall the so called ICP algorithm

![[Pasted image 20251119083836.png]]

so you should write down a flow chart

![[Pasted image 20251119084101.png]]

And one possible solution, if we talk about hybrid acquisitions

![[Pasted image 20251119085442.png]]

let me show you a video of that...

![[Pasted image 20251119090231.png]]

now, with this kind of approach you can really get

![[Pasted image 20251119090558.png]]

Our second problem is now

![[Pasted image 20251119090618.png]]

We should not forget that when we get to the final representation


![[Pasted image 20251119090649.png]]


and frame by frame we are able to animate

![[Pasted image 20251119091021.png]]


![[Pasted image 20251119091329.png]]
now, for the following lessons


***

Specific references to radiation oncology...

***


VIRTUAL MODELLIN 6

**Participants**   

**Date**    2025-11-19

Known geologically and that exists two variants of this technology the fixed one and the handheld one and these are the reference technologies for this specific then we learn that there is also another possibility of pure passive acquisition with the let's say stereo camera without the need to project any energy any light any energy on the subject they work with receiving and they require trivial depth from disparity, so the problem in that case was to try to find the disparity the disparity between the horizontal disparity between two images taken from two stereo cameras with optical axis more or less parallel one another with an analogy with the vision system with the human vision system of the mama's vision system itself.  
  

We still have to do one thing because we understood that in many cases, especially if we are using, which is mostly the case, a fixed system, a triangulation based fixed system.  
  

There is not the need, the possibility to acquire with a unique acquisition, the complete surface that we are interested to describe. Because these systems have, for the way in which they are realized then they have a limited field of view.  
  

So you can imagine a situation in which you place your fixed system in front of the subject, you acquire the frontal plane of the subject, but you might be interested also in acquiring part of the sides of the subject or maybe the entire closest surface, body surface of the subject. It is required with this kind of systems multiple acquisitions in which you leave the subject still and you move around.  
  

The fixed system in different positions so to enlarge the field of view of the system with multiple acquisitions.  
  

This of course requires that the subject stays still because any motion of the subject between one acquisition and the other is a source of error, is a source of noise, so this takes time so motion of the subject can be a sure easy issue.  
  

And the other problem is that due to the fact that the cloud of pomits.  
  

That are determined in 3D by this kind of systems are expressed with respect to a reference system solid with the system. If I change the position of the system, I will have the different patches of surface that I acquire expressed with respect to different reference systems.  
  

So there is the need to identify a unique reference system, maybe the one belonging to the device in the first acquisition and express the other patches acquired and reconstructed in 3D and express with respect to other reference systems, the same solid reference system in the system.  
  

But displaced in space with respect to this unique reference system.  
  

This problem is solved by the so-called surface stitching procedures or surface registration procedures.  
  

Stitched together.  
  

Different touches acquired and expressed with respect to different references. That is a sort of surface matching case that is faced by means of iterative algorithms.  
  

In particular, we recall the so-called.  
  

ICP algorithm, that is not an important iterative closest point algorithm, Teresa the prototype, if you wish, of all the surface matching procedures that have been proposed in the literature.  
  

How does this algorithm works?  
  

It works by trying to find the roto-translational operator, rigid operator, that takes one patches and superimposes these patches to another one, to another reference surface. So we have a moving reference, a moving surface, that is described by comments in 3D. So this happens before the reconstruction of the action, because of the reconstruction. We have a moving cloud of comments, a moving surface, and we want to find the robot translational operators that takes this moving surface and superimposes it to another surface which is considered fixed and has irreverence.  
  

The problem here.  
  

That looks a lot like the auto-translational operator estimation in case of using physical markers. Remember what we talked about in terms of the mapping procedure after the calibration with the non-triple points.  
  

Here the problem is that the two patches do not possess the corresponding points.  
  

So it is not that I have a data set which is common and clearly identifiable in terms of correspondence between points as I had in that mini calibration procedure that we described when we talked about the mapping procedure to take the reference system from the camera up in the ceiling and bring it to the reference system of the lab. Here I have a cloud of points that may be m points irregular cloud of points in 3d and i need to superimpose this moving cloud of points with respect to a reference cloud of points irregular with m points with no chance of describing or having available limited a correspondence between points so point number one in the moving cloud points is not the corresponding point in space of point number one in the reference data set. Okay.  
  

So I do not have this information and the algorithm needs to estimate this correspondence. So if you should write down the flowchart of this algorithm, here is how it works.  
  

We have an initial estimation of the parameters of the rocket translation What was the initial of the 4x4 matrix?  
  

In homogeneous coordinates.  
  

This estimation can be trivial, then we will discuss about it. But we give, we provide an initial estimation. We try to behave as if we were treating corresponding points of physical markers.  
  

So what I do is to build with this initialization of the parameters of the autoconsolidational matrix, I build an initial operator 4x4 autoconsolidational operator.  
  

And I apply this rototranslation to the moving dataset. So I take every point of the moving dataset and then pre-multiply the coordinates of these points with the rototranslational operator that I just built in the first iteration. Okay.  
  

Then I need to estimate a metric of comparison between the moving dataset and the reference dataset. Something that tells me the level, the degree of superimposition that this rotor translational operator has brought into my program. So the way in which by rotor translating the moving data set I was able to superimpose this moving data set on the reference data set.  
  

In order to calculate this matrix of comparison we need to establish a priori a criteria of correspondence between points and the idea of the iterative closest point also the name tells how it works is that the correspondence is established by finding for any point on the moving data set the point belonging to the reference data set that is the closest point possible okay so if i had like a situation.  
  

Like this and my move my reference data set with the points okay is this at a certain point the first iteration or end iteration this is the moving data set which has been brought in whatever position by applying the end.  
  

Proto-translational operator which was estimated at the end iteration. When I want to establish my negative comparison, I need to establish a correspondence. So I take the first point of my moving dataset and I look at the distance that this point has with respect to all the points on the reference dataset. So I calculate this distance and this distance.  
  

This distance, this distance.  
  

And I establish the correspondance between point number one on the moving data set with the closest point of the reference data set. In this case, this one.  
  

And these two points become brothers. The two points become the corresponding point in this specific iteration.  
  

Then I take the second point on the other set and repeat the operation point by point, establishing the consisteness between all the points of the moving data set. and the points, the closest points on the reference.  
  

Once I have determined the correspondence.  
  

The metric calculation is trivial because I behave as if these corresponding points were physical markers. So I just compute the square distance of the corresponding points, I sum everything together and I have my overall metric comparison metric called superimposition of the moving data set with respect to the reference data set.  
  

Then I go on, here is the metric below the threshold, okay, I'm out. And this is the error of translation of operator that is the best operator that will superimpose the moving data set with the reference data set.  
  

If I'm above the threshold that I established a priori, I will have the updater data. according to whatever minimization criteria will update the parameters of the ROTO-translation operator and I start with the following iteration in which I will rebuild the ROTO-translation operator according to the updated parameters I will apply the ROTO-translation operator to the moving points I will find again a new correspondence because things will change so that correspondence at the previous iteration will never be the same correspondence in the following iteration, I compute my matrix and I go on till I find a acceptable degree of superimposition according to the metric above or below the fraction.  
  

Do these algorithms work?  
  

More or less. They are not robust.  
  

So there is the need, first, to have a good initial estimation of the transformation. That is to say, I cannot pretend to align successfully the moving dataset on the reference dataset if I start from the situation like this.  
  

Okay, so the cross are the reference dataset and the balance are the current dataset. If I'm very far away from the alignment.  
  

I will never succeed.  
  

Because the first correspondence that we found in the first iterations will lead the algorithm to converge towards a local minima with no hopes to get out from this local minima and fall down in the absolute minimum of the problem.  
  

That is to say for our application that when I change the position of the static system to perform different acquisitions, I cannot rotate and change a lot the position of the static system.  
  

I have to move the system slightly, with slight rotation around the subject, possibly multiplying the number of acquisitions, but not changing too much the position of the static system of acquisition from one acquisition to the other. Otherwise the two patches will be too far away.  
  

And when I will pretend to stitch them together, I will have a lot of troubles.  
  

Okay, so first the two patches need to be not too far away. There must be, I mean, the parameters of the rotor foundation needs to be small for the superimposition of the patch.  
  

And the second issue here is that we have to count on a common layer between the two patches.  
  

And that also forces the motion of the static system to be very small. because we have to ensure that there exists a whole layer of superimposition, a common layer between the two patches, otherwise they will never work. Okay, I will not have the data that I need to perform a superimposition, to perform the stitch.  
  

And another issue is that this algorithm works if and only if there exists sufficient information in terms of.  
  

Surface morphology.  
  

Because if I pretend to superimpose, as it is written here.  
  

One hemisphere on the other, on another hemisphere.  
  

I will have some degrees of freedom of the problem, which are left free.  
  

Because think about two hemispheres to be superimposed on one another, the rotation around the symmetry axis is left free.  
  

This is a whole set of possible solutions. in the space of the parameters like this.  
  

The degree of freedom of rotation between two hemispheres, because I don't have any information that forces the problem to converge towards a unique absolute minima.  
  

This degree of freedom is left free. So I have an infinite number of solutions of the problem with the metric very nicely below the threshold, but leading to a wrong solution of the problem.  
  

So I need to have even the patches that I want to superimpose a sufficient level of information in terms of morphology of the surfaces that I want to superimpose. So it's good if I want to superimpose the face, two faces or two patches of surfaces belonging to the face.  
  

In which I have the nose, I have a lot of morphology that is leading and is anchoring the superimposition.  
  

In small possible solutions. But if I do not have this kind of information, for example, I want to register pseudo-spheric surfaces or planar or pseudo-planar surfaces, then I will never get to the final solution. the proper solution and we have too many possible solutions available and the stitching will.  
  

Be typically leading to very wrong superimposition of the two patches.  
  

One possible solution in the critical case.  
  

Let's put some physical points on the two patches.  
  

So if I'm not acquiring simply the surface but I have an optical system capable not only to to recognize the light point projected on the surface or the pattern of structured life projected on the surface but i add also a couple of physical markers not necessarily the three that i need to detect estimate position and orientation of the energy body in space this physical marker can serve as constraints for the stitch okay in that case I'm able to couple the acquisition of the surface expressed as cloud of points in space with the acquisition of a small number of physical points of markers that will be needed in order to detect the position and orientation of the different edges and ensure a proper stitching of the different patches that i have then you see here they are confrontational heavy yes because when i need to find the correspondence i have to look at all the points if I have thousands of points in the two patches then they they are we can take a lot of time and it is a computational certainly okay now till now we spoke about the problem of describing the morphology infinity of a human surface and as I told you at the beginning of this discussion.  
  

We said that in this case what we need to take care of, but in order to ensure the quality of the representation, of the description, is that the motion is not there.  
  

So we need to ensure that any motion of the subject is possibly, as much as possible, cancelled away.  
  

And we spoke about the cysts, so any technology that we spoke about should be judged. also in terms of the speed of acquisition. The faster is the acquisition.  
  

The lesser will be the effects of any motion typically performed by the subject, the voluntary motion, during the acquisition. So very nice the two three seconds scanning acquisition of the static system.  
  

Not nice the long acquisitions of handheld devices.  
  

Very good the snapshots which are taken by the stereo passive camera systems.  
  

Working completely passive because in that case time is not an issue. Very nice also in this respect the systems that work with structured light projection because then we acquire two snapshots of the surface illuminated by the structured light of pattern light with no issues related to time.  
  

But due to the fact that the highest accuracy potential is obtained by triangular base of aperture, The problem of motion needs to be solved somehow. And one possible solution, if we talk about hybrid applications, so if we talk about the use of systems capable of detecting the position in TV and then in 3D on a couple of optical tracking cameras.  
  

Not only of light points or light features as the ones that we use for when we project the structure light pattern on the subject but capable also in the same time to acquire to identify and reconstruct in 3d a configuration of a small configuration of passive control points of conventional math, yes, which is rich.  
  

Well, this solves most of our problems. problems related to motion even if the acquisition takes time because in this case as the sketch is describing during the acquisition so any frame that i acquire in the acquisition will be composed by an information consisting of not only the position of the light point projected on the surface of the subject or the entire light line that is scanning the surface of the subject. But it also consists of the position of the configuration of passive markers that I have placed on my subject.  
  

And in this case it is possible to express the position of the light point and the position of all the light points captured during a prolonged acquisition.  
  

With respect to a local reference frame mounted on the subject, and built by means of the knowledge of the position of the configuration of the passive control points that I'm able to acquire together with the live points frame by frame.  
  

So the idea is, okay, I have my frame.  
  

I will have on the surface of the subject with the configuration of, let's say, three control points, This is the light point that is projected to frame number N.  
  

I see this situation on two TV cameras.  
  

So I will have a second image, very similar to this one, or let's say, with a proper 90 degrees optical axis angle in this case, because we are falling back into the conventional stereometric situation.  
  

I will use the three markers reconstructed in 3D. to build a local patient-mounted reference system. For example, I take the barycenter of the three markers.  
  

I use one marker as the one defining the first axis, I take another one and I calculate the vectorial problem in these two vectors, so I will have a vector perpendicular to the board, which will be my z-axis coming out, and then I will apply another vectorial problem to obtain the third. axis, the y-axis completing my reference system mounted on the subject. Okay?  
  

Pictorial algebra, easy to do. It is exactly what we do when we want to identify position orientation, the orientation of the rigid body in space. We need three non-collinear points and we use them according to specific rules to build a local reference frame mounted on the rigid body in space that will in turn provide us with the operators, rotational matrix and transnational vector, describing position and orientation of the rigid body in space with respect to the laboratory reference frame, the observer.  
  

That's exactly what we do here.  
  

Once we have this reference frame built, the local one.  
  

I will take this point, the light point reconstructed in 3D by the optical tracking system and initially.  
  

Expressed with respect to a laboratory reference frame, the one with respect to which we have calibrated the optical tracking system, and I will map the coordinates of this point to be expressed with respect to the local reference frame, using the in-depth of the auto-translational operator that express position and orientation of a rigid-body patient in space with respect to the laboratory.  
  

Okay, so I will have the point, the right point with respect to the patient will be the inverse, that is the transpose, I don't want to say the inverse in this case, of the rotor translational operator, the expressed position of the patient with respect to the laboratory, multiplied by the point expressed in the constructed attribute with respect to the optical tracking system. That is expressed with respect to the laboratory.  
  

Is obtained by building the reference frame after the sample. So I can align the X-scala products of the versor of the axis of the local reference system in the rotational matrix, and I take the position vector of the orange of the local reference frame as the translational vector to be placed in the fourth column of our rototranslational operator 4x4 matrix in an homogeneous form.  
  

And the game is done.  
  

And I do this at every frame.  
  

If I do this at every frame.  
  

The cloud of points that I will reconstruct will be always expressed with respect to the patient.  
  

And if the patient moves.  
  

The rigid component of this motion.  
  

By means of this method, is cancelled out.  
  

Because I will take the motion the rigid component of this motion of the patient and I will take it out from my talk. So I will take out the effects of this rigid component of the patient motion in the description of the 3D position of the cloud of points belonging to the surface that I am acquiring.  
  

Okay.  
  

Let's see and this is particularly important. as a solution when I'm using handheld devices because I really, I mean if the fixed systems are two three seconds faster, so they are really fast.  
  

The handheld device acquisition takes a long time so this solution is more or less required.  
  

Nevertheless.  
  

If it is already difficult for the operator to ensure that the handheld device is pointing to the surface. This is not a big problem. But the handheld device is being seen by the optical tracking system that needs to localize the tracker, the handheld device. And the optical tracking system now needs also to look at the patient to track the configuration of passing markers placed on the subject. So the situation becomes a little bit complicated to be.  
  

Realized in a laboratory, even in a laboratory. So you need a lot of control conditions in order to come up with this kind of solution. Let me show you a video of that.  
  

So this was an experiment that was mimicking exactly what we're seeing. So what do we see here? We see a phantom.  
  

We see the configuration of passive control points placed on the phantom.  
  

We had an optical tracking system watching the scene, so looking at the subject.  
  

While an operator was performing.  
  

First.  
  

An automatic scanning acquisition with a fixed static system.  
  

And second, a second acquisition with an un-held device that was tracked by the same optical tracking system that was looking at the subject. Here on the right you will see the cloud of points coming out from in real time, reconstructed in 3D from this kind of a position. Let's see what happens.  
  

Now we should see the first scanning.  
  

Here it goes. This is the automatic scanning by the fixed reference system. It's the static reference system that is projecting this pattern of the points on the subject and it is getting.  
  

The acquisition, it is generating this cloud of points here on the right. The operator here is moving the phantom rigidly.  
  

Mimicking or simulating a rigid motion component of the patient and you see that there is no effect on the cloud of points. Let's see it again. So we should expect we do not correct things as I just explained to you. that the cloud of points being acquired in presence of motion is very much displaced with respect to the cloud of points portion acquired with no motion.  
  

And then after this first acquisition, the handheld device, the prototype of it, comes into play. You see this is the laser point, this is the camera with the known geometry there, so it is a triangulation based approach on a handheld device. you have the markers that are captured by the same optical tracking system that is now watching not only the markers on the subject but the markers also on the handheld device. and the acquisition is completed in the part of the subject that are not visible by the static system that acquired the first the first position okay that's the way in which the at least the rigid component of the motion of the subject can be it is something that.  
  

Leads us to hybrid acquisitions.  
  

Only right points or patterns, but also passive markers, very useful to cancel out the motion and useful also to perform the stitching in a robust way and do just the same. Okay.  
  

Now with this kind of approach you can really get to very high accuracy in the representation of your models, of your patients, with a complete acquisition, also on the sides of the subjects, of the patients in this case, in plastic and reconstructive surgery, with very high accuracy.  
  

Now our second problem is now to try to mount motion on the surfaces. Okay, so once we got to the.  
  

Goal to be able to describe with high accuracy the static morphology of the surface, we can also think of trying to animate this surface. So try to see what are, to estimate what are the effects of motion on the surface patch that we just acquired and described in 3D. What are the purposes of this? It's to realize and render.  
  

Of the kinematic behavior of the surface fracture in presence of motion.  
  

So if you think, for example, of the application of plastic and reconstructive surgery, which I saw a figure there.  
  

The outcome of the surgery should not only be expressed in terms of restoration of the morphology in a static fashion, right?  
  

So like there are no asymmetries.  
  

The dimensions are comparable between the left and the right, where the right is reconstructed and the left is not reconstructed, after the ecology demolition, ecological demolition.  
  

But one could also expect that the outcome of the surgery can be judged in terms of the behavior of the whole surface in presence of motion.  
  

A dynamic assessment of the surgical process.  
  

This requires modeling. So this requires to try to model the dynamic parameters of the surface structure that we have just generated. And we have two choices here.  
  

The first one is a physics-based approach.  
  

So we use finite element modeling to obtain the propagation, the effects of the propagation of motion. on the surface patch that we have available in terms of our morphed-tack morphology.  
  

The problems here are that we may find a lot of singularities. The more the richer is the patch in terms of number of points and of surface elements.  
  

The bigger is the probability to find singularities in the inversion procedure of big magnetism as the filter involves the path.  
  

Plus, we do not have any possibility of online, real-time representation.  
  

The second possibility is to use a simulation. So not a physics-based approach.  
  

But a pseudo-mechanical approach.  
  

And the pseudo-mechanical approach is based on the so-called mass-spring-dump term. models that allows us to perform fast simulations, not physics-based, but where the goal is the reality of the good agreement of the behavior that this model gives with respect to the real case. It's a simulation, it's not a physics-based approach, physics-based calculation, it is a simulation. But if we are good enough to select the proper mechanical properties of the mass-spring modus, the mass-spring-dump-dump modus, then the reality of the representation can lead, can reach a really very high degree of realisticity, let's say.  
  

Let's see what they are.  
  

We should not forget that when we get to the final representation of the morphology of the patch, of the surface patch, we will have an action made up by elements, not necessarily triangular.  
  

But polygonal elements that will be characterized by the position in 3D of the vertices of these elements.  
  

So if we have the delunite triangulation, so I have my mesh generated like this, and you saw the other day.  
  

For every vertex we have its three-dimensional coordinates in the face, expressed with respect to whatever reference system.  
  

Then we have the rules of connection of these points.  
  

So point number one.  
  

Is connected in the mesh to point number 42. It could be. So we need to bring along the information of the way in which the points, the vertices of my mesh are connected one another. What are the sizes of the triangular elements that compose my mesh.  
  

And then we need to know the normal.  
  

So the three scalar components of the normal versor to each of the elements of the surface mesh.  
  

In order to know how this element is oriented in space.  
  

These are the information that I need to bring along after I have generated the mesh. And it's not a low amount of information. information it's a big amount of information for many many points thousands of points it's a lot of bytes that are needed to bring along this kind of information but if i have this the mechanical parameters that i can assign to the surface measure are a mass that is assigned to each vertex of the mesh.  
  

So the vertex of the mesh becomes a material point possessing a mass.  
  

Then for any side connecting different points.  
  

I will assign a parallel on this segment of a spring with a specific elastic constant and a damping element with a specific damping factor.  
  

Mass will be proportional to acceleration of the material point.  
  

Spring will exert the force proportional to the elongation of the side.  
  

And the damping will exert the force proportional to the velocity of the displacement. So we have all the ingredients that are needed to write down for each point, for each vertex.  
  

The equations of equilibrium between the forces that are exerting, that are present on each of the points, each of the vertex of the mesh.  
  

If we take a snapshot, we will have a point which will have a force proportional to the acceleration that this point has at this moment, another force proportional to the velocity of the displacement, and the third force proportional to the elongation that exists between this point and another point connected by line okay plus the external forces the gravity right so if we have a mesh and we perturb the equilibrium of this mesh we are able to write down a set of equations for each vertex.  
  

That express the equilibrium, the new equilibrium that the mesh needs to find in that specific frame. And frame by frame we are able to animate.  
  

We are able to find out the different configurations of the mesh in order to respect the equilibrium frame by frame.  
  

Giving rise to a set of configurations of the mesh that in turn will represent the motion of the mesh cell. Let me show you an example.  
  

Which is not...  
  

Maybe this one. This one. This is a planar membrane. Okay? Triangular mesh. What happens? Let's start from the beginning.  
  

What happens is that the initial equilibrium of the membrane is perturbed by an external application of the force.  
  

In this case, I'm not showing you.  
  

One of the vertex was raised up and then left.  
  

And this membrane is under gravity. So.  
  

Frame by frame, the calculation of the new equilibrium of the membrane gives rise to the animation that we see here. by selecting properly the damping factor, the plastic constant, and the mass applied to each of the vertices of the mesh, it is possible to obtain a very nice representation in this case. Right? Let's see it again. You see at the beginning it is pulled up, then left, and this is the result of the motion.  
  

But if you are able to do this.  
  

That if we have an anatomical surface that is.  
  

Described statically in 3D.  
  

We can think of the way in which we can mount motion units by assigning the dynamic parameters to the mesh. Mass.  
  

Constant, elastic constant, and damping factor.  
  

And using the motion coming from a configuration of points belonging to the surface, for which we have the motion in order to perturb the static equilibrium, the initial static equilibrium of the mesh, of the anatomical surface.  
  

So if the same configuration of control points have been used previously to acquire motion, during the execution of whatever gesture by the subject.  
  

Running.  
  

Walking, raising the arms and stuff like that. I realized during the execution of this motion, in a position of a configuration of passing markers belonging to the surface, then I have available the trajectories of these markers in 3D during the execution of motion, which represent the motion with a very big under sampling of the surface. I'm gonna have this back in here. complete representation of this surface that I'm interested in.  
  

So I can take one of these points on the subject.  
  

On the morphology, on the static morphology of the surface, I take one of these markers, that was here, and I use the trajectory displacement of this marker as a way of per... to be the equilibrium of a morphological representation, the static morphological representation. As if it happens with the membrane, it will be the motion of the marker that will be attached to one of the closest vertex of the surface to perturb the equilibrium of the static mesh.  
  

And if the static mesh is characterized by the dynamic parameters that we saw before, then this perturbation can be propagated over the whole surface.  
  

And we are not using only one static matter, we use more than one. We use, for example, the classical anatomical lammas that recognize on the torques of a woman, for example. And we use all of them, we use all of the motions of the whole configuration of the passive matters to perturb the static equilibrium of the surface mesh that we have generated.  
  

By applying the proper dynamic parameters, we obtain a propagation of this motion onto the whole surface and ultimately the dynamic behavior, the estimation of the dynamic behavior of the surface during the execution of the solution.  
  

And I show you a couple of examples always in referred to the plastic and reconstructive surgery for outcomes generation. This is the same phantom with the motion of running acquired by a real subject so the representation is quite realistic but more of that we have other representations here like.  
  

A depth map during the raising of the arms by a patient that received the prosthesis implants in one of the breasts. And you can really assess in this case the dynamic behavior of the surface.  
  

So not only a static evaluation assessment of the surgical outcome, but also a dynamic assessment of the surgical album. So, the dynamic behavior of the.  
  

Target of the surgery in presence, for example, in this case of the implant of the breast prosthesis. And you see the different behavior of the two breasts, the healthy one and the operated one.  
  

With the presence of a simple motion of arm raising. And this is something that we are moving on, let's say, in terms of surgical outcome assessments, not only on the static morphology, but also on the dynamic.  
  

Any questions guys?  
  

Now for the following lessons, we will try to make some examples of the way in which we can model motion in specific parameters. Among the different applications that we have available, we will talk about the way in which we can perform, realize, and apply motion models in the specific case of surgery.  
  

And among the surgeries that we have available, and this is only an example, but it is the one very close to what we do, so I think it is interesting for you to hear this. Among the surgeries that we have available.  
  

Motion is particularly important when we have surgeries that need to reach an internal target.  
  

An internal target that is not visible or not available directly.  
  

Let's suppose this situation. This situation is that we have a subject with this one, the large one.  
  

And we want to reach this tumor.  
  

To treat this tumor.  
  

Either by inserting a needle from outside and reaching the target for a biopsy.  
  

Or we want to shoot a radiation beam from outside and reaching this target with an x-ray beam. But the problem here is that the target moves.  
  

And we don't know how it moves and we have no means available to understand and measure the way in which this target moves in real time one solution could be okay let's suppose i have available technologies to visualize in real time this target in 3d because this is the information that I should provide to my machine.  
  

The VIA accelerator, the radiation oncology, that will shoot the beam with the direction that will be proper to reach the target in presence of this motion. So I will provide the machine with the motion of the target, the technique in real time, and the machine will obey to this pattern of motion, changing the direction of the beam in such a way that the beam is always covering the target.  
  

We don't have that technology. Or maybe we could have it and it would be a couple of X-ray tubes with diagnostic energies looking at the target so that we can recognize in the two X-ray projections the position of this target in 2D and if the system of the two X-ray tubes are calibrated then we can reconstruct the position of the target frame per second up to 15 so it could be good because the frequency content of the motion is not that high.  
  

But the problem here is that due to the fact that the radiotherapy radiation lasts many, many minutes because we have to deliver a lot of energy on the target.  
  

We will expose the patient to a continuous fluoroscopic imaging energy scanning up from two tubes for the whole duration of the radiation. This boost submits the patient a non therapeutic energy.  
  

Ionizing energy with potential big damages for the patient and potentially generation of secondary malignancies due to the exposition of the patient to this non-therapeutic energy.  
  

So we need to find another solution. Some people do that, the Japanese do that.  
  

But we have to find another solution. And the solution is to establish.  
  

Emotion to define a motion model that describes the relationship in terms of motion that exists between our moving target that is invisible and a set of technical points, technical markers that are much more easy to detect and measure in real time. So we are now experts in up. acquiring the position of external markers.  
  

By means of an optoelectronic system.  
  

An optical frame. We know how to do it.  
  

So if there is a way to establish a correlation between the motion of this configuration of external markers that are easily to be captured and reconstructed with the beam.  
  

By means of an optoelectronic system being present in the thermal band. in the surgical room and the motion of the target to sufficient accuracy.  
  

The game is done.  
  

I will establish this correlation and then I will let the optical tracking system measure the external markers in real time during the evaluation and through this model of correlation, I will estimate frame by frame with the frequency of the optical tracking system, the position of the target.  
  

And then we provide the machine with the estimation of the position of the traffic in such a way that the machine adapts the direction of the beam in order to always cover the target. That's the solution that we will explore, the way in which we are able to do this.  
  

With specific characteristics as a function of the specific nature of the project. peculiarities of the surgical intervention or radiotherapy okay and let me show you some introductory slides in these last 10 minutes in order to understand what is the problem it's specific reference to radiation oncology which is in terms of exemplifying the case of motion modeling is very interesting from the engineering point of view. Why? Because Vaginational Oncology is nowadays one of the three main cures for cancer along with surgery and chemotherapy, but with promising outcomes in terms of total control of the disease. So it is not that we irradiate a patient just for palliative reasons, we irradiate a patient with curative intentions most of the time.  
  

On the other hand, radiation oncology has very interesting engineering points of view for the artists because during the intervention we don't see the target, as I will say in a minute.  
  

We use an instrument that is not visible because it is an x-ray beam that is not visible. There is nobody beside the patient during the intervention.  
  

There is no opening of the patient, so there is not the possibility for any medical operator to observe what is going on and then undertake other measures or corrections in case things are not going as planned. And so the operator is just switching on a switch and the the irradiation takes place in a completely automated fashion.  
  

It is the machine that erogates the treatment according to the treatment plan.  
  

And the operator can do only one thing, verify.  
  

Control that nothing is going really very bad, like the patient is raising up or going down from the couch or coughing or whatever.  
  

So there is a whole first phase of the radiotherapy oncology workflow that is focused on planning the correct treatment for that specific.  
  

And this is a personalized activity. So it is a plan that will define certain parameters of the treatment, geometrical parameters, physical parameters of the treatment, that are personalized for that specific patient with that specific lesion, in that specific site, with that specific model.  
  

And it will be based on this treatment plan. on the most sophisticated biomedical imaging technologies that we have available nowadays. CT and MRI.  
  

Or typically the combination of the two.  
  

This first phase is needed in order to establish, for example, the number of beams that we need to focus proper amount of dose on the target.  
  

Without delivering too much dose on the surrounding tissues.  
  

And typically, we like to multiply the number of pinnacles in order to obtain, coming from different directions in the patient, as you see here, in order to focus the 100% of the nominal dose in the target while sparing healthy tissues and organs that are on the pathway of each pinnacle that we have defined to be present.  
  

And other parameters like the way in which the beam is conformed.  
  

So it's shaped by external elements, I'll show you in a moment what it is, by specific collimators in order to shape the beam in such a way that it will cover nicely the specific morphology of the lesion along that direction, along the direction of that specific beam. So something very complex.  
  

After this effort.  
  

The patient is brought to the therapy table.  
  

Is placed in a nominal position of treatment with respect to the treatment plan, and everyone is brought to believe that the treatment plan that has been defined for that specific patient maybe two days before is valid also in that specific irritation.  
  

Let's think of the geometrical parameters. We do believe, we have to believe.  
  

That the way in which we are positioning the patient, in respect to the beam.  
  

The way in which we are producing the beam.  
  

The way in which we are conforming the beam, so shaping the beam.  
  

Is valid for the current anatomical pathological situation of the patient on that specific day of the evaluation.  
  

And this of course is never true.  
  

Plus.  
  

A radiotherapy treatment is composed by many daily evaluations, not by only one.  
  

In some cases there are 40 functions, 40 days of evaluation, 40 times the patient needs to be placed on the treatment couch.  
  

Brought into the treatment position and then radiated by the machine.  
  

Always according to the treatment plan that has been initially elaborated.  
  

With no possibility to look into the patient, at least a priori.  
  

To look into the patient and to verify on the fly whether the beam is really going on to the target and whether what I saw.  
  

In terms of those deposition patterns during the treatment planning phase is being effectively realized in that specific irradiation.  
  

And motion is one of the major source of inaccuracies between the treatment plan indications and what really happens during a specific irradiation.  
  

During the treatment delivery. These are the so-called intrafractional patient deviations so motion that the patient is producing during their addiction due to respiration for example but not only and that jeopardize the geometrical relationships between the beam for the pins because there are not any white ones in the fracture and the position of the.  
  

We can do something about it. It's exactly the example that I was showing you before. Yes, we can do something about it. We need to do something about it. And indeed, something is done about it.  
  

Let me just show you the level of complexity of the linear acceleration machine.  
  

These are the machines that produce the X-ray beams that are used to deliver the dose onto the target.  
  

And the important thing to notice is the presence of these multi-leaf collimators that according to the direction of incoming of the beam.  
  

Adapt their shape in order to shape the radiation beam so that the section of this beam is really equal to the section of the target that is being seen by the machine during the rotation.  
  

So for every angle of the mobile part of it. machine which is called the gantry, the collimator assumes a specific shape so that the beam exiting the collimator is shaped to be very similar to the morphology of the target being seen by the beam from that specific angle of income.  
  

And you can imagine the level of complexity for all of these machines.  
  

The necessity of QAs, of quality assurance tests every day. But the level of complexity of the plan, the level of effort that is produced not only to build these machines, which are robots, we talk a lot about robotic surgery, that's really a robotic surgery, because that's really landed to a machine that performs things completely in autonomy.  
  

Obeying to a set of rules that are sent to the controller of the machine.  
  

So there's no guy changing this thing manually during the beaming relation. Everything is done automatically. So this is a real robotic surgery.  
  

So this level of effort in building this kind of machine and in building personalized treatment plans with this level of complexity needs to be valorized, needs to be enhanced by canceling out all the source of in-app pool assist that may occur between.  
  

What we plan and what we really do on the patient.  
  

So the same level of effort should be produced to keep the balance between what we do in treatment planning and what we do in treatment delivery. And unfortunately that's not really the case. So the effort is more unbalanced in favor of enhancing the level of control. complexity of the machines, the potentiality, the potentials of the machines, and of the treatment plan with respect to what we are really able to control and to verify during the treatment. But we have to keep up with that. We have to try to reach that balance.  
  

And the effort nowadays is really to try to fill the gap that still exists between treatment planning and treatment delivery. Let me show you just one last slide, and then we will come back to follow up.  
  

In the following stuff this is what is really done nowadays to let's say to cope with our inability to solve all the inaccuracies that take place between the treatment planning and the treatment we enlarge the body so if we have a CT slice.  
  

In which we can see clearly in the lung the pathological volume. We see it with the radiologists, with the radiation oncologists.  
  

And it can contour manually or less manually this volume, clearly pathological. This is called the gross tumor volume, so what is really visible on the diagnostic images.  
  

Then.  
  

According to the histology of the disease.  
  

We clinicians know that there is always a margin of invisible infiltration of the disease around the visible volume. Okay.  
  

So what is called here the subclinical involvement.  
  

We don't see pathology but we know that there is pathology.  
  

So to the gross tumor volume a margin is added around the gross tumor volume. typically isotropic in all the directions. It can be 1 mm, 2 mm.  
  

5 mm. It depends upon the histology of the disease and the stadium.  
  

The stage of the disease. The bigger is the disease, the bigger will be the virus.  
  

The resulting volume is the so-called clinical target volume.  
  

That's the volume that you want to treat with the radiation.  
  

That's the volume that we would like to be able to target with our radiation beam.  
  

Unfortunately, we know that there are the uncertainties in terms of the mutual geometric relationship between the target and the beam at each radiation section. Because the patient is bleeding, because the operators cannot be... We need to sublimate the capture to imposition. Imposition of the patient, because the patient changes day by day.  
  

So also the characteristics of the anatomy and the pathology of the patient are changing from fraction to fraction. So we need to add other margins, other margins which are safety margins.  
  

And these margins are larger. the lesser is our ability to master the uncertainties.  
  

So.  
  

The first margin that we have to take into account is the so-called internal margin.  
  

It is a margin that we have to add to the target, to the clinical target volume.  
  

As a function of the variation that the patient undergoes day by day. And... during the radiation.  
  

It is anatomical changes, tumor shrinkage, tumor enlargement, edema coming in, displacing the target.  
  

And intratraccional uncertainty, typically caused by respiration in the structures that are involved by this kind of physiological process.  
  

If we have imaging techniques available in the bunker with which we can, for example, reacquire a CT on the patient immediately before treating the patient, then this margin can be highly reduced. But again, this technique of performing and acquiring a daily CT on the patient is not acceptable. We would have to acquire 20 CTs on the patient for 20 days of the rotation.  
  

So typically the in-room imaging technologies are based on double X-ray projections in which you can see the target or surrogates of the target.  
  

So structures which are visible in X-ray projections that can be a reliable surrogate of the position and of the target. It depends a lot what the target is and not on the specific pathological characteristics.  
  

But we need to add the margin. So the more technology we have available to detect the physiological variations interfraction from one day to the other day and intrafraction during the specific irradiation, the smaller can be this margin.  
  

If we have no control.  
  

Then we need to stay on the safe side. So we enlarge a lot the clinical target volume with a big internal margin. Then we have the setup margin. This is another margin that we have to add according to the.  
  

Or as a function to our ability to set up the patient initially at each radiation session.  
  

And this can be highly valuable as a function of the technologies that we have available to verify the position of the patient with respect to the reference system which is valid in the treatment room. The one with respect to which the whole treatment is expressed.  
  

Can we just simply use an optical tracking system to track the configuration of external macro on the patient before the evaluation to check 3D the position of the patient? Yes, and that's exactly what it's done.  
  

Plus, the position of X-ray imaging with low dose to at least have a bony anatomy representation of the position of the patient with respect to the machine so that the position of the patient can be rigidly correct. according to this information that are acquired immediately before the evaluation.  
  

And this set of margins, by means of these procedures, can be highly used.  
  

This is to say that there is a balance between our ability to master the uncertainties, to measure and correct the uncertainties, statically or dynamically, and we can talk about motion, it will be necessarily a dynamic measurement at the beginning of each radiation session and during the radiation day.  
  

And the amount of tissue that we need to include within the target that we treat with our radiation.  
  

If we enlarge a lot because we are not sure of what we are doing, then we are involving potentially a lot of healthy tissue in the volume that we treat.  
  

Potentially harming the patient, causing side effects of the radiation beam, of the radiation treatment.  
  

Because of our inability, technical inability, to master these receptors. And this is our job. to master these uncertainties. It's not a job of the radiation oncologists, it's a work offered us by medical engineers and medical physicists to try to find the best way to master the inaccuracies between treatment planning and treatment delivery so that these margins can be reduced to a minimum. Because if I'm sure on the way in which I am setting up the patient.  
  

Because I have a nice electronic system, because I place a nice configuration of markers on the patient, because I take a couple of x-rays, then I have a.  
  

3D image registration techniques, which are robust, and I apply them on all my patients, then that set of markers become zero.  
  

I cancel it out.  
  

I take away healthy tissue from that set of markers, because I'm sure that the lesion will be always inside the CTV and the internal.  
  

And if I'm able to master nicely the intrafractional variations due to respiration, because I will make extensive use of motion models, the ones that we will talk about in the future.  
  

Then I can reduce to a minimum the internal variation. And this goes into a certain amount of advantages of the ratio. between the therapeutic effect of the treatment, the control of the disease, so the sterilization of the cancer.  
  

And the side effects that the treatment can lead and introduce can elicit in my patient.  
  

So in this respect we'll try to find what are the possibilities of making motion models so that we are able to.  
  

You know, make the most of our knowledge in the way in which we are able to detect the motion with our optical technologies typically coupled with biomedical imaging technologies so that we are able to estimate the position on the fly of our target and refuse to eliminate the margins of safety that only other evidence should be forced to introduce naturally.  
  

Guys, tomorrow you will have Fabio with practical lessons.  
  

Many come also with him to discuss again with your motion. So did you all selected your motion?  
  

Are you all prepared to discuss it and justify your choices before you go into the practical exercise and experience and you find out that something is wrong? That's the beauty of tomorrow. Tommy will give you some hints on the practical lesson, more tools let's say, and then we'll discuss.  
  

Some of your decisions if you like. I think it's very important to eventually highlight possible problems related to the choice that you make.


