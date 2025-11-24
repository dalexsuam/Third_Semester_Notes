
20/10/2025
***

# <span style="color:rgb(223, 109, 109)">Internal Temperature Sensor</span>

Most STM32 microcontrollers include an internal temperature sensor connected to the ADC. This sensor is designed to provide an approximate measurement of the microcontroller’s own internal temperature. Its purpose is **not** high-accuracy temperature monitoring but rather safety and system monitoring.

## <span style="color:rgb(239, 179, 1)">Purpose of the Internal Temperature Sensor</span>

The internal sensor is intended to:
- Detect whether the microcontroller is overheating.
- Verify that the device is operating within its safe thermal range.
- Enable basic thermal protection mechanisms if necessary.
    

It is **not** designed for:

- Precise temperature measurement.
- Measuring ambient temperature.
- Measuring temperature of external objects or systems.
    
Because of this, the typical accuracy is around **±1.5°C**, which is relatively low. However, this level of precision is sufficient for its intended purpose: verifying that the chip is functioning correctly and not reaching damaging temperatures.

![[Pasted image 20251122211504.png]]
# <span style="color:rgb(223, 109, 109)">Temperature Computation Process</span>

The sensor output is read through the ADC, so the temperature calculation consists of two steps: converting the ADC reading to a voltage, and then converting that voltage into a temperature value.
## <span style="color:rgb(239, 179, 1)">1. Converting ADC Value to Voltage</span>

The ADC range is from 0 to 3.3 V with a 12-bit resolution.  Thus, the sensed voltage is computed as:
$$V_{sense} = \text{ADCvalue} \times \frac{3.3}{4096}$$
This step is identical to converting the ADC reading of a potentiometer.

## <span style="color:rgb(239, 179, 1)">2. Converting Voltage to Temperature</span>

The microcontroller datasheet provides a linear formula relating voltage to temperature:

$$Temperature(^{\circ}C)=\frac{V_{sense}-V_{25}}{AvgSlope}+25$$

Where:

- $V_{sense}$​ is the voltage obtained from the ADC reading.
- $V_{25}$​ is the sensor output voltage at 25°C (typically around 0.76 V).
- $AvgSlope$ is the average slope of the sensor in mV/°C (typically around 2.5 mV/°C).
- $25°C$ is the reference temperature used for calibration.

### <span style="color:rgb(161, 40, 226)">Interpretation of the Formula</span>

The internal temperature sensor behaves as a linear sensor:
- At $25°C$, the voltage equals $V_{25}$.
- For each degree change in temperature, the sensor output changes by $AvgSlope$
    
The formula computes:
1. The difference between the measured voltage and the reference voltage.
2. The corresponding temperature difference using the slope.
3. The final temperature by adding the reference 25°C.

***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 6a: ADC with DMA and Timer Trigger</span>

**Objective:**  
Acquire **three voltages**—

1. Potentiometer (external analog input)
2. Internal temperature sensor
3. VREFINT (internal reference voltage)
…every **1 second**, using:
- **Hardware triggering** of the ADC by **Timer 2**
- **DMA** to automatically transfer all conversion results into memory.
- **UART** to send the measured values to a remote terminal.

The ADC must perform **3 consecutive conversions**, and DMA stores all results in an array.

### <span style="color:rgb(161, 40, 226)">1. Enabling Internal ADC Channels</span>
![[Pasted image 20251020151137.png|400]]
The internal channels (Temperature sensor and VREFINT) are **disabled by default**. ADC settings, you must **enable them**.
![[Pasted image 20251020151257.png|400]]
### <span style="color:rgb(161, 40, 226)">2. ADC Configuration for Multiple Conversions</span>

#### <span style="color:rgb(2, 141, 192)">a. Number of conversions</span>

![[Pasted image 20251025231448.png|500]]

Since we need **3 different measurements**, the ADC must be configured in **scan mode**, with:
- **Scan Conversion Mode = Enabled**
- **Number of conversions = 3**
- **Channels ordered in the rank table**

For example:

