
# <span style="color:rgb(223, 109, 109)">Revision for de-bouncing implementation from software approach</span>

The thing is that the microphone doesn't count with a anti-bouncing circuit. That is why we need to work around with two approaches at the moment of implementing the snap detection.

In the following code you can evidence:
* **Blocking version:** uses a HAL_Delay
* **Non-blocking version:** uses HAL_GetTick and allows inputs greater than threshold.
```C#
#define LED GPIOA, GPIO_PIN_5

//PRIVATE VARIABLES
uint32_t tick;
uint32_t last_tick=0;
uint32_t delta;


// the HAL_GPIO_EXTI_Callback checks any falling or rising edges
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_PIN){
	
//Blocking version
	if(GPIO_PIN == GPIO_PIN_8){
		HAL_GPIO_TogglePin(LED);
		HAL_Delay(5);//inserts 5ms to not generate any changes within this time
		__HAL_GPIO_EXTI_CLEAR_IT(GPIO_PIN); //clears the interruption, it is over
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
***
***

## <span style="color:rgb(223, 109, 109)">Project 3a: Play note through speaker </span>

Objective of this project is to play a tone for 3 seconds using the speaker, using a PWM.

The note decided to play was SOL#4

![[Pasted image 20250929151724.png]]
To obtain a frequency of $415 Hz$ for SOL#4, we have first, divided the timer from $84MHz-> 840KHz$ with a $PSC$ of $100-1$.

And to get a $f = 415 Hz$, (with a square wave with 50% of DC)
$$
f_{desired}=\frac{840KHz}{ARR+1}
$$
$$
ARR=\frac{840KHz}{415Hz}-1
$$
$$
ARR=2024.09 -1
$$
And to get 
$$
CCRX = ARR/2
$$
Hence 
$$CCRX = 1012.04$$
Based on the frequency characteristics we were given in the excel file

![[Pasted image 20250929151759.png]]
*The TIM1_CH2 PWM is the one linked to the speaker*

In the code
```
HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_2);
HAL_Delay(3000);
HAL_TIM_PWM_Stop(&htim1, TIM_CHANNEL_2);
```
# <span style="color:rgb(223, 109, 109)">Project 3b: Play a song using the speaker</span>

Objective of this project is to play a song using the speaker. We again enable the TM1CH2 of the PINA9 as PWM generator CH2.
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

//We declare a list of struct called note score
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
***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Homework 3a: Play a song using speaker -triggered by mic - Timer (instead of HAL_Delay)</span>

Now. Objective of this project is to play a song using the speaker when the microphone detects a loud sound

![[Pasted image 20251004225511.png]]
For the GPIO_EXTI8, we have that. It is important to set a priority lower than the tick timer (In order to use the Non-blocking version debouncing implementation for the microphone)

![[Pasted image 20251004234613.png]]

To activate it, and we might check if we want to trigger it with rising edge, what is the event we're detecting...

![[Pasted image 20251004225749.png]]

Now, for the TIM1-CH2, the PWM of the Microphone, we set the $PSC-1 = 100-1$, and the $ARR$ and $CCR$ as desired for any note

| ![[Pasted image 20251004225944.png]] | ![[Pasted image 20251004224409.png]] |
| ------------------------------------ | ------------------------------------ |
Prescaler 99, counter 1098 and pulse 954. To start from LA#

Now, we would like to implement the code without a HAL_Delay, for this we configure a timer simply with the internal clock and dividing it by $PSC=8400-1$ and $ARR= 10-1$. So its $f=1KHz \rightarrow T=1 ms$

![[Pasted image 20251213081232.png]]

And we also enable the timer global interrupt in the Nested Vector Interrupt Controller 
![[Pasted image 20251213081320.png]]

#### Declaring some variables

As before, we have the definition of the values of the $ARR$ to obtain the desired frequency. We considered the $PSC = 100-1$ is static
~~~~c#
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
~~~~

Now, we assigned to each note, the duration according to the song this is the *score*
~~~c#
struct note {int tone; int duration;};
//We declare a list of struct called note score
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
~~~

We also define some other variables that we are going to use :)

~~~c#
//The following for non-blocking antibouncing
uint32_t tick;
uint32_t last_tick = 0;
uint32_t delta;
uint8_t song_playing = 0;
//This to go through the song score
int song_index;
int song_length;
~~~

*How do we trigger the song?* With the snap/loud sound at the microphone, so, once an event is detected in this GPIO_PIN, we trigger an interruption
~~~c#
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){
	if(GPIO_Pin == GPIO_PIN_8){
	//You see here we implement non-blocking antibouncing
		tick = HAL_GetTick();
		delta = last_tick-tick;
		if (delta>=100 && song_playing==0){
			play_song();
		}
	}
}
~~~

We see once we trigger the song with the microphone we enter to the `play_song()` function

~~~~c#
void play_song(){
	//We set song_playing flag to 1 so no song can be retriggered while it is playing
	song_playing = 1;
	//Define song_index, so, we start from all 
	song_index = 0;
	//sizeof(score) = 23 × 8 = 184 bytes, sizeof(score[0])= 8 bytes, song_length = 184 ÷ 8 = 23
	//We obtain that from this song score we have to play 23 notes
	song_length = sizeof(score)/sizeof(score[0]);
//We start by playing one note at a time by means of its song_index (starting from 0 and finishing to 23)
	playnote_INT(song_index);
	}
~~~~
So, by using the function `playnote_INT(song_index)` in this case we aim to play the first note of the song score.

~~~~c#
void playnote_INT(int song_index){
	//Stops PWM and timer interrupt, just to start from reset
	HAL_TIM_PWM_Stop(&htim1, TIM_CHANNEL_2);
	HAL_TIM_Base_Stop_IT(&htim2);
	//Check if song is over
	if(song_index>=song_length){
		HAL_TIM_Base_Stop_IT(&htim2);
		__HAL_TIM_CLEAR_IT(&htim2, TIM_IT_UPDATE); //We have to clear the interrupt
		//Otherwise, we'll get a queue of songs played in infinite loop
		song_playing = 0;
		return;
	}
	//If song is not over
	//PWM timer
	//Direct access to registers of tim1
	//We set ARRX
	htim1.Instance->ARR = score[song_index].tone;
	//We set CCRX
	htim1.Instance->CCR2 = score[song_index].tone/2;
	//We set counter starts from 0;
	htim1.Instance->CNT = 0;
	//These previous settings changes the freq of my PWM signal corresponding each note
	
	//We don't set a prescaler cos we created the excel file in function to the 100-1 prescales
	
	//Normal Timer
	htim2.Instance->ARR = score[song_index].duration*TEMPO*10;
	//Basically the note duration (4,8)/16 (Tempo = 75 ~1/16) and the x10 makes it slower in time cos we have a timer of 1ms of period
	htim1.Instance->CNT = 0;
	//We make sure again the tim1 counter starts from 0 
	//Play the note
	HAL_TIM_PWM_Start(&htim1, TIM_CHANNEL_2);
	HAL_TIM_Base_Start_IT(&htim2);
	//We make sure there isn't interrupts triggered interrupts bef
	__HAL_TIM_CLEAR_IT(&htim2, TIM_IT_UPDATE);
}
~~~~
Now, after setting the configuration of our PWM and the interruption of our timer, we'll play the song and initialize our timer, to produce an interruption at the time of this note being played. That is, after playing this note, an interruption will be triggered due to the timer.
~~~~c#
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim == &htim2){
	playnote_INT(++song_index);
	}
}
~~~~
That is why in our `HAL_TIM_PeriodElapsedCallback()` we check if an interruption is done by timer 2, and if so, we execute `playnote_INT()` by increasing the index of the song (the following note in the score) and again we go through this function but now changes will be made w.r.t the current note that has to be played.

TY :)
