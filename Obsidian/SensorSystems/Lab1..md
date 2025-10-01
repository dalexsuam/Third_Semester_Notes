	
# <span style="color:rgb(223, 109, 109)">General Purpose Input/Outputs</span>
![[Pasted image 20250922143233.png]]
Diodes used for protection $\rightarrow$ Against Electrostatic charge.

Pull-up or Pull-down resistor enable for reading out the I/O pin. 

Input top and output at the bottom.

Input taken as analog value. Alternate function.

Output control $\rightarrow$ P-MOS, N-MOS for the three config: Push-pull, open-drain (only goes to the low value) or disabled.

# <span style="color:rgb(223, 109, 109)">External Interrupt/Event (EXTI) Peripheral </span>

Peripheral used to handle interrupts triggered by external events.

It can detect event not only in states but in falling or rising edges or both. They can be connected to GPIO pin.

EXTI are connected to NVIC to manage interrupt priorities and enables or disables them globally.

Interrupts and events are different. Both are triggers. Events are hardware related and interrupts are processing/software approached. 

##  <span style="color:rgb(239, 179, 1)">Line Mapping</span>

![[Pasted image 20250922144300.png]]

## <span style="color:rgb(239, 179, 1)">How to select EXTI?</span>

![[Pasted image 20250922144436.png]]

We use the registers described above.


## <span style="color:rgb(239, 179, 1)">GPIO HAL functions</span>

``` C
GPIO_PinState HAL_GPIO_ReadPin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin)
void HAL_GPIO_WritePin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, GPIO_PinState PinState)
void HAL_GPIO_TogglePin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin)
__weak void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
```

# <span style="color:rgb(223, 109, 109)">TIMERS</span> 

**Trigger / clock controller** 
* selects input clock
* Synchronization with other clocks (Master $\rightarrow$  Output Trigger, Slave $\rightarrow$ Input Trigger)

 **Prescaler** 
 * Divides the frequency the counter increases, skipping a portion of the incoming events. 

**Counter** 
* Up, Down, Up/Down counter 

**Capture and Compare registers** 
* One for each channel, we can use it to compare two values in time

 **Auto-reload register** 
 * Sets the timer FSR (Full scale range of the counter)

## <span style="color:rgb(239, 179, 1)">Timer functionalities</span> 

Apart from already described

**PWM generation**
* Edge aligned: counter Up or Down mode 
* Center aligned: counter Up/Down mode

![[Pasted image 20250922145918.png]]

$$
PWM frequency = \frac{f_{TIM}}{(ARR+1)(PSC+1)}
$$
$$
PWM Duty Cycle = \frac{CCRX+1}{ARR+1}
$$
## <span style="color:rgb(239, 179, 1)">Timer HAL functions</span> 

```C
HAL_StatusTypeDef HAL_TIM_PWM_Start(TIM_HandleTypeDef *htim, uint32_t Channel) 
HAL_StatusTypeDef HAL_TIM_PWM_Stop(TIM_HandleTypeDef *htim, uint32_t Channel) 
//Starts (stops) the PWM signal generation HAL_StatusTypeDef 

HAL_TIM_Base_Start(TIM_HandleTypeDef * htim) 
HAL_StatusTypeDef HAL_TIM_Base_Start_IT(TIM_HandleTypeDef * htim) HAL_StatusTypeDef HAL_TIM_Base_Stop(TIM_HandleTypeDef * htim) HAL_StatusTypeDef HAL_TIM_Base_Stop_IT(TIM_HandleTypeDef * htim) //Starts (stops) the TIM Base generation (x_IT with interrupt generation)
```



---

# <span style="color:rgb(223, 109, 109)">Project 1a: Pushbutton - polling</span>

Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. A polling operation will be used to monitor the state of the pushbutton

![[Pasted image 20250922152829.png]]

We identify the pins and define them as input and output respectively

We identify the both pins and types of GPIO in the data sheet. And in the code, we write
``` c#
//In include section

#define BUTTON GPIOC, GPIO_PIN_13
#define LED GPIOA, GPIO_PIN_5

//In int main we define a variable for the status of the button

int main(void){
GPIO_PinState pushbutton;
}
//Then within the while. We, check the status of the button and write in the led

while(1){
pushbutton = HAL_GPIO_ReadPin(BUTTON);
HAL_GPIO_WritePin(LED, !pushbutton); //We consider !pushbutton cos it is in pull-up configuration, thus a 0 when this is normally-open
}
```
![[Pasted image 20250925151918.png]]
# <span style="color:rgb(223, 109, 109)">Project 2a:</span>

Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. The pushbutton input will be used in interrupt mode

