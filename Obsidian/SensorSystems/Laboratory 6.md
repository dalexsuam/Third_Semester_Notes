
20/10/2025
***

# <span style="color:rgb(223, 109, 109)">Project 6a: Objective of the project is to acquire 3 voltages (potentiometer, temperature sensor, Vref) every 1 s and to send them to a remote terminal. The acquisition are started via hardware by a timer and data are saved in the microcontroller memory using DMA.</span>

![[Pasted image 20251020151137.png]]


| ![[Pasted image 20251020151257.png]] | The TSVREFE bit must be set to enable the conversion of both internal channels: the ADC1_IN16 or ADC1_IN18 (temperature sensor) and the ADC1_IN17 (VREFINT). |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
![[Pasted image 20251020151548.png]]

![[Pasted image 20251020151819.png]]

![[Pasted image 20251020151948.png]]

Also set parameter baud rate at 9600 bit/s

![[Pasted image 20251020152108.png]]