
13/11/2025
***

you're still missing one point, it is to recover the laboratory reference frame because we know that one of the simplifications that we made is that we can create one kind on the other so we need to understand what we need to do in order to recover the laboratory reference frame as the reference frame in which we will express the three-dimensional coordinates of the... the markers on the subject that we will obtain after the calibration with the non-control points and then we will make some considerations for guiding you a little bit about the selection and the motion for your practical project. So I hope that many of you here present are willing to perform a practical project, so that's what we will do today. It's not going to be a long lesson.  
  

So let's start from understanding what are we still missing for concluding the calibration with unknown control points. The situation is that after we have calibrated our camera system we will have the camera system.  
  

Being calibrated with respect to a reference system mounted on one camera.  
  

And this is most of the time unacceptable, because what you want to do in your laboratory is to have a common reference frame, while also including reference frames of other devices. The typical case is that you will have a force platform in your laboratory.  
  

That will express the reaction force and the point of application of the reaction force with respect to a reference system which is solid with the force platform and so what you want to do is to obtain to express the dynamic data reaction forces given by the fourth platform and the kinematics data.  
  

You want them to be expressed with respect to a common reference frame.  
  

And the common reference frame needs to be the one of the force platform, which comes embedded in the force platform. This one is typically centered in one of the corners of the force platform, and then we cannot do anything about it in order to change it. So it would be very hard to find a way to map this reference system of the force platform into the reference system the camera system but we can do something in the opposite direction so we have to implement the procedure in order to estimate the parameters of the auto translation matrix that allows us to map the coordinates of the markers reconstructed in 3d when our subject moves of the force platform with markets here.  
  

Not to be expressed with respect to the reference system mounted on one of the cameras that we selected as the basic basis one but being expressed with respect to the force platform of the reference system okay so at the end.  
  

Of the acquisition of the control points cloud with a known coordinate that we will be using for estimating the parameters of the elements of the fundamental matrix and then to extract from the fundamental matrix. the focal length of the cameras eventually the extrinsic parameters of camera one camera two with respect to camera one and the principal points according to the large scale optimization algorithms that we saw last week we need to add to the calibration procedure overall a sort of mapping procedure or sort of mini calibration procedure.  
  

In order to estimate the parameters of this mapping rotor translation matrix.  
  

So what you always have to do.  
  

And this is included in the commercial software that you find, in the commercial systems that you will be calibrating with the magic wand, is the so-called external calibration or external procedure.  
  

That is that requires the definition of the configuration of control points with known coordinates so somehow we fall back in the conventional procedure the only difference here is that the aim now is not to calibrate completely the system which would require at least five points in the ideal case but in reality it would require hundreds of points as it was in the the conventional equation. procedure. Here we need a small number of known control points that are needed only to estimate the parameters of the roto-translational matrix for mapping.  
  

If we stick to the case that I just outlined here.  
  

What we could do for example if this is x.  
  

Y and z of the force platform.  
  

The user is required to to define a configuration of control points for example placed on the corner of the center force map.  
  

The minimal number of control points that we need to estimate the parameters of the aerobic gravitational mapping is how many? How many points do we need to define the position and orientation of the rigid body in space?  
  

How many points do we need?  
  

Three points, okay? Three non-collinear points. Come on, speak out.  
  

And that's exactly the same minimal number that we need to put what exactly we want to do. So at least three points.  
  

Typically we'll put a little bit more than them, but not a lot more than the minimal number of required points. Let's say we will put four points. The four corners of the force plan.  
  

We need to align them, to position them in a very accurate way.  
  

That's a manual procedure.  
  

So it's kind of, okay, we paid a lot of prices, we made a lot of simplifications to perform a calibration with unknown control points, but still we need to stick to a mini procedure requiring the definition. of a configuration of control points with known coordinates in order to complete our procedure and to have available a laboratory reference frame which is handy which is practical okay which is not solid to a camera which is hanging somewhere in the ceiling at the ceiling of our lab so we need to position this marker very accurately and we need to assign to these markers known coordinates.  
  