| Rank | Channel                        |
| ---- | ------------------------------ |
| 1    | Potentiometer (e.g., ADC1_IN1) |
| 2    | Temperature Sensor             |
| 3    | VREFINT                        |
#### <span style="color:rgb(2, 141, 192)">b. Sampling Time = 480 cycles</span>

This is important for _internal_ channels:
- The temperature sensor and VREFINT require **long acquisition time** due to internal impedance.
- STM recommends **≥ 10 μs** sampling time.

At 21 MHz ADC clock, **480 cycles ≈ ~22.9 μs**, satisfying the requirement. Thus, 480 cycles ensures **stable and reliable readings**.

### <span style="color:rgb(161, 40, 226)">3. Timer 2 Trigger Event</span>

Instead of starting conversions manually, we configure:

**Timer 2 → TRGO (Trigger Output) → ADC External Trigger**


| Timer                                     | ADC                                       |
| ----------------------------------------- | ----------------------------------------- |
| ![[Pasted image 20251025231346.png\|400]] | ![[Pasted image 20251025231448.png\|400]] |


Steps:

1. Timer 3 is configured to overflow every **1 second**.
2. In TIM3 settings, the TRGO event must be:
    - **"Update Event"**  
        (not "Reset", which only resets the timer but does not generate a trigger)

3. ADC trigger is set to:    
    - **External Trigger Conversion Source→ Timer 3 Trigger Out Event**
    
Now, once per second:

- Timer overflows → TRGO event
- ADC receives the trigger → performs the 3-channel conversion sequence.

No polling or software trigger is needed.

### <span style="color:rgb(161, 40, 226)">4. DMA Configuration (Circular, Halfword)</span>

#### <span style="color:rgb(2, 141, 192)">Why Circular Mode?</span>

![[Pasted image 20251025173946.png|400]]

Because the ADC receives a trigger _every second_, and we want:

- DMA to continually overwrite the same memory buffer
- No manual restart

Circular mode means:

> After the last data transfer, DMA returns to the beginning of the buffer and waits for the next conversion sequence.

#### <span style="color:rgb(2, 141, 192)">Why Halfword (16-bit) Data Size?</span>

![[Pasted image 20251025231346.png|600]]

The ADC produces **12-bit** results stored in a **16-bit register** (right-aligned).  
Thus:
- DMA peripheral size = **Halfword**
- DMA memory size = **Halfword**

Using 32-bit would waste memory and transmit unnecessary data.


### <span style="color:rgb(161, 40, 226)">5. UART Configuration</span>

![[Pasted image 20251025231641.png|600]]

Baud rate: approximately **9600 baud**. This ensures compatible communication with the serial monitor.

UART is used at the end of each conversion (in the callback) to transmit:

- Potentiometer voltage
- Converted temperature value
- VREFINT reading

### <span style="color:rgb(161, 40, 226)">6. Code Explanation</span>

**Definitions**
```C#
#define ACQUISITIONS 3
#define VDDA 3.3 // Analog voltage supply
#define VSSA 0.0 // Analog ground
#define RESOLUTION_BITS 12
#define V25 0.76 //Temperature sensor voltage
#define AVG_SLOPE 0.0025 //Temperature sensor average
```
Meaning:

- **ACQUISITIONS** = number of ADC channels converted (3)
- **VDDA** = analog supply (converts ADC counts → voltage)
- **V25** = temperature sensor voltage at 25°C
- **AVG_SLOPE** = temperature sensor slope in V/°C

**Global Variables**
~~~C#
float FSR;
float RESOLUTION_STEPS;
uint16_t voltages[ACQUISITIONS];
~~~
`voltages[]` will be automatically filled by DMA as:
- voltages[0] → potentiometer
- voltages[1] → temperature sensor
- voltages[2] → VREFINT

