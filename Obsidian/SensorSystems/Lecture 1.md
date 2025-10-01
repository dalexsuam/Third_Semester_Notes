
Date: 18/09/2025
***


# <span style="color:rgb(223, 109, 109)">Introduction about sensors</span>

Let's start with some definition. We will define what is a transducer, a sensor and an actuator.

## <span style="color:rgb(239, 179, 1)">Transducer</span>
Transducer include both <span style="font-weight:bold; color:rgb(2, 141, 192)">sensors</span> and <span style="font-weight:bold; color:rgb(2, 141, 192)">actuator</span>. In fact a transducer is a device which transforms one type of energy to another type of energy. 

## <span style="color:rgb(239, 179, 1)">Sensor</span>
In particular sensors are those devices which monitor a physical parameter in systems and transform it in an electrical signal. 

==**Examples of physical parameters are**: force, pressure, motion, temperature.== Instead electrical signals are typically voltages or currents. 

## <span style="color:rgb(239, 179, 1)">Actuators</span>
Actuators are transducers which transform an electrical signal to a physical quantity. So for instance in machines they are responsible for moving or controlling mechanical systems.

***
![[Pasted image 20250921161854.png]]


In many applications we see this typical sensor electronics and actuator chain. Let's start from an example.

So if we want to drive a servo motor we need all this chain which is composed not only by the actuator which is the servo motor itself but we need also sensors and also some electronics. 

So let's start from the what is a servo motor. 

<span style="font-weight:bold; color:rgb(161, 40, 226)">servo motor</span>: It is a motor which is able to precisely control the **angular and the linear position**, **velocity and acceleration of a motor**, a rotary or a linear actuator.

In order to drive precisely this motor we need many type of sensors. For instance we need a pressure sensor, <span style="font-weight:bold; color:rgb(71, 215, 140)">we need the angular sensor or position sensor like potentiometer and also current sensors</span>. 

![[Pasted image 20250921163219.png]]

All these sensors can communicate with the electronics which is the brain of this chain through a digital standard communication protocols or the output of the sensor can be an analog signal and in this case we need to first of all convert the analog signal, the output signal of the sensor in a digital signal using an **analog to digital converter.**

![[Pasted image 20250921163255.png]]

Then here we have the main core of the electronics which is the processor. In this example the processor is a Raspberry Pi but other processor can be for instance a microcontroller as we will see during this course. The processor will acquire the output of each sensor and then **will process this information in order then to drive the actuator** for instance using in this example a PWM controller or more generally speaking using a generic driver.

# <span style="color:rgb(223, 109, 109)">Classification of sensors</span>

We have mainly two ways to classify sensors. The first one is the classification <span style="font-weight:bold; color:rgb(2, 141, 192)">based on the physical phenomena</span>. The second one instead is <span style="font-weight:bold; color:rgb(71, 215, 140)">based on the measuring mechanism.</span>


## <span style="color:rgb(239, 179, 1)">Classification of sensors by physical phenomena</span>

So let's start with the first one, the classification based on physical phenomena. With this classification we can have the following sensors:
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Optical sensors</span> able to measure visible or infrared light like a photodiode but also image sensors like a CCD camera, arctipixel sensor cameras and infrared sensors. 
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Thermal sensors</span> which are able to measure the temperature of an object for instance we have the resistive temperature detector, the thermistors, the thermocouple and so on.
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Magnetic sensor</span> able to measure the magnetic field such as Hall-effect sensors and magneto-resistive sensors. 
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Mechanical sensors</span> able to measure strain for instance with strain gauges or forces for instance with piezoelectric sensors or displacement and distance through capacitive, inductive, acoustic or optical sensor and acceleration and orientation typically with MEMS or microelectromechanical systems and then other quantities like viscosity, pressure and so on.
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Chemical sensors</span> that are mainly used to measure for instance pH but also the presence of other molecules like glucose, oxygenated hemoglobin and so on.

# <span style="color:rgb(239, 179, 1)">Classification of sensors by measuring mechanism</span> 

