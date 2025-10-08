07/10/2025

![[Pasted image 20251002190154.png]]

Here we show the activation of several muscles typically in repetitive movements, walking. It is highlighted by the sin-like-shape on the right, showing the knee displacement in time. We'll have at the beginning just stayed, and we arrive to the same position at the end.

This muscles (first three ones) are extensors of the knee, while the following four ones are flexor muscles. What don't we wanna see here? the extensors and the flexors working together, if this happen, we will have something pathological (esplasticity something). Also it could be seen when an accident affect the patient, the muscles are no longer working synchronously correct. 

Now, the red boxes represent the duration of activity or inactivity of the EMG of walking. 

In order to get the red boxes, we see the initiation and the end of the burst by visual inspection, and it is easy to identify the active burst. While the visual inspection is easy to take place, though introducing discretionality, because the borders (beginning and end of the burst) need something which make them more objective measurement when the muscle is activated or inactivated. And this is something that need to be found by automatic recognition method in order to achieve reproducibility and objectivity in the measurement. 


![[Pasted image 20251007130644.png]]

We see the states of the muscular activation pattern, with their labels, LR loading response, midstance MSt, ...

In order to obtain this kind of graphs

![[Pasted image 20251007130842.png]]

We start from raw EMG data, and from this we should determine the activity when muscles are active or inactive. (Need to figure out the y-axis labels). 

![[Pasted image 20251007131128.png]]
How do we process the EMG in order to obtain an image of pattern activation?

First we need to clean the rising edge, by means of Band pass filter, in order to reduce the noise of the data, 10-250Hz it is suppose to be processing the surface electrodes data. Second step a full wave rectification, to rectify the signal, computing the module of the signal. After full wave rectification, to get something that is a bit easier to analyze we low pass the data at a cut-off freq of 5-10Hz, 

* Bandpass
* FWR
* LPF : MA, BW, RMS (This last one can be used without FWR)

![[Pasted image 20251007131642.png]]

If you do this in a digital way with data collected on sampled signal, then, half-wave or Full-wave, have this implementation.

if...

But if you're using analog components like diodes, it depends on the configuration how we apply either half- or full-wave rectification. This is the digital approach :)


![[Pasted image 20251007131830.png]]

![[Pasted image 20251007132231.png]]

Not only we'll see a 0 amplification around this freq, but also, we see that this black line has passed through . It is due to the FWR is a non-linear procedure, and this non-linear procedure can also analyze the avera of the sinusoid inserted into the input of the data and it is approximately ...
![[Pasted image 20251007132440.png]]

The summation...

![[Pasted image 20251007132604.png]]

Here some examples of the filters.

We're gonna define the reliability of the filters in signal processing... So, what we observe is that we compute the area of the three in each channel, to see if it is realiable information or stands something that changes time to time. We see we have, row data, area, mean, maximum peak. In the first filter, the MA, we have the same area, the same mean, so there is a high consistency with the MA and the raw data measurement, while the peak is not.

For the Butterworht, we have the same value for area, but RMS is not. See that peaks are always random values, but we might find mean and area consistent values. However, RMS is not performing that well, if you look at higher number of sample you'll see that RMS=  1.35 x linear filter, this is cos of the RMS we use some multiplicative effect, but anyway we can use it because we know their relation.

![[Pasted image 20251007133141.png]]

bla bla bla

![[Pasted image 20251007133810.png]]

We use this formula. If we're aligned with the window it means we're in phase. 

![[Pasted image 20251007134221.png]]

Original signal is too 
The first is 11 points, and the 51 points, you see there is presence of data loss, so it is important the number of points, the higher the number of points, the larger the data loss. 

More points, more smoothness, less detail. What about the frequency behavior of the MA filter?

![[Pasted image 20251007134510.png]]

It has a certain transfer function H(f) and depending on the number of points we determine the cutoff frequency. Look that at 3 points, the cutoff freq is larger. 

Note that after the filter reaches 0, i'll bounce. The larger the number of points, the smaller the bounces and also the faster the decay or the faster the H(f) crosses the -3dB line.

The freq cut-off is computed by the forula shown :) it is an approximation, it reaches the correct value in the range of 3 or more number of points (I guess). It is also possible to compute the sidelobes: n of points -2.  Look at 3 points, we have only one we can capture, in the case of 11, we should see 9 but idk :)

![[Pasted image 20251007135237.png]]

Another important point :) how we can normalize the data, and why, because there is reproducibility issues depending on where you're placing the electrodes , depending on which will be the user...

The maximum voluntary contraction (MVC) that is considered for electrical activity. We call it MVC but is the electrical effect of the MVC, we can not rely of an effect cos it depends on the contraction of the muscle. and so...

![[Pasted image 20251007135554.png]]

This is a calibration phase, that shows a muscular contraction, and what we have todo is to rescale electrical info, MVC which has to do with the electrical activity, and this is normalize by the MVC and multiplied by 100.

![[Pasted image 20251007135712.png]]

Pros-cons. READ THEM :)
![[Pasted image 20251007140129.png]]

Now, we consider the estimation of parameters in the time domain.

![[Pasted image 20251007142019.png]]

One point in the mean value to estimate the electrical activity, and the rms. 

![[Pasted image 20251007142336.png]]


![[Pasted image 20251007142544.png]]

In the time domain: we can measure the information in particular, the neurological EMG, which is related with the depth electrodes. Zero crossing count is a measurement that might work as a threshold for a signal and it is quite evident, the differences between the physiological signal, the one of the myopathy/acute neuropathy. 

![[Pasted image 20251007143138.png]]

![[Pasted image 20251007143526.png]]

Here we see some of the parameters we could calculate in freq domain. These are used to implement some statistics that define the shape.

![[Pasted image 20251007143726.png]]

This points relates the pathological info extracted by the freq domain. 

![[Pasted image 20251007144434.png]]

Here we can see the fiber characteristics and the recruitment policy which stands ...

![[Pasted image 20251007144831.png]]
Statistical domain, moments, involved in the analysis of the freq, we have the mean, median...

![[Pasted image 20251007145314.png]]


![[Pasted image 20251007145632.png]]

An example with positive skewness and kurtosis :), the peak region depending if it is wide or narrow tells us the kurtosis.

![[Pasted image 20251007145720.png]]

![[Pasted image 20251007145832.png]]