So if this is the reference system, let's say if z is like that.  
  

So x is going to be like this.  
  

And probably the z is going to be the other, the opposite way, but nevertheless it should be a right-handed coordinate system.  
  

This marker will have which coordinates?  
  

0, 0, 0, okay? It will be in the origin.  
  

This one will have only y coordinates, so it will have 0. The length of the fourth platform, 40 centimeters, okay, let's say 400.  
  

0.  
  

And so forth and so on. We need to know the real coordinates of the markers that we are using to perform this mini mapping procedure. I call it a mini calibration procedure, but it is not a calibration procedure, because we are not estimating anything regarding the calibration parameters of our stereo.  
  

Camera system because this we have already done with unknown control points. The only problem is that we have already done but we refer everything to this reference system which is something we don't want.  
  

But still we need to place, and this is only one example, you could do it in any case, we need to define the configuration of control points with known coordinates with respect to the laboratory reference system that will be the one with respect to which we will express and we want to express the coordinates of the markers placed on the subject and acquired by my camera system during the utilization of the camera system after the calibration procedure. Okay.  
  

So we place the four markers and then we have to implement an estimation procedure.  
  

In order to estimate the parameters of the rototransmational matrix for Mark. How do we do this?  
  

So let's see, let's write down a small flowchart of an iterative procedure for the estimation of these parameters. What should we give to this algorithm? We will give an initialization of the parameters of R and T.  
  

We will give the real coordinates that we have measured.  
  

Of the markers on the force platform, so the manual coordinates that we have available when placing the markers on the force platform. Let's call them the P real.  
  

Or let's say the P with respect to the force platform, right? And then we have to give to this algorithm the three-dimensional coordinates of these same control points seen by the camera system. and expressed in 3D with respect to the reference system solid to camera 1. So we switch on the system and we let the system look at the force platform placed markers. The system is calibrated, it will reconstruct in 3D these four points and express the three-dimensional coordinates of these four points with respect to the.  
  

Camera 1 mounted reference system, the one with respect to which we have calibrated the stereo camera system.  
  

So it will be another input of the same points expressed with respect to the camera mounted reference system, BCM.  
  

Now we want to estimate The roto-translational matrix that describes position and orientation of the camera 1 with respect to these references.  
  

The force platform 1, the laboratory. Because this same roto-translational matrix describing position and orientation of camera 1 with respect to the laboratory is the same roto-translational matrix that allows us to map points.  
  

Expressed in 3D with respect to the camera mounted reference system to the reference system of the laboratory. Okay.  
  

So what we have to do is to make the first station here and use the first estimation of the rototranslational matrix that we can compose in a unique 4x4 auto-translational operator expressed in homogeneous coordinates in such a way that we can write that the P asterisks estimated with respect to the force platform equals the multiplication of T asterisks because it will be built by means of an initial estimation of the parameters.  
  

Multiplied by the vector P seen by the optical tracking system, expressed with respect to this reference system, so the one that we call PCM.  
  

Can we do this? Yes, because we are providing the algorithm with an initial estimation of the parameters of this ROTO-translational matrix, so we can build this matrix equation. in the first iteration of the optimization algorithm that we are implementing.  
  

Then we need to come up with a metric.  
  

With a merit function that we want to minimize.  
  

What is this merit function? We are dealing with physical points.  
  

The merit function will be the squared sum of the differences.  
  

The distances between corresponding points. Right? So it is easy to implement a merit function that will be the sum for the n which goes from 1 to n, where n is the number of my control points.  
  

Pi asterisk minus pi cm squared.  
  

The sum of the squared, the sum of the distances between corresponding points seen.  
  

Expressed with respect to the laboratory reference system, the real ones that I have measured and the ones that I have estimated by multiplying the one seen by the optical tracking system.  
  

