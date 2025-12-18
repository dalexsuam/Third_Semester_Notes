
24/11/2025
***
# <span style="color:rgb(223, 109, 109)">IR Communication</span>

![[Pasted image 20251216223312.png|400]]

In this final part of the course, we look at the **last peripheral we have not studied yet: infrared (IR) communication**. On your board, there are two IR components placed next to each other:

- an **infrared LED** (transmitter)
- an **infrared receiver** (decoder)
    
These two components allow us to transmit information using infrared light. This means that one board can send a message using the IR LED, and another board—placed nearby—can receive, decode, and process that message.

It is even possible for a board to communicate with itself, since the emitted light can still reach the receiver. In practice, however, this may cause reliability issues, so the typical use case is **communication between two boards**. Once the data is received, it can be forwarded via UART, displayed on an LCD, or processed in any other way.

---

![[Pasted image 20251216223347.png]]

Here you can see the **pins** to which the IR LED and the IR receiver are connected. I want you to notice two important aspects:

1. **The infrared LED is connected to a timer.**  
    This is because we will use it to transmit data following a UART-like protocol. Instead of using the hardware UART transmitter, we will _manually generate_ the signal using timers and PWM. In other words, we will build our own UART transmission using timing logic.
    
2. **The infrared receiver is connected to UART1.**  
    The UART peripheral is configured normally, but instead of receiving data from a wire, the data arrives through infrared light. From the UART’s point of view, this looks exactly like a standard serial signal.
    

So effectively, we are **implementing our own UART transmitter**, while using a **standard UART receiver**.

---

![[Pasted image 20251216223510.png]]

Let’s now look more closely at how the **infrared receiver** works internally. It is not just a simple photodiode. Inside the receiver chip we have:

- A **four-cell photodiode**, which you have already studied in theory
- An **amplifier with automatic gain control (AGC)**, which adapts the gain depending on ambient light conditions
- A **band-pass filter**, centered around **38 kHz**
- A **demodulator**
    
All of these blocks are integrated inside the chip.

Why do we need filtering and demodulation?

Without them, the receiver would detect _all_ infrared light: sunlight, lamps, computer screens, smoke detectors, and so on. This would generate unwanted signals on the UART line.

By filtering around **38 kHz**, the receiver only reacts to infrared light modulated at that specific frequency. Therefore, we must program our IR LED to transmit data **modulated at 38 kHz**.

When the demodulator detects this modulated signal, it drives the output stage (a transistor). When a valid IR signal is present, the output is pulled **low**; otherwise, it stays **high**.

This behavior matches the UART logic perfectly:

- Idle line: logic 1 (high)    
- Active signal: logic 0 (line pulled low)
    
---

![[Pasted image 20251216223831.png]]

The **transmitter** side is much simpler. It consists mainly of an infrared LED driven by an **amplifier**, because the microcontroller pin alone can only source about **8 mA**, which is not enough for reliable IR transmission.

Since the LED is connected to a **timer**, we can drive it using **PWM**. The required parameters are:

- **Frequency:** 38 kHz
- **Duty cycle:** 50%
    
If we were to drive the LED with a constant signal (no modulation), the receiver would not detect it, because the demodulator would filter it out. This is why PWM modulation at 38 kHz is mandatory.

---

![[Pasted image 20251216223931.png]]

This slide is a reminder of how **UART communication** works.

- When the bus is idle, it stays at logic 1
- Transmission starts with a **start bit** (line pulled low)
- Data bits follow
- Transmission ends with a **stop bit** (line goes back high)
    
In this project, **you must implement the start and stop bits yourself**.

The IR transmission logic is as follows:

- To transmit a **logic 1**, the LED stays **off**
- To transmit a **logic 0**, the LED emits a **38 kHz PWM signal**
    
The duration of each bit is determined by the **baud rate**. I suggest using a baud rate **below 2450 bps**. This is slower than a wired UART, but still sufficient for reliable communication.

---

The receiver side uses the UART hardware, so it automatically decodes the incoming bits. The transmitter, however, must be implemented manually using:

- One timer to generate the **38 kHz PWM**
- One timer to control the **bit timing** (baud rate)
- A state machine to send start bit, data bits, and stop bit
    

You can start by transmitting a single **character (8 bits)**. Once that works, you can build a higher-level function to transmit **strings**, by repeatedly sending characters.

---

For the **receiver**, the implementation is easier. I suggest the following steps:

