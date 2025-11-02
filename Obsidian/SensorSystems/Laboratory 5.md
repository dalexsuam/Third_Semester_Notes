 
13/10/2025
***

Then I think we can start with the theory class. Which, as I said today, is related to the ADC, or the analog-to-digital conversion. So, the analog-to-digital conversion, in particular the ADC on our microcontroller, is a 12-bit ADC. This means that it can have a resolution of 12 bits, and it means that it has a resolution of 4096 levels, digital levels, to get an analog signal. However, of course, like on all microcontrollers, on all electronics, you will never find some registers with values different from powers of two. So we will have a register equal to 16-bit. So when we read out the data, we will not have actually 16 bits that are full, four of them will be zero. However, we need 16-bit to read 12 bits of the ADC. They are stored in a register, and we will see that we have some functions to actually get the data from those registers. They're already defined in the HAL, as usual. In particular, on our microcontroller we only have one sample and hold circuit and one ADC. Why? Simply because our microcontroller is quite simple. However, on some bigger or more complex or more expensive microcontrollers we can have multiple ADCs. This means that we can actually read out different data at the same time. In our case, we can just read one sensor at a time. Of course, like all ADCs, we have an input range. In our case, our input range is set by two pins on our microcontroller. In our case, in our Nucleoboard, we have the whole of the input range is exploited, so we have a value between 0 and 3.3. This is important because when we will have to convert from the digital value back to the analog value, you have to remember that the bits are mapped between 0 and 3.3. A very short, very little recap on the sample and hold circuit I'm going to show you. I think all of you are familiar with it. The sample and hold circuit is nothing too complicated, it is just a switch and a capacitor and a resistor. So we have an RC circuit with a switch. In the sample phase the switch is closed, this means that the signal can go through, can reach the capacitor and charge the capacitor. The sample phase has to be long enough to actually charge the capacitor to the level of the input. Why do I say this? Because the sample phase will have to be set, in general, in your projects, in everything, also in the microcontroller, to be long enough to have the Rc charge, let's say it has to be long enough to be equal to more or less four or five times the Rc charge. Of course we will not have the exact number, we don't really need it right now, but however, remember that you have to be longer than this charge time. Otherwise we don't give enough time to the capacitor to charge, or discharge of course. In this case the ADC does not do anything. On the other hand, on the old phase we open the switch, so we only have the second part of the circuit, the capacitor is charged, and what happens is that the ADC reads out the voltage stored on the capacitor. Of course, this means that our signal will not be like a smooth signal, it will be kind of a staircase, because of course it is a digital signal, it's not an analog signal anymore. Of course, the hold phase also depends on the ADC we are using, because depending on the ADC architecture, the hold phase can be longer or shorter. Because if we have a lot of bits, for example, to be approximated, this means that the hold phase has to be long enough to allow the ADC to read out everything. In particular, in our board we have a successive approximation ADC. I think, again, all of you are familiar with it. How does it work? It tries to guess. So it starts off by saying, is my value above or below the medium value of my voltage? If it is above, it means that it's going to have a 1 in the first bit. Then you move on to the second bit, and it's going to check again if the half value between, let's say, the half and the top half is above or below. And it's going to check again if it is above its one, if it is below its zero. And it goes smaller and smaller until we reach the last bit. If we have 12 bits, this means that this is done 12 times. We need a lot of time to actually have the check of the value. This means that we have a lot of clock cycles to be done before we have the final value in our IEC. Here there's just a GIF just to show you if... It is a bit complicated to explain but it is very simple to see. So I think you can actually see here how it works. So it keeps guessing until we reach all of the bits. In this case it's just four bits of course. Some features of our ADC. We have 16 external input channels. This means that there are 16 channels that can be taken from outside of the microcontroller, so they go to pins. This means that we can connect some sensors. However, we also have two internal channels. These internal channels do not have a pin outside of the microcontroller, they are inside. Please remember that the ADC is inside the microcontroller, it's not a component on the board, neither on the white one or on the green one, it is inside of the chip. Remember this, okay, for the ExaM or the future in general, it is inside. The two internal channels can have can check the reference voltage, which is a voltage that is internal to the microcontroller, so we can check it to see if there are some errors. On the other hand, we can also check a temperature sensor. And why do we have a temperature sensor inside of the chip? Because we want to see maybe if the microcontroller is overheating. Or maybe if it is overheating, we can stop it because something is very wrong. If the microcontroller is too hot, it's going to break down. But also, we have a battery charge monitor. a battery, there's no battery on our board. Yes, there is inside of the microcontroller. For example, when you have an analog device, one of the old devices that keeps up with the time, but also, I'd say your computer, but your computer has a big battery and we know it. How does it keep up with the time, with the date and the hour? There's a small battery that keeps alimenting the clock. So there's something that keeps alimenting the real-time clock, and the real-time clock can then actually keep up with time even if the system is turned off. We can check this battery level, for example. It's not important to us, but it could be important to someone who is doing some applications. How do we start the conversion? How do we tell the ADC to convert some data? We have the software, so we have a function that says convert some data. Via timer, we can give the timer directly as an input to the ADC. We don't have to write the code. We can use it directly as a trigger of the ADC. I say trigger because it is not an interrupt. We're not using the timer in interrupt mode. We are using it as a trigger. Finally, we can also have an external trigger. So, for example, we can connect a button to one of these two XT lines. Whenever we press the button, the ADC converts something. Again, it is not an interrupt because there is no software. The connection is via hardware. We don't have to write the code. Everything is connected internally. This is great for optimization. We are not having interrupts. The CPU can do whatever it wants. The ADC works on its own. And finally we have different conversion modes. We have the polling mode, which is we keep checking the end of conversion EOC flag. You keep checking. When the EOC says I'm done converting, we read out the data. Is this optimized? Not at all. It is very bad. But the first project will be like this because we have to learn how the ADC works. We can have an interrupt. So for example, the ADC raises an interrupt whenever it's done converting. So we'll have the complete callback, the conversion complete callback. And finally we have the DMA. The DMA does not wait for you to read out the data because in the interrupt mode, inside of the interrupt, we'll have to read the data. The DMA just takes the data and puts them inside of a buffer that we tell the ADC. We say, "Okay, please convert and fill in this buffer." And we will have an interrupt that will tell us when the buffer is full. When the buffer is full, we read it out. So this means that we call the interrupt maybe once every, I don't know, 1000 values converted. It is very optimized. Some new other features that we will have to set. We have the continuous or the single acquisition. The continuous acquisition, we will not really use it because it is needed when you need a very fast acquisition. At every time one single sample is converted, the EOC flag is automatic at the start of conversion, so not the EOC but the SOC flag is raised and the next conversion is done. It is like a chain, it does it on its own and is very fast. On the other hand, the single acquisition, it means that the starter conversion flag is actually provided, but we are one of the triggers that we talked about. Software, timer, or an external trigger. We will not need it because we'll never go at such high speeds that we need the conversion to be as fast as possible in our case. And finally, this one is something that we will use. We can scan a single channel or we can have the scanning mode. Why? Because maybe we want to read out multiple sensors. What if we want to read out both the internal temperature sensor and an external sensor? We have to set multiple channels and we tell the ADC scan through them. In particular we can have up to 16 regular channels and we can have up to 4 injected channels. The injected channels are high priority channels. For example, I want, there's a request coming in to check that channel from a battery, which is a very important battery for my system. I stop whatever I'm doing with ADC, I convert that one, and then I go back to doing what I was doing. Just like the priorities of the interrupts. Why? Because some sensors are more high priority than others, in general, in the world. Finally, something that can be done is that all of the channels are converted in sequence. Okay, so I have kind of a continuous mode, but actually with multiple channels. So the continuous mode, if one single channel goes on, in this case I have maybe the temperature, the battery, and the potentiometer. On the other hand, I can also have some specific ways, for example the discontinuous mode, which if I have, I don't know, 10 sensors, I can tell it every five channels raise me an end of conversion. We will not use it, but it means that we can like break down the cycle through the various sensors. You will see that all of these can be set in the IOC very easily. You have like the usual tab where you just click it and you have all of the options. We can also set from the IOC if we want the data in right or left alignment because of course this changes completely the data we are reading. So please check when you're reading out the data that they're reading correctly. Then we have the sampling time. As I said, we have to set the sampling time. Why do we set it? Because different sensors require different sampling times. Okay, we have the fixed capacitor, a sensor which provides a higher resistance, means that we have a longer RC time, a tau, which means that we need more time to charge the capacitor. In particular, in general, it is said that the maximum clock frequency of the ADC is 36 MHz. However, it is not an integer divider of 84 MHz because we have the ADC with maximum 36, but we have to divide the clock from the microcontroller, which is 84. So actually the real maximum clock frequency in our microcontroller is 21 MHz. Moreover, we have to set not just the sampling time, but as I said, the resolution, so how many bits we use, also gives some issues with the time required to read out the data. So this means that the timing will change based on how many bits we will read out. In particular, as you can see there's the formula here, and let's say that the maximum sampling frequency at 12-bit resolution is equal to 1.4 MHz if we read out only 3 bits instead of having all of 12 bits, which is the smallest possible value. So the fastest we can go is this one. We cannot go faster. If you want a higher resolution, automatically this frequency drops because we have to read out more data. It takes more clock cycles. Mind you that you have, it is expressed in clock cycles in the IOC. It is not expressed in a time, mainly seconds, but how many clock cycles do you want? We will always try to set it as the highest value. However, if in the exam it is asked of you to change these values, please remember that they are all interconnected. You cannot change the sampling time without considering the clock cycle, without considering all of it. So remember this formula, remember that they're all interconnected. One thing, it's more of a curiosity because we will not use it, the ADC features an analog watchdog. What is an analog watchdog? It allows to check if a value goes outside of a certain range. Again, example, the temperature sensor. If the temperature sensor overheats, the ADC automatically raises an interrupt and tells us, look, the temperature is too high. And it is done in an analog way, so we don't have to check it via software. We can set the thresholds, and we want the data to stay in certain thresholds. Same with the battery. The battery is too low, please check. Finally, as I was saying, the ADC can work with DMA, so we can enable some DMA requests. So this means that the ADC takes data and puts them directly in a buffer. We will see that the function for enabling the ADC in DMA mode does not only ask for which ADC do we want to start, but also for where to put the data. Because of course we're not reading them out directly, manually let's say, it's going to go in an automatic way. We can generate some interrupts, in particular two. One of them when the buffer is full, and one of them when the buffer is half full. Why the buffer is half full looks kind of useless, it is fundamental. Because the DNA can be set in two modes, which we saw also before. In normal mode, which means it fills in the buffer, and then it waits for you to read it out. Or in circular mode. Circular mode means that it fills in the buffer, and then it starts filling it again, kind of like a circle. This one is great because it means that even if we are doing something the data keeps coming in. But what happens if when the buffer is full we get the interrupt, we try to read and while we are reading the data are overwritten because the data starts being written again. This is where the half complete callback comes in useful because we can read out the first half. While we read the first half the data keeps being filled in we get the complete, the full complete interrupt within the second half of the buffer, but the first half of the buffer is being filled in. So we will, let's say, play with two of the interrupts, the half complete and the full complete for the circular mode. I don't know if this was very clear, I don't think so, but I'm just going to do this because I think it is better. We get an interrupt here, we read out this data, and meanwhile the microcontroller fills it in. Then we get an interrupt here, we read out this data, but the microcontroller fills this one in. If I just get this one, and I say, okay, read all of them, the microcontroller is filling it in. So I get some broken data. Because maybe while I'm reading, this one changes, and I get some wrong bits, because they were overwritten while I was reading, so the data is lost. So remember, when you have to read a lot of data, circular mode, and you'll have to play with two interrupts. Keep this in mind for the future. This is just a schematic of the ADC, you can look at it on your own. However, you can see that above we have the ADC interrupt sent to the AR and the IC. We have here the flex for the end of conversion, for example, or the analog watchdog, which is over here. We have the clock of the ADC, which comes from a pre-scaler. The pre-scaler scales the clock of the microcontroller. Here we have every single trigger that we can have. We have all of the timers, but we also have the two XT lines. And finally here we have the inputs of the ADC. Here is a view of the IOC, you find it in the analog tab ADC, and you can see that we have everything that we set. So we have the clock piece scalar, we have the resolution, the data alignment, and all of the settings that we have. Here you can see that the sampling time is set in cycles, which are clock cycles. 3 clock cycles is the smallest one, we can set it up to I think 480. And here is a bunch of functions. There are a lot, but you will see that they're all kind of the same. So we have, first of all, we have to start the ADC. And we can start it in three ways. Normal mode, let's say, interrupt mode, or DMA mode. And as you can see, the DMA mode requires also the buffer to be filled in. Mind you that when you start the ADC in interrupt mode, you always have to call the code, this function, at the start of the code because it sets up the peripheral as well. So always call this one. And then the same for stopping the ADC because maybe we want to stop the ADC at a certain point. Here are the other functions. So how do we check the end of conversion flag? There's the pollforconversion function. This function checks out if the end of conversion flag is raised or not, and it gives us back "Hallok" if the conversion is over. So we will check the output. We see is it "Hallok" in the while, maybe, in polling mode. Is it "Hallok"? Yes. Okay, good. I read out the data. How do I read it? With getValue. careful that the get value gives us back a new int32, an unsigned int32 value, so we have to store some space like that. And finally we have the two interrupts, which I talked to you about. So we have the conversion complete callback and the conversion half complete callback, which will be mostly used for the DMA functions. These are all of them, they're not complicated, you will see that the structure is always the same. So we have the interrupts, we have the normal interrupt and DMA nodes, and we can just read out the data. So, today we will try to do two projects, hopefully the first one for sure, the second one I will maybe give you just the solution, just so you can see it, because it's the same, there's just one difference. and you have to read out the data from the potentiometer. So you have to look on the green board schematic, so you have to find the potentiometer and see where it goes to the microcontroller and enable that pin. You have to enable that pin as an ADC input and then you have to go on the tab of the ADC and set up everything. So the objective of this first project is to acquire the voltage of the potentiometer every one second and send the value to a remote terminal using the ADC in polling mode. Polling mode means pull for conversion and get value in the while. You can use an ALT delay in this case, when in the homework, don't. Just a few things I want to show you because I will forget. As I said, set the sampling time to the maximum, which is 480 clock cycles. And here, For every project where you will have to send some data with the UART with a float value, please follow this little tutorial, it's written in the slides. But it will also be written as a warning and the warning will be actually, it's a warning but it's in red, and if you hover with the mouse over it, it will tell you what to do. Please learn to check the problems and warnings before saying it doesn't work because STM32 tells you everything. Here, in the problems tab, usually it tells you what warning and how to solve it. A lot of time it also tells you the solution. For example, I forget to include the library, it will tell you "please include this library". It also tells you the name of the library. I think you can start and we will be here for questions. You can try and fix this first project on your own.

