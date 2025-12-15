 
13/10/2025
***
# <span style="color:rgb(223, 109, 109)">Analog Digital Converter (ADC)</span>

Now we can begin today’s theory class, which is about **ADCs — Analog-to-Digital Conversion**.  As I mentioned, we will focus on the ADC inside our microcontroller, because we will use it to read the analog sensors on our board.

These sensors output **analog voltages**, and we need to convert those voltages into **digital values** so the microcontroller can process them. Once converted, we can do whatever we need with the data — for example, send it through UART or use it in our program logic.

Our board — or more precisely, our **microcontroller** (because remember, the ADC is inside the STM32 itself, not on the Nucleo board) — features a **12-bit ADC**. A 12-bit ADC means we have **4096 possible digital levels** to represent an analog signal.

Of course, as in most microcontrollers and electronic systems, registers usually come in powers of two, so the ADC data is stored in a **16-bit register**.  
That means when we read the conversion result, we get a 16-bit value, but the **upper 4 bits are always zero** — only the lower 12 bits carry actual ADC data.  
The HAL library already provides functions to read these registers easily.

On our specific STM32, we only have **one sample-and-hold circuit and one ADC**.  
This is simply because the microcontroller is relatively simple. More advanced or expensive microcontrollers may have **multiple ADCs**, allowing parallel sampling of different channels. But in our case, we can read **only one analog channel at a time**.
![[Pasted image 20251122083500.png]]
$$V_{REF_-}=V_{SSA}=GND$$
$$V_{REF_+}=V_{DDA}=3.3V$$
Like any ADC, ours has an **input voltage range**. On the Nucleo board, the full range is available: **0 to 3.3 V**. This is important, because when converting a digital value back to an analogue voltage, we must remember that the ADC maps its 12-bit output across this **0–3.3 V range**.

![[Pasted image 20251122084147.png|400]]

Here’s a very short recap of the sample-and-hold circuit I’m going to show you. I think most of you are already familiar with it. A sample-and-hold circuit is not very complicated — it’s basically just a switch, a capacitor, and a resistor. In other words, it’s an RC circuit with a switch.

During the **sample phase**, the switch is closed. This allows the input signal to reach the capacitor and charge it. The sample phase must be long enough for the capacitor to charge to (approximately) the input level. Why do I say this? Because in your projects — and even inside a microcontroller — the sampling time must be chosen so that the RC network has enough time to charge. ==Typically, this means the sampling interval should be around four to five times the RC time constant==. It doesn’t have to be exact, but it must be long enough; otherwise, the capacitor won’t fully charge (or discharge), and the ADC won’t receive the correct value.

During the **hold phase**, the switch opens. Now only the capacitor remains in the circuit, holding the voltage it reached during sampling. The ADC then reads this stored voltage. As a result, the output signal won’t be smooth but will look like a staircase, because once digitized it is no longer a continuous analog signal.

Finally,==the duration of the hold phase depends on the architecture of the ADC. For example, if the ADC has many bits and needs more time to approximate the input voltage, then the hold phase must be long enough for it to complete the conversion.==
## <span style="color:rgb(239, 179, 1)">SAR ADC</span>

Now, in our board we specifically use a **successive approximation (SAR) ADC**. I think you are all familiar with this type of converter. How does it work? Essentially, it _guesses_ the value step by step.

It may sound a bit tricky to describe verbally, but it’s very easy to understand when you see it visually. In the example here, the ADC shown has only four bits, but the idea is exactly the same for more bits.

| ![[Pasted image 20251122084541.png\|300]]<br>It begins by checking whether the input voltage is above or below half of the reference voltage. If it is above, the first bit is set to **1**; if it is below, the first bit is **0**.<br>                                                                                                  | ![[Pasted image 20251122084556.png\|300]]<br>Then it proceeds to the second bit. Now it checks whether the input is above or below the midpoint of the remaining interval (for example, between half of the range and the upper half). Again, if the input is above that threshold, the bit is **1**; if it is below, the bit is **0**. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![[Pasted image 20251122084629.png\|300]]<br>This process continues, each time narrowing the range, becoming more precise at every step, until it reaches the final bit. If we have a 12-bit ADC, this means the comparison is performed **12 times**. That requires time — many clock cycles — before we obtain the final digital value. | ![[Pasted image 20251122084651.png\|300]]<br>This process continues, each time narrowing the range, becoming more precise at every step.                                                                                                                                                                                                |