1. Configure **UART2** (USB connection to the PC)
2. Receive one byte in **interrupt mode**
3. Display the received data on the terminal or use LEDs to visualize the bits
4. Once this works, switch from UART2 to **UART1**, which is connected to the IR receiver

This way, you can debug the receiver logic using the PC before introducing infrared communication.

---

A possible final project is the following:

- Scan the **push-button matrix** (code already available)
- Send the pressed key via **infrared UART**
- Receive it on the other board and process it
    
Eventually, you should merge **transmitter and receiver** into a single project, running on the same board. This is important because during the exam you may be asked to both send and receive using one board.
### Homework

For next week, you must:

1. Implement the **IR transmitter**    
2. Implement the **IR receiver**
3. Combine both into a **single complete project**

You may also create a custom project (for example, sending temperature data, keyboard input, or controlling sounds), but it is recommended to first complete the standard version.

Although this project may look complex, if you follow the steps shown in the slides and reuse what you already know about **timers, PWM, and UART**, it becomes quite manageable—and even fun.

That concludes the explanation for infrared communication.


***
***
***
***
***


![[Pasted image 20251216231313.png]]

![[Pasted image 20251217002410.png]]



![[Pasted image 20251216231951.png]]
~~~~c#
uint8_t matrix[5][2] = {
	{0,16},// y0 content (row), address (column)
	{0,8},//y1
	{0,4},//y2
	{0,2},//y3
	{0,1}//y4
};

uint8_t matrix_QM[5][2] = {
	{32,16},// y0 content (row), address (column)
	{64,8},//y1
	{69,4},//y2
	{72,2},//y3
	{48,1}//y4
};

uint8_t matrix_A[5][2] = {
	{31,16},// y0 content (row), address (column)
	{36,8},//y1
	{68,4},//y2
	{36,2},//y3
	{31,1}//y4
};

uint8_t matrix_B[5][2] = {
	{127,16},// y0 content (row), address (column)
	{73,8},//y1
	{73,4},//y2
	{73,2},//y3
	{54,1}//y4
};

uint8_t matrix_C[5][2] = {
	{62,16},// y0 content (row), address (column)
	{65,8},//y1
	{65,4},//y2
	{65,2},//y3
	{34,1}//y4
};

uint8_t matrix_D[5][2] = {
	{127,16},// y0 content (row), address (column)
	{65,8},//y1
	{65,4},//y2
	{65,2},//y3
	{62,1}//y4
};

uint8_t matrix_E[5][2] = {
	{127,16},// y0 content (row), address (column)
	{73,8},//y1
	{73,4},//y2
	{73,2},//y3
	{73,1}//y4
};

uint8_t matrix_F[5][2] = {
	{127,16},// y0 content (row), address (column)
	{72,8},//y1
	{72,4},//y2
	{72,2},//y3
	{72,1}//y4
};


uint8_t matrix_0[5][2] = {
	{62,16},// y0 content (row), address (column)
	{113,8},//y1
	{73,4},//y2
	{71,2},//y3
	{62,1}//y4
};

uint8_t matrix_1[5][2] = {
	{16,16},// y0 content (row), address (column)
	{33,8},//y1
	{127,4},//y2
	{1,2},//y3
	{0,1}//y4
};

uint8_t matrix_2[5][2] = {
	{33,16},// y0 content (row), address (column)
	{67,8},//y1
	{69,4},//y2
	{73,2},//y3
	{49,1}//y4
};

uint8_t matrix_3[5][2] = {
	{34,16},// y0 content (row), address (column)
	{65,8},//y1
	{73,4},//y2
	{73,2},//y3
	{54,1}//y4
};

uint8_t matrix_4[5][2] = {
	{120,16},// y0 content (row), address (column)
	{8,8},//y1
	{8,4},//y2
	{8,2},//y3
	{127,1}//y4
};

uint8_t matrix_5[5][2] = {
	{114,16},// y0 content (row), address (column)
	{81,8},//y1
	{81,4},//y2
	{81,2},//y3
	{78,1}//y4
};

uint8_t matrix_6[5][2] = {
	{62,16},// y0 content (row), address (column)
	{73,8},//y1
	{73,4},//y2
	{73,2},//y3
	{38,1}//y4
};

uint8_t matrix_7[5][2] = {
	{64,16},// y0 content (row), address (column)
	{64,8},//y1
	{79,4},//y2
	{80,2},//y3
	{96,1}//y4
};

