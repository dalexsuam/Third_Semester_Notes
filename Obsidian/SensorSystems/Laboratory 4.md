
# <span style="color:rgb(223, 109, 109)">Universal Synchronous and Asynchronous Receiver-Transmitter (USART)</span> 

The **USART** is a **serial interface device** that can be programmed to communicate in either **synchronous** or **asynchronous** mode.
In simple terms, it allows **serial communication** between a microcontroller (like the STM32 board) and another device, such as a computer.

- **Synchronous communication** uses a **shared clock line** between the two devices. The data transfer happens in sync with this clock signal, ensuring that both devices operate in perfect timing.
- **Asynchronous communication**, on the other hand, does **not use a shared clock**. Instead, both devices must **agree beforehand** on the communication parameters — for example, the **baud rate**, which defines how fast data is transmitted. This ensures that each side interprets the data correctly even without a common clock.

Although most modern computers **no longer have physical USART ports**, the protocol can be **emulated via a COM port** over **USB**. When you connect your STM32 board, you can check the **Device Manager** under the **Ports (COM & LPT)** section to find the virtual COM port assigned to your device.

## <span style="color:rgb(239, 179, 1)">Working Principle</span>

![[Pasted image 20251011162735.png]]

The **USART** is very simple to understand. It uses **two main lines** — one for **transmitting (TX)** and one for **receiving (RX)**. For the other device, these two lines are **swapped**, since what one sends, the other receives. Both devices must also share a **common ground**, which is always required for proper communication.

Because there is **no shared clock line**, both sides must **agree on the communication parameters** — mainly the **baud rate** and the **frame format**. This configuration must be set **both on the STM32** and **on the receiving side** (for instance, the computer’s COM port). The settings ensure that both devices interpret the transmitted data correctly.

Data is sent **serially**, meaning **bit by bit** in a sequence, grouped into **frames (or packages)**.

![[Pasted image 20251011162826.png]]

Each frame starts with an **idle line**, followed by a **start bit**, then the **data bits**, and finally a **stop bit**. These special bits mark where the data begins and ends. The UART hardware automatically adds these bits — you don’t need to handle them manually.

You can configure the **number of data bits** per frame and, optionally, include a **parity bit** for **error detection**.

- In **even parity**, the parity bit is set to 1 if the number of 1s in the data is even.
- In **odd parity**, it’s set to 1 if the number of 1s is odd.
    
This simple check helps detect transmission errors — though it’s not perfect, it provides basic protection against corrupted data.

All these options (baud rate, data bits, stop bits, and parity) can be adjusted in the **CubeMX IOC configuration**.

That’s essentially all there is to UART communication — a straightforward and widely used protocol for reliable serial data transfer.

## <span style="color:rgb(239, 179, 1)">UART HAL Functions</span>

The **HAL library** provides several functions to handle UART communication. The main ones are quite intuitive — they allow us to **send** and **receive** data packages through the microcontroller.

The **basic functions** are:

```c
HAL_StatusTypeDef HAL_UART_Receive(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint32_t Timeout);
HAL_StatusTypeDef HAL_UART_Transmit(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint32_t Timeout);
HAL_StatusTypeDef HAL_UARTEx_ReceiveToIdle(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint16_t *RxLen, uint32_t Timeout);
```

- `HAL_UART_Transmit()` sends data to another device.
- `HAL_UART_Receive()` receives data from another device.
- `HAL_UARTEx_ReceiveToIdle()` waits to receive data until an idle period occurs, meaning no data is being transmitted for a while.

For each of these, we must specify:

- **Which UART** we are using (`UART1` or `UART2`).
- A **pointer to the data** we want to send or store.
- The **size** of that data.
- A **timeout**, which defines how long to wait before returning an error if no response is received.
    
Every HAL function returns a **status type** that helps us verify if it worked correctly. If the function returns `HAL_OK`, it means the communication succeeded. This convention is consistent across most HAL functions in STM32.

If you want to handle UART communication more efficiently, you can use **DMA (Direct Memory Access)** versions of these functions. DMA transfers data directly between peripherals and memory, freeing the CPU from handling each byte.

```c
HAL_StatusTypeDef HAL_UART_Receive_DMA(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size);
HAL_StatusTypeDef HAL_UART_Transmit_DMA(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size);
```

