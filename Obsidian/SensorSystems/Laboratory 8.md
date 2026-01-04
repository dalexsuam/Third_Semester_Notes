
03/11/2025
***

# <span style="color:rgb(223, 109, 109)">Accelerometer</span>

Today we focused on using an accelerometer, specifically reading data from it, not just a single measurement but multiple ones. This is because an accelerometer measures acceleration along multiple axes—in our case, three axes: X, Y, and Z. The accelerometer we are using is a MEMS accelerometer, which means it measures linear acceleration only. It doesn’t include a gyroscope, so it cannot measure angular velocity, just straight-line acceleration in three dimensions.

On the board, there can be two different types of sensors. This happens because the first sensor went out of production, and then the second one is also now discontinued. This is a common situation in electronics: when a sensor reaches the end of its lifecycle, a new compatible one must be used. Usually, the new sensor works similarly, but there can be small differences. In this case, the difference is the I2C address. Each sensor has an address, so when you communicate with it, the microcontroller can identify which sensor is responding. If you see an error when trying to read data, it usually means the sensor at that address isn’t responding.

![[Pasted image 20251123122901.png|500]]

To help identify sensors more reliably, there is a special register inside the sensor, commonly called "Who am I?" in ST devices. This register contains a predefined value that uniquely identifies the sensor model. So even if two sensors share the same I2C address, reading this register will tell you exactly which sensor you are talking to. This is especially useful if the board has multiple sensors that might have overlapping addresses. The microcontroller, acting as the I2C master, writes and reads data from the sensor using standard protocols. Writing involves sending the address of the target register and the data you want to write, while reading involves sending the register address and then retrieving its value.

An important feature of this accelerometer is the auto-increment function for multiple reads. Each axis—X, Y, Z—has its own memory space in the sensor. By enabling auto-increment, the sensor automatically moves from the X register to Y and then to Z, so the microcontroller can read all three axes in sequence without having to manually update the pointer each time. This is efficient and avoids extra communication steps. However, the memory addresses must be contiguous for this to work; you cannot skip addresses and still use the auto-increment function. This is especially helpful for sensors with multiple axes, as it allows reading multiple values in one operation.

![[Pasted image 20251123122511.png|400]]

The datasheet for this accelerometer is much larger than that of a simple temperature sensor. While a temperature sensor may have only a few registers, the accelerometer has dozens. This is because it supports more features and configurable options. ==One of the main configurable features is the full-scale range, which determines the maximum acceleration the sensor can measure==. You can set it from -2g to +2g, up to -16g to +16g, depending on your application. The choice of full-scale range affects resolution: the number of bits per measurement stays the same (for example, 8 bits per register), but if the range is smaller, each bit represents a smaller acceleration increment, giving higher resolution. For small-scale measurements, like wearable devices, a large range like ±16g is unnecessary. On the other hand, the sensor datasheet also provides other crucial information, such as sensitivity per scale, operating temperature range, pin descriptions, and ADC configuration.

![[Pasted image 20251123122602.png|400]]

The accelerometer has multiple communication options. Primarily, it uses I2C, and the datasheet includes details about the I2C protocol, including how to read and write registers. There is also support for SPI, which can be used in other projects. The sensor includes various modes, such as low-power mode, which may not be necessary for the current experiments but can be important in energy-constrained applications. 

![[Pasted image 20251123122937.png|400]]

The registers themselves are where most of the functionality lies. Control registers determine the sensor’s behavior. For example, Control Register 1 is used to set the data rate (how fast the sensor updates measurements) and which axes are enabled. By default, all registers are zeroed, which means the sensor is inactive until you configure it. 

![[Pasted image 20251123123040.png|400]]

Other control registers allow you to enable internal filtering, configure interrupts such as “data ready” signals, or other advanced functions.

![[Pasted image 20251123123132.png|300]]

The actual acceleration data is stored in specific registers, usually three: one for each axis. The values are stored in two’s complement format, so both positive and negative accelerations can be represented. When reading these registers, it’s important to remember the format, because interpreting the bits correctly is essential for getting accurate acceleration values.

Finally, the sensor may include a small internal temperature sensor, which isn’t needed for most acceleration measurements, but can be useful in some applications. Every chip has an internal ID register, like the "Who am I?" register, which helps identify the model. This is key when using multiple sensors or when troubleshooting. Overall, this accelerometer is more complex than a basic temperature sensor, offering many features, configurable settings, and multiple ways to read data efficiently.