***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 5a: ADC single acquisition - polling</span> 

Objective of this project is to acquire the voltage of the potentiometer every 1 second and send this value to a remote terminal. The ADC will be used in polling mode

1. Set the GPIO connected to the potentiometer as an analog input and configure the ADC to acquire one value from that channel, triggered by software. Set the sampling time to 480 clock cycles.

![[Pasted image 20251013152410.png]]
![[Pasted image 20251013155219.png]]
Analog input of PA1 for potentiometer and USART TX and RX

![[Pasted image 20251006130716.png]]
DO NOT FORGET TO MUCH THE BAUD RATE OF THE USART with your serial monitor, in this case, let's put simply 9600
![[Pasted image 20251013153103.png]]
Here we just enable the channel 1 of the ADC, because we would like to read out that pin. We might leave the prescaler divided by 4, the resolution to 12 bits and the End of Conversion selection to EOC flag at the end of single channel conversion. Why? Because we have just 1 single channel. The number of conversion is set to 1. We have that the trigger conversion is launched by software 480 clock cycles sampling time. In Rank, we have only 1 channel, and we can modify for each channel the sampling time, and we set it in clock cycles.

2. Generate the c code.

The adc work in a way that we start the conversion, it converts and it raises a flag, the end of conversion flag, we check the flag and once it is done, we read the data. First of all, we start the adc and then we have a `if(HAL_ADC_PollForConversion(&hadc1, 10) == HAL_OK)`
and then we make the reading. We get an integer called `conversion` which will get a value between 0-4065 (from the 12 bits resolution). Then, since the range of the ADC is 0-3.3V, so we make a conversion by means of the variable `voltage` and then we simply create the string and we limit the number of decimals to 3 `%.3f` and transmit the voltage value to the serial terminal. 