The other type of classification is the one based on the measuring mechanism. In this case we can distinguish:
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Resistive sensors</span>: Sensors which are based on a resistance which changes its value depending on the value of the physical quantity that it is measuring. Just to make an example RTDs so resistive temperature detectors are resistive sensors that are used to measure temperature so it means that the value of the resistance changes correspondingly with changes in temperature.
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Capacitive sensors</span>
* <span style="font-weight:bold; color:rgb(161, 40, 226)">Inductive sensors</span> 
And sensors which exploit the <span style="font-weight:bold; color:rgb(161, 40, 226)">piezoelectricity</span> or <span style="font-weight:bold; color:rgb(161, 40, 226)">Hall-effect</span> sensors and finally <span style="font-weight:bold; color:rgb(161, 40, 226)">MEMS or microelectromechanical systems</span>.


# <span style="color:rgb(223, 109, 109)">Which sensors will we study?</span>

![[Pasted image 20250921172700.png]]

In particular which kind of sensor we will study during the sensor system course? Mainly most of the ones that I mentioned before but let's see more in detail..
* We will study light and image sensor and in particular photodiode and charge coupled devices CCD and active pixel sensor CMOS.
* We will study sensor to measure temperature and in particular we will study resistance temperature detectors, thermistors, thermocouple and infrared thermometers. 
* We will study a sensor for measuring magnetic field such as Hall-effect sensors and magnetic resistances. Then sensor to measure strain, force and pressure like strain gauges and piezoelectric sensors.
* Sensor to measure displacement, proximity, distance and rotation and in particular we will study capacitive sensing, inductive sensing, acoustic and optical sensors. 
* Other important sensors are the ones that measure acceleration and orientation and typically this is done with microelectromechanical systems so accelerometers and gyroscope. 
* Finally we will study sensor to measure the sound and in particular we will study the microphones. Now we will define many different parameters that are used to characterize sensors. So the first one most important probably is the sensitivity.


# <span style="color:rgb(223, 109, 109)">Sensors' Characteristics</span>

## <span style="color:rgb(239, 179, 1)">Sensitivity</span>

The sensitivity is defined as the ratio between the output signal, output electrical signal and the input signal.
$$
S= \dfrac{\partial _{out}}{\partial _{in}}
$$
So just to make an example:
* If I have a **resistive temperature sensor** then the variation of the <span style="font-weight:bold; color:rgb(71, 215, 140)">output is the variation in the resistance of your resistor</span>, <span style="font-weight:bold; color:rgb(2, 141, 192)">the variation of the input is the variation in the temperature that you are measuring</span>. 

## <span style="color:rgb(239, 179, 1)">Resolution</span>

A second important parameter is the resolution that is also called least significant bit (LSB)

The resolution is the smallest increment that we can measure with the sensor. ==Typically for digital sensors the resolution is related to the least significant bit of the ADC that is used to convert the analog output of the sensor in a digital signal.== 

## <span style="color:rgb(239, 179, 1)">Full Scale Range</span>

Then the Full scale range is the maximum interval that we can measure with our sensor

## <span style="color:rgb(239, 179, 1)">Number of Bits</span>

The number of bits $n$ in a digital sensor, so a sensor that uses an analog to digital converter to digitalize the output of the sensor is defined as $n$ where $2^{n}$  is the number of levels in which we divide the entire full scale range.
$$
2^n = \frac{FSR} {LSB}
$$

## <span style="color:rgb(239, 179, 1)">Accuracy</span>
Another important parameter is the accuracy. The accuracy is defined as the error between the result of the measurement and the true value that we want to measure.

![[Pasted image 20250921183800.png]]

So let's have a look to this example. Imagine to have a rule. *The notches of the ruler define the resolution, so the minimum distance between two notches is the resolution.*

**Resolution is different from accuracy**. In f act, imagine that you want to measure an object which is in the position of the red arrow, so this is the true value that we would like to measure, but our sensor instead performs a different measurement that is the one which is indicated by the black arrow. 

> [!note] The difference between the true value and the measured value is the **ACCURACY**, that you see that is completely different from the resolution which is just the distances between two consecutive notches in your measurement system that can be for instance a ruler.

## <span style="color:rgb(239, 179, 1)">Repetability or Precision</span>

Then another important parameter is the repeatability or precision. The repeatability is the ability of the sensor to output always the same value when you repeat many times your measurement and typically the precision or repeatability is measured in terms of standard deviation of the measurement or full width at half maximum of the distribution of the measurement loop.

