

Revision for de-bouncing implementation from software approach.
```C#
if (GPIO_PIN == GPIO_PIN_8){
	tick=
}

```
---

Project 2: Play note through speaker Objective of this project is to play a tone for 3 seconds using the speaker, using a PWM.

![[Pasted image 20250929151724.png]]
![[Pasted image 20250929151759.png]]
In the code
```
HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_2);

HAL_Delay(3000);

HAL_TIM_PWM_Stop(&htim1, TIM_CHANNEL_2);
```

|SOL#4|G#4|415||2024.096|1012.048|