Pre-multiplied by the Rotor translational mapping matrix is supposed to map these points to be expressed from the camera mounted reference system to the laboratory reference system.  
  

When the parameters of this matrix are correct.  
  

This difference, the distances between the real one that I have measured on the false platform and the roto-translated one, from being expressed with respect to the camera mounted reference system to be expressed with respect to the false platform reference system, the distance between these two points dataset is zero. so this merit function.  
  

Needs to go towards zero.  
  

Right?  
  

So is this the case?  
  

So is this distance below the predefined threshold that can be nicely 10 to the minus 3 millimeters? Because it's going to be very, very accurate.  
  

Yes, then, okay, my rotor translational matrix is correct, the first estimation. Typically, this will not... be the case. So I will have an updater that will update the parameters of the lotto-translational matrix according to whatever criteria.  
  

Steepest gradient, descent or whatever. It will be an updater.  
  

Update what? The parameters of the lotto-translational matrix and I will get back here for the second alteration.  
  

And I will go on for.  
  

20, 30 iterations in a very quick way until I will find the parameters, the elements of the 4x4 robot translational operator mapping the coordinates of the markers seen by the camera system to be expressed with respect to the force platform reference.  
  

From that moment on.  
  

Every time I will switch on my camera system and have my subject perform the motion and being acquired by the camera system, the markers on the subject will be first expressed with respect to the camera mounted reference system because the system will work always expressing and reconstructing in 3D the markers with respect to its own camera mounted reference system. but then mapped through the T that I have estimated with this additional mini calibration procedure to be expressed with respect to the force platform, lab-monotonic reference platform.  
  

That's the way in which we recover the first of the set of simplifications that we have introduced for obtaining a calibration of the stereo camera system with a cloud of unknown control points control points with unknown coordinates all the cameras refer with respect to one basic camera scale factor we calibrate everything regardless of scale factor we supposed to know the position of the principal point of all the of the two cameras or the cameras that are participating in the calibration. These are the three main simplifications that we need to introduce along with the highest ideal case, no skew, no optical distortion and stuff like that.  
  

That is needed to be introduced in order to have everything work nicely.  
  

Okay.  
  

So for every simplification we pay a price.  
  

For the one camera with respect to the cameras with respect to the first camera, this is the price that we pay, which has a procedural implication, not trivial.  
  

Because if I make an error here.  
  

By manually displacing the configuration of control points and measuring their position with respect to the laboratory reference frame, then I make a mess.  
  

But the advantage is that I have to deal with... 4 or 5 markers, not hundreds of them.  
  

But still you need to be very very careful what you're doing because if you are making a mess here then this laboratory reference frame will be.  
  

Somehow distorted or displaced in space and you will not be able to count on the coincidence between the laboratory reference frame with respect to which you want to express the kinematic data that this system is able to acquire and the one that you are reading expressing your three-dimensional coordinates of the map with respect to which okay so you're making a mess.  
  

Second simplification that is the scale factor. We have the two markers on the magic wand.  
  

Third simplification.  
  

Principal point knowledge. We need to implement large scale optimization algorithms in order to come up with an estimation of the principal points of the cameras using the three dimensional reconstruction error plus the estimated feature respect by means of the third marker based on that one. the magic wand for having the availability to rank the calibrations that compose the generate the generations in the large scale optimization algorithm in the case of let's say the genetic algorithm that is what we saw the other day okay is everything clear about this so you will need to be able to answer our questions like okay let's talk with the with the laboratory technicians.  
  

Let's highlight advantages and disadvantages of this new calibration method with respect to the conventional one. Shall I count on a completely exclusion of any manual measurement in the new and conventional calibration method with no control points? The answer, of course, is no. You still have to do something in order to express your three-dimensional kinematic data. With respect to a convenient laboratory reference frame, we always have to do that. And the difference is between the two approaches, the two procedures, the conventional one and the unconventional one, is to be known very well. The simplifications that we need to introduce and the price that we need to pay in order to recover the simplification that we used.  
  