![[Pasted image 20251122084712.png|400]]

This process continues, each time narrowing the range, becoming more precise at every step, ==until it reaches the final bit==. If we have a 12-bit ADC, this means the comparison is performed **12 times**. That requires time — many clock cycles — before we obtain the final digital value.
## <span style="color:rgb(239, 179, 1)">ADC Features</span>

Here are some features of our ADC. First, we have **16 external input channels**. These are channels that come from outside the microcontroller and correspond to actual pins, meaning we can connect external sensors to them.

Additionally, we have **two internal channels**. These channels are _inside_ the microcontroller and are not connected to any external pin. Remember: **the ADC is inside the microcontroller**, not on the development board—neither the white nor the green board. It is part of the chip itself. Keep this in mind for the exam or for future projects.

These two internal channels allow us to measure:

1. **The internal reference voltage**, which we can read to check for possible errors or inconsistencies ($V_{REFINT}=1.21 \space V$).
2. **The internal temperature sensor**, which helps monitor the microcontroller’s temperature. If the chip overheats, the system can stop operation to prevent damage—since excessive temperature will eventually cause the microcontroller to fail.
    
There is also a **battery charge monitor**. You might think: “But our board has no battery.” True—but microcontrollers often contain a tiny internal battery used to maintain the real-time clock (RTC). This keeps track of time and date even when the system is powered off. We can read the level of that internal battery if needed. It’s not relevant for our project, but it might be useful for others.

### <span style="color:rgb(161, 40, 226)">How do we start a conversion?</span>

There are three main ways to trigger the ADC:

1. **Software trigger**  
    We call a function in our code that starts the conversion.
2. **Timer trigger**  
    The timer can directly trigger the ADC through hardware.  
    This is not an interrupt; the timer simply acts as a hardware trigger, and no additional software is required. This is efficient and avoids CPU load.
3. **External trigger**  
    For example, we can connect a button to an EXTI line. When the button is pressed, the ADC starts a conversion. Again, this is hardware-triggered—not an interrupt—so the CPU can continue doing other tasks.
    
This hardware-driven approach is great for optimization, since the ADC operates independently of the CPU.
### <span style="color:rgb(161, 40, 226)">Conversion modes</span>

We have several different ways to manage the conversion process:

- **Polling mode**  
    We constantly check the _End Of Conversion_ (EOC) flag.  
    When EOC becomes true, we read the result.  
    This is simple but **very inefficient**. Still, your first project will use polling so you can learn the basics.
- **Interrupt mode**  
    The ADC generates an interrupt when the conversion finishes.  
    In the interrupt callback, we read the result.
- **DMA mode**  
    The DMA automatically transfers the ADC results into a buffer.  We only get an interrupt when the buffer is full.  This is the most optimized approach because the CPU is barely involved.
    
### <span style="color:rgb(161, 40, 226)">Continuous vs. Single Acquisition</span>

- **Continuous mode**  
    The ADC continuously samples. Each time a conversion finishes, the next one starts automatically. This is used when high-speed sampling is required. We won’t use it in our course because we do not need such fast acquisition.
    
- **Single acquisition mode**  
    A conversion only starts when a trigger (software, timer, or external) occurs.  
    This is the mode we will normally use.
    
### <span style="color:rgb(161, 40, 226)">Scanning multiple channels</span>

We can configure the ADC to read:
- **A single channel**, or
- **Multiple channels in sequence** (scan mode).
    
Scan mode is useful when we want to sample more than one sensor—for example, both the internal temperature sensor and an external sensor. The ADC will convert each channel one after another.

We can configure:

- **Up to 16 regular channels**, and
- **Up to 4 injected channels**.
    

Injected channels have **higher priority**. If a conversion request arrives for an injected channel, the ADC interrupts whatever it is doing, converts the injected channel first, and then returns to the regular sequence. This is similar to interrupt priorities in CPUs.

We can also configure:

