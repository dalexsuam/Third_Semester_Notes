02/10/2025


For critical situations. Do we prefer floating node or not grounding? The grounding is made such that any leakage current is independent from other. We have to take care there is no strong interdependency between the grounds. 

Why grounding and earthing? They´re the same, ty USA and UK :)

Also see that in this enviromental model of the device, we can find the current flux (the yellow/greenish line).  (Something about the differences between diff grounds might make a current loop that needs to be discharged)

![[Pasted image 20251002162844.png]]

Here we have essentially an approach of removing noise by filtering. Noise can be rejected if this is outband of the signal operation. Also,  we might increase SNR...
![[Pasted image 20251002164746.png]]

Here we also apply the Shannon-Nyquist theorem. 

And...

![[Pasted image 20251002165018.png]]

This is an example of SNR. 
Since the noise is not superimposed, we can setup something that can separate the both frequencies and go back to the initial 10Hz
![[Pasted image 20251002165604.png]]

Any processed noise passing through a linear filter would generate noise afterwards cos not all processing is linear.

![[Pasted image 20251002165943.png]]
We have the 10mV amplitude with noise of 100mV and weĺl see that the output would be in the top S+N. 

If I have a non-linear component, and apply the filter before, the 100mV would be reduced and we would see at the final output something not that corrupted.

![[Pasted image 20251002170256.png]]
this is the real spectrum of a EMG signal. THe main spsectrum and the noise signal spectrum . We see some classical errors and noise due to the main freq. 50Hz. 220v rms, which will provide noise and its harmonics, due to EMI.


![[Pasted image 20251002170933.png]]

We reduce the thickness of the Notch by means of the Q parameter.

![[Pasted image 20251002171308.png]]

Here are set requierements for bandwidht to be chosen and used properly in EMG systems. What we see is that we have requierements for surface and electrodes which are different.

The low-pass filter will remove the part of the noise from the limitations of the harmonics, and for special wideband application.

THen for wire electrode analysis we have higher low pass filter use, and then in monopolar,, we have very high 

![[Pasted image 20251002171801.png]]

Digital filter have better performance w.r.t the analog. Here we have some analog filters, and its different families 

![[Pasted image 20251002173051.png]]
Low pass filter can be implemented by using a capacitor and inductor, like used in speakers or as the Sallen Key config where the inductor is simulated by the amplifier. and this config has a gain  which is non inverting 
$$
G=\left(1+\frac{R_2´}{R_2}\right)
$$

![[Pasted image 20251002173318.png]]

See the freq response next to this Sallen key cell and the difference is that we have now a couple of resistors that gives a gain between output and input whereas the other doesn´t have it. If we look at the freq response we see that there are a couple of parameters that can be used
$\omega_n$ and $\zeta$

![[Pasted image 20251002173729.png]]

We see that the number of polynomials would make sharper the decay curve of the low-pass filter Butterworth. 

![[Pasted image 20251002174201.png]]

Let´s look back at these. For each pole we increase by 20dB the decay. However, depending of the type of filter the part of the decay might be steeper or less steeper. And so, in the case of the Butterworth filter, if we have the -3dB point butterworth family it all pass exactly for the following point:

![[Pasted image 20251002174410.png]]
And the more increases the number of poles, the steeper the curve. 

![[Pasted image 20251002174501.png]]
Depending on the values given to these cells, we might change the type of filter.
At top we have a second order filter, a second order polynomial of Butterworth.

The bottom one is suppose to be a fourth order
![[Pasted image 20251002174624.png]]
Note fourth order Butterworth filter is not 2 times the 2-nd order, note the values of the polynomials are different. And they need to be different 

![[Pasted image 20251002174752.png]]

Let´s compare these three: **Butterworth, Bessel and Chebyshev**.

We see Chebyshev have also a pretty steep behavior. The three filters are different only at the beginning cos note that the slopes are parallel. The higher the frequencies, the more similar the behavior of the three filters. 