***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">Project 8a: Read the acceleration measured by the accelerometer and send it to a remote terminal every 1 second</span>

![[Pasted image 20251027195344.png|500]]
To communicate with the accelerometer we use **I2C1**, exactly as we did for the temperature sensor. Nothing changes in the IOC except enabling **I2C1** and configuring **PB9 = SDA** and **PB8 = SCL**.

### <span style="color:rgb(161, 40, 226)">Understanding and Programming the Accelerometer</span>

Let me start again and show you the full solution.  Some of you were able to communicate with the sensor, and a few even read the _WHO_AM_I_ register. That’s great. But many of you got only zeros from the accelerometer.  This happens because **the sensor is not enabled by default**.  
We must **configure its control registers** before it outputs valid data.

#### <span style="color:rgb(2, 141, 192)">1. Sensor I2C Addresses</span>

We have two possible sensors, so we define both addresses:
~~~c#
uint8_t ACCEL_ADD = 0b01010000;
uint8_t LIS2DE12_ADD = 0b00110000; //ONLY USE THIS
~~~
Later, we will try one address; if communication fails, we switch to the other.

#### <span style="color:rgb(2, 141, 192)">2. Control Registers Configuration</span>

A convenient trick is to store each register address **together with the value you want to write**, inside a 2-byte array:

~~~c#
//reg address, 1Hz + Normal mode + XYZ enabled
uint8_t CTRL_REG1[] = {0x20, 0b00010111};
//reg address, No High Pass Filter (Default value at startup)
uint8_t CTRL_REG2[] = {0x21, 0b00000000};
//reg address, Continuous update + 2g FSR + Self test disabled (default)
uint8_t CTRL_REG4[] = {0x23, 0b00000000};
~~~

From the datasheet:
![[Pasted image 20251123131602.png|500]]
- In **CTRL_REG1**, we set:
    - Output Data Rate = 1 Hz → bit 4 = 1        
    - Enable X, Y, Z → bits 0–2 = 1
- In **CTRL_REG2** and **CTRL_REG4** we keep default values, but we still write them to be sure.

We also store the addresses of the output registers:

~~~c#
uint8_t OUT_X_ADD = 0x29;
uint8_t OUT_Y_ADD = 0x2B;
uint8_t OUT_Z_ADD = 0x2D;
~~~

#### <span style="color:rgb(2, 141, 192)">3. Detecting Which Accelerometer Is Installed</span>

In `main`, we find out which of the two possible sensors is on the board:
 ~~~c#
 char str[64];
 int len=0;
 
 
 if (HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG1, sizeof(CTRL_REG1), 50) == HAL_OK){
	 len = snprintf(str, sizeof(str), "LIS2DE found\r\n");
 } else{
	 ACCEL_ADD = LIS2DE12_ADD;
	 if(HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG1, sizeof(CTRL_REG1),50) == HAL_OK){
	 len = snprintf(str, sizeof(str), "LIS2DE12 found\r\n");
	 }
	 else{
	 len = snprintf(str, sizeof(str), "Accelerometer Error \n");
	 }
 }
 
 HAL_UART_Transmit(&huart2, str, len, 100);
 
 //These are not strictly nedeed, they are already set by default
 
 HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG2, sizeof(CTRL_REG2), 50);
 HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG4, sizeof(CTRL_REG4), 50);
 ~~~
Only **one** address will respond with `HAL_OK`.  If both fail, we report an error.

If you want an additional check, you may read the **WHO_AM_I** register, but this is optional.

#### <span style="color:rgb(2, 141, 192)">5. Reading the X, Y, Z Axes</span>

