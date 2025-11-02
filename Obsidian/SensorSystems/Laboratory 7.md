
27/10/2025
***




***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 7a: Read the temperature measured by the LM75 and send it to a remote terminal every 1 second. </span>

As a first step we will read only the MSB 8 bit.

![[Pasted image 20251027195344.png]]
You have to make sure what are the two pins corresponding to the SDA, and SCL of the I2C1


~~~c#
uint8_t LM75_ADDRESS = 0b10010000; //Address left-shifted by 1, 0 padded
uint8_t LM75_TEMP_ADDRESS= 0x00; // Address of pointer register

~~~

We have then two addresses, the one of the device and the one of the register of the sensor, like an internal address
![[Pasted image 20251027193542.png]]

First, we try to transmit something to the sensor which is not obvious, and we put it outside of the while (in the init)

~~~c#
HAL_I2C_Master_Transmit(&hi2c1, LM75_ADDRESS, &LM75_TEMP_ADDRESS, 1, 10);
~~~

in this case we initialize the LM75, we set up pointer register to temperature register 


```c#
while(1){

	uint8_t temperature = 0; // we want to read only 1 byte -> 8 bits
	int len = 0;
	char str[32];
	if(HAL_I2C_Master_Receive(&hi2c1, LM75_ADDRESS+1, &temperature, 1, 20)== HAL_OK){ // we check if the communication went right before we send the data
	//Note the LM75_ADDRESS+1, the last bit is to read/write, 0->write, 1->read, thus +1, we want to read 
	//Instead of indicating where to write, we add where to save the read data &temperature
		char str[32];
		len = snprintf(str, sizeof(str), "Temperature: %d °C \r\n", temperature);
		} else{
		
			len = snprintf(str, sizeof(str), "Error reading from LM75 \r\n");
		}
		
		HAL_UART_Transmit(&huart2, str, len, 100);
		HAL_Delay(1000);
}
```


***
***
***
***
***

# <span style="color:rgb(223, 109, 109)">Homework 7a: Now we will modify the code to read all 11 bits within an interrupt routine </span>

![[Pasted image 20251028082435.png]]
![[Pasted image 20251028190915.png]]
![[Pasted image 20251028091117.png]]
![[Pasted image 20251028190938.png]]

![[Pasted image 20251028190841.png]]


```c#
uint8_t LM75_ADDRESS = 0b10010000;
uint8_t LM75_TEMP_ADDRESS = 0x00;

int8_t temperature_buffer[6];
int16_t temperature = 0;

char string[32];
int length = 0;
```

`temperature_buffer[2]` and `temperature`. Both need to be either int or uint. Otherwise there might be some errors when extending the variable to accommodate the bit size.
~~~c#
//Main init
HAL_I2C_Master_Transmit(&hi2c1, LM75_ADDRESS, &LM75_TEMP_ADDRESS, 1, 100);
HAL_TIM_Base_Start_IT(&htim2);0
~~~


``` c#

void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim == &htim2){
		HAL_I2C_Master_Receive_DMA(&hi2c1, LM75_ADDRESS+1, temperature_buffer, 6);
	}
}

void HAL_I2C_MasterRxCpltCallback(I2C_HandleTypeDef *hi2c){
	if(hi2c == &hi2c1){
		if(temperature_buffer[0]==temperature_buffer[2] || temperature_buffer[0] == temperature_buffer[4]){

			temperature = temperature_buffer[0]<<8 | temperature_buffer[1];
			}
		else{
			temperature = temperature_buffer[2]<<8 | temperature_buffer[3];
			}
//
// //for +25.375
// temperature_buffer[0] = 0b00011001; // 0x19
// temperature_buffer[1] = 0b01100000; // 0x60
// //for −12.875
// temperature_buffer[0] = 0b11110011; // 0xF3
// temperature_buffer[1] = 0b00010000; // 0x10

		temperature = temperature_buffer[0]<<8 | temperature_buffer[1];
		float temperature_celsius = temperature/256.0;
		length = snprintf(string, sizeof(string), "Temperature: %.3f °C \r \n", temperature_celsius);
		HAL_UART_Transmit_DMA(&huart2, string, length);

	}
}
```