Let me tell you that in many cases.  
  

Instead of placing.  
  

The markers on the force platform, the system comes with a little object.  
  

A little reference system let's say, already built.  
  

Carrying some markers on it.  
  

And this little object is aligned manually to the force platform, making things manually, practically a little bit easier with respect to placing single would have any markers on the corners of the force.  
  

Okay. That's the way it is done. But it doesn't just just the way to make things a little bit more practical.  
  

Practical and less prone to errors.  
  

When we need to perform this manual alignment and definition of the configuration of control points with no coordinates with respect to the lab. Okay.  
  

Any question guys on this?  
  

Very good. So we can do...  
  

I know that you are reasoning about the motion selection for the practical project. Are you in this mindset?  
  

Many of you? Okay.  
  

Let's discuss a little bit some of the criteria for doing it, and if we have time we'll continue with the students. Otherwise we'll do that on Tuesday.  
  

Because it is important, I mean, next week I'd like to spend some hours discussing your choices, as I told you already.  
  

But I'd like to spend some time in order to give you some recommendations in order to avoid that you make selections or you make some choices, and then we tell you, no.  
  

It's not going to work.  
  

So the first rule is keep things simple.  
  

Do not select very complex motion.  
  

You will need really to select like a simple gesture, right?  
  

I'm talking about like a squat.  
  

Or a throw or like a simple motion because your problem in order to select this motion or one of them is to ensure that your double camera system.  
  

Made up by your smartphones will be able to capture this motion.  
  

Seeing for the whole duration of this motion production all the markers that you will define on the subject.  
  

So you want to avoid rotational motion.  
  

That will in any case hide some of the markers during the execution of the motion so exclude the line of sight or close the line of sight between the cameras and your markers so the.  
  

Maintenance of a proper line of sight from your double camera system to the markers placed on the subject is the basic criteria that needs to guide you in the selection option.  
  

So, simple and line of sight.  
  

But before going on into the selection of the motion.  
  

Look at the available muscle skeletal models that are there on the web of the OpenSim.  
  

Because at the end.  
  

You will need to describe the motion in OpenSim and perform some of the analysis in OpenSim. So you will need a certain one to enter in the environment of the OpenSim software.  
  

So if you select a motion and you don't find a reliable corresponding mass of spiritual model open seam with which, by means of which you are able to represent the motion that you want to capture and you are in trouble.  
  

Okay.  
  

So look for the proper model.  
  

It can be a full body model, if you select a motion that is a full body motion. It can be an upper trunk, upper body model.  
  

It can be a double side model, a single side model.  
  

But you need to have at the very beginning the selection of the proper mass of skeletal model of open scene that you will be using to represent your motion in open scene and to perform the analysis in open scene. Okay?  
  

So the second rule, and we are not yet deciding the motion, is select the human motion model in open scene.  
  

And when you do that.  
  

You will always be careful to understand what are the technical markers that are present already in the model of offensive.  
  

Because these models, they come already.  
  

In many cases, with a configuration of technical markers already positioned in proper anatomical landmarks of the model.  
  

This is a guide, a very strong guide, that will guide you in selecting the anatomical landmarks on your subject.  
  

So if the musculoskeletal model of open seam comes with some markers already placed on it, for example, the atromion.  
  

The shoulder.  
  

On the lateral humeral condyle.  
  

These are exactly, and you will understand what they are by looking at the names typically, that are self-explaining. Well, these are the anatomical landmarks that you will select as sites of the markers on your subject.  
  

Okay? Because if you change something, like say, no, I don't like the lateral condyle, I want to place it somewhere else.  
  

So what you will need to do.  
  

You know, it's to cancel this already existing marker.  
  