**main.c Initialization**
~~~c#
int main(void){

FSR = VDDA-VSSA;
RESOLUTION_STEPS = (1)<<RESOLUTION_BITS; //ADC resolution steps calculation 2^(RESOLUTION)

HAL_TIM_Base_Start(&htim2); //Timer not used in interrupt mode, we simply use its output by our timer
HAL_ADC_Start_DMA(&hadc1, voltages, ACQUISITIONS);
~~~
This starts:

- Timer triggering every second
- ADC converting all 3 channels
- DMA storing results in `voltages[]`
    
No interrupts are needed for ADC start.

### <span style="color:rgb(161, 40, 226)">7. Conversion Complete Callback</span>

DMA finishes transferring all three conversion results, and the ADC interrupt triggers:
~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef *hadc){
	//DMA GETS AUTOMATICALLY THE GetValue
	float vpot= voltages[0]*FSR/RESOLUTION_STEPS;
	float vtemp = ((voltages[1]*FSR/RESOLUTION_STEPS)-V25)/AVG_SLOPE+25;//
	float vrefint = voltages[2]*FSR/RESOLUTION_STEPS;
	static char string[74];
	snprintf(string, sizeof(string), "Potentiometer: %.3f V, Temperature: %.3f degrees, VRef: %.3f V \r \n", vpot, vtemp, vrefint);
	HAL_UART_Transmit_DMA(&huart2, string, sizeof(string)); 
}
~~~

### Explanation

1. **DMA automatically fills the array**, so no need for `GetValue()`.
2. Potentiometer and Vref readings are simply ADC → voltage.
3. Temperature is computed using the formula:
    
$$T(°C)=\frac{V_{sense}-V_{25}}{AvgSlope}+25$$
1. UART transmits the complete formatted string using DMA.
### **Summary of Operation**

1. **Every 1 second**, TIM3 issues a **hardware trigger** to ADC.
2. ADC performs **3 sequential conversions** (pot, temp, vref).
3. DMA transfers all results into `voltages[]`.
4. ADC complete callback executes:
    - Converts values to physical units
    - Sends them to UART using DMA
5. DMA ready for next second (circular mode).
Everything runs **automatically**, without any polling in the `while(1)` loop.
---
---
---
---
---

# <span style="color:rgb(223, 109, 109)">Homework 6a: ADC scan using DMA</span> 

The task is to acquire **one ADC sample every 1 ms**, store them using **DMA**, and every **1 second** compute the average of the latest 1000 samples.  
This average is converted into:

1. **Voltage**
2. **LDR resistance**
3. **Light level in lux**

Finally, the result is sent via **UART**.

### <span style="color:rgb(161, 40, 226)">Hardware Connection and ADC Setup</span>

![[Pasted image 20251026000734.png|400]]

The Light-Dependent Resistor (LDR) is connected to **PA0**, which corresponds to **ADC1_IN0** in the STM32F4.

Therefore, we enable **ADC1** and activate **channel 0**.

### <span style="color:rgb(161, 40, 226)">Timer (TIM2) Configuration for the Trigger</span>

The ADC must convert **every 1 ms**, and instead of using software, we use **TIM2 as a hardware trigger**. This gives precise timing.

![[Pasted image 20251026001355.png|500]]
<span style="font-weight:bold; color:rgb(2, 141, 192)">TIM2 Clock</span>
To get an update event every **1 ms**:

Prescaler = 8400 – 1  
ARR = 10 – 1

So the timer generates an **update event every 1 ms**.

<span style="color:rgb(2, 141, 192)"><b>TIM2 Trigger Output (TRGO)</b></span>

TIM2 is configured with:
- Trigger Event Selection = **Update Event**
- TRGO = **Update**
Thus every time TIM2 updates (every 1 ms), it sends a trigger to the ADC.

### <span style="color:rgb(161, 40, 226)">ADC Configuration</span>

| ![[Pasted image 20251026001036.png\|500]] | ![[Pasted image 20251026001146.png\|500]] |
| ----------------------------------------- | ----------------------------------------- |

The ADC is configured so that it **starts a conversion only when TIM2 TRGO arrives**.
Key settings:

  <span style="font-weight:bold; color:rgb(2, 141, 192)">External Trigger</span>