uint8_t matrix_8[5][2] = {
	{54,16},// y0 content (row), address (column)
	{73,8},//y1
	{73,4},//y2
	{73,2},//y3
	{54,1}//y4
};

uint8_t matrix_9[5][2] = {
	{50,16},// y0 content (row), address (column)
	{73,8},//y1
	{73,4},//y2
	{73,2},//y3
	{62,1}//y4
};



// Keypad column pin definitions
#define PIN_C0 GPIOC, GPIO_PIN_11
#define PIN_C1 GPIOC, GPIO_PIN_10
#define PIN_C2 GPIOC, GPIO_PIN_9
#define PIN_C3 GPIOC, GPIO_PIN_8

// Keypad row pin definitions  
#define PIN_R0 GPIOC, GPIO_PIN_3
#define PIN_R1 GPIOC, GPIO_PIN_2
#define PIN_R2 GPIOC, GPIO_PIN_13
#define PIN_R3 GPIOC, GPIO_PIN_12

// Debounce time in multiples of timer period (4ms)
#define DEBOUNCE_TIME 2  // 4ms × 2 = 8ms debounce time

char map[16] = "FB73EA62D951C840";  // F, B, 7, 3, E, A, 6, 2, D, 9, 5, 1, C, 8, 4, 0

// Array to track how long each key has been pressed (in timer cycles)
uint32_t keypress[16];  
// Array to track if a key press has been acknowledged/sent already
uint32_t ack[16];       

// Current column being scanned (0-3)
int column_index = 0;
~~~~

~~~~c#

char RX_byte = 0;
char command = 0;
int new_command = 0;

int BaudElapsedFlag = 0;
char RX_byte2 = 0;
char UART_RX_byte;
char UART_RX_flag;

char string[32];

uint8_t CharMAP[256][5][2] = {
	{32,16},
	{64, 8},
	{69, 4},
	{72, 2},
	{48, 1}

};


~~~~

~~~C#
void initCharMAP(void){
	for(int i = 0; i<256; i++){
		memcpy(CharMAP[i], matrix_QM, sizeof(matrix_QM));
	}
	memcpy(CharMAP[(uint8_t) '0'], matrix_0, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '1'], matrix_1, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '2'], matrix_2, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '3'], matrix_3, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '4'], matrix_4, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '5'], matrix_5, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '6'], matrix_6, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '7'], matrix_7, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '8'], matrix_8, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) '9'], matrix_9, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'A'], matrix_A, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'B'], matrix_B, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'C'], matrix_C, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'D'], matrix_D, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'E'], matrix_E, sizeof(matrix_0));
	memcpy(CharMAP[(uint8_t) 'F'], matrix_F, sizeof(matrix_0));
}

void showletter(char digit){
		memcpy(matrix, CharMAP[(uint8_t) digit], sizeof(matrix));
}

void UART_IR_sendByte(char byte){
	HAL_TIM_Base_Start_IT(&htim10);
	
	HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_3);
	BaudElapsedFlag = 0;
	
	while(BaudElapsedFlag ==0){
	}
	
	for(int bit_ctr = 0; bit_ctr<8, bit_ctr++){
		if((byte & (0x01<<bit_ctr))==0){
			HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_3);
		}
		else{
			HAL_TIM_PWM_Stop(&htim2, TIM_CHANNEL_3);
		}
		BaudElapsedFlag=0;
		while(BaudElapsedFlag==0){
		
		}
	}
	HAL_TIM_Base_Stop_IT(&htim10);
	BaudElapsedFlag=0;
}

void UART_IR_Send(char *payload, int size){
	for(int i =0; i<size; i++){
		UART_IR_sendByte(payload[i]);
		HAL_Delay(1);
	}

}



~~~

~~~~c#
//Init
//One timer for scanning the keyboard, and the other for printing out the LED
//Another timer for scanning the timing of the UART, based on the baudrate. turning on and of PWM
HAL_TIM_Base_Start_IT(&htim11);
HAL_TIM_Base_Start_IT(&htim5);

initCharMAP();

HAL_UART_Receive_IT(&huart1, &RX_byte, 1);

