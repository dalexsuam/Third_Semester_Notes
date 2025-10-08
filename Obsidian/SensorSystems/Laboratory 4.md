
# <span style="color:rgb(223, 109, 109)">Universal Synchronous and Asynchronous Receiver-Transmitter (USART)</span> 
There are many HAL functions for UART. Basics functions: 

``` C#
HAL_StatusTypeDef HAL_UART_Receive(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint32_t Timeout) 
HAL_StatusTypeDef HAL_UART_Transmit(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint32_t Timeout) 
HAL_StatusTypeDef HAL_UARTEx_ReceiveToIdle(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size, uint16_t *RxLen, uint32_t Timeout) 
```

Direct Memory Access functions:
```c# 
 HAL_StatusTypeDef HAL_UART_Receive_DMA(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size) 
 HAL_StatusTypeDef HAL_UART_Transmit_DMA(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size)
```
---
---
---
---
---

# <span style="color:rgb(223, 109, 109)">Project 4a: Send information using USART interface</span>

The objective of this project is send information from the microcontroller to the PC, using the USART interface for the Virtual COM. You will send a string containing your name and your year of birth followed by a new line every second. We will use a terminal emulator (Arduino IDE, Vscode, Putty) to receive the string.

Check that the two pins for USART are enabled
![[Pasted image 20251006130522.png]]

Since it is asynchronous, we have to set and match the baud rate with the terminal emulator
![[Pasted image 20251006130716.png]]

We identify the port of our STM board :)

![[Pasted image 20251006131027.png]]

To correctly create the data to be sent to the PC, use the snprintf function to generate a string. • Example:

```C#
int length = snprintf(string, sizeof(string), "%.3f\n", voltage);
HAL_UART_Transmit(&huart2, string, lenght, 100);

int length = snprintf(string, sizeof(string), "%.3f, %.3f\n", voltage, voltage2);
HAL_UART_Transmit(&huart2, string, lenght, 100);
```


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


![[Pasted image 20251007182455.png]]


# <span style="color:rgb(223, 109, 109)">Homework 4</span>

## <span style="color:rgb(239, 179, 1)">Homework 4a</span>
Complete the UART project with DMA, as in slide 10 of pack 06. Tip: enable the global interrupt for the UART!

1. We activate the pins with USART RX and USART TX

![[Pasted image 20251007182952.png]]
1. We go to connectivity and select USART2 and set the baud rate that must match with our serial port since it is an unsynchronous communication.
![[Pasted image 20251007182911.png]]
2. We enter to DMA settings, add USART2_TX and set high priority
![[Pasted image 20251007183253.png]]

3. We activate the USART2 global interrupt in the NVIC (idk why)
![[Pasted image 20251007182837.png]]
4. we program
~~~ C#
//Same procedure!!
char string[100];
char Name[] = "Diego";
char DOB[] = "07.05.2001";
/* USER CODE END 2 */
int length = snprintf(string, sizeof(string), "%s, %s \r \n", Name, DOB);
/* Infinite loop */
/* USER CODE BEGIN WHILE */

while (1)

{

/* USER CODE END WHILE */

HAL_UART_Transmit_DMA(&huart2, string, length); // NO TIMEOUT NEEDED
HAL_Delay(1000);

/* USER CODE BEGIN 3 */

}
~~~
## <span style="color:rgb(239, 179, 1)">Homework 4b</span>

Write on the LCD the name of each member of your group, one per line, in alphabetical order. Scroll every one second such as indicated below:

![[Pasted image 20251007222104.png]]
Remember we have to import the files PMDB16_LCD.c and PMDB16_LCD.h in the folders Inc and Src.

![[Pasted image 20251007184855.png]]
``` C#
int main(void){

char *names[]={"Diego", "Luis", "Rodrigo", "Mohanesh"};; // stores the group members in **alphabetical order**.
int total_names = sizeof(names)/ sizeof(names[0]);

lcd_initialize();
lcd_backlight_ON();
int index = 0;

}
while(1){
	lcd_clear(); // clears the display before printing the next two names.
// Print first name on row 0
	lcd_println(names[index], 0); // prints one line at a time (`row = 0` for top, `row = 1` for bottom).

// Print second name on row 1 (if it exists)
	if (index + 1 < total_names){
	    lcd_println(names[index + 1], 1);} //  prints one line at a time (`row = 0` for top, `row = 1` for bottom).

    // Wait 1 second
	HAL_Delay(1000);//After showing two names, the code waits 1 second and moves to the next pair.

    // Move to next pair
    index += 2;
    if (index >= total_names)
        index = 0;  // restart from beginning
    }
}

```