==So be careful because also accuracy and precision are different things, sometimes they are mixed up, but they are really different things.

| Example 1                                                                                                                                                                                                                                                                                                                                 | Example 2                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Example 3                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| ![[Pasted image 20250921184426.png\|200]]                                                                                                                                                                                                                                                                                                 | ![[Pasted image 20250921184306.png\|200]]                                                                                                                                                                                                                                                                                                                                                                                                                            | ![[Pasted image 20250921184342.png\|200]]                             |
| If you repeat many times the measurement you always obtain almost the same value, so it means that this measurement is very precise, but you see that the value that you measure is different from the true value that you would like to measure, so it means that the accuracy is not very good. Hence, **high precision, low accuracy** | If you repeat many times the measurement you obtain a very spread value, so very different measured values, but on average the measured value is correct, so it's very similar to the true value.<br><br>So in this case it means that your measurement is not precise because you have a very large standard deviation of your measurement, but it is very accurate because on average you are measuring the correct value. **Hence, low precision, high accuracy** | Here, you have a measurement that is both accurate and also precise.  |
## <span style="color:rgb(239, 179, 1)">Linearity</span>

Typically when we plot the output of the sensor with respect to the input that we provide to the sensor we would like to have a straight line characteristic. 

In the case we consider a digital sensor we can define two figures of merit for the linearity which are:

* Differential non-linearity, DNL
* Integral non-linearity, INL

![[Pasted image 20250921185017.png]]
So in a digital sensor you can have this graph in which you plot on the vertical axis the output code of your digital sensor and on the horizontal axis the analog input that you want to measure.

Ideally if you have a sensor with a perfect linearity you would like to have all steps corresponding to each digital value of the same width, and the width should correspond to the least significant bit, the LSB. But if you consider the characteristic of a real sensor you will see that the steps for each digital code are not exactly of the same width. 

<span style="font-weight:bold; color:rgb(161, 40, 226)">Differential Non-linearity: </span>So, we can define the differential non-linearity as the difference between the actual step width $\Delta in(i)$ minus the ideal step width which would be the least significant bit, the LSB.

| ![[Pasted image 20250921185719.png]] | ![[Pasted image 20250921185844.png]] |
| ------------------------------------ | ------------------------------------ |

$$
DNL(i) = \Delta in(i) - LSB
$$
And you can define the DNL, so it's the $DNL(i)$, because you can define the DNL of each step. So sometimes you will have positive DNL like in this case because the step is larger than the LSB and sometimes you will have negative DNL because the real step is smaller than the LSB. 

<span style="font-weight:bold; color:rgb(161, 40, 226)">Integral Non-linearity:</span> Then the integral non-linearity instead is a measure of the difference between the centroid of your real step, the one in red, with respect to the ideal position on this best fit straight line of the perfect linear characteristic.
![[Pasted image 20250921185803.png]]

So in this case the INL for this step is the difference between this red spot and the white spot here. You can compute the INL as the summation of the DNL until that step.
$$
INL(i) = \sum _{k=1}^{i} DNL(k)
$$

## <span style="color:rgb(239, 179, 1)">Transfer Function</span>

Another important parameter of the sensor is the transfer function which represents the frequency response of the sensor.
![[Pasted image 20250921190053.png]]
So mainly it represents the relationship between the output and the input of the sensor at the different frequencies and it can be represented with the **body diagram of the magnitude of the gain of the sensor**. We can be also interested to the phase difference between the output and the input and this is represented by the phase body diagram. And you see in this diagram we represent both magnitude and phase in respect to the frequency.

## <span style="color:rgb(239, 179, 1)">Bandwidth</span>

We can define as bandwidth of a sensor, the frequency range in which our sensor has a pretty constant transfer function. So in this example this portion here in the middle is the bandwidth of our sensor. 

## <span style="color:rgb(239, 179, 1)">Noise</span>

Noise is an unwanted effect that we have in every sensor and it is a random fluctuation in the measured value. 
![[Pasted image 20250921190232.png]]
So look at this example, imagine that your output should be a perfect sinusoid. But in this case the real output signal is not a perfect sinusoid but is a sinusoid which superimpose some fluctuation. ==So this fluctuation of the signal are due to the sensor noise or to the noise introduced by the front end circuit of the sensor.==

