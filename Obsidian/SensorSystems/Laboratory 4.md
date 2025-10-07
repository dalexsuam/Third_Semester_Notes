
# <span style="color:rgb(223, 109, 109)">Universal Synchronous and Asynchronous Receiver-Transmitter (USART)</span> 

---
---
---
---
---
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