- **Continuous scanning** (similar to continuous mode but for multiple channels).
- **Discontinuous scanning**, where the ADC converts a few channels, raises an EOC, then continues. This allows grouping channels—for example, converting 10 sensors in groups of 5.  
    We won’t use this feature, but it exists.
    
We can configure all of these options easily in the CubeMX IOC interface through simple checkboxes.

![[Pasted image 20251122105232.png]]

We can also choose **right or left data alignment** in the IOC, and this matters because it changes the numerical value we read from the ADC register. Always double-check that the alignment matches the way you are interpreting the data in your code.
### <span style="color:rgb(161, 40, 226)">Sampling Time</span>

As mentioned earlier, we must configure the **sampling time**. Why? Because different sensors behave differently electrically. The sample-and-hold capacitor is fixed, but the sensor’s impedance changes the **RC time constant**. A sensor with higher resistance results in a longer τ (tau), meaning the capacitor needs more time to charge properly.

In general, the maximum ADC clock frequency is **36 MHz**. However, the microcontroller’s main clock is 84 MHz, and since 36 is not a clean divider of 84, the actual maximum ADC clock for our device becomes **21 MHz**.

In addition to sampling time, the **resolution** (the number of bits) also affects conversion time.  A higher resolution (e.g., 12 bits) requires more comparison steps in a successive approximation ADC, increasing the total conversion duration.

$$f_{sampling}=\frac{f_{ADC_{clock}}}{(T_s+RES)}$$

The timing is given in **clock cycles** in the IOC, not in seconds. For our project, we will typically select the highest sampling time available. But if in an exam you are asked to modify these values, remember that **all timing parameters are interconnected**: ==sampling time (in clock cycles), ADC clock, and resolution== must be considered together. The formula shown in the slide reflects this relationship.

For example, ==the maximum sampling frequency at 12-bit resolution is about **1.4 MHz**==. If we reduce the resolution to 3 bits, we can sample much faster because far fewer steps are required. In other words: **higher resolution $\rightarrow$ lower maximum sampling frequency**.
$$T_{s_{min}}=3  \space clock \space cycles ;\space RES=12\space bits$$
This is the maximum sampling frequency at a resolution of 12 bits, for a sampling frequency of $1.4\space MHz$. (Remember the $f_{ADC_{clock}}=21\space MHz$)
### <span style="color:rgb(161, 40, 226)">Analog Watchdog</span>

A feature we will _not_ use, but is good to know, is the **analog watchdog**.  
This feature allows the ADC to monitor whether a signal leaves a predefined range _in hardware_, without needing software checks.

![[Pasted image 20251122110018.png|300]]

Example:

- If the internal temperature sensor detects an abnormally high temperature, the ADC can automatically raise an interrupt.
- If the battery voltage goes below a threshold, it can also trigger an alert.

You define the thresholds, and the ADC checks them continuously.
### <span style="color:rgb(161, 40, 226)">ADC and DMA</span>

The ADC can work with DMA, and we can enable DMA requests directly.  
When using DMA, the data is automatically placed into a buffer without CPU intervention. The function that starts ADC–DMA conversion asks for two things:

1. Which ADC to start.
2. The memory buffer where DMA should store the samples.
    
There are two DMA interrupts:
- **Half-complete interrupt**
- **Complete interrupt**
    
Why do we need the half-complete interrupt? Because DMA can operate in two modes:

- **Normal mode**:  
    DMA fills the buffer once and stops, waiting for the CPU to read it.
- **Circular mode**:  
    DMA keeps filling the buffer in a loop.  
    This is extremely useful for continuous sampling.

However, in circular mode, reading the buffer at the wrong time may cause overwritten data. If you wait until the buffer is fully filled, DMA may already be writing over the first part of the buffer while you’re trying to read it.

This is where the half-complete interrupt becomes essential:

- When the first half of the buffer is filled → **half-complete interrupt**  
    → you read the first half while DMA fills the second half.
- When the second half is filled → **complete interrupt**  
    → you read the second half while DMA starts overwriting the first half.
    
This alternating process ensures you never read data while it is being overwritten, preventing corruption.

So, when you need continuous, high-speed sampling:  **Use circular mode + both interrupts (half and full).**

### <span style="color:rgb(161, 40, 226)">Schematic of the ADC</span>