Place somehow a new technical marker on the muscle skeletal model of OpenSane, corresponding to the site that you have decided as a site of marker on your subject, but the correspondence between the virtual marker that you place on the model and the real marker that you place on the subject, I mean.  
  

It will be a qualitative positioning of this marker. So the correspondence of the position of the real marker on the subject and the virtual marker on the model is a big source of inaccuracies.  
  

Okay, if you don't get it and you have uncertainties in the positioning, this will turn out in inaccuracies during the scaling of the model.  
  

And the inverse kinematics procedure that the open scene will be doing in order to transform the trajectories of the markers into joint angles for motion representation and all the subsequent analysis. So the principle should be the less I change in the human muscle-skeletal model of open scene mapping.  
  

But the more I can adhere in the selection of the anatomical markers on my subject, as it is already present in the muscle-skeletal model, you can see, the better it is.  
  

And look that in many cases.  
  

Let me open this little bracket in the place where we focused on the so-called anatomical topography.  
  

In many cases, the markers that you will find in the model correspond to classical anatomical landmarks that are used in human motion analysis.  
  

And I'd like to mention here for you. These are typically corresponding with bony processes that you can easily find on any subject.  
  

Let's talk about some of the basic joints that you will be for sure using.  
  

Shoulder.  
  

The shoulder is typically represented, identified by a marker on the acromion. The acromion is the distal process of the collarbone. You can feel it very easily.  
  

It's very easy to find. And of course if you find a model that has a marker on the acromion.  
  

Called acrobium left.  
  

With no fantasy then you will know that you will find and place a marker on the acromion of your subject let's go let's talk about the upper limbs after the acromion we go down the elbow you can feel nicely the lateral condyle of the humerus it's very easy to feel it so you will place a nice touch there.  
  

Then you have the distal and the medial condyles, the ulnar and the radius condyle at the level of the wrist.  
  

You may decide to place both of them on the wrist, medial and lateral condyle. Then you have the metacarpal, probably you will never place anything on the fingers. You might place a marker at the end of the third finger, like. In order to have somehow a possible representation of the hand that gives you the flexion of the wrist, otherwise you don't have it.  
  

What about the lower limbs? The lower limbs we have the hip.  
  

The hip you need to find the so-called great trochanter. The great trochanter is the bony process of the pelvic bone. You can easily feel it. By flexing your hip, you can feel a bony process that is representative of the hip joint. And we place a marker there, for sure.  
  

Then what about the knee? You have the lateral femoral condyle and the medial femoral condyle. Again, two very easily recognizable processes. What about the ankle? Medial and lateral malleus. You can feel them very nicely.  
  

Then he has the metatarsal head and you can place probably, if you want to acquire the position of the foot, a marker or a couple of markers in correspondence of the first metatarsal head.  
  

Where the first finger gets to the foot.  
  

And the fifth metatarsal head, where the fifth finger gets to the foot.  
  

So look at the markers which are already present in the model of open cement. Try to mimic what is already present in the configuration of the points that you will place on your subject.  
  

Now, there is another very important situation here in terms of the way in which you want to define the configuration of markers on your subject. Typically.  
  

As we told at the very beginning of this module, every body segment is an independent rigid point.  
  

So let's take the 4-iron for example, let's isolate it.  
  

It is an independent rigid body.  
  

Theoretically we would need at least three non-collinear points in order to define completely the position and orientation of this rigid body in space.  
  

So, theoretically speaking, for every body segment you should place.  
  

Three points on this rigid top.  
  

That starts to be really too much.  
  

Typically for the forearm you will have a marker on the lateral humeral process and maybe one or two on the lateral and medial.  
  

Bone in process is at the level of the wrist. This would be already the three points that are enough to define position and habilitation of the rigid body. If you don't have the one of the medial lateral condyle, the medial condyle, you will have only two.  
  

So you have a degree of freedom which is left uncertain for open ceiling. And this will be most of the time, in most of the cases, real. Because you will never be able to place three markers for every body segment in your muscle skeletal model and on your subject. So you will have some of the degrees of freedom of this body segments left free.  
  

