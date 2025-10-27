
20/10/2025
***

# <span style="color:rgb(223, 109, 109)">Project 6a: Objective of the project is to acquire 3 voltages (potentiometer, temperature sensor, Vref) every 1 s and to send them to a remote terminal. The acquisition are started via hardware by a timer and data are saved in the microcontroller memory using DMA.</span>

![[Pasted image 20251020151137.png]]


| ![[Pasted image 20251020151257.png]] | The TSVREFE bit must be set to enable the conversion of both internal channels: the ADC1_IN16 or ADC1_IN18 (temperature sensor) and the ADC1_IN17 (VREFINT). |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
![[Pasted image 20251025231346.png]]

![[Pasted image 20251025231448.png]]

We set the continuous conversion move to enable, and the number of conversion to three cos we want three diff conversions. 

and the timer 2 trigger out event. The sampling time is better to have it at 480 cycles so we have time to do the conversion. 

![[Pasted image 20251025173946.png]]

we enable the DMA, we set it circular and halfword? Why so? we have an ADC which saves the data in 12 bits, to a register which has 32bits, so, we have enough with 16 bits. Otherwise, it'll save it into an array, it is better to say to the DMA we have to move 16 bits to the register. This is because of the way the ADC works, we have 32 bits register. 

Also set parameter baud rate at 9600 bit/s

![[Pasted image 20251025174322.png]] 


![[Pasted image 20251025231641.png]]
and set the baud rate as desired.

```C#
#define ACQUISITIONS 3
#define VDDA 3.3 // Analog voltage supply
#define VSSA 0.0 // Analog ground
#define RESOLUTION_BITS 12
#define V25 0.76 //Temperature sensor voltage
#define AVG_SLOPE 0.0025 //Temperature sensor average
```

~~~C#
float FSR;
float RESOLUTION_STEPS;
uint16_t voltages[ACQUISITIONS];
~~~

~~~c#
int main(void){

FSR = VDDA-VSSA;
RESOLUTION_STEPS = (1)<<RESOLUTION_BITS; //ADC resolution steps calculation 2^(RESOLUTION)

HAL_TIM_Base_Start(&htim2); //Timer not used in interrupt mode, we simply use its output by our timer
HAL_ADC_Start_DMA(&hadc1, voltages, ACQUISITIONS);
~~~

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

---
---
---
---
---

# <span style="color:rgb(223, 109, 109)">Homework 6a: ADC scan using DMA</span> 

Objective of the project is to acquire LDR resistance value every ms and to send its average value to a remote terminal every 1s. Step 2: convert the resistance value to a lux level and send that to the remote terminal

![[Pasted image 20251026000734.png]]

![[Pasted image 20251026001036.png]]

![[Pasted image 20251026001146.png]]

![[Pasted image 20251026001615.png]]


![[Pasted image 20251026001355.png]]

![[Pasted image 20251026001433.png]]

![[Pasted image 20251026001505.png]]