Since the average value of the noise is always zero, noise is quantified with its root mean square value. 

## <span style="color:rgb(239, 179, 1)">Dynamic Range</span>

Dynamic range is another very important parameter and it is defined as the ratio between the **maximum signal that you can measure** divided by the **minimum input amplitude that you can measure**. Typically dynamic range is expressed in decibel so it is defined as:
$$
DR = 20*log\frac{MaxInputAmplitude}{MinInputAmplitude} [dB]
$$

But what is the maximum input amplitude? So for sure ==the maximum value that we can measure is the full scale range of our sensor==. **So the difference between the maximum value that we can measure and the minimum value that we can measure**. And the min input value is the noise.

> [!warning]
We might think that the minimum input amplitude is simply the least significant bit (LSB), which is the resolution of the instrument. However, in practice, we are not only limited by resolution. The real limiting factor is usually the noise.
Even if the instrument has very high resolution—so that it can theoretically detect very small changes—if the signal is buried under random fluctuations (noise), those fine details become useless. In other words, the smallest signal we can actually detect is the one that rises above the noise level.

That’s why, when we calculate the dynamic range of a sensor, the denominator in the formula is not just the resolution but the noise level.

These parameters that we have seen are typical parameters of all the sensors that we will study and they are very important to characterize the sensor and also to select the best sensor for your application.

In fact if you buy a sensor you should have a look to its data sheet so a sheet which explains how to use the sensor but also the performances of the sensor so in the data sheet of the sensor you will find all the parameters that we listed now.

## <span style="color:rgb(223, 109, 109)">Analog Sensor Readout</span>

So there exist two types of sensors the analog sensor and the digital sensor. Analog sensors are those sensors which output is an analog voltage.

## <span style="color:rgb(239, 179, 1)">ADC+Microcontroller</span>

![[Pasted image 20250921191649.png]]

**So how can we read out analog sensors?** Typically in order to read out analog sensors we need first of all a front-end circuit which amplifies the signal, that is, the output of your analog sensor and then if you want to process the information you need to convert your analog signal into a digital signal. ==So you can use for instance an ADC to convert the signal and then a microcontroller to process the information.== 

In our laboratory we will have some analog sensor that we will directly connect to our microcontroller because our microcontroller that we will use during the labs already includes an analog-digital converter inside the microcontroller chip.

So many microcontrollers have built-in ADC and typically they are 8-bit up to 12 or even 16-bit analog-to-digital converter. 

## <span style="color:rgb(239, 179, 1)">Data Acquisition Cards</span>

![[Pasted image 20250921191707.png]]
Another possibility which is easier for people maybe not very expert in electronics is to use **data acquisition cards** which are those cards for instance from *National instruments* in which you can connect the output of your sensor and you have different type of connectors like a BNC and this card directly provides the front-end for your analog input and also provides the analog-to-digital conversion. 

Then you can connect it to USB to your computer and you can display the output of the sensor and directly you can process the information on your PC.

# <span style="color:rgb(223, 109, 109)">Smart Sensors Readout</span>

On the other hand digital sensors are sensors which output is directly a digital signal. **Digital sensors are also called smart sensors.** ==They are smart sensors because in the same chip they both include the sensor itself but also a built-in signal processing so the front-end circuit of the sensor and the analog-to-digital conversion and sometimes also some filtering and something to announce the signal from the sensor.==

And then smart sensors also include the communication parts. **They implement communication protocols in order to send the digital information from the sensor to your processor.** There are different ways to communicate the output of the digital sensor to your processor.

In particular we have different type of digital standards for the output. 

## <span style="color:rgb(239, 179, 1)">Parallel Bus</span>

We can have a parallel bus. A parallel bus is simply a bus which has one wire and one connection for each of the output bits that represent the conversion of the value measured by the sensor.

## <span style="color:rgb(239, 179, 1)">Serial Interfaces</span>

Or you can have serial interfaces. Serial interfaces can be either <span style="color:rgb(2, 141, 192)">synchronous</span> or<span style="color:rgb(71, 215, 140)"> asynchronous.</span> 