If there is an error, it doesn't send anything
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
	
	HAL_Delay(1000);
	/* USER CODE BEGIN 3 */
}
~~~


![[Pasted image 20251017190302.png]]
3. Modify the code to acquire a value every 1 second
4. Convert the ADC value into a voltage.
5. Send the value to the remote terminal.
6. Debug the project.

# <span style="color:rgb(223, 109, 109)">Project 5b: ADC single acquisition - Interrupt</span> 

1. Set GPIO of the potentiometer as ADC1_IN
![[Pasted image 20251017195151.png]]

2. We enable its interrupt in the NVIC settings
![[Pasted image 20251017195234.png]]

3. For the UART communication we set the desired baud rate.
![[Pasted image 20251006130716.png]]

but now in the code, I have an interruption routine. First we start the conversion every second and then

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


```c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[100];
	int length = snprintf(string, sizeof(string), "VoltageIT: %.3f V\n \r", voltage);
	HAL_UART_Transmit(&huart2, string, length, 100);
	}
```

The main difference here is that we don't have here to check in the while the flag to see if the conversion is completed. With the interrupt the conversion executes automatically when it is done, previously we checked the flag.

![[Pasted image 20251017223443.png]]

There is no conflict between the interrupt of both. 
![[Pasted image 20251017224021.png]]