What is the trick in order to resolve this situation? You have the possibility, not only if you have already seen this, to freeze some degrees of freedom.  
  

For example, if you have only two markers on the forearm.  
  

The degree of freedom of the rotation of the forearm around the longitudinal axis of the forearm is left free.  
  

In this case you will be able to freeze this degree of freedom. The recommendation is that it is feasible and reasonable to freeze the minor degrees of freedom of the joints and therefore of the body segment that we are focusing on. But never try to left...  
  

Not settled and not controllable the major degree of freedom of the rigid body segment.  
  

So if we would have only these two markers.  
  

Only forearm, then the flexion, extension.  
  

So the relative motion of the forearm with respect to the arm would be left.  
  

Unsolved and would be a bad thing for the representation of the motion because you have no information related to the major degree of freedom flexion extension of the elbow that is the flexion extension of the forearm with respect to the afterarm right so when you get rid of the three markers saying I will not use the three markers on the rigid body but I will use only two of them.  
  

Let's try to displace them in such a way that at least the major degree of freedom in terms of relative motion of this polysegment with respect to the previous one in the kinematic chain is determined, is calculated. Only the minor degree of freedom, the minor relative motion of this segment with respect to the previous one in the kinematic chain is left. and determined and can be freezed without losing a lot of information in terms of motion description okay a special uh consideration special considerations deserve the head and the trunk okay the trunk is very important because we know it is the site where our by center.  
  

It is the location.  
  

It is the source.  
  

The basis of all the kinematic chains of the upper limbs and lower limbs also.  
  

So it is always a good idea to determine fully position and orientation of the trunk in space. That is.  
  

Let's place three markers on the trunk.  
  

Okay, it may be two markers halfway on the collarbone.  
  

Another one on the ombilicals or two at the costal bridge cage margins and another one on the ombilicals. So let's put three markers on the truncate so that the OpenSIM software knows exactly position and orientation of the truncate in space, which is the the source, the basis of all the kinematics. chains over the upper limbs and lower limbs. Okay, so if you're doing only an upper body motion then three markers on the upper body are more than enough.  
  

If you're doing a lower body motion then it's better maybe to place markers on the anterior iliac spines, other two very evident anatomical lammas that you you can feel it very easily, plus another one at the sternum for example.  
  

So focusing the attention on the lower trunk with respect to the upper trunk, which is less relevant for a lower body motion with respect to an upper body motion.  
  

But at least the trunk.  
  

Let's try to define position and orientation of it by means of a configuration of at least three marks.  
  

The head again is very important. Sometimes, but many times, many cases it doesn't really.  
  

It is not involved in the motion that you will be doing.  
  

You may be willing to identify positional orientation of the head that would mean let's place three markers on the head or you can also leave the head segment free and freeze manually All the degree of freedom and the level of the C7 it opens in such a way that the head will be solid with the trunk. This is also...  
  

It is not really...  
  

...description of your motion. It will always be a trade-off between the number of markers that you want to put on your model and the...  
  

...in this case, the higher is the number, the more rich is the configuration, the more detailed will be and accurate will be the motion representation in OpenSim.  
  

On the other hand the higher is the number of markers the more workload.  
  

Will be present for you when you will be willing to digitize manually all these market configurations on your subject for 20, 30, 40 frames.  
  

So, third principle then is to try to complete representation.  
  

Of the body segments, the most relevant body segments in your motion ok so try to think of the configuration of markers that allows you for a complete identification of position and augmentation of the most relevant body segments involved in your motion that's all about the trade-off workload and accurate representation the third thing is visibility of course if you place a lot of markers on the subject but you use them during the motion because you don't see them then then it's unusable.  
  