![[Pasted image 20251122110752.png|500]]
These diagrams show the internal structure of the ADC. You don’t need to memorize them, but it helps to understand the general idea.


![[Pasted image 20251122110909.png|300]]
- At the top you can see the **ADC interrupt line** going to the NVIC.  
    This interrupt can be triggered, for example, at the **end of a conversion** or by the **analog watchdog**.

![[Pasted image 20251122110945.png|300]]
- The ADC receives its **clock** through a **prescaler**.  
    The prescaler simply divides the microcontroller’s main clock to generate a suitable ADC clock frequency.

![[Pasted image 20251122111107.png|400]]
- Here you can also see all the possible **triggers** for the ADC.  
    It can be triggered by different timers or by the two **EXTI** (external interrupt) lines.
![[Pasted image 20251122111130.png|300]]
- At the bottom, you have the **ADC input channels**, which are the analogue inputs it can sample.
    
![[Pasted image 20251122111208.png|400]]
In the IOC (the configuration interface), under the _Analog → ADC_ tab, you see all the settings we choose:

- ADC clock prescaler
- Resolution
- Data alignment
- Sampling time, which is expressed in **ADC clock cycles**
    

The **sampling time** can be set as low as **3 cycles** and as high as about **480 cycles**.  
These cycles represent how long the ADC sample-and-hold capacitor spends sampling the input signal.

### <span style="color:rgb(161, 40, 226)">Functions and more :)</span>

We have several ADC functions, which follow a similar structure. Here’s a breakdown:

~~~c#
HAL_StatusTypeDef HAL_ADC_Start(ADC_HandleTypeDef* hadc) HAL_StatusTypeDef HAL_ADC_Start_IT(ADC_HandleTypeDef* hadc) /*(needed at the beginning of the code also just to setup the peripheral)*/
HAL_StatusTypeDef HAL_ADC_Start_DMA(ADC_HandleTypeDef* hadc, uint32_t* pData, uint32_t Length)
~~~
1. **Starting the ADC**
    - The ADC can be started in three modes: **Normal**, **Interrupt**, or **DMA**.
    - **DMA mode** requires a buffer to store the data.
    - When using **Interrupt mode**, you must always call the setup function at the start of your code. This initializes the peripheral correctly.
~~~c#
HAL_StatusTypeDef HAL_ADC_Stop(ADC_HandleTypeDef* hadc)
/*(simply aborts the conversion)*/
HAL_StatusTypeDef HAL_ADC_Stop_IT(ADC_HandleTypeDef* hadc) HAL_StatusTypeDef HAL_ADC_Stop_DMA(ADC_HandleTypeDef* hadc)
~~~
2. **Stopping the ADC**
    - You can stop the ADC at any point using the corresponding stop function.

~~~c#
HAL_StatusTypeDef HAL_ADC_PollForConversion(ADC_HandleTypeDef* hadc, uint32_t Timeout) 
uint32_t HAL_ADC_GetValue(ADC_HandleTypeDef* hadc)
 
__weak void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc) __weak void HAL_ADC_ConvHalfCpltCallback(ADC_HandleTypeDef* hadc)
~~~
3. **Checking End of Conversion**
    - Use `PollForConversion` to check if the conversion is finished.
    - The function returns `HAL_OK` when the conversion is complete.
    - Typically, you would use this in a polling loop in normal mode to wait for the result.
4. **Reading ADC Data**
    - Use `GetValue` to read the converted data.
    - Note: This returns an **unsigned int32**, so allocate appropriate storage.
5. **Interrupts**
    - There are two main callbacks for DMA mode:
        - **Conversion Complete Callback**
        - **Conversion Half Complete Callback**
    - These are mostly used with DMA transfers to handle data when it’s partially or fully available.

**Summary:**  
The functions are straightforward. You have setup/start functions, stop functions, conversion checkers, data readers, and interrupts. The overall structure is consistent across modes (Normal, Interrupt, DMA).

---
***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 5a: ADC single acquisition - polling</span> 

The goal of this project is to measure the voltage coming from a potentiometer once every second and send that value to a remote terminal using UART. In this case, the ADC operates in **polling mode**, meaning the CPU manually waits for the conversion to finish.