In short, UART communication in STM32 is simple to use thanks to HAL — and DMA can make it even faster and more efficient.

# <span style="color:rgb(223, 109, 109)">Liquid Crystal Display - LCD</span>
![[Pasted image 20251011164401.png]]  

Here we can see the **LCD**, which I’m sure all of you can easily spot on your board — it’s the large rectangular component located right here.

![[Pasted image 20251011164423.png]]


**LCD** stands for **Liquid Crystal Display**. As the name suggests, it works using _liquid crystals_, special materials that can change their orientation when an electric field is applied.

The key idea is that the orientation of these crystals determines whether light can pass through the display or not.

- When the LCD is **off**, the crystals are arranged so that light **cannot** pass through — the display looks dark.
- When the LCD is **on**, the crystals align in a way that allows light to **pass through**, making the displayed characters visible.
    

So, by controlling how these crystals are polarized, the LCD can show or hide light in specific regions, forming numbers, letters, or symbols on the screen.

| Segments Display                     | Dots Matrix                          |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251011164552.png]] | ![[Pasted image 20251011164605.png]] |

The simplest type of LCDs are **segment displays**, which are quite common but somewhat old-fashioned. Our board, however, uses a **dot matrix display**.

Unlike segment displays, which light up predefined segments to form numbers or characters, the dot matrix display works by turning on individual **dots** in a grid. On our Polimi expansion board, for example, the characters you see on the screen are formed by selectively activating these tiny dots, based on the voltages applied to the crystals in each position.


![[Pasted image 20251011164634.png]]

Here’s a schematic example of how the LCD is connected — you also have the full file to check in detail. On our board:

- **RS (Register Select):** Configures the LCD mode.
- **E (Enable):** Signals whether the LCD is active.
- **Four data lines:** Send the actual data to be displayed.
- **BL_ON:** Controls the backlight.

When we enable the LCD and the backlight, the selected dots light up to show the numbers or characters.

![[Pasted image 20251011164756.png]]

More details about the LCD can be found in the datasheet in the WeeBeep documentation folder. It’s a full datasheet, so you can refer to it for all technical details. As we saw, the LCD pins can be used to **read**, **write**, or **enable** signals, and the bus lines correspond to the data pins we discussed earlier. 

![[Pasted image 20251011164903.png]]
Again, same.

![[Pasted image 20251011164922.png]]

So, how do we actually display characters on the LCD? Each character is stored in a **character generator ROM (Read-Only Memory)**. The ROM contains all the predefined characters. Importantly, the memory addresses are mapped to **ASCII codes**, meaning that the ASCII value of a character directly corresponds to the location in ROM. This makes it easy to write characters without manually looking up addresses in the datasheet.

![[Pasted image 20251011165021.png]]

The character data from the ROM is written into the **display RAM**, which controls what is actually shown on the screen. You read the character data from the ROM address you need and store it in RAM.

There is also a **character generator RAM**, which allows you to define **up to 8 custom characters** in the standard 5×8 dot matrix. This RAM is **volatile**, so custom characters are lost when the LCD is powered off.


![[Pasted image 20251011165145.png]]


To write characters, you specify the RAM address and then shift the data for subsequent characters. This lets you write **multiple characters sequentially**.

![[Pasted image 20251011165214.png]]

Each operation involves several steps, so initializing the LCD and performing tasks like clearing the display can take **more than one millisecond**. These are not instant operations and require multiple instructions.

![[Pasted image 20251011165145.png]]

As you can see, every LCD operation—like clearing the display—takes some time, usually **more than one millisecond**. These are not instant processes, as the LCD requires several steps to execute each command.

```c#
void lcd_initialize(); 
void lcd_backlight_ON(); 
void lcd_backlight_OFF(); //Initializes the LCD controller. Turns ON(OFF) the LCD backlight. 
void lcd_println(char string[], uint8_t row); //Prints the string on the top (0) or bottom (1) row of the LCD. Maximum string length = 16 characters. 

void lcd_drawBar(int value); //Prints a bargraph on the bottom row of the LCD controller. Value range: 0 to 80. Each increment corresponds to enabling one extra column of the dot matrix display. 
void lcd_clear(); Clears the entire display
```
To simplify all these operations, you already have **two pre-made libraries** available on **WeeBeep**. These provide **high-level functions** that handle all the initialization and communication steps automatically.

