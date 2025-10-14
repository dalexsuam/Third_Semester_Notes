
13/10/2025
***


***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 5a: ADC single acquisition - polling</span> 

Objective of this project is to acquire the voltage of the potentiometer every 1 second and send this value to a remote terminal. The ADC will be used in polling mode

1. Set the GPIO connected to the potentiometer as an analog input and configure the ADC to acquire one value from that channel, triggered by software. Set the sampling time to 480 clock cycles.

![[Pasted image 20251013152410.png]]
![[Pasted image 20251013155219.png]]
Analog input of PA1 for potentiometer and USART TX and RX
![[Pasted image 20251013153103.png]]
480 clock cycles sampling time

2. Generate the c code.
3. Modify the code to acquire a value every 1 second
4. Convert the ADC value into a voltage.
5. Send the value to the remote terminal.
6. Debug the project.