So you need the third element to be considered in your selection is to ensure that all the markers that you choose are visible to the camera system during the execution of the motion. And this has to do a lot with the specific characteristics of the motion that you select. The more simple it is, the higher will be the possibility to keep the line of sight between the markets, between all the markets.  
  

The camera couple that will be watching the motion execution.  
  

And with this respect I come to another very important situation.  
  

You have to choose whether to observe your subject on the frontal plane or on the surgical plane.  
  

If you want to perform a double-sight analysis.  
  

So a complete analysis, you will be forced to watch the motion from the frontal plane.  
  

Will execute the motion when the two cameras are facing the two telephones facing the two cameras okay because that's the only way to ensure the visibility of the markers during the execution of an asymmetric motion okay.  
  

This means that many of the markers that we have selected here may change. The acronym can be there, but maybe all the lateral markers can be hardly visible.  
  

On the frontal plane. So you might be called to change a little bit the position of the lateral markers of the joints to be visible on the frontal plane.  
  

Typically also in the human muscle skeletal model of open skin. Introducing some naturopathies, but these naturopathies and this procedure will be necessary in order to obtain a full body bilateral representation of the motion.  
  

In other cases.  
  

If the motion is very symmetrical, think of a squat, the squat is very symmetrical.  
  

You can also choose to acquire the subject on a sagittal plane.  
  

Single side.  
  

But in this case we have a hard time to mount the motion on the human muscle skeletal model of the scene which is bilateral typically.  
  

Okay.  
  

But there is a trick there. So you can choose really to acquire the subject only monolateral.  
  

To assume that the motion is highly symmetrical, and to project or to mount the motion that you have acquired only on one single side to the other side of the motion.  
  

Like supposing that there are other markers on the subject that you were not able to acquire because your subject was facing with the sagittal plane, the two cameras.  
  

But markers that will perform the exactly same trajectory of the ones that you were able to acquire, simply displaced of a certain amount of space, the one corresponding to the anthropometric measure that you can obtain easily by measuring your subject along one specific direction.  
  

So if your reference system will be this one with the.  
  

X pointing this way and the subject is performing the motion sagittally.  
  

You will be able to recreate the same marker on the other side of the body doing exactly the same motion. Artificially.  
  

By creating a virtual marker, distance and exactly the amount of space along the X direction to be the transversal axis on your subject, being careful that your subject is really oriented conveniently with respect to the reference system that you are working on.  
  

That you are working with.  
  

Creating artificial markers with the same trajectory. but displaced of a certain amount of space according to the anthropometrical measure that you can take on your subject in such a way that you can perform a monolateral acquisition, complete acquisition monolateral on the sagittal plane, and that you can obtain a complete bilateral motion prone to be important in a complete bilateral... human motion skeletal model in open scene okay this can be absolutely done and it is a trick that solves a lot of time the problematics related to be willing of acquiring a complete motion even if the complete motion is a is a very symmetrical motion and it would not require we need to have a complete bilateral acquisition.  
  

Okay?  
  

So think also...  
  

...of this specific, of this possibility to acquire a monolateral motion and then to perform a sort of.  
  

Let's say, artificial creation of motion on the side of the body that was not directly applied. This simplifies a lot the stuff, okay? So a motion, a squat motion can be easily acquired on the sagittal plane, in the sub... performing the motion with the side facing the cameras all the markers will be very nicely visible the whole time and you are able to recreate the motion of course making an assumption that the motion is symmetrical but this is something that is uh let's say fair and acceptable to be done okay of course it requires a little bit of uh let's say some software.  
  

Manipulation there, but it's something that is absolutely acceptable, declared and done and explained. What else? Keep the motion slow.  
  

The motion needs to be performed slowly because you will under sample a lot your acquisition and you don't want to have any blur on your data stream otherwise you have to guess the position of the markers.  
  

Look in many cases you will be guessing the position of some markers. The important thing is that you don't have a lot of frames in which you have to guess the position of the post.  
  

The more is the frame set in which you don't see a marker, the worse will be the result if you guess for many many frames the position of the marker.  
  

