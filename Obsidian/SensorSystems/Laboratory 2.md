

Revision for de-bouncing implementation from software approach.
```C#
#define LED GPIOA, GPIO_PIN_5

//PRIVATE VARIABLES
uint32_t tick;
uint32_t last_tick=0;
uint32_t delta;


// the HAL_GPIO_EXIT_Callback checks any falling or rising edges
void HAL_GPIO_EXIT_Callback(uint16_t, GPIO_PIN){
	
//Blocking version
	if(GPIO_PIN == GPIO_PIN_8){
		HAL_GPIO_TogglePin(LED);
		HAL_Delay(5);//inserts 5ms to not generate any changes within this time
		__HAL_GPIO_EXIT_CLEAR_IT(GPIO_PIN); //clears the interruption, it is over. 
	}

//Non-blocking version -- Here we just consider interruptions >100ms


	if (GPIO_PIN == GPIO_PIN_8){
		tick= HAL_GetTick();
		delta = last_tick - tick;
		
		if (delta>=100)
			HAL_GPIO_TogglePin(LED);
		
		last_tick = tick;
	}
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


Objective of this project is 
to play a song using the speaker


We again enable the TM1CH2 of the PINA9 as PWM generator CH2.
And we initialize it in certain freq.

![[Pasted image 20251002114326.png]]

And pulse 954 to get for instance LA4. IT IS NOT REPORTED HERE BUT ==SET Internal Clock as Clock Source!!!==

Now, the song is
![[Pasted image 20251002114455.png]]

And the musical notes having 99 as prescaler ($84MHz \rightarrow 840kHz$)

![[Pasted image 20251002114615.png]]

But, if we initialize the Timer after setting everything in the .io file we might find the MX_TIM1_Init(void)

We realize the htim1. commands let us to set manually the parameters and we might change them to perform the song.

```C# 
static void MX_TIM1_Init(void){

/* USER CODE BEGIN TIM1_Init 0 */
/* USER CODE END TIM1_Init 0 */
  
TIM_MasterConfigTypeDef sMasterConfig = {0};
TIM_OC_InitTypeDef sConfigOC = {0};
TIM_BreakDeadTimeConfigTypeDef sBreakDeadTimeConfig = {0};

/* USER CODE BEGIN TIM1_Init 1 */
/* USER CODE END TIM1_Init 1 */

htim1.Instance = TIM1;
htim1.Init.Prescaler = 99;
htim1.Init.CounterMode = TIM_COUNTERMODE_UP;
htim1.Init.Period = 1908;
htim1.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
htim1.Init.RepetitionCounter = 0;
htim1.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_DISABLE;

if (HAL_TIM_PWM_Init(&htim1) != HAL_OK)

{
Error_Handler();
}

sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_DISABLE;

if (HAL_TIMEx_MasterConfigSynchronization(&htim1, &sMasterConfig) != HAL_OK)

{

Error_Handler();

}
//And it continues 
```

Then first thing to do is define the musical notes

``` C#
#define _DO4 3205
#define _DOD4 3031
#define _RE4 2856
#define _MI4 2544
#define _FA4 2405
#define _FA4D4 2269
#define _SOL4 2141
#define _SOLD4 2023
#define _LA4 1908
#define _LA 1801
#define _SI4 1699
#define TEMPO 75 // 1/16 is the tempo of the music score
```

And we implement the song with their musical notes and their duration! :)


```C#
//First we implement a structure called note, and with it
struct note {int tone;int duration;};

//We declare a list of struct calle note score
struct note score[]={
 {_SOL4, 6},
 {_LA4, 2},
 {_SOL4, 4},
 {_FA4, 4},
 {_MI4, 4},
 {_FA4, 4},
 {_SOL4, 8},
 {_RE4, 4},
 {_MI4, 4},
 {_FA4, 8},
 {_MI4, 4},
 {_FA4, 4},
 {_SOL4, 8},
 {_SOL4, 6},
 {_LA4, 2},
 {_SOL4, 4},
 {_FA4, 4},
 {_MI4, 4},
 {_FA4, 4},
 {_SOL4, 8},
 {_RE4, 8},
 {_SOL4, 8},
 {_MI4, 4},
 {_DO4, 12}
};
```

And then, after the init of the TIM1, we might set a playsong() function

```C#
void playsong(){
	int lenght = sizeof(score)/sizeof(score[0]);
	for (int i=0; i<lenght; i++){
		playnote(score[i]);
	}
}
```

And then it comes in the playnote function the configuration of the timeeeer
```C# 
void playnote(struct note note_playing){

//copied from MX_TIM_1_INIT
TIM_ClockConfigTypeDef sClockSourceConfig = {0};
TIM_MasterConfigTypeDef sMasterConfig = {0};
TIM_OC_InitTypeDef sConfigOC = {0};
TIM_BreakDeadTimeConfigTypeDef sBreakDeadTimeConfig = {0};

  
/* USER CODE BEGIN TIM1_Init 1 */

/* USER CODE END TIM1_Init 1 */

htim1.Instance = TIM1;
htim1.Init.Prescaler = 99;
htim1.Init.CounterMode = TIM_COUNTERMODE_UP;
htim1.Init.Period = note_playing.tone; //We change this
htim1.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
htim1.Init.RepetitionCounter = 0;
htim1.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_DISABLE;

if (HAL_TIM_Base_Init(&htim1) != HAL_OK){
	Error_Handler();
}
sClockSourceConfig.ClockSource = TIM_CLOCKSOURCE_INTERNAL;

if (HAL_TIM_ConfigClockSource(&htim1, &sClockSourceConfig) != HAL_OK){
	Error_Handler();
}

if (HAL_TIM_PWM_Init(&htim1) != HAL_OK){
	Error_Handler();
}

sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_DISABLE;

if (HAL_TIMEx_MasterConfigSynchronization(&htim1, &sMasterConfig) != HAL_OK){
	Error_Handler();
}

sConfigOC.OCMode = TIM_OCMODE_PWM1;
sConfigOC.Pulse = note_playing.tone/2; //ALSO CHANGE THIS
sConfigOC.OCPolarity = TIM_OCPOLARITY_HIGH;
sConfigOC.OCNPolarity = TIM_OCNPOLARITY_HIGH;
sConfigOC.OCFastMode = TIM_OCFAST_DISABLE;
sConfigOC.OCIdleState = TIM_OCIDLESTATE_RESET;
sConfigOC.OCNIdleState = TIM_OCNIDLESTATE_RESET;

if (HAL_TIM_PWM_ConfigChannel(&htim1, &sConfigOC, TIM_CHANNEL_2) != HAL_OK){
	Error_Handler();
}

sBreakDeadTimeConfig.OffStateRunMode = TIM_OSSR_DISABLE;
sBreakDeadTimeConfig.OffStateIDLEMode = TIM_OSSI_DISABLE;
sBreakDeadTimeConfig.LockLevel = TIM_LOCKLEVEL_OFF;
sBreakDeadTimeConfig.DeadTime = 0;
sBreakDeadTimeConfig.BreakState = TIM_BREAK_DISABLE;
sBreakDeadTimeConfig.BreakPolarity = TIM_BREAKPOLARITY_HIGH;
sBreakDeadTimeConfig.AutomaticOutput = TIM_AUTOMATICOUTPUT_DISABLE;

if (HAL_TIMEx_ConfigBreakDeadTime(&htim1, &sBreakDeadTimeConfig) != HAL_OK){
	Error_Handler();
}


//HERE WE MAKE IT SOUND

HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_2);
HAL_Delay(note_playing.duration*TEMPO);
HAL_TIM_PWM_Stop(&htim1, TIM_CHANNEL_2);

/* USER CODE END TIM1_Init 2 */

HAL_TIM_MspPostInit(&htim1);

}
```
And after having all this we just playsong();  :)