- **`lcd_initialize()`** prepares the LCD for use.
- **`lcd_backlight_ON()` / `lcd_backlight_OFF()`** control the screen’s illumination.
- **`lcd_println()`** displays text on either of the two available lines.
- **`lcd_drawBar()`** shows a bar graph, useful for representing values visually.
- **`lcd_clear()`** resets the display.


![[Pasted image 20251011165606.png]]

Finally, make sure that in your **IOC file**, all the necessary pins for the LCD are properly enabled so the communication works correctly.

---
---
---
---
---

# <span style="color:rgb(223, 109, 109)">Project 4a: Send information using USART interface</span>

The objective of this project is send information from the microcontroller to the PC, using the USART interface for the Virtual COM. You will send a string containing your name and your year of birth followed by a new line every second. We will use a terminal emulator (Arduino IDE, Vscode, Putty) to receive the string.

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">USART pins Enabled: </span>Before running the code, make sure that the **two USART pins** are **enabled** in your IOC configuration file to ensure proper communication.
![[Pasted image 20251006130522.png]]
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Set baud rate:</span> Since the communication is **asynchronous**, there is **no shared clock line** between the devices. For this reason, you must **set and match the baud rate** between the microcontroller and the **terminal emulator** (for example, **Arduino IDE**, **VS Code**, or **PuTTY**) to ensure proper data transmission.

![[Pasted image 20251006130716.png]]

3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Identify the COM port:</span> We also need to **identify the COM port** assigned to our **STM board** on the computer — this is the port the terminal emulator will use to receive the transmitted data.

![[Pasted image 20251006131027.png]]

4. <span style="font-weight:bold; color:rgb(161, 40, 226)">Write the code:</span>
To correctly create the **data string** that will be sent from the microcontroller to the PC, we can use the `snprintf()` function.  This function allows us to **format multiple variables** into a single string before transmission

For example:
```C#
int length = snprintf(string, sizeof(string), "%.3f\n", voltage);
HAL_UART_Transmit(&huart2, string, lenght, 100);

int length = snprintf(string, sizeof(string), "%.3f, %.3f\n", voltage, voltage2);
HAL_UART_Transmit(&huart2, string, lenght, 100);
```

In our specific case, we can build a simple string containing **our name** and **date of birth**, and then send it every second through the UART interface:
```C#
//I put this in the void Init after the init of the USART 
char string[100];
char Name[] = "Diego";
char DOB[]= "07.05.2001";

int length = snprintf(string, sizeof(string), "%s, %s \r \n",Name, DOB);
/// `string = "Diego, 07.05.2001\n"`

while (1)

{

HAL_UART_Transmit(&huart2, string, length, 100); //100 is the timeout of the message sent or give back error
HAL_Delay(1000);
/* USER CODE BEGIN 3 */
}
```

This simple program will **continuously send** the formatted message through the **USART2 interface** every second, which can be visualized on the **terminal emulator** once the correct **COM port** and **baud rate** are set.
![[Pasted image 20251007182455.png]]

***
***
***
***
***

# <span style="color:rgb(223, 109, 109)">Homework 4</span>

## <span style="color:rgb(239, 179, 1)">Homework 4a</span>
Complete the UART project with DMA, as in slide 10 of pack 06. Tip: enable the global interrupt for the UART!

>[!tip] _Tip:_ remember to **enable the global interrupt** for the UART!

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Activate the USART RX and TX pins: </span> We activate the pins with USART RX and USART TX
![[Pasted image 20251007182952.png]]

2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Set baud rate:</span> We go to connectivity and select USART2 and set the baud rate that must match with our serial port since it is an unsynchronous communication.
![[Pasted image 20251006130716.png]]


3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Open DMA settings:</span> We enter to DMA settings, add USART2_TX and set high priority

![[Pasted image 20251007183253.png]]

4. <span style="font-weight:bold; color:rgb(161, 40, 226)">Enable USART2 Global interrupt:</span> We activate the USART2 global interrupt in the NVIC. Why?
In the description of the code says that it is used to set the last byte sending completion detection in DMA non circular mode. In short: **we enable the global interrupt so the DMA (Direct Memory Access) can “talk back” to the microcontroller once it finishes sending data.**


![[Pasted image 20251007182837.png]]