One possibility to recover marker missing is interpolation.  
  

You can absolutely try to come up with.  
  

Let's say, post-processing analysis in which you recover the position of missing markers by int. interpolating the position of the marker which is not there looking at the previous frame before it disappears and the frames in which it reappears again with sufficient, let's say.  
  

Security that it was not guessed the position of the markers.  
  

During the interval you can interpolate the position of the marker.  
  

Keep it stable if it is a stable marker. Hit them by stable markers. Don't let a lot of holes. Try to work with it in a post-processing analysis. Right? Then another thing, filtering.  
  

Once you have reconstructed the 3D motion, it will be noisy.  
  

But the high frequency noise can be cut out and smooth away by simple filtering with fourth-order filters in very easily implementable in mata do it because this This will make your motion much smoother.  
  

And the representation in the scene will be much smoother. Of course, you will have some samples that lock your motion, so smoothing could really take away a lot of the motion. a lot of the content of information from your motion but still try to filter your data in order to take away especially if you see a lot of high frequency noise.  
  

Then all the considerations that I made already in terms of calibration.  
  

Keep the distribution of the points to occupy the whole field of view.  
  

Keep the field of view of the cameras in such a way that your subject is occupying the widest possible.  
  

Portion of your field of view. So don't keep your subject very small in one corner of the image. Don't keep the configuration of control clients occupying a small portion of the image in the field of view of the cameras. These are the considerations that are... essential in order to count on specific accuracy that is acceptable in the three-dimensional reconstruction of the motion.  
  

Do try to assess the accuracy that you have in terms of 3D reconstruction and 3D description of the motion. In MoCA.  
  

Look at the stable stability of the distance between two markers belonging to the same rigid body, and so forth and so on. Okay, he's in a stanchion.  
  

Data that you need to have available and to include in your presentation is a way to make us understand that you are aware of the errors and the accuracy that you were committing by doing this practical experience.  
  

Ask me questions.  
  

Any doubts?  
  

So typical motion are again the squat, the kick, the throw.  
  

But you know avoid turning around.  
  

This kind of motion are very very hard to do.  
  

Very hard to do.  
  

And really apply.  
  

Jump or you know some sport motion very easy sport motion and stuff like that okay but important things that you and this is all the rational of the practical project that you really get yourself organizing before making the real acquisition you try to study the experiment you look at what your smartphones are looking and understand whether the visibility of the magnet is there whether you have to change it a little bit, keep the focus principal axis of the two phones possibly.  
  

90 degrees typically they will be more open especially if you are looking at the frontal end of the subject but do not put them parallel you need to have an angle between them okay otherwise the two lines will never intersect and you will lose the depth right so the principal axis of the two cameras needs to be 90 degrees 60 degrees 45 degrees.  
  

But not 10 degrees or 5 degrees one another right so they do not have to be parallel absolutely any questions.  
  

What will happen is that we need to have from you the group formation and the models and the motion selection.  
  

Next week you will find a slot in order to discuss your choices and and see your choices.  
  

Whether it's going to be Tuesday or next Thursday, we'll see. I don't know exactly the deadline that Fabio asked you to expect. It will be most probably next Thursday, which we will spend... one hour with you saying which is your motion, what you're gonna do.  
  

How you want to implement the stuff, where you want to do your acquisition, please keep in mind the labrador that we have. The built-in 32 is available for you, just talk with Fabio, reserve your slot, you can go there, there is a nice corner in the room in which you can place your control points and perform the motion without any problem. Okay.  
  

It's absolutely doable, but we are approaching fasting. end of november it's time to get yourself organized and schedule your acquisition because it requires will require a little bit of time in order to get to the point in which you have your results and you can implement your powerpoint presentation before christmas okay i'm done There you are guys. If there's no problem, no questions.  
  

We'll see us on Tuesday. We start again with the surfaces, okay?