![[Pasted image 20250925152829.png]]

In this case to be used as interrupt what we have to do is going to the Nested Vectored Interrupt Controller (or NVIC) and enable the EXTI (External Interrupt/Event) line $[15:10]$ interrupts peripheral to receive events through the pins 10, 11, 12, **13**, 14, 15

The priority is ok to leave it as 0. Since there are not any other events with higher priority so far. ==Remember, the lower the number the higher the priority==

![[Pasted image 20250925154030.png]]
Now, in order to detect when the button is being push and not, what we do is detecting both rising and falling edges, we would like to well know both transitions, and that's why we configure the PIN13 to perform the detect these both events,  GPIO>PIN13>GPIO_EXTI13> GPIO mode> Rising/Falling Edge trigger detection

In this case we are not setting anything in the code regarding the while loop but we need to define the interrupt routine function.

``` C#
#define BUTTON GPIOC, GPIO_PIN_13
#define LED GPIOA, GPIO_PIN_5

void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){
	GPIO_PinState pushbutton;
	switch(GPIO_Pin){
	case GPIO_PIN_13: //It checks if that PIN generated the interrupt
		pushbutton = HAL_GPIO_ReadPin(BUTTON); //reads the value of the BUTTON
		HAL_GPIO_WritePin(LED, !pushbutton);// Change the LED
		break;
	default:
	break;//otherwise, break
}

}
```


# <span style="color:rgb(223, 109, 109)">HOMEWORK 02</span>

**Due date: Squad A:** Sunday, September 28, at 2:30 pm

1- Prepare the basics for the project “Play a song”:

**a. Modify the status (switch on / off) of the NUCLEO green LED, every time you snap your fingers.**
**(Use the pin connected to the microphone as an External Interrupt)**

*Hint: look at the files “Green PCB board schematic” and “Nucleo Schematic” and “Nucleo user*
*manual” on Webeep in “Material/Laboratories/Documentation” and find the STM32 pin that*
*connects to SND_IN.*

Ok, this part is quite easy if we've understood the lab_1b. We basically implement the same approach. However, now the interrupt is produced by the mic which is in the pin PINA8. First, we enable the EXIT peripheral  $[9:5]$ cos the one we want to use is the PA8, EXTI8
![[Pasted image 20250925233600.png]]

We leave the priority 0 so far it is not necessary to change it and we set the GPIO trigger detection as only interrupt by rising edge detected (I assume this is the best one since we want to toggle the LED with a snap, so we're not reading two states, but only an incoming one). Also we set the A5 to output (LED)

Thus, the define are

```c#
#define MIC GPIOA, GPIO_PIN_8
#define LED GPIOA, GPIO_PIN_5
```
Then we have the interrupt routine as following:
```C#
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){
	GPIO_PinState snap;
	switch(GPIO_Pin){
	case GPIO_PIN_8: //It checks if that PIN generated the interrupt
		snap = HAL_GPIO_ReadPin(MIC); //checks arriving snap
		if (snap){//if snap detected
		HAL_GPIO_TogglePin(LED);//LED toggles
		}
		break;
	default:
	break;//otherwise, break

}

}
```


b. Make the NUCLEO green LED blink at a 1 Hz rate using PWM generation on the corresponding
channel.


![[Pasted image 20250928213711.png]]
![[Pasted image 20250928213819.png]]

HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_1);

``` C#
MX_TIM2_Init(); /* USER CODE BEGIN 2 */ HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_1); // Add this line! /* USER CODE END 2 */
```


![[Pasted image 20250929144309.png]]


---


melodia = [
    392, 440, 392, 330, 392, 523, 494, 440,  # Frase 1
    349, 349, 330, 294, 330, 349,             # Frase 2
    392, 440, 392, 330, 392, 523, 494, 440,  # Frase 3
    392, 523, 392, 330, 262, 392              # Frase 4
]