Inside the main loop:
~~~c#
while(1){
	//Get x
	int8_t acc_x = 0;
	HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, &OUT_X_ADD, 1, 50);
	HAL_I2C_Master_Receive(&hi2c1, ACCEL_ADD+1, &acc_x, 1, 50);
		
	//Get y
	int8_t acc_y = 0;
	HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, &OUT_Y_ADD, 1, 50);
	HAL_I2C_Master_Receive(&hi2c1, ACCEL_ADD+1, &acc_y, 1, 50);
	
	//Get z
	int8_t acc_z = 0;
	HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, &OUT_Z_ADD, 1, 50);
	HAL_I2C_Master_Receive(&hi2c1, ACCEL_ADD+1, &acc_z, 1, 50);
	
	//You can simply look at the dataset to understand the sensitivity or remember that the resolution is 8-bits
	float acc_g_x = acc_x/ 64.0;
	float acc_g_y = acc_y/ 64.0;
	float acc_g_z = acc_z/ 64.0;
	
	len = snprintf(str, sizeof(str), "X: %+.2f g\r\nY: %+.2f g\r\nZ: %+.2f g\r\n", acc_g_x, acc_g_y, acc_g_z);
	
	HAL_UART_Transmit(&huart2, str, len, 100);
	HAL_Delay(1000);
}
~~~
The `%+` in `%.2f` forces printing the sign (`+0.12 g`, `-0.03 g`, etc.).

***
***
***
***
***

# <span style="color:rgb(223, 109, 109)">Homework 8a: Read the acceleration measured by the accelerometer and send it to a remote terminal every 1 second. Using timer interrupts and UART DMA.</span>






# <span style="color:rgb(223, 109, 109)">Homework 8b: Read the acceleration measured by the accelerometer and send it to a remote terminal every 1 second. Using timer interrupts, I2C DMA and UART DMA.</span>

### <span style="color:rgb(161, 40, 226)">Hardware Setup</span>

![[Pasted image 20251123170824.png|500]]

First, for the I2C we have to enable it and set the SCL and SDA as we did for the temperature sensor.
![[Pasted image 20251123170904.png|500]]
Also, enabling TX and RX DMA for the I2C.

![[Pasted image 20251123180630.png|500]]
As well as its interrupt in the NVIC.

![[Pasted image 20251123183038.png|500]]
We also enable the DMA TX for the USART

![[Pasted image 20251123183054.png|500]]
As well as its interrupt.

![[Pasted image 20251123213439.png]]
And finally, we set our timer in 1Hz and enable its interrupt in the NVIC

![[Pasted image 20251123213424.png]]

### <span style="color:rgb(161, 40, 226)">Code and Explanations</span>

**1. Sensor Identification and Configuration Registers**
This code defines the possible I2C addresses for the two supported accelerometers and the configuration data to be written to its control registers to set it up for 1Hz output on all axes.

```c
uint8_t ACCEL_ADD = 0b01010000;
uint8_t LIS2DW_ADD = 0b00110000;

// 1Hz + XYZ Enabled
uint8_t CTRL_REG1[] = {0x20, 0b00010111};
//Reg address, no HPF, default value
uint8_t CTRL_REG2[] = {0x21, 0b00000000};
//reg address, continuous update +2g FSR + self test disabled
uint8_t CTRL_REG4[] = {0x23, 0b00000000};
```

*   **Explanation:** The code starts by defining the I2C addresses for two possible accelerometer models. It then prepares the data for three control registers (CTRL_REG1, CTRL_REG2, CTRL_REG4) that will be sent to the sensor to configure its data rate, enable axes, and set the full-scale range.


**2. Reading Strategy and Buffer Setup**

To efficiently read the acceleration data, the code uses the sensor's "auto-increment" feature and defines a buffer to hold the raw data bytes.

```c
uint8_t OUT_BASE_ADD_AUTOINCREMENT = 0x29 + 128;
int8_t RX_BUFFER[5];

uint8_t OUT_X_ADD = 0x29;
uint8_t OUT_Y_ADD = 0x2B;
uint8_t OUT_Z_ADD = 0x2D;

char str[64];
```

*   **Explanation:** The `OUT_BASE_ADD_AUTOINCREMENT` variable holds the address of the first output register (X-axis high byte, `0x29`) with the most significant bit set (by adding 128). This tells the sensor to automatically increment the register address on subsequent reads. The `RX_BUFFER` is a 5-byte array because reading starts at the X-high byte, and the sensor will return data for registers `0x29`, `0x2A`, `0x2B`, `0x2C`, and `0x2D`. We are only interested in the most significant bytes at indices 0 (X), 2 (Y), and 4 (Z).

**3. Sensor Initialization and Detection**

In the `main` function, the code identifies which accelerometer is present on the board and initializes it.