### <span style="color:rgb(161, 40, 226)">1. GPIO and ADC Configuration</span>
![[Pasted image 20251013152410.png|300]]
- The potentiometer is connected to **PA1**, which must be configured as **analog input** (no pull-up, no pull-down). *ADC1_IN1*

| ![[Pasted image 20251013153103.png\|300]] | ![[Pasted image 20251013155219.png\|300]] |
| ----------------------------------------- | ----------------------------------------- |
- In the ADC configuration:
    - Enable **Channel 1**, since PA1 corresponds to ADC1_IN1.
    - Use a **12-bit resolution**, giving a numerical range of **0–4095**.
    - The **prescaler** can remain at **/4**.
    - The **End of Conversion (EOC)** setting should be “EOC flag at end of single conversion,” because we are using only **one channel**.
    - **Number of conversions = 1.**
    - **Sampling time** is set to **480 ADC clock cycles**.
    - The conversion is triggered **by software**, which means the user manually starts the conversion in the code.

![[Pasted image 20251006130716.png|300]]

- The USART must be configured with a baud rate matching your serial monitor.  
    Example: **9600 baud**.
    
These settings ensure the ADC correctly acquires one sample from PA1 and the UART can transmit the processed result.

### <span style="color:rgb(161, 40, 226)">2. ADC Operation in Polling Mode</span>

The ADC operation follows a strict sequence:
1. **Start the conversion** using `HAL_ADC_Start()`.
2. **Wait for the End-of-Conversion flag** using  
    `HAL_ADC_PollForConversion(&hadc1, timeout)`.
    - This function blocks the CPU until the conversion is complete or the timeout expires.
3. If the function returns `HAL_OK`, the conversion is ready and we can read the value.
4. **Read the ADC value** using `HAL_ADC_GetValue()`, which returns a **uint32_t**.
5. Convert the raw ADC value to a real voltage:
    $$V = \frac{\text{ADC\_value} \times 3.3}{4096}​$$
    Because the ADC uses 12 bits, the maximum value is 4095 ≈ 4096 for scaling.
    
1. Format the voltage into a string with 3 decimal places.
2. Transmit it via UART using `HAL_UART_Transmit()`.
    

If `HAL_ADC_PollForConversion()` does **not** return `HAL_OK`, it means the conversion did not finish before the timeout, so nothing is sent.

~~~C#
while (1){
/* USER CODE END WHILE */
	HAL_ADC_Start(&hadc1);
	if(HAL_ADC_PollForConversion(&hadc1, 10) == HAL_OK){
		int conversion = HAL_ADC_GetValue(&hadc1);
		float voltage = conversion*3.3/4096.0;
		char string[64];
		int length = snprintf(string, sizeof(string), "Voltages: %.3f", voltage);
		HAL_UART_Transmit(&huart2, string, length, 100);
		}
	
	else{
	//error
	}
	
	HAL_Delay(1000);// Acquire a new value every 1 second
	/* USER CODE BEGIN 3 */
}
~~~

This loop performs one complete ADC acquisition and UART transmission every second.


![[Pasted image 20251017190302.png|300]]
Now, the approach to do it out of the `while()` and with a timer is by setting a timer interrupt and using its PeriodElapsedCallback, remember set it with the frequency we aim for. And don't forget initialize the timer as an interrupt :)

~~~~c#
HAL_TIM_Base_Start_IT(&htim2);


void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim==&htim2){
		HAL_ADC_Start(&hadc1);
		if(HAL_ADC_PollForConversion(&hadc1, 10)==HAL_OK){
			int conversion = HAL_ADC_GetValue(&hadc1);
			float voltage = conversion*3.3/4096.0;
			char string[100];
			int lenght = snprintf(string, sizeof(string), "Voltage Polling: %.3f \r\n", voltage);
			HAL_UART_Transmit(&huart2, string, lenght, 100);
		}
	}
}
~~~~
# <span style="color:rgb(223, 109, 109)">Project 5b: ADC single acquisition - Interrupt</span> 
In this project, we perform the same single conversion, but instead of polling we use **interrupt mode**. This means that the CPU does _not_ wait for the conversion to finish.  Instead, the ADC triggers an interrupt automatically when the conversion is complete, and a callback function is executed.

