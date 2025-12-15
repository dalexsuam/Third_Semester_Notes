# <span style="color:rgb(223, 109, 109)">Projects in Class</span>

## <span style="color:rgb(239, 179, 1)">Project 2a: Pushbutton - polling</span> $->$ [[Laboratory 2]]
Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. A polling operation will be used to monitor the state of the pushbutton.
## <span style="color:rgb(239, 179, 1)">Project 2b: Pushbutton - Interrupt</span> $->$ [[Laboratory 2]]
Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. The pushbutton input will be used in interrupt mode
## <span style="color:rgb(239, 179, 1)">Project 3a: Play note through speaker</span> $->$ [[Laboratory 3]]
Objective of this project is to play a tone for 3 seconds using the speaker, using a PWM.
## <span style="color:rgb(239, 179, 1)">Project 3b: Play a song through speaker</span> $->$ [[Laboratory 3]]
Objective of this project is to play a tone for 3 seconds using the speaker, using a PWM.
## <span style="color:rgb(239, 179, 1)">Project 4a: Send information using USART interface</span> $->$ [[Laboratory 4]]
The objective of this project is send information from the microcontroller to the PC, using the USART interface for the Virtual COM. You will send a string containing your name and your year of birth followed by a new line every second. We will use a terminal emulator (Arduino IDE, Vscode, Putty) to receive the string.

## <span style="color:rgb(239, 179, 1)">Project 5a: ADC single acquisition - Polling</span> $->$ [[Laboratory 5]]
The goal of this project is to measure the voltage coming from a potentiometer once every second and send that value to a remote terminal using UART. In this case, the ADC operates in **polling mode**, meaning the CPU manually waits for the conversion to finish.
## <span style="color:rgb(239, 179, 1)">Project 5b: ADC single acquisition - Interrupt</span> $->$ [[Laboratory 5]]

In this project, we perform the same single conversion, but instead of polling we use **interrupt mode**. This means that the CPU does _not_ wait for the conversion to finish.  Instead, the ADC triggers an interrupt automatically when the conversion is complete, and a callback function is executed.
## <span style="color:rgb(239, 179, 1)">Project 6a: ADC with DMA and Timer Trigger</span> -> [[VirtualModelling/Lecture 6|Lecture 6]]

**Objective:**  Acquire **three voltages**—
1. Potentiometer (external analog input)
2. Internal temperature sensor
3. VREFINT (internal reference voltage)
…every **1 second**, using:
- **Hardware triggering** of the ADC by **Timer 2**
- **DMA** to automatically transfer all conversion results into memory.
- **UART** to send the measured values to a remote terminal.

The ADC must perform **3 consecutive conversions**, and DMA stores all results in an array.

# <span style="color:rgb(223, 109, 109)">Homework</span>
## <span style="color:rgb(239, 179, 1)">Homework 2a: Toggle led with Snap</span>  $->$[[Laboratory 2]]
Modify the status (switch on / off) of the NUCLEO green LED, every time you snap your fingers.(Use the pin connected to the microphone as an External Interrupt) Debouncing implementation cos the microphone doesn't have a filter :)

## <span style="color:rgb(239, 179, 1)">Homework 2b: Blink LED at certain freq using PWM on its channel</span> $->$ [[Laboratory 2]]
Make the NUCLEO green LED blink at a 1 Hz rate using PWM generation on the corresponding channel.

## <span style="color:rgb(239, 179, 1)">Homework 3a: Play a song using speaker -triggered by mic - Timer (instead of HAL_Delay)</span> $->$ [[Laboratory 3]]
Objective of this project is to play a song using the speaker when the microphone detects a loud sound

## <span style="color:rgb(239, 179, 1)">Homework 4a: Send Information using DMA interface</span> $->$ [[Laboratory 4]]
The objective of this project is send information from the microcontroller to the PC, using the USART interface for the Virtual COM. You will send a string containing your name and your year of birth followed by a new line every second. We will use a terminal emulator (Arduino IDE, Vscode, Putty) to receive the string. project with DMA

## <span style="color:rgb(239, 179, 1)">Homework 4b: Display names of group in LCD every second as shown in pattern</span> $->$ [[Laboratory 4]]
Write on the LCD the name of each member of your group, one per line, in alphabetical order. Scroll every one second such as indicated below:
![[Pasted image 20251007184855.png|300]]


## <span style="color:rgb(239, 179, 1)">Homework 5a: Try to send data from the PC via UART a string of variable length that is displayed on the LCD. </span> $->$ [[Laboratory 5]]
The objective of this exercise is to send a string from the PC (via UART) and display that string on the LCD. The string can be of variable length, and the reception can be implemented in two different ways:
1. **Character-by-character using DMA**,
2. **Using “Receive-To-Idle” DMA**, which captures an entire message at once.

## <span style="color:rgb(239, 179, 1)">Homework 5b: ADC triggered by TIM. </span> $->$ [[Laboratory 5]]
In this exercise, the ADC conversion is not started manually or by an ADC interrupt. Instead, a timer generates a hardware trigger that starts each ADC conversion automatically. (Here we do it by means of the UART, however in lab 6 we do it with DMA)

## <span style="color:rgb(239, 179, 1)">Homework 5c: ADC triggered by TIM -Displayed LCD</span> $->$ [[Laboratory 5]]

This exercise is identical to Homework 5b; however, instead of sending the voltage via UART, the value is printed on the LCD.
## <span style="color:rgb(239, 179, 1)">Homework 6a: ADC scan using DM</span> $->$ [[Laboratory 6]]
The task is to acquire **one ADC sample every 1 ms**, store them using **DMA**, and every **1 second** compute the average of the latest 1000 samples.  
This average is converted into:

1. **Voltage**
2. **LDR resistance**
3. **Light level in lux**

Finally, the result is sent via **UART**.