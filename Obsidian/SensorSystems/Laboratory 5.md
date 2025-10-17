
13/10/2025
***


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
			memset(&string, 0, sizeof(string));
		}
		else{
			i++;
		}
		HAL_UART_Receive_DMA(&huart2, &singlechar, 1);
	}
}

~~~

Homework 5b: ADC triggered by TIM (instead of having an interrupt that causes the ADC conversion, the ADC itself must have a setting that uses this timer to trigger the conversion and then we use the complete conversion callback and send it to the UART)

Homework 5c: Instead of send it through the UART, display it in the LCD.