HAL_UART_Receive_IT(&huart2, &RX_byte2, 1);
~~~~
~~~~c#

	while(1){
		if(new_command){
			showletter(command);
			new_command=0;
		}
		
		for(int i=0; i<16; i++){
			if (keypress[i] > DEBOUNCE_TIME) {
                // Key is validly pressed (debounced)
                if (ack[i] == 0) {
                    // First time detecting this debounced press - send character
                    UART_IR_sendByte(map[i]);
                    ack[i] = 1;  // Mark as acknowledged
                }
            } else {
                // Key is not pressed (or not yet debounced)
                ack[i] = 0;  // Reset 
		}
	
	}
~~~~




~~~~c#
void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart){
	if(huart==&huart1){
		HAL_UART_Receive_IT(&huart1, &RX_byte, 1);
		command = RX_byte;
		new_command = 1;
	}
	
	if(huart==&huart2){
		HAL_UART_Receive_IT(&huart2, &RX_byte2, 1);
		command = RX_byte2;
		new_command = 1;
	}
}

void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim==&htim10){
		BaudElapsedFlag =1;
	}
	if(htim == &htim11){
		if (HAL_GPIO_ReadPin(PIN_R0) == GPIO_PIN_SET) {
            keypress[4 * column_index] = 0;  // Key not pressed, reset counter
        } else {
            keypress[4 * column_index]++;    // Key pressed, increment counter
        }
        // Check Row 1 for current column  
        if (HAL_GPIO_ReadPin(PIN_R1) == GPIO_PIN_SET) {
            keypress[4 * column_index + 1] = 0;// Key not pressed, reset counter
        } else {
            keypress[4 * column_index + 1]++;// Key pressed, increment counter
        }
        // Check Row 2 for current column
        if (HAL_GPIO_ReadPin(PIN_R2) == GPIO_PIN_SET) {
            keypress[4 * column_index + 2] = 0;// Key not pressed, reset counter
        } else {
            keypress[4 * column_index + 2]++;// Key pressed, increment counter
        }
        // Check Row 3 for current column
        if (HAL_GPIO_ReadPin(PIN_R3) == GPIO_PIN_SET) {
            keypress[4 * column_index + 3] = 0;// Key not pressed, reset counter
        } else {
            keypress[4 * column_index + 3]++;// Key pressed, increment counter
        }
        
        column_index = (++column_index) % 4;  // Cycle through columns 0→1→2→3→0...        
        // Activate only the current column (active-high drive)
        // Only one column is active at a time to prevent ghosting
        HAL_GPIO_WritePin(PIN_C0, (column_index == 0) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C1, (column_index == 1) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C2, (column_index == 2) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C3, (column_index == 3) ? GPIO_PIN_SET : GPIO_PIN_RESET);
		
	}
	
	if(htim==&htim5){
		//Option 1
		//HAL_SPI_Transmit_DMA(&hspi1, matrix[column_index],2);
		//
	
	
		HAL_GPIO_WritePin(RCLK_PIN, GPIO_PIN_SET);
		if(++column_index_rec>4)
			column_index_rec=0;
		HAL_GPIO_Write_Pin(RCLK_PIN, GPIO_PIN_RESET);
		HAL_SPI_Transmit_DMA(&hspi1, matrix[column_index_rec], 2);
	
	}
	

}

~~~~