***
***
***
***
***

# <span style="color:rgb(223, 109, 109)">Homework 5a: Try to send data from the PC via UART a string of variable length that is displayed on the LCD.</span>

First of all, we need to set up the pins for the LCD

![[Pasted image 20251011165606.png]]

And also setting up the pins for the LCD and UART. 


Then configure our UART as desired, if DMA or non circular. 

![[Pasted image 20251017230052.png]]
I set baud rate

![[Pasted image 20251017230120.png]]
Set DMA settings and receiver and

![[Pasted image 20251017230138.png]]

Enable its interrupt.

Private variables 

~~~ c#
UART_HandleTypeDef huart2;
DMA_HandleTypeDef hdma_usart2_rx; //this are already defined from the ioc


#define UART_RX_BUFFER_SIZE 17
char singlechar;
char string[UART_RX_BUFFER_SIZE];
int i = 0;
~~~

	
```c#

int main(void){
	lcd_initialize();
	lcd_backlight_ON();

/* USER CODE END 2 */
	HAL_UART_Receive_DMA(&huart2, &singlechar, 1); //To receive just 1 element (1Byte) and store it in singlechar
}
```

And then

~~~c#
	void HAL_UART_RxCpltCallback(UART_HandleTypeDef* huart){
		if(huart==&huart2){
			string[i]= singlechar;
			if(singlechar == '\n'){
				lcd_println(string, 0);
				i=0;
				memset(&string, 0, sizeof(string));//this clears the array buffer after displaying in the LCD and set it to 0
			}
			else{
				i++;
			}
			HAL_UART_Receive_DMA(&huart2, &singlechar, 1);
		}
	}