### <span style="color:rgb(161, 40, 226)">1. GPIO and ADC Interrupt Configuration</span>

![[Pasted image 20251017195151.png|500]]
- Configure the potentiometer pin (PA1) as **ADC1_IN1**, the same as in Project 5a.
![[Pasted image 20251017195234.png|500]]

- Enable the **ADC interrupt** in the NVIC settings. This allows the processor to jump to the interrupt service routine once the ADC raises the interrupt.
![[Pasted image 20251006130716.png|500]]

- Configure the UART baud rate for communication (e.g., 9600 baud).

### <span style="color:rgb(161, 40, 226)">2. ADC Operation in Interrupt Mode</span>

The process differs from polling:

1. In the main loop, we start the conversion using  
    `HAL_ADC_Start_IT()`.
2. The CPU then continues executing the program (in our case, it simply waits 1 second).
3. Once the ADC finishes the conversion, it automatically triggers the interrupt.
4. The HAL library calls the function:`HAL_ADC_ConvCpltCallback()`
5. Inside this callback, we read the ADC value, convert it to voltage, format the string, and transmit it via UART.

Inside the **while loop**, there is **no need** to check the EOC flag, because the interrupt handles everything.

#### Main Loop
```c#
while (1){
	/* USER CODE END WHILE */
	HAL_ADC_Start_IT(&hadc1);
	HAL_Delay(1000);
	/* USER CODE BEGIN 3 */
	}
/* USER CODE END 3 */
}
```

#### Interrupt Callback
```c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[100];
	int length = snprintf(string, sizeof(string), "VoltageIT: %.3f V\n \r", voltage);
	HAL_UART_Transmit(&huart2, string, length, 100);
	}
```


![[Pasted image 20251017223443.png|400]]

Now, if I would like to do the implementation with the timer interrupt, instead of `HAL_Delay()` within the `while()

~~~c#
//Don't forget here we use the ADC as IT
//Don't forget also to initializate the Timer in the main
HAL_TIM_Base_Start_IT(&htim2);


void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim==&htim2){
		HAL_ADC_Start_IT(&hadc1);
	}
}

void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef *hadc){
	int value = HAL_ADC_GetValue(&hadc1);
	float voltage = value*3.3/4096.0;
	char string[100];
	int length = snprintf(string, sizeof(string), "Voltage IT: %.3f V \r \n", voltage);
	HAL_UART_Transmit(&huart2, string, length, 100);
}
~~~


### <span style="color:rgb(161, 40, 226)">Key Difference Between Polling and Interrupt Mode</span>

- **Polling Mode:**  
    The CPU manually waits for the conversion to finish by checking the EOC flag.  
    This blocks the processor.
    
- **Interrupt Mode:**  
    The CPU does _not_ wait.  
    The ADC notifies the CPU automatically when the conversion is done, triggering the callback. This is more efficient, especially when timing is critical.

![[Pasted image 20251017224021.png|400]]
Additionally, there is **no conflict** between ADC interrupts and UART interrupts because they operate independently with separate interrupt vectors.

***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Homework 5a: Try to send data from the PC via UART a string of variable length that is displayed on the LCD.</span>

The objective of this exercise is to send a string from the PC (via UART) and display that string on the LCD. The string can be of variable length, and the reception can be implemented in two different ways:
1. **Character-by-character using DMA**,
2. **Using “Receive-To-Idle” DMA**, which captures an entire message at once.
### <span style="color:rgb(161, 40, 226)">1. Initial Setup: LCD Pins and UART</span>
First, configure the microcontroller pins connected to the LCD.  Next, configure the UART peripheral. Ensure:

| LCD pins                             | UART config                          |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251011165606.png]] | ![[Pasted image 20251017230052.png]] |

- Correct baud rate (must match your PC’s terminal).
![[Pasted image 20251017230120.png|400]]
- DMA is enabled for reception.
![[Pasted image 20251017230138.png|400]]
- The UART receive interrupt is enabled.

### <span style="color:rgb(161, 40, 226)">2. DMA Reception Method 1: Receiving One Character at a Time</span>

In this method, DMA transfers **one byte at a time** into the variable `singlechar`.  Each time one byte arrives, an interrupt is generated, and the callback assembles the message manually.

**Private Variables**
~~~ c#
UART_HandleTypeDef huart2;
DMA_HandleTypeDef hdma_usart2_rx; //this are already defined from the ioc

#define UART_RX_BUFFER_SIZE 17
char singlechar;
char string[UART_RX_BUFFER_SIZE];
int i = 0;
~~~

**Initialization**
```c#
int main(void){
	lcd_initialize();
	lcd_backlight_ON();
/* USER CODE END 2 */
	HAL_UART_Receive_DMA(&huart2, &singlechar, 1); //To receive just 1 element (1Byte) and store it in singlechar
}
```

**How the Callback Works**
~~~c#
void HAL_UART_RxCpltCallback(UART_HandleTypeDef* huart){
	if(huart==&huart2){
		string[i]= singlechar;
		if(singlechar == '\n'){ // End of message
			lcd_println(string, 0);// Display on line 0 of LCD
			i=0; // Reset index
			memset(&string, 0, sizeof(string));//this clears the array buffer after displaying in the LCD and set it to 0
		}
		else{
			i++;// Add next character
		}
		  // Re-enable DMA to receive the next char
		HAL_UART_Receive_DMA(&huart2, &singlechar, 1);
	}
}
~~~
**Explanation**

In this approach:
- The CPU receives **one interrupt per received character**.
- The message is constructed **manually character-by-character**.
- The LCD displays the string when the newline character `\n` is detected.

#### <span style="color:rgb(2, 141, 192)">Alternative Method</span>
This method is much more efficient. Instead of receiving each character individually, the DMA fills a buffer **until one of these events occurs**:
1. The UART line becomes **idle** (no data for > 1 character time, that is, UARTRX line stays **inactive**).
2. The **buffer becomes full**.
3. A **transfer complete** event occurs.
    
This generates only **one interrupt per entire message**.

**Buffers and Initialization**
``` c#
#define BUFFER_SIZE 16
uint8_t buffer[BUFFER_SIZE+1];      // DMA receive buffer
uint8_t lcd_buffer[BUFFER_SIZE+1];  // Display buffer