Okay, I'll start again. It immediately stopped. So, as I was saying, I'm going to show the solution of the integrated homework, let's say. So it's going to be a receiver and sending out of the data. And in particular, I'm going to show you the solution that was suggested in the slides. So it's going to be the keyboard pressing and the data being sent to the infrared, received to the infrared, and then printed out on the LED market. So it's going to be the basic, that one, mostly autofocus. Simplicity, I don't know if some of you did. Other types of tasks, good to you. However, in general, the important part was the transmission. So in this case, the first thing that we have to do is, of course, put together all of the pins of the peripheral that I'm interested in. So in my case, I get to enable both the pins for the keyboard, so the four inputs and the four outputs. Then I also enable the SPI, just like the last time, because I'm going to pilot the LV matrix. And also, the different thing from the usual is going to be the UART1 line instead of the UART2 because I also enabled the UART2, but in this case I enabled the UART1 because I'm going to use it to receive data from my LED. Okay, so it's going to be just like a normal peripheral on the UART1. I think I prefer to show you the code mostly because I have a lot of peripherals enabled. So I'm going to show you the code and talk to you through the code, even though it's a bit of a complex code to explain, but I will try. Okay, so my task was to have, in my case, all of the letters of the keyboard codified in a way to send them out to the LED matrix. One thing that I did is I defined all types of matrices. Why? Because I want to have, of course, all of the characters embedded in an SPI manner so that I can send them out. to the matrix. This is an example, of course, you could have done anything with this. It's just to show you a way to do this, which is, of course, a lot of characters. And then I'm going to have the same code kind of as the last time. So I'm going to have the map of the chapters. I'm going to have the key press and the acknowledgement arrays, which are defined just like the same as the keyboard letters. OK, which is useful because I used to have to do all of the checks that I used to do in the past. OK, just because we're mixing together different homeworks, please remember that you have to maintain all of the checks. If I ask to use the microphone in my homework and going to a in-phone in your exam, you're going to have to do the bouncing correctly, OK, or the clearing of the flag or anything like that. So please keep in mind all of the things you've learned on the specific so that you can take them and put them together. In this case, I'm still going to have to do the same thing. So I'm still going to have to check the bouncing. and I'm going to check if the data has already been sent, so I don't send it again. In this case, it's not that useful because I'm not going to see multiple letters, I'm still going to see the same on the LED matrix, but I'm still going to check it so that I don't send out data to SPI uselessly. Okay, then one thing I do here is that I have this function which is going to actually copy some data, okay, from one part to a matrix. And this is just out of simplicity again. I have this rotation in which I have the character map which is copied inside of another matrix. Why do I do this? You remember, I think, from the past that I showed you, that it's better to do this copy of the matrix and only work on one matrix. Why? Because in that way I don't have to change my code every time. Because the name of the variable will always be the same. In this case I do this even more than usual, because when I receive a character, I'm going to have to change the matrix to be sent to the LED. But in that case I don't have like 16 cases of what I want to send. I'm always going to send the same thing. I will have a part of my code that when I receive a certain character is going to copy the specific character inside of the matrix that I send out. It's just the same that I did with that if else, but in this case I'm going to do it easily because I have a lot of things to do. And same for the letter to be shown. Okay, so I do kind of the same thing. I copy the matrix inside of the letter to be shown. Inside of my main code, what I do is I have my two timers. We will see why any two timers are already enabled. We can think about it. One of them will be for scanning the keyboard and or printing out the LED. And the other one could be, for example, I mean, one of them will be for the LED, one of them will be for the keyboard actually. We will need another timer, which will be a timer scanning the timing of the UART byte size based on the baud rate. because I need to actually turn on and off the BWM based on what is happening. And then I start out with a new word, receive, interrupt. Why? Because my code in particular ignores this, but it also can print out data from the UART tool. So I can also send data from a character from my keyboard. This is an additional thing that I did in my code. I do some things in the Y, we will see later what I do. But the first thing I do is, for example, Let's say, for example, I want to receive data from the UART. I will receive some data, but I don't want to show you that. I want to show you this one. And I will have some flags that we will see later. Sorry, it's a lot of functions. What I'm mostly interested in is this one, which is the timer period elapsed callback, which has, as you can see, a lot of different timers. First of all, this part of the code is exactly the same as last time for the key press. I just copied and pasted it. However, if you can see, there's something missing, which is the check on the validity of the things that I pressed. I do this in the while, which is what I skipped before, simply because I want to have fewer things in my interrupt of the timer, because as you can see, I have a lot of things. OK, so the part that you saw last time is here actually. OK, instead of being inside of the timer callback. It should still work in the timer callback. I just want to be sure that I put it here. So let's say I separate the two things, which is something that some of you did last time as well. Instead of sending out the data through the inter-viewart, I use this function that I built, which is a function that sends out one byte through the inter-viewart. Let's call it the inter-viewart. What I'm interested in is this function. This function is not that complicated. I start yet another timer in intrapod. Why? Because I want yet another timer that is going to go to one byte, from one bit to the next of the UART, correct? Because every bit has to have a certain duration based on the baud rate. And then I also start out the PWM. Why? Because I always have to send the start byte. The start byte is a zero. So that means that the LED is turned on. In particular, my PWM will have the frequency of a square wave with frequency duty cycle just as the ones that I showed you in the slides last time. So I have a certain PWM, instead of just simply turning on the LED, I turn on this PWM. It's not too complicated, but on Wednesday I think some people were not really, it was not really clear. So instead of simply doing a GPIO turn on, I turn on the PWM of the driver. I have this border-elapsed flag, which is a flag that I use. And you will see that this flag interacts between various things inside of my interact. In particular, I have this one, which is a global variable. So I can modify it outside. It's a global variable because I defined it so. I didn't define it inside of the interact. I defined it inside of my space outside of the main code. Why? Because in this way, multiple interacts can access it at the same time. You will say this is blocking because I'm doing a while it is zero, do nothing. So my code is stuck inside of this interrupt service routine. However, do you remember what happens if I get another interrupt at the same level of priority? This one is stopped and it goes inside of the other interrupt. So actually this while can be stopped. When is it stopped? When I have one bit, which is given to me by this timer, timer 10. And in fact, if you go here in timer 10, what it's doing is I start the timer. I don't know. Let's act as if every beat lasts one second. Okay. I'll make it simple. I start my timer. I start my PWM. After one second, I raise one flag, which is going to modify the value of Baudelap's flag. And so I get out of this cycle. The while is interrupted. Do you remember that you can have multiple interrupts with the same level? So it's it is blocking, but it's not truly blocking because I have another intracellular routine which accesses the same thing. So this process is paused, I do the other one, I send it to one. When I go back, this one is to one, so I leave the while cycle. So the while took the priority level of the fraction... In this case, yes, because it's not the alune, mind you. It doesn't have a priority while. Simply this code is stopped, I suppose, I do the other part, and then when the other part is done, I restart from the exact same moment. The same moment is I'm checking the value of all the last tracks. So this thing, we can do this thing only if we put while in another function, because if we put in the while, Exactly, yes. But I think maybe it could still work if you have an interrupt that is going to change the value. It could still work because the interrupt stops the CPU. Correct? You cannot do it with the L delay because the L delay is an interrupt of itself. So you cannot block the L delay function. So when you are counting something with the LDA, it is very different from a while, because the while it is the code running, it's doing an if forever, okay? Like it keeps checking. On the other hand, if I have the LDA, I cannot interrupt it, because if I stop it, it means I'm stopping the system clock, and I cannot stop the system clock. So just to show you, there are very different things. This one is some kind of counting, it's not a peripheral doing something, it is not an interrupt. So I can interrupt it and start again. I cannot interrupt the LPA and start again. That's something different. Okay? So what happens is that I leave this one. So finally I'm done with the start bit. I can go on with the sending of every bit. And to do this, if you might have understood that I'm supposed to do what? I'm supposed to actually add some checks with a mask, which is going to check for every bit of my diet. if it is a 0 or a 1, because I want to send out 0 PWM stays up, 1 stays down. And in my case, I simply start or stop the PWM. You could have done something even smarter and checking this next bit too. In that way, maybe you leave the PWM on for multiple bits. For example, if you have three zeros, you can leave it on for three zeros without doing the start and stop. That's just an idea. And I do the same. And I keep doing the same. until I'm done with my bits that I want to send. So what I'll do is I'll re-put the vote flag to zero for every bit that I'm supposed to send. The timer will be counting, so it will put it back to one when it's done. I go back here, I change bit, I turn on or off the PWM, I put it to zero and it's like a ping pong table. So you have on one side my interrupt timer, sorry my send UART let's say, is going to put it back to zero when I have a new bit and my timer is going to reset it when the bit is done. Is this clear? It's just one way. There are infinite ways, of course. This is an idea which is going to exploit the fact that we can have multiple interrupts. One that interrupts the other and then restarts again. Correct? Do you understand it? This is one way. When I'm done, I need to send the stop bit. The stop bit is a one. So that means the PWA will not be turned off. So I turn it off. I count yet another bit. And then I stop my timer because I'm done with the counting of the duration of the baud rate for every beat. So that timer is going to be stopped. I don't look at it anymore. Okay? Okay. Let me go back to where I was. Sorry. I need to find it again. Okay, okay. Okay, so I do this send byte. I do send the byte. On the other hand, I will have my UART being enabled and waiting. So when I'm done sending the byte, my UART will either receive something from the two or from the line two or line one. In my case, I will get something from line one. If I packaged correctly my bits and my start and the stop, at the stop, I will get this one. So I will receive the UART here. So I get to save it inside of this data. And in my case, I do have my value that I need to sign here. Okay? Give me just one second. I also put it back inside of the UART receive. What I want to show is over here. Oh my god, I got lost, sorry. Give me one second. Okay, on the other hand, I always have my LED matrix that keeps printing out something if actually, I mean, it has to keep printing out the data in this case, correct? I do not have to send out one character, like with the homework from last time. What did we do? We sent out the character that was done. In this case, I received my data and I sent again the UART in receiving trap mode. However, my LED matrix needs to keep being printed, so I have my timer, in particular timer 5, which keeps doing what we did last time from the LED matrix. So my timer 5, that's why I wasn't finding it, there is no actual flag that is going to enable it. It's always enabled from the main, because it keeps sending out data. Of course, until I receive my first character from the keyboard, nothing is going to be printed. In this case, I simply copied, if you remember, the code from the last time, in which I do have the enabling and disabling of the rclk pin, I increase or decrease my column index, and I have my transmitting DNA. And I'm going to send the two bytes referred to the character that I received. The things that changed in this case was this part related to they both have flags and they interrupt of the UART sending out the data, not really receiving because receiving is not going to do much, but it was mostly sending out the data. I know it's very confusing, I'm sorry, but it's a lot of interrupts and a lot of code, so it's difficult to actually explain it out loud. So if I wasn't clear on something, please tell me so I can actually re-explain it. Of course, this is not the only solution. What I wanted to show you instead is the the backer. Okay, I just want to show you, remind you mostly, because I've already shown you some of the functionalities and how this can actually help us find the errors. Mind you, the errors do not always show here because this one only shows you the errors related to the syntax on how you wrote the code. There's a semicolon missing, there's a missing paragraph, there's a missing variable inside of the function, I gave it an int instead of a float. These are the errors that show up here. If the code logic doesn't work, our software doesn't know it. So we will not see an error here. I'm saying this because I got some answers about this. So my code can be perfect from either side, but not work. And I'm going to show you how you can maybe, for example, figure out what you can do. First of all, you should remember that the little bug is actually the debugger. If I press it and you have to keep your board connected, what I'm going to do is I'm going to program the board, but instead of having the code running on its own, I'm going to be able to double click on the number of a row of my code, and that's going to allow me to stop the code execution at that point. For example, it always automatically puts a breakpoint, that's what they're called, on the "all init". My code right now is not doing anything, it's frozen. Okay? I post the execution of my code, it is frozen, but I can unfreeze it by pressing some buttons, which are over here. You have the play button, just like in music, and you have the stop. If I press the stop, everything is going to be stopped, the code execution, and I can restart it again, but it's going to stop everything. If I want to go to the next breakpoint, what I do is I press this one. And as you can see in this case, it goes directly. I put a key point here inside of my code that's checking my keyboard and it simply stops there. I can do this multiple times. And of course, what it's going to do in my case, I put one red point in each of my interrupts. What it's going to do is it's going to check my column. And as you will see, the light is on on the second column. Why? Because I'm checking the second column and I'm frozen inside of the check. But also what it's going to do is it keeps checking, of course, but also I don't do anything. So what changes here is I'm actually going through the values. And if you want to see what call I'm actually doing, looking at it, I can add some data here. In particular, here you have the variables. Some of them should already be automatically inserted. If I want to see a specific expression, for example, here, I want to see what is happening to my column index variable. Right now it's set to 3. It's a bit slow, but you will see. If I go to the next cycle, it should go back to 0 if my code is running correctly. Exactly. So it's cycling through my keyboard. 1, 2, 3. I'm not pressing anything, so nothing is happening. If I start pressing one button, something should happen. It's not happening. Oh no! My code is correct, but it's not working. So what do we do? For example, we can use this. What we understand is it's not going inside of the interrupt of my keyboard. It's not going to do anything. It's not going to go in here, for example. What I would like to do is I want the key press to actually change. If I were to put the key press there, I would see it's changing. It is running through my interrupt. Where is it not going, my code? Well, I put-- first of all, it's not receiving anything. OK. So could it be that I didn't enable something? Could be. It's not going at all inside of my interrupt, but I did press and release. So why is it not going inside? This is a suggestion, for example, of my code that it's not looking, the UART interrupt is not being looked at, for example. Mind you that you can also check very complex expressions. So if I were to copy the whole row here, okay, for example, this whole row, I will be able to check what is happening to this value. So I can copy this one and put it inside of the expression and I'm able to check if also if my complex computations that I did are correct. Why this? Because maybe I'm not simply accessing an array with an index and doing some computations like here. I want to check what is happening. So I can use this one. But also for example, I can do multiple things here and I can simply take them and see what happens. I can also put this one back, this one, this whole expression, I can put it inside there and see what's happening. I know, of course, this is a very dumb example that I made you. What is going on here, I'm not going inside of the timer related to, I'm going inside of the timer related to the keyboard, I'm not going inside of the UART, but I did enable the UART. Yes, I did it in the main, so I did, the code is correct. What could be incorrect is, for example, very simply, I did not enable the interrupt. Again, I know this is very dumb, but in this case, for example, if I'm not enabling the interrupt, it's not going to go inside of the interrupt, so you are going to see. So maybe I am sending out data and if you do a more complex and complete debug, I'm not going to do it because it could take hours to do this, if you're very thorough. But an idea is you should figure out, check everything, every step of your code is working correctly. In my case, let's act as if I checked everything, everything is working. The only thing that is not going inside is the UART1 interrupt. That means that the UART1 interrupt is not enabled somehow, either via code or by MVIC. In this case, I reveal the code and we will be able to see, of course, here it's going to remake the code, so everything should work now. If I do go back in the debugger mode, we will see that it should go inside of the interrupt. Of course, you never know because this is all live. Okay, again, the same is happening. So one, two, three, four. Why it's not going now? Okay, amazing. It's not working for some reason. I checked it 10 minutes ago and it was 30 minutes ago. Anyway, this is one way. It should go inside of the Intel, I don't know why. I went there and checked the code and it was. So I'm going to do it again. I'm sorry about this, but you know the code never does what you want it to do. Okay, now it should go. If you see, I pressed a letter and it printed it out, so it should work. In general, mind you that of course the debugger is very useful because you are able to understand what is happening and where. I don't know why it's not working in the debugger now. Maybe I take this one out. Okay. Of course, since we are going to look at timings, what happens is that if I interrupt my sending out of the data during, right, with the debugger, for example, What happens is that I'm delaying the data being sent out via UART. So this one will not receive the data correctly. I don't know if you understood it, but the point is when I'm doing some time sensitive applications, the debugger can help me figure out where the error is, but then maybe the code is not running out of time issues. Because if I'm stopping for one whole second during the bit transmission, the UART will not see it as a bit. Anyway, now it does work. Okay, now it did go through the receive, as you can see. When I press a button, it goes to the receive function. Because I'm not interrupting anything, it's waiting, now my code is running. Okay, it printed out a seven because I did something. If I press something else, of course it stops because my code is stopped. So I do not see anything printed on my LV matrix. Why? Because everything is stopping. So it stopped when I printed out this column by chance. However, if I print it out again, I could get the correct letter because I interrupted my running of the code. This helps not really to check the peripheral working, it helps to see where the code is going and where the code isn't going. You say, I'm not receiving anything on my terminal. But is it because it's not sending? Is it because the timer is not running? Or is it because I'm not receiving? Again, it is difficult to explain physically without being made in a little group, but if you have questions about the debugger, you can ask during this class as well, me and Ilania, because it's fundamental in general for when you write code, but also for coding software. I mean, Python has a debugger and it works exactly the same. If any of you have used Python, I think you will know how it works. Questions? Doubts? Please use the debugger in your life because it's fundamental. Or at least try to get practical with it. Here, as I was, I just want to show you some other things about in general. Let's say that here, some variables appear automatically when you're running the code based on where you put the breakpoints. So it's actually like the value of the variable. The expressions is computations. So for example, accessing a register, having an index, some divisions or something like that. Another thing is the breakpoint stops before executing that line. So if I want to see if the UART is receiving, I should put the breakpoint in the next one. However, in this case, the command variable has not been updated yet. If I want to see the command variable, I should put it here, for example. So always put it if you want to see if something works on it. next line compared to that one. Also, when you're in debug mode, if you float with your mouse on some values, it will show you, right now not in debugger mode, but if, for example, let me do this, if you float over the variables, it will show you the data, the details. So, for example, I can see that rx_by has a d value. Why? Because I pressed the d button. Another thing that is useful, it shows you in all of the types of the decimal, the hexadecimal and the binary. Why is the binary useful? Because in this case, for example, I can check if I brought the register correctly in a sensor, which is fundamental. I know this was just a lot of things that I don't know what is happening. It's not moving. No, it's not me. I don't know. Someone at home probably. Doubts about this specifically? How many of you have never used a debugger? Not out of shame, but out of knowing how to use it. I don't know how you manage to complete the homework, I'll be honest. Okay, so I think I can stop the recording here. Thank you