~~~

However, if instead we use 
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

what does this function? It triggers an interrupt when few things happen: When the state of the UART goes to IDLE, that means, I get some data and after a while I stop getting data, it gets silent, or when the buffer is filled, or half of the buffer is filled. 

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
**UART Idle** = When the TX line stays at logic high (1) for longer than the time needed to transmit one complete character.

**At 115200 baud:**

- 1 character time = ~87μs 
- **Idle condition** = Line stays high for >87μs
    
### **What Creates Idle:**

- You stop typing in Serial Monitor
- You press Enter (gap after sending line endings)
- Between words when typing slowly
- End of message transmission

## **Side-by-Side Comparison:**

### **When You Type "Hello" + Enter:**

**CODE 1 Behavior:**

text
Timeline: H → e → l → l → o → \r → \n
Interrupts: █   █   █   █   █   █   █   (7 interrupts)
CPU Work:   7 callback executions
LCD Update:                          DISPLAY!
Process:    Builds string character by character

**CODE 2 Behavior:**

text

Timeline: H → e → l → l → o → \r → \n → [IDLE]
Interrupts:                                 █   (1 interrupt)
CPU Work:   1 callback execution  
LCD Update:                                 DISPLAY!
Process:    Receives everything at onc


# <span style="color:rgb(223, 109, 109)">Homework 5b: ADC triggered by TIM </span>