int main(void)
{
    lcd_initialize();
    lcd_backlight_ON();
    
    // Start DMA to receive UP TO 16 CHARACTERS
    // Stops when buffer full OR UART becomes idle
    HAL_UARTEx_ReceiveToIdle_DMA(&huart2, buffer, BUFFER_SIZE);
}

```

**Callback**
```c#
void HAL_UARTEx_RxEventCallback(UART_HandleTypeDef* huart, uint16_t size){
    if(huart==&huart2){
        
        //We check idle mode or full buffer
        if((huart->RxEventType == HAL_UART_RXEVENT_IDLE) ||
	        huart->RxEventType == HAL_UART_RXEVENT_TC){
	        
	        memset(&lcd_buffer, 0, sizeof(lcd_buffer));  // Clear display buffer
	        memcpy(&lcd_buffer, &buffer, size);          // Copy received data
	        
	        lcd_println((char*) lcd_buffer, 0);          // Display "Hello\n"
	        
	        // Restart DMA for next message
	        HAL_UARTEx_ReceiveToIdle_DMA(&huart2, buffer, BUFFER_SIZE);
	        }
    }
}
```
**What “UART Idle” Means**
UART Idle occurs when the RX line stays high (logic 1) **longer than one character transmission time**.

Example at **115200 baud**:
- One character ≈ **87 µs**
- Idle condition: line high for **>87 µs**

This naturally happens:
- When you stop typing,
- When you press Enter, 
- Between bursts of characters,
- At the end of a message.

### <span style="color:rgb(161, 40, 226)">Comparison Between the Two Methods</span>

#### <span style="color:rgb(2, 141, 192)">Method 1 (RxCplt, 1 byte at a time)</span>
- Generates **one interrupt per character**
- CPU workload is higher
- Message is built manually
- Good for teaching, not efficient
    
#### <span style="color:rgb(2, 141, 192)">Method 2 (Receive-To-Idle DMA)</span>
- Generates **one interrupt per message**
- Much lower CPU overhead
- Buffer already contains complete string
- Ideal for receiving variable-length messages

# <span style="color:rgb(223, 109, 109)">Homework 5b: ADC triggered by TIM </span>
In this exercise, the ADC conversion is not started manually or by an ADC interrupt. Instead, a timer generates a hardware trigger that starts each ADC conversion automatically.

![[Pasted image 20251019001803.png|400]]
### <span style="color:rgb(161, 40, 226)">1. Timer Configuration</span>

![[Pasted image 20251019002008.png|500]]
Configure **TIM2** (or the selected timer) so that:
- It produces an **Update Event** (UEV) when the counter reaches the ARR value.
- This update event becomes the **Trigger Output (TRGO)**.
    
To do this:
- Change the Trigger Event Selection from **Reset** to **Update Event**.
This allows the timer to serve as a trigger source for another peripheral.

### <span style="color:rgb(161, 40, 226)">2. ADC Trigger Configuration</span>

![[Pasted image 20251019002317.png|500]]

In the ADC settings:
- Keep the sampling time at **480 cycles**.
- Set the **External Trigger Source** to:  
    **TIM2 Trigger Out Event**
This means the ADC will begin a conversion every time the timer overflows.


**Main code init**
~~~ c#
HAL_TIM_Base_Start(&htim2); //Timer not used in interrupt mode, we simply use its output by our timer
HAL_ADC_Start_IT(&hadc1);//initialized it just in the main
~~~

 **ADC Conversion Complete Callback**: Every time the TIM triggers a conversion and the conversion finishes, this callback runs:
~~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[64];
	int length = snprintf(string, sizeof(string), "VoltageTRG: %.3f V \r \n", voltage);
	HAL_UART_Transmit(&huart2, string, length, 10);
}

~~~~

![[Pasted image 20251019002735.png]]
The ADC works entirely in the background; the timer triggers it, and the callback sends the result via UART.

Do not forget matching both baud rate. Since, we're not using the DMA, we still have to define the interruption routine for the ADC

>[!missing] We could implement it with DMA
# <span style="color:rgb(223, 109, 109)">Homework 5c: Instead of send it through the UART, display it in the LCD.</span> 

This exercise is identical to Homework 5b; however, instead of sending the voltage via UART, the value is printed on the LCD.

![[Pasted image 20251019004200.png|400]]
### <span style="color:rgb(161, 40, 226)">1. Timer Configuration</span>

![[Pasted image 20251019002008.png|500]]
Configure **TIM2** (or the selected timer) so that:
- It produces an **Update Event** (UEV) when the counter reaches the ARR value.
- This update event becomes the **Trigger Output (TRGO)**.
    
To do this:
- Change the Trigger Event Selection from **Reset** to **Update Event**.
This allows the timer to serve as a trigger source for another peripheral.

### <span style="color:rgb(161, 40, 226)">2. ADC Trigger Configuration</span>

![[Pasted image 20251019002317.png|500]]

In the ADC settings:
- Keep the sampling time at **480 cycles**.
- Set the **External Trigger Source** to:  
    **TIM2 Trigger Out Event**
This means the ADC will begin a conversion every time the timer overflows.


**Initialization**

It is important to initialize the LCD **before** the ADC, because LCD initialization takes a noticeable amount of time.

~~~ c#
/* USER CODE BEGIN 2 */
lcd_initialize();// it needs to be initialize before the ADC, cos it takes time to initialize
lcd_backlight_ON();
lcd_clear();
char string[16];
snprintf(string, sizeof(string), "Voltage:");
/* USER CODE END 2 */
HAL_TIM_Base_Start(&htim2); //Timer not used in interrupt mode, we simply use its output by our timer
HAL_ADC_Start_IT(&hadc1);//initialized it just in the main
~~~

**ADC Callback for LCD Output**

~~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[64];
	snprintf(string, sizeof(string), "Voltage: %.3f V \r \n", voltage);
	lcd_println(string, 0);
	lcd_drawBar((conversion/4096.0)*80.0);	 // make sure the input of drawBar is an int, since it is defined like that
}
~~~~

The ADC reading is converted to voltage, printed on the LCD, and represented graphically with a bar.

>[!check] 
>![[Pasted image 20251019002735.png]]
>**Don't forget to match both baud rate and also importing the corresponding LCD libraries**