Butterworth is maximal flatness
Chebyshev is maximal steep 
Bessel is maximal in terms of distortion, no distortion.

![[Pasted image 20251002175046.png]]

Note that group delay of these would give the frequencies of the phases entering and exiting and see that in bessel they remain the same. 

![[Pasted image 20251002175312.png]]

The location of the poles depend on the order. Even order we´ll have pair of complex conjugated poles, if it is odd there will be a real pole included. 

![[Pasted image 20251002175722.png]]
We exchange resistors and capacitors. Basically the same configuration but swapping the components but for the gain.

![[Pasted image 20251002182154.png]]

Now, we see here the characteristics of the A/D conversion. We start by knowing three different types of A/D devices from faster to slower conversion. Flash, Ramp, SAR. The faster the A/D might trade-off with complexity and not feasible in terms of budget and also accuracy.

The bigger the number of bits, the slower the device and we can design the part of the A/D device by starting from the amplitude of the signal we want to convert that is usually 5-10-15V and the resolution would depend on the number of bits. The least significant bit in the A/D converter is the Vrange/2^N

![[Pasted image 20251002183220.png]]
Last but not least :). We take into account the Shannon-Nyquist theorem to have the proper sampling frequency for the reconstruction of the signal after A/D  

![[Pasted image 20251002183727.png]]
After the conversion we are suppose to do some preprocessing and parameters stimation for diagnosis purposes and maybe  for data processing.

![[Pasted image 20251002183800.png]]
We see how EMG signal does appear a repetition of bursts of the signal which is completely non-reproducible cos there is a generation depending of an stochastic signal. 

Between bursts there is some resting period.
![[Pasted image 20251002183933.png]]

From where the problem arises? From the stochastic activation of the fibers. It is something that changes each time, an excitation of fibers that will produce a motor unit action potential in train which is subjected to stochastic behavior. Another problem is the cancellation; adding Action potentials could add to 0 instead of increase, this is a phenomenon called a reduction, underestimation on the EMG signal, and then we have a displacement. 

![[Pasted image 20251002184216.png]]
For this reason, we use Power Spectrum of EMG which in some way is a bit independent on the problems we´ve highlighted in the MUAP summation. In the Power Spectrum we can identify the peak frequencies.

We´re suppose to apply a HP-Filter in order to get rid of the noise of the movement of the electrodes on the skin surface

This kind of distribution is not a gaussian. 


![[Pasted image 20251002184823.png]]


![[Pasted image 20251002185148.png]]


![[Pasted image 20251002185301.png]]

Crosstalk, we have two muscles one in blue and red, and in overall the EMG is the sum of the two EMG´s, so, we´ll see which would be the summation of all the muscle EMG´s involved.
![[Pasted image 20251002185416.png]]
The other problem that comes with the EMG data. The geometry of the muscle and the place where the electrode is placed

And then, we´ll have to deal with noise. External noise which is due to electrical appliances, EMI coming from the power supplies, another instrumentations etc.

Also noise of the electrodes, due to the variation of the activity of the contact and changes in the surface on the skin. and also electronic noise coming from the amplifiers.

![[Pasted image 20251002185618.png]]

Noise effects. 50-60Hz hum it is a straight line between one burst and another. The reason is that we have an interference in power supply that transforms it into this.
The baseline´s offset is also affected by the zero due to the amplifier direct current. The baseline shifts due to the movement of the electrodes and another noise which can happen is the ECG artifacts, peaks that are effect of internal noise which is carrier noise that can be seen easily cos the amplitude of the ECG is bigger than the EMG. 

How can we remove cardiac artifacts? Filtering it at 1 Hz? But it is just the first harmonic, it doesn´t remove every spike, don´t forget about them :)
The only way is to move the electrodes somewhere to a correct position (far away from the chest activation)

![[Pasted image 20251002190154.png]]