(instead of having an interrupt that causes the ADC conversion, the ADC itself must have a setting that uses this timer to trigger the conversion and then we use the complete conversion callback and send it to the UART)

![[Pasted image 20251019001803.png]]
 
 
![[Pasted image 20251019002008.png]]

We change the trigger event selection from reset, in which simply when the ARR is achieved, it simply resets to update event in order to generate a signal to use it as a trigger to other peripherals.

![[Pasted image 20251019002317.png]]

Then in ADC parameters, apart from the 480 cycles of sampling time we set as source of the conversion trigger, we do it through hardware directly from the out event of our timer. The Timer 2 trigger out event. 

![[Pasted image 20251019002735.png]]

DONT FORGET SETTING BAUD RATE 

~~~ c#
HAL_TIM_Base_Start(&htim2); //Timer not used in interrupt mode, we simply use its output by our timer
HAL_ADC_Start_IT(&hadc1);//initialized it just in the main

~~~
Since we're not using DMA, we still have to define the interruption routine for the ADC. 
~~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[64];
	int length = snprintf(string, sizeof(string), "VoltageTRG: %.3f V \r \n", voltage);
	HAL_UART_Transmit(&huart2, string, length, 10);
}

~~~~


# <span style="color:rgb(223, 109, 109)">Homework 5c: Instead of send it through the UART, display it in the LCD.</span> 


![[Pasted image 20251019004200.png]]
 
 
![[Pasted image 20251019002008.png]]

We change the trigger event selection from reset, in which simply when the ARR is achieved, it simply resets to update event in order to generate a signal to use it as a trigger to other peripherals.

![[Pasted image 20251019002317.png]]

Then in ADC parameters, apart from the 480 cycles of sampling time we set as source of the conversion trigger, we do it through hardware directly from the out event of our timer. The Timer 2 trigger out event. 

![[Pasted image 20251019002735.png]]

DONT FORGET SETTING BAUD RATE, AND WHEN USING LCD IMPORT THE LIBRARIES

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
Since we're not using DMA, we still have to define the interruption routine for the ADC. 

~~~~c#
void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef* hadc){
	int conversion = HAL_ADC_GetValue(&hadc1);
	float voltage = conversion*3.3/4096.0;
	char string[64];
	snprintf(string, sizeof(string), "Voltage: %.3f V \r \n", voltage);
	lcd_println(string, 0);
	lcd_drawBar((conversion/4096.0)*80.0);	
}
~~~~