5. <span style="font-weight:bold; color:rgb(161, 40, 226)">Set out timer in interrupt mode:</span> Since we would like to send information every 1s, it is always a good practice to avoid the `HAL_Delay()`. We set the pre-scaler and ARR with those values since we're aiming an interrupt every 1s, thus a frequency of 1Hz.
![[Pasted image 20251017163421.png]]

And we shouldn't forget also to turn on its interrupt in the NVIC settings.
![[Pasted image 20251017163557.png]]

6.  <span style="font-weight:bold; color:rgb(161, 40, 226)">Write the code</span> 

Don't forget to include the following libraries to avoid errors or warnings. Also, we define our variables as global variables
``` c#
#include "stdio.h"
#include "string.h"

//As global variables
char string[100];
char Name[] = "Diego";
char DOB[] = "07.05.2001";
/* USER CODE END 2 */
```

```C#
//We start the timer in interrupt mode in the main
HAL_TIM_Base_Start_IT(&htim2);
```

~~~ C#

//We define our timer interruption routine 
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim==&htim2){
		int length = snprintf(string, sizeof(string), "%s, %s \r \n", Name, DOB);
		HAL_UART_Transmit_DMA(&huart2, string, length); // NO TIMEOUT NEEDED
		}
}

~~~

However, the communication is slow, it takes place every 1s. For faster communications we would like to know if the message has been sent, or if it is done in order to send the following information.
![[Pasted image 20251017165744.png]]

If we delve into the IRQ of the USART2 in the it.c file we might find the collection of the UART functions. 

We see in part 3 we have some with the word `Callback` in their definition as.

~~~C#
HAL_UART_TxCpltCallback(UART_HandleTypeDef *huart) //It is going to let us know when our transmission is done. 
~~~

We can take a flag and make it 0 when the communication is starting and when the interrupt `TxCpltCallback` is called, we change the flag to 1. Hence, we enable availability of the channel, and when we want to start a new communication we set the flag again to 0. 

~~~C#
HAL_UART_GetState(const UART_HandleTypeDef *huart) // It will give us the state of the UART as a HAL_State something. HAL_Error, HAL_Busy, HAL_Ok
~~~

When `HAL_Ok` it means we can send some data 
## <span style="color:rgb(239, 179, 1)">Homework 4b</span>

Write on the LCD the name of each member of your group, one per line, in alphabetical order. Scroll every one second such as indicated below:
![[Pasted image 20251007184855.png]]

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Import the LCD library files</span>
We need to import the **LCD driver files** into our project to use the LCD functions.

- Copy the files **PMDB16_LCD.c** and **PMDB16_LCD.h**    
- Place them inside the following folders:
    - `PMDB16_LCD.c` → in **Src**
    - `PMDB16_LCD.h` → in **Inc**

2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Configure the LCD pins in the IOC file</span> Make sure to enable and configure all the **LCD pins** (RS, E, D4–D7, and DL_ON) correctly in your **.ioc** configuration file, so the microcontroller can communicate properly with the display.
![[Pasted image 20251007222104.png]]
3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Set out timer in interrupt mode:</span> Since we would like to display information in the LCD every 1s, it is always a good practice to avoid the `HAL_Delay()`. We set the pre-scaler and ARR with those values since we're aiming an interrupt every 1s, thus a frequency of 1Hz.
![[Pasted image 20251017163421.png]]

And we shouldn't forget also to turn on its interrupt in the NVIC settings.
![[Pasted image 20251017163557.png]]

4. <span style="font-weight:bold; color:rgb(161, 40, 226)">Initialize the LCD</span>
Before printing anything, we must initialize the LCD and turn on its backlight using the provided library functions:


``` C#
//Declare as global variables
int index = 0;
char names[5][10]= {"Diego", "Luis", "Pedro", "Rodrigo", "Mohanesh"}; //5 limits the number of elements, 10 the number of characters per element.


int main(void){
//we initialize timer 2 as interrupt
HAL_TIM_Base_Start_IT(&htim2);
//we initialize the LCD
lcd_initialize();
lcd_backlight_ON();
int index = 0;

	while(1){
	}
}

//define IRQ of timer 2 every 1 second

void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	index++;
	if (htim==&htim2){
		lcd_println(names[index-1],0);
		
		if(index%5==0){
			index=0;
		}
		
		lcd_println(names[index],1);
	}
}


```