Synchronous means that you have at least two wires in order to communicate your digital world.
*
* One for the clock
* One for the data. 
 
So the data is given out from your smart sensor synchronous with a clock which defines the transition of the data. 

There are exist different type of synchronous protocols and in particular during our labs we will use the **serial peripheral interface SPI and the I2C inter-integrated circuit.**

<span style="font-weight:bold; color:rgb(161, 40, 226)">Serial Peripheral Interface (SPI):</span> SPI we will see that it's a simpler communication protocol with respect to I2C and mainly we have just one clock and one bidirectional data and one chip select in order to communicate and to enable different slaves in the communication. 

<span style="font-weight:bold; color:rgb(161, 40, 226)">Inter-Integrated Circuit (I2C):</span> The inter-integrated circuit I2C protocol is a bit more complex because we will see that there is a very well fixed protocol in which you:
* Send the address of the slave with which you want to communicate
* Send one bit to say if you want to do a read or write operation 
* Send your data.

So I2C is a more complex and articulated protocol in respect to SPI but we will study both in detail during the laboratory part. Then we also have asynchronous communication protocol.

<span style="font-weight:bold; color:rgb(161, 40, 226)">Asynchronous Communication Protocol</span>: So in asynchronous communication protocol we don't have a clock which establish when the data is being transferred so when we have to read out the data

**So how can we set the communication between transmitter and receiver on which the data can be sample?** Imagine to have just one wire communication and the one wire communication is the wire of the data. 


| Synchronous                          | Asynchronous                         |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20250921193010.png]] | ![[Pasted image 20250921193143.png]] |

Look at the asynchronous and ask yourself. How can I understand if this word is  1 1 1 0 1 or if it is just 1 1 0 1. As you see they are different words because in one case we have three ones and in the other case we have only two ones.

==In case of this one-wire-asynchronous-communication it is very important that the baud rate of the transmitter must match with the baud rate of the receiver==. We will see that it's very important that you fix a certain baud rate in your microcontroller so the microcontroller will send a new data at a certain frequency and you provide the same baud rate also to the receiver that for instance in the case of the **UART** will be our personal computer. 

There are also different type of asynchronous communication protocols an example can be <span style="font-weight:bold; color:rgb(161, 40, 226)">frequency encoded protocols</span> in which we exploit some timing peripherals of your processor and then you can measure the pulse width or the frequency of the pulses that you provided and depending on the frequency of the pulses that you provide or on the pulse width of these pulses then you can understand if you are trying to send in a logic 0 or logic 1.

# <span style="color:rgb(223, 109, 109)">Sensor Calibration</span>


In general, sensors are not perfect and can show **non-ideal effects**:

- **Offset**: This is a fixed error. It means there is a constant difference between the measured value and the true value. For example, if you use a scale and it always shows **2 kg more** than the actual weight, that is an offset.
    
- **Non-linearity**: This happens when the relationship between input and output is not a straight line. Instead of being proportional, the sensor’s response could follow a curve (e.g., exponential, quadratic). In this case, the error changes depending on the input value.
    
- **Cross-sensitivity**: This occurs when the sensor’s output is influenced not only by the quantity we want to measure but also by another, unwanted factor. For example, a strain gauge changes resistance under stress (which is what we want to measure). However, resistance also depends on temperature. So, if the resistance changes, we might not know if it’s due to stress or temperature variation.


When these errors are predictable (like a fixed offset), we can apply **calibration**. Calibration adjusts the sensor’s output so that it matches the true value, reducing or compensating for these errors.

## <span style="color:rgb(239, 179, 1)">Analog Signal Conditioning</span>

Here we're subtracting or removing the offset provoked by the error

## <span style="color:rgb(239, 179, 1)">Look-up Table</span>

If you perfectly know that measuring a certain input value we'll have a corresponding output value

## <span style="color:rgb(239, 179, 1)">Digital Calibration</span>

We're implementing an equation which is used to transform the measured value into the real parameter that we want to measure. If we are dealing with the offset we'd subtract it digitally.

$$
T = a+bV+cV^{2}
$$
$T$ is temperature, $V$ sensor voltage,  $a$ $b$ and $c$ are calibration coefficients