```c

int len=0;

if (HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG1, sizeof(CTRL_REG1), 50) == HAL_OK){
    len = snprintf(str, sizeof(str), "LIS2DE found\r\n");
} else{
    ACCEL_ADD = LIS2DW_ADD;
    if(HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG1, sizeof(CTRL_REG1),50) == HAL_OK){
        len = snprintf(str, sizeof(str), "LIS2DW found\r\n");
    }
    else{
        len = snprintf(str, sizeof(str), "Accelerometer Error \n");
    }
}
HAL_UART_Transmit(&huart2, str, len, 100);

HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG2, sizeof(CTRL_REG2), 50);
HAL_I2C_Master_Transmit(&hi2c1, ACCEL_ADD, CTRL_REG4, sizeof(CTRL_REG4), 50);

HAL_TIM_Base_Start_IT(&htim10);
```

*   **Explanation:** The code first tries to communicate with the LIS2DE. If that fails, it tries the LIS2DW address. The result is printed to the terminal. Then, the remaining control registers (CTRL_REG2 and CTRL_REG4) are configured. Finally, the 1Hz timer is started in interrupt mode, which will trigger the reading process.

**4. Timer Interrupt: Initiating a Read**

The 1Hz timer interrupt is the master trigger for the entire read-and-transmit sequence.

```c
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
    if(htim == &htim1){
        HAL_I2C_Master_Transmit_DMA(&hi2c1, ACCEL_ADD, &OUT_BASE_ADD_AUTOINCREMENT, 1);
    }
}
```

*   **Explanation:** Every time the 1Hz timer elapses, this callback function is executed. It uses DMA to send the auto-increment register address (`0x29 + 128`) to the sensor. This prepares the sensor for a multi-byte read.

**5. I2C Transmit Complete: Starting Data Reception**

Once the register address has been sent, the next step is triggered automatically.

```c
void HAL_I2C_MasterTxCpltCallback(I2C_HandleTypeDef *hi2c){
    HAL_I2C_Master_Receive_DMA(&hi2c1, ACCEL_ADD+1, RX_BUFFER, 5);
}
```

*   **Explanation:** This callback is called after the I2C transmit (of the register address) is complete via DMA. It immediately initiates a DMA read request for 5 bytes from the sensor. Note that the address is `ACCEL_ADD+1` because the I2C protocol uses the least significant bit to indicate Read (`1`) or Write (`0`).


**6. I2C Receive Complete: Processing and Transmitting Data**

This is the final step, where the raw data is converted into meaningful values and sent to the terminal.

```c
void HAL_I2C_MasterRxCpltCallback(I2C_HandleTypeDef *hi2c){
    float acc_g_x = RX_BUFFER[0] / 64.0;
    float acc_g_y = RX_BUFFER[2] / 64.0;
    float acc_g_z = RX_BUFFER[4] / 64.0;

    int len = snprintf(str, sizeof(str), "Double_DMA:\r\nX: %+.2f g\r\nY: %+.2f g\r\nZ: %+.2f g\r\n", acc_g_x, acc_g_y, acc_g_z);
    HAL_UART_Transmit_DMA(&huart2, str, len);
}
```

*   **Explanation:** This callback is executed once the I2C DMA has received all 5 data bytes. It extracts the most significant bytes for X, Y, and Z from the buffer (indices 0, 2, and 4) and converts them to acceleration in `g` units by dividing by 64 (for an 8-bit reading at ±2g range). The `%+.2f` format specifier forces the printing of a sign (`+` or `-`) for all values. Finally, the formatted string is sent to the serial terminal using UART DMA.

### <span style="color:rgb(161, 40, 226)">Summary of the Data Flow</span>

1.  **Timer Interrupt:** A 1Hz timer interrupt starts the process.
2.  **I2C Write (DMA):** The MCU sends the "read from register 0x29 with auto-increment" command to the accelerometer.
3.  **I2C Read (DMA):** Upon transmit completion, the MCU reads 5 consecutive bytes of acceleration data from the sensor.
4.  **Data Processing & UART Transmit (DMA):** Upon receive completion, the MCU processes the raw bytes, formats them into a string, and transmits it to the serial terminal.

This chained callback structure, driven by DMA and interrupts, allows the CPU to perform other tasks while the data is being moved and processed in the background.