- External trigger source: **Timer 2 TRGO**
- Trigger detection: **Rising edge**
    
<span style="font-weight:bold; color:rgb(2, 141, 192)">Continuous Conversion Mode</span>
Continuous mode is **disabled**.
**Reason:**  Continuous mode would cause the ADC to “free-run” at maximum speed without waiting for the timer.  We want strictly **1 conversion per 1 ms**, and that must be **timer-controlled**, so continuous mode is turned off.

<span style="font-weight:bold; color:rgb(2, 141, 192)">End-of-Conversion Flag</span>
Set to “End of single conversion”.  This ensures DMA gets new data every time one conversion finishes.

<span style="font-weight:bold; color:rgb(2, 141, 192)">DMA continuous requests</span>
Enabled so that DMA keeps receiving samples without CPU involvement.

### <span style="color:rgb(161, 40, 226)">DMA Configuration in ADC</span>

DMA is configured as:
![[Pasted image 20251026001615.png|500]]
- **Circular mode**
- **Half-word memory size** (16-bit ADC data)
- **Memory increment enabled**
- **Peripheral fixed**
    
Buffer defined as:
~~~c#
#define LENGTH 1000;
uint16_t ADC_Values[2*LENGTH];
~~~

The DMA therefore operates on a **2000-element circular buffer**. Because TIM2 triggers the ADC every **1 ms**, the DMA receives:

- 1000 samples in 1 s (for the first half)
- 1000 samples in 1 s (for the second half)


<span style="font-weight:bold; color:rgb(2, 141, 192)">Why Use Half-Complete and Complete Callbacks?</span>
DMA circular **mode** generates two interrupts:

***Half-Complete Callback*** Called when **first half (0 → 999)** is filled.
***Complete Callback*** Called when **second half (1000 → 1999)** is filled.

<span style="font-weight:bold; color:rgb(2, 141, 192)">Advantage of using both:</span>
1. **Real-time processing**  
    You process data every 500 ms instead of waiting 1 full second.
2. **No blocking**  
    While you process the first half, the DMA is filling the second half.
3. **Efficient memory usage**  
    You do not need two separate buffers; a single circular buffer is enough.
4. **No data loss**  
    Because DMA writes continuously while the CPU processes the other half.

This is a classical technique in embedded systems called **double-buffering**.

### <span style="color:rgb(161, 40, 226)">USART and NVIC</span>

![[Pasted image 20251026001433.png|500]]
![[Pasted image 20251026001505.png|500]]

### <span style="color:rgb(161, 40, 226)">Data Processing in the Callbacks</span>

***Main init***


~~~C#
HAL_TIM_Base_Start(&htim2);
HAL_ADC_Start_DMA(&hadc1, ADC_Values, 2*LENGTH);
~~~

***Routines***
~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	uint32_t Average = 0;
	for(int i=1000; i<2000; i++){
		Average = Average + ADC_Values[i];
	}
	float voltage = (Average/1000.0)*3.3/4096.0;
	float resistance = (voltage*100000.0)/(3.3 - voltage);
	float light = 10*pow((100000.0/resistance), 1.25);
	char string[64];
	int length = snprintf(string, sizeof(string), "R = %.1f Ohm, Light: %.1f Lux \r \n", resistance, light);
	HAL_UART_Transmit_DMA(&huart2, string, length);
}

void HAL_ADC_ConvHalfCpltCallback(ADC_HandleTypeDef* hadc){
	uint32_t Average = 0;
	for(int i=0; i<1000; i++){
		Average = Average + ADC_Values[i];
	}
	float voltage = (Average/1000.0)*3.3/4096.0;
	float resistance = (voltage*100000.0)/(3.3 - voltage);
	float light = 10*pow((100000.0/resistance), 1.25);
	char string[64];
	int length = snprintf(string, sizeof(string), "R = %.1f Ohm, Light: %.1f Lux \r \n", resistance, light);
	HAL_UART_Transmit_DMA(&huart2, string, length);
	}
~~~