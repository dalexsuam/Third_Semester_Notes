
# <span style="color:rgb(223, 109, 109)">General Purpose Input/Outputs</span>

This is actually the schema of what a GPIO inside our STM32 is like. So let me just go over it again, maybe in a little bit more detail than last time.
![[Pasted image 20250922143233.png]]

![[Pasted image 20251005111831.png]]
Starting from the right, we have the **input-output pin**, which is the actual physical connection on the board. Just inside the chip, there are **two protection diodes**. Their purpose is to **protect the internal circuitry** from electrostatic discharge (ESD) or accidental voltage spikes. Without these diodes, a simple static charge from a person’s touch or an unexpected input could damage or even destroy the delicate electronic components inside the board. In short, these diodes act as a **safety barrier**, ensuring that any excess charge is safely redirected and doesn’t reach the sensitive internal circuits.
![[Pasted image 20251005111846.png]]
Moving further to the left, we can see **two resistors** — a **pull-up** and a **pull-down** resistor. You might already be familiar with them, but let’s quickly review what they do.

When an output pin isn’t connected to anything, it becomes what we call a **floating pin**. This means it doesn’t have a defined voltage level — it could randomly fluctuate between high and low, and we wouldn’t know its actual value. To avoid this uncertainty, we can use a **pull-up** or **pull-down** resistor to give the pin a **default or stable value**.

| **pull-up resistor**                                                                                                                     | **pull-down resistor**                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| connects the pin to the supply voltage (VDD), so when nothing else is driving the pin, it will naturally stay at a **high logic level**. | connects the pin to ground, keeping it at a **low logic level** when inactive. |
For example, think of a **button input**: when the button is open, we might use a pull-up resistor so the pin stays high by default. When the button is pressed, the pin is connected to ground, and the value drops to low.

You usually won’t need to manually change these settings, but it’s important to **understand the concept** — that pull-up and pull-down resistors are used to prevent floating inputs and to set a defined baseline voltage for a pin.

![[Pasted image 20251005112431.png]]
Next, we move inside the **actual circuitry**. Here, we can see that the **upper path** corresponds to the **input**, while the **lower one** corresponds to the **output**.

![[Pasted image 20251005112654.png]]
Starting with the **input**, if it’s an **analog input**, the signal comes in as it is — a continuous value — and nothing is changed at this stage. The microcontroller simply **reads the analog voltage** from this line. Inside the microcontroller, there is usually an **ADC (Analog-to-Digital Converter)** that converts this analog signal into a **digital value**, because ultimately we want to work with digital data.

Alternatively, the signal might already come in as **digital**, for instance through a **trigger circuit** that converts an analog level into a digital “high” or “low” state before it even enters the microcontroller.
![[Pasted image 20251005112833.png]]
Once the signal becomes digital, it can be used in several ways:

- It can be **stored in an input data register**, so the microcontroller can read it when needed — for example, checking whether a button has been pressed or not.
    
- It can also be routed to **alternate function inputs**. This means the signal can directly trigger certain actions inside the microcontroller — for example, pressing a button could start an ADC conversion, play a sound, or perform another hardware-controlled function without needing extra code.
    
- Finally, the input pin could also be configured for **communication purposes**, such as receiving signals for **I²C** or **UART** protocols.

>[!Warning] # <span style="color:rgb(239, 179, 1)">What do we mean by Alternate Function Inputs?</span>
![[Pasted image 20251005113122.png]]
If you remember from last time, we looked at a table showing all the possible configurations for each pin. Normally, a pin can simply act as a **GPIO** — a **General Purpose Input/Output** — which means it can be used in a very basic way to read or write a digital signal. 
However, many pins can also be assigned a **different, specialized role**, and that’s what we call an **alternate function**. For example, instead of just reading the state of a button, that same pin might be used as a **communication line** — like the data line of a UART interface, or the clock line in an I²C connection. In these cases, the pin is no longer used to store a simple “high” or “low” value in memory; instead, it becomes part of a communication or control system, driven by internal hardware inside the microcontroller.
So, an alternate function essentially means that the **same physical pin** is being used for a **different internal purpose** — it could handle a serial communication signal, a timing clock, or even a PWM output, depending on how it’s configured.
![[Pasted image 20251005113816.png]]


Below that, we find the **output driver** section. As we’ve already mentioned, this part isn’t just about simple reading or writing — it can also operate in **alternate function mode**, where the microcontroller itself generates specific signals, such as those used for communication or timing, and sends them out through this pin.

![[Pasted image 20251005113834.png]]
Right after that, we have the **output control circuit**, which includes **two MOSFETs** — a **PMOS** and an **NMOS** transistor. These are essential because the output pin can work in **three different configurations**. You won’t need to modify these settings in your projects, but it’s still important to understand what they mean.

1. **Push-pull configuration:**  
    In this mode, both transistors are active, allowing the pin to drive the output **either high (to VDD)** or **low (to ground)**. This is the most common configuration and is used when we want strong, fast transitions between logic levels.
    
2. **Open-drain configuration:**  
    Here, only the **NMOS** transistor is used. This means the output can only pull the line **down to a low level**, but it cannot drive it high. If we want a high value, we need an **external pull-up resistor**. This configuration is often used for communication lines, like I²C, where multiple devices can share the same line safely.
    
3. **Disabled configuration:**  
    In this case, both transistors are turned off, and the output pin is **left floating** — it doesn’t drive any signal at all.
    

Even though you won’t need to change these settings manually, it’s good to know how they work. If you look in the **STM32CubeIDE** interface, for instance, you can easily select these modes through a dropdown menu. But for our current functions, we’ll just use the default configuration.


![[Pasted image 20251005114137.png]]
You might remember this graph from last time. As we discussed, each pin on the microcontroller can be configured as either **input** or **output**. Beyond these basic functions, pins can also have **other specialized roles**, which we will explore later.

One of the most important features to know right now is **GPIO EXTI**. **EXTI** stands for **External Interrupt**, and it’s a function we will use frequently. This allows a pin to **trigger an interrupt** when a specific event occurs, such as a button press or a signal change, so the microcontroller can respond immediately without constantly checking the pin’s state.

# <span style="color:rgb(223, 109, 109)">External Interrupt/Event (EXTI) Peripheral </span>

An **external interrupt** means that the microcontroller has a **peripheral dedicated to handling events coming from outside**. These are events that occur on the input pins, such as a change in a GPIO value, which can **trigger an interrupt**.

You might remember what an interrupt does: it allows the **CPU to temporarily pause its current task** and execute a special piece of code called an **interrupt service routine (ISR)**. This routine is executed **only when the event happens**, so we don’t need to constantly check the pin’s state in our main program. For example, if a button is pressed, the ISR can handle it automatically.

The EXTI (External Interrupt) system is flexible: it can detect interrupts when the line **rises (rising edge)**, **falls (falling edge)**, or **both**. In practice, this allows us to detect both **presses and releases** of a button.

Each EXTI line can be connected to a specific GPIO pin, and most microcontrollers have **multiple EXTI lines**, although in some simple examples, we may only use one. The EXTI lines are connected to the **NVIC (Nested Vectored Interrupt Controller)**, which manages **priorities**, deciding which interrupt should be handled first if multiple interrupts occur at the same time.

We will see this in practice during the class project, where we detect both **press and release events** on a button using EXTI.

>[!Warning] ## <span style="color:rgb(239, 179, 1)">Interrupt == Event?</span>
>The **EXTI system** can handle both **interrupts** and **events**, and it’s important to understand the difference between them.
>
>An **interrupt** is mainly **software-related**. When an interrupt occurs, the **CPU temporarily stops its current task** and executes an **interrupt service routine (ISR)**. Once the ISR is finished, the CPU resumes what it was doing before. Interrupts require you to **write code** that defines what should happen when the interrupt is triggered.
>
>An **event**, on the other hand, is **hardware-related**. The CPU does **not stop or run an ISR**; it continues executing its current code. Instead, the hardware automatically reacts to the event. For example, if you press a button and this triggers an event, the hardware could start an **ADC conversion** without involving the CPU at all. You don’t need to write any code for the event to occur — it’s handled directly by the hardware.
>
>In practice, interrupts and events are both **triggers**, but they operate differently:
>- **Interrupts**: trigger a software routine you must write.
>- **Events**: trigger a hardware action without stopping the CPU or requiring software intervention.
>    
>For example, consider this sequence:
>1. You press a button. This generates an **event**, which starts the ADC conversion automatically in hardware.
>   
> 2. When the ADC conversion is complete, it generates an **interrupt**, so the CPU executes your ISR to **read and process the ADC result**.
>    
>    So, **events** are useful when you want hardware to act autonomously, while **interrupts** are used when you need the CPU to run code in response to a specific signal.
>
>

![[Pasted image 20251005115854.png]]

Now let’s look at **how the EXTI lines are connected**. Each EXTI line is actually connected through a **multiplexer**, which allows multiple pins to share the same EXTI line. For example, **EXTI line 0** can be connected to **all the pin 0s** of the STM32 microcontroller across different ports (PA0, PB0, etc.).

This raises an important question: **how do we know which pin triggered the interrupt** if multiple pins are connected to the same EXTI line? The answer is that we have to **check it in software**. When an interrupt occurs, your code needs to determine **which pin actually generated it**, so that you can respond appropriately. This is especially important if multiple pins are enabled for the same EXTI line but are supposed to trigger **different actions**.

In addition to the 16 EXTI lines associated with GPIO pins, the STM32 microcontroller has some **additional EXTI lines** numbered 16 to 22, making a total of **23 EXTI lines**. These extra lines are connected to other peripherals, not the standard GPIOs. For example:

- The **RTC (Real-Time Clock) alarm** can trigger an interrupt through one of these lines.
- USB communication can also trigger an interrupt through a dedicated EXTI line.

While we won’t go into detail about these additional lines, it’s useful to know about them. Otherwise, when you see the number 23 in the documentation, it might be confusing, because it seems like there are only 16 EXTI lines for the GPIOs.
## <span style="color:rgb(239, 179, 1)">How to select EXTI?</span>

![[Pasted image 20250922144436.png]]

So, how do we **select which EXTI line** we want to use? This is done through the **register map** of the microcontroller. There is a specific **portion of memory** where we can set bits to choose the EXTI line that will be connected to a particular GPIO pin.

Even if a microcontroller has only, for example, six EXTI lines, the selection field often uses **four bits**. This might seem more than necessary, but it’s a **standardized approach** that allows the same register format to work with more complex microcontrollers that have **more than six lines**. This way, the configuration method is consistent across different devices.

## <span style="color:rgb(239, 179, 1)">How the interrupt mechanism work?</span>



![[Pasted image 20251005144112.png]]
Here’s how the **interrupt mechanism** works. An input line first (on the right) goes into an **edge detector**, which can detect either a **rising edge** (signal going from low to high) or a **falling edge** (signal going from high to low). As we discussed earlier, we can even configure it to detect **both edges** if needed.

Next, we need to decide whether this signal should generate an **interrupt** or an **event**. This choice is made using a **mask** in a specific register (left side). The mask determines whether the trigger on this input line is **enabled as an interrupt** or **enabled as an event**. The edge detector checks the input, and if the mask is set correctly, the system responds according to the selection — either generating an interrupt that executes an ISR or triggering a hardware event without involving the CPU.

![[Pasted image 20251005144358.png]]

Finally, we have the **pending request register**. This register **keeps track of events or interrupts** that have occurred. Each time an event or interrupt happens, the corresponding flag in this register is set to **1**.

When we execute an **interrupt service routine (ISR)**, this flag must be **cleared back to 0**. If we forget to clear it, the flag will remain set, and the system could repeatedly trigger the same interrupt, causing an **infinite interrupt loop**, which we definitely want to avoid. Usually, clearing the flag is done **automatically**, but in some exercises or homework, you may need to handle it manually to understand how it works.

As mentioned before, the pending request register has **23 bits**, one for each EXTI line: **16 bits for GPIO pins**, and the remaining bits are for other peripherals of the microcontroller, such as the RTC alarm or USB events.
## <span style="color:rgb(239, 179, 1)">EXTI Location in Memory & Registers</span>

![[Pasted image 20251005144536.png]]

Just to give you an idea, there is actually a **portion of memory dedicated to the EXTI lines**. We won’t go into the details of these memory locations, but it’s useful to know they exist.

![[Pasted image 20251005144746.png]]
In this memory, we can see **all the registers** that we mentioned in the previous slides: for example, the **pending register**, the **interrupt mask register**, the **event mask register**, and so on. These are the actual registers that control how the EXTI lines behave.

We won’t need to set these registers manually — the **code and the GUI interface handle it automatically**. I just wanted to show that when we configure something in the interface, like enabling an interrupt or an event, this is what actually happens behind the scenes in the microcontroller’s memory.

## <span style="color:rgb(239, 179, 1)">How does the Microcontroller Knows when there is an interrupt?</span>

**Interrupt vector table**
![[Pasted image 20251005145055.png]]

How does the **microcontroller know what to do when an interrupt occurs**? Unlike an event, which is hardware-driven, an **interrupt requires executing code**. To handle this, the microcontroller uses a **vector table**, which is an array of pointers located at a **fixed memory address**. This table is always present in the microcontroller.

When a specific interrupt occurs, the microcontroller looks in the **vector table** and executes the **interrupt service routine (ISR)** stored at the corresponding memory location. This creates a **one-to-one mapping**: for example, pressing the blue button triggers a specific GPIO pin, which is connected to a particular EXTI line, which in turn is associated with a specific interrupt — and that interrupt has a dedicated entry in the vector table telling the CPU what code to run.

However, we don’t have a **unique memory pointer for every single pin or line**. Some pins are grouped through **multiplexers**, meaning one vector table entry may serve multiple pins. This is why the ISR often needs to **check which pin actually triggered the interrupt**.

The reason for using **multiplexers and shared memory addresses** is mostly **to save space**. Instead of having multiple hardware inputs and multiple memory locations for each pin, we can use a single multiplexer and one vector table entry, making the system more efficient in both hardware and memory usage.

## <span style="color:rgb(239, 179, 1)">Interrupt Priorities</span>

![[Pasted image 20251005145421.png]]

A quick reminder about **interrupt priorities**. On CubeIDE, there is a page for the **NVIC (Nested Vectored Interrupt Controller)** where we can set the **preempt value** for each interrupt. This number determines the **order in which interrupts are handled**.

Here’s how it works:

- **Lower preempt numbers mean higher priority.** For example, a preempt value of 0 is higher priority than 1.
- If an interrupt with a **lower preempt number (higher priority)** occurs while a lower-priority ISR is running, the CPU **preempts** the current ISR, executes the higher-priority ISR first, and then resumes the previous ISR.
- If an interrupt has a **higher or equal preempt number** (lower priority) compared to the currently running ISR, it will **wait** until the current ISR finishes before being executed.

In short, **the smaller the preempt value, the earlier the ISR runs**. Understanding this is important when multiple interrupts can occur at the same time.

## <span style="color:rgb(239, 179, 1)">GPIO HAL functions</span>

```c  
GPIO_PinState HAL_GPIO_ReadPin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);

void HAL_GPIO_WritePin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin, GPIO_PinState PinState);

void HAL_GPIO_TogglePin(GPIO_TypeDef* GPIOx, uint16_t GPIO_Pin);

__weak void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin);  
// Function called in the interrupt routine (after flag reset),  
// it can be redefined by the user in main.c  
```

---

# <span style="color:rgb(223, 109, 109)">Timers</span> 


![[Pasted image 20251005150515.png]]
In general, a **timer input** is usually given by a **clock**. This clock can be either **internal** or **external**, and we can select it through the **clock tree** we discussed last time. The input clock can then be **pre-scaled** to reduce its frequency, and we’ll see how this works in the next slides.

After the prescaler, the signal goes into a **multiplexer**. Why a multiplexer? Because the timer can count **different sources**: either the clock cycles themselves, or some **external events**, like how many times a button is pressed. This allows the timer to be flexible for different applications.

Next, the signal enters a **counter**. The counter simply **counts numbers**, either **up** from 0 to a maximum, or in some microcontrollers it can also **count down** or **up and down**. You can read the counter at any time to see, for example, how many clock cycles occurred or how many times a button was pressed.

The counter value can then be used in two main ways:

1. **Auto-reload and compare**: The counter is compared with a value in the **Auto-Reload Register (ARR)**. When they match, the timer can generate a **trigger event**.
    
2. **PWM generation**: Using the **Capture/Compare Register (CCR)**, the timer can generate a **Pulse Width Modulated signal**.
    

![[Pasted image 20251005150935.png]]
We are looking at a more detailed timer schematic, but the principle is the same.

### <span style="color:rgb(161, 40, 226)">Clock Input</span>

The timer receives a **clock signal**, which is essentially a square wave with a **50% duty cycle**. This means the signal alternates between low and high at a fixed frequency. By counting how many clock cycles occur, we can measure **how much time has passed**. For example, if the clock is 84 MHz, counting a certain number of cycles directly gives the elapsed time.

### <span style="color:rgb(161, 40, 226)">Prescaler</span>

The **prescaler** allows us to reduce the clock frequency before it reaches the counter. It’s a **16-bit register**, so we can set values from 0 up to 65535.

- **Prescaler = 0:** Every clock cycle is counted (no division).
- **Prescaler = 1:** We count 1 cycle, skip 1 cycle → effectively halves the frequency. For an 84 MHz input, the scaled clock is 42 MHz.
- **Prescaler = 2:** Count 1, skip 2 → divides input by 3.
- **Prescaler = N:** Count 1, skip N → divides input by N+1.
    
This lets us adjust the timer resolution and range.

### <span style="color:rgb(161, 40, 226)">Counter</span>

The **counter** simply counts numbers:

- **Up-counting:** from 0 to a top value.
- **Down-counting:** from a top value down to 0 (not supported in all MCUs).
- When it reaches the top or bottom, it **resets** back to the starting value.
- The counter can be **16-bit or 32-bit**, depending on the timer.

### <span style="color:rgb(161, 40, 226)">Capture and Compare Registers (CCR)</span>

Each timer channel has its own **Capture/Compare Register**. These can be used for different purposes, for example:

- **Measuring time intervals:** When you press a button, the counter value is saved in the first capture register; when you release it, the second value is saved. The difference gives the duration of the press.
- **PWM generation:** CCR can define when to switch output signals during a timer period.
    
### <span style="color:rgb(161, 40, 226)">Auto-Reload Register (ARR)</span>

The **ARR** sets the **full-scale range of the counter**. For instance:
- By default, a 16-bit counter counts up to 2¹⁶ – 1.
- If we only need to count 10 clock cycles, we can set ARR = 10.
- When the counter reaches ARR, it resets to 0, and optionally triggers events.

## <span style="color:rgb(239, 179, 1)">Pulse Width Modulator (PWM)</span>

PWM is a square wave signal where we can control the **duty cycle** (the fraction of time the signal is high in a period) and the **frequency** using timer registers.

![[Pasted image 20250922145918.png]]

**In STM32F4:**
- Only **edge-aligned PWM** is available.
- **Center-aligned PWM** is not supported.

<span style="color:rgb(161, 40, 226)"><b>Frequency Calculation:</b>  </span>
The PWM frequency is determined by:

$$
PWM frequency = \frac{f_{TIM}}{(ARR+1)(PSC+1)}
$$
Where:

- $f_{\text{TIM}}$​ = input clock frequency of the timer
- $ARR$ = Auto-Reload Register
- $PSC$= Prescaler
    

> The “+1” appears because in C programming, counting starts from 0. So zero counts as 1 in practice.


<span style="color:rgb(161, 40, 226)"><b>Duty Cycle Calculation:</b></span>
$$
PWM Duty Cycle = \frac{CCRX+1}{ARR+1}
$$


Where $CCR$ = Capture/Compare Register for the channel.

**Notes:**

- $ARR$ sets the **full-scale range** of the counter.
- $PSC$ divides the input clock to reduce the timer frequency.
- The combination of $ARR$ and $PSC$ allows precise control of both **PWM frequency** and **duty cycle**.

>[!Warning] The prescaler divides the clock first, then the counter counts from 0 to ARR, giving you a second division stage. Together they let you achieve very large division ratios
>
>Each PWM period, the counter counts from 0 to ARR and resets. Meanwhile:
>1. **Counter < CCR**: Output is HIGH (or LOW, depending on polarity setting)
>   2. **Counter ≥ CCR**: Output switches to LOW (or HIGH)
>
>The CCR value determines **how long** the output stays in each state.
   
## <span style="color:rgb(239, 179, 1)">Timer HAL functions</span> 


```c  
// Start and stop PWM on a specific channel  
HAL_StatusTypeDef HAL_TIM_PWM_Start(TIM_HandleTypeDef *htim, uint32_t Channel);  
HAL_StatusTypeDef HAL_TIM_PWM_Stop(TIM_HandleTypeDef *htim, uint32_t Channel);

// Start and stop the base timer (with optional interrupt)  
HAL_StatusTypeDef HAL_TIM_Base_Start(TIM_HandleTypeDef *htim);  
HAL_StatusTypeDef HAL_TIM_Base_Start_IT(TIM_HandleTypeDef *htim); // with interrupt  
HAL_StatusTypeDef HAL_TIM_Base_Stop(TIM_HandleTypeDef *htim);  
HAL_StatusTypeDef HAL_TIM_Base_Stop_IT(TIM_HandleTypeDef *htim); // with interrupt

// Timer callback (called automatically on period elapsed interrupt)  
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim);  
```
---
---
---
---
---

# <span style="color:rgb(223, 109, 109)">Project 2a: Pushbutton - polling</span>

Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. A polling operation will be used to monitor the state of the pushbutton.

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Identifying the pins</span>: 
 
Before starting, we need to identify which pins correspond to the **blue push button** and the **green LED** on our STM32 board.  
According to the documentation:

- The **green LED (LD2)** is connected to **pin PA5**.    
- The **blue push button (B1)** is connected to **pin PC13**.

| Blue Button                          | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005160950.png]] | ![[Pasted image 20251005160756.png]] |
 
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Defining the Pins in the `.ioc` File:</span>

In STM32CubeMX (the `.ioc` configuration file), we set up both pins appropriately:
- **PC13** (the button) is configured as an **External Interrupt GPIO pin**, so that an **interrupt service routine (ISR)** can be triggered when the button is pressed or released.
- **PA5** (the LED) is configured as a **GPIO Output** to control it from the code.


| Blue button                          | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005155751.png]] | ![[Pasted image 20251005155805.png]] |

3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Configuring the Interrupt Controller</span>:

Next, we open the **NVIC (Nested Vectored Interrupt Controller)** settings to enable the **EXTI line** corresponding to our button — in this case, **GPIO_EXTI13**.  Since we are only dealing with one interrupt source, we don’t need to modify the **preemption priority**. 

>[!success] It is going to be useful if we are using an external interruption. However, in this case we're reading the state of the GPIO pin through polling.



![[Pasted image 20251005155855.png]]

4. .<span style="font-weight:bold; color:rgb(161, 40, 226)"> Setting the GPIO Modes</span>

We now verify that both pins have the correct GPIO configurations:

- **PA5 (LED)** → set as **Output Push-Pull**.
- **PC13 (Button)** → set to detect both **rising and falling edges** (so we can sense both press and release events).

| Blue button                             | Green led                            |
| --------------------------------------- | ------------------------------------ |
| ![[Pasted image 20251005160005.png]]    | ![[Pasted image 20251005155914.png]] |
| Not mandatory since we're using polling |                                      |

5. <span style="font-weight:bold; color:rgb(161, 40, 226)">Writing the Code</span>:

**We**’ll use **polling** (not interrupts) to read the button’s state in the main loop.  
To make the code cleaner, we define the pins as macros and create a variable to store the button state.

![[Pasted image 20250925151918.png]]
Since the button uses a **pull-up configuration**, it normally outputs logic `1` (HIGH) when not pressed, and logic `0` (LOW) when pressed.  

For this reason, we use the **negated value** (`!pushbutton`) when writing to the LED, so that the LED turns on when the button is pressed.

``` c#
//In include section

// Define pin macros
#define BUTTON GPIOC, GPIO_PIN_13
#define LED GPIOA, GPIO_PIN_5

int main(void)
{
    GPIO_PinState pushbutton; //It’s used to store the logical state (HIGH or LOW) of a GPIO pin.

    while(1)
    {
        // Read the state of the button
        pushbutton = HAL_GPIO_ReadPin(BUTTON);

        // Write the opposite state to the LED
        HAL_GPIO_WritePin(LED, !pushbutton);
        // The '!' is used because the button is in pull-up configuration:
        // it reads 0 when pressed, and 1 when released.
    }
}
```

---
---
---
---
---
# <span style="color:rgb(223, 109, 109)">Project 2b: Pushbutton - Interrupt</span> 

Objective of this project is to switch on the green LED on Nucleo board (LD2), every time the blue pushbutton is pressed and to switch it off when the pushbutton is released. The pushbutton input will be used in interrupt mode

1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Identifying the pins</span>: 
 
Before starting, we need to identify which pins correspond to the **blue push button** and the **green LED** on our STM32 board.  
According to the documentation:

- The **green LED (LD2)** is connected to **pin PA5**.    
- The **blue push button (B1)** is connected to **pin PC13**.

| Blue Button                          | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005160950.png]] | ![[Pasted image 20251005160756.png]] |
 
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Defining the Pins in the `.ioc` File:</span>

In STM32CubeMX (the `.ioc` configuration file), we set up both pins appropriately:
- **PC13** (the button) is configured as an **External Interrupt GPIO pin**, so that an **interrupt service routine (ISR)** can be triggered when the button is pressed or released.
- **PA5** (the LED) is configured as a **GPIO Output** to control it from the code.


| Blue button                          | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005155751.png]] | ![[Pasted image 20251005155805.png]] |

3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Configuring the Interrupt Controller</span>:

Next, we open the **NVIC (Nested Vectored Interrupt Controller)** settings to enable the **EXTI line** corresponding to our button — in this case, **GPIO_EXTI13**.  Since we are only dealing with one interrupt source, we don’t need to modify the **preemption priority**. 

>[!warning] It is going to be mandatory to check the EXTI line 13 interrupt since we're going to use it to detect the rising/falling edges.



![[Pasted image 20251005155855.png]]

4. .<span style="font-weight:bold; color:rgb(161, 40, 226)"> Setting the GPIO Modes</span>

We now verify that both pins have the correct GPIO configurations:

- **PA5 (LED)** → set as **Output Push-Pull**.
- **PC13 (Button)** → set to detect both **rising and falling edges** (so we can sense both press and release events).

| Blue button                          | Green led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005160005.png]] | ![[Pasted image 20251005155914.png]] |

5. <span style="font-weight:bold; color:rgb(161, 40, 226)">Writing the Code</span>:
```c#
//pin definitions

#define BUTTON GPIOC, GPIO_PIN_13
#define LED GPIOA, GPIO_PIN_5

//callback function
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin){
	GPIO_PinState pushbutton;
	switch(GPIO_Pin){
	case GPIO_PIN_13: //It checks if that PIN generated the interrupt
		pushbutton = HAL_GPIO_ReadPin(BUTTON); //reads the value of the BUTTON
		HAL_GPIO_WritePin(LED, !pushbutton);// Change the LED
		break;
	default:
	break;//otherwise, break
}

}
```

---
---
---
---
---
# <span style="color:rgb(223, 109, 109)">Homework 2</span>

**Due date: Squad A:** Sunday, September 28, at 2:30 pm

**1- Prepare the basics for the project “Play a song”:**

## <span style="color:rgb(239, 179, 1)">Homework 2a</span>

Modify the status (switch on / off) of the NUCLEO green LED, every time you snap your fingers.(Use the pin connected to the microphone as an External Interrupt)

*Hint: look at the files “Green PCB board schematic” and “Nucleo Schematic” and “Nucleo user*
*manual” on Webeep in “Material/Laboratories/Documentation” and find the STM32 pin that*
*connects to SND_IN.*


1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Identifying the pins</span>: 
 
Before starting, we need to identify which pins correspond to the **Microphone** and the **green LED** on our STM32 board.  
According to the documentation:

- The **green LED (LD2)** is connected to **pin PA5**.    
- The **Microphone ** is connected to **pin PA8**.

| Microphone                           | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005183025.png]] | ![[Pasted image 20251005160756.png]] |
 
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Defining the Pins in the `.ioc` File:</span>

In STM32CubeMX (the `.ioc` configuration file), we set up both pins appropriately:
- **PA8** (the microphone) is configured as an **External Interrupt GPIO pin**, so that an **interrupt service routine (ISR)** can be triggered when an snap is detected.
- **PA5** (the LED) is configured as a **GPIO Output** to control it from the code.


| Microphone                           | Green Led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005183649.png]] | ![[Pasted image 20251005155805.png]] |

3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Configuring the Interrupt Controller</span>:

Next, we open the **NVIC (Nested Vectored Interrupt Controller)** settings to enable the **EXTI line** corresponding to our microphone — in this case, **GPIO_EXTI8.  Since we are only dealing with one interrupt source, we don’t need to modify the **preemption priority**. 

>[!warning] It is going to be mandatory to check the EXTI line 8 interrupt since we're going to use it to detect the rising. (An incoming event)

![[Pasted image 20251005183809.png]]

4. .<span style="font-weight:bold; color:rgb(161, 40, 226)"> Setting the GPIO Modes</span>

We now verify that both pins have the correct GPIO configurations:

- **PA5 (LED)** → set as **Output Push-Pull**.
- **PA8 (Microphone)** → set to detect **rising edges** (Only when a snap is detected).

| Microphone                           | Green led                            |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20251005183913.png]] | ![[Pasted image 20251005183931.png]] |

5. <span style="font-weight:bold; color:rgb(161, 40, 226)">Writing the Code</span>:

```c#
//Pin definitions
#define MICROPHONE GPIOA, GPIO_PIN_8
#define LED GPIOA, GPIO_PIN_5

//private variables
uint32_t tick;
uint32_t last_tick=0;
uint32_t delta;


// the HAL_GPIO_EXTI_Callback checks any falling or rising edges
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_PIN){
//The following two Blocking/Non-blocking are anti-bouncing workarounds since we don't count with anti-bouncing hardware...

//Blocking version
	if(GPIO_PIN == GPIO_PIN_8){
		HAL_GPIO_TogglePin(LED);
		HAL_Delay(5);//inserts 5ms to not generate any changes within this time
		__HAL_GPIO_EXTI_CLEAR_IT(GPIO_PIN); //clears the interruption, it is over. 
	}

//Non-blocking version -- Here we just consider interruptions >100ms
	if (GPIO_PIN == GPIO_PIN_8){
		tick= HAL_GetTick();//current time in ms
		delta = last_tick - tick;//time difference in ms
	
		if (delta>=100)// more than 100ms state?
			HAL_GPIO_TogglePin(LED);
		
		last_tick = tick;
	}
}
```
## <span style="color:rgb(239, 179, 1)">Homework 2b</span>

Make the NUCLEO green LED blink at a 1 Hz rate using PWM generation on the corresponding
channel.


1. <span style="font-weight:bold; color:rgb(161, 40, 226)">Identifying the pins</span>: 
 
Before starting, we need to identify which pins correspond to the **green LED** on our STM32 board.  
According to the documentation:

- The **green LED (LD2)** is connected to **pin PA5**.    

| Green Led                            |
| ------------------------------------ |
| ![[Pasted image 20251005160756.png]] |
 
2. <span style="font-weight:bold; color:rgb(161, 40, 226)">Defining the Pins in the `.ioc` File:</span>

In STM32CubeMX (the `.ioc` configuration file), we set up pins appropriate:

- **PA5** (the LED) is configured as a **TM2-CH1** this time because we're aiming to use it's time to control it through a PWM signal from the code.

| Green Led                            |
| ------------------------------------ |
| ![[Pasted image 20251005190334.png]] |

3. <span style="font-weight:bold; color:rgb(161, 40, 226)">Configuring the TM2-CH1</span>:

Next, we open the **Timers** settings, select the TIM2, set Internal Clock as Clock source and enable *Channel1* and set it as PWM Generation CH1 corresponding to the PWM signal of our LED
![[Pasted image 20251005192229.png]]

4. .<span style="font-weight:bold; color:rgb(161, 40, 226)"> Setting Frequency & Duty Cycle</span>

We now perform the calculations to obtain our $1 Hz$ frequency and $50\%$ duty cycle.

$$
PWM frequency = \frac{f_{TIM}}{(ARR+1)(PSC+1)}
$$

Since we know our clock source has a $f_{TIM}= 84MHz$ and the pre-scaler is $16-bits = 65535$. Then, we set $PSC$ as $8400-1$. Auto-reload register is $32-bits = 4294967295$, we set then ARR as $10000-1$, so I'll have the same $84MHz$ in the denominator to set my desired frequency.

$$
PWM Duty Cycle = \frac{CCRX+1}{ARR+1}
$$
For $50\%$ DC I must set Capture/Compare Register (Also of 32-bits) half as ARR. Then $5000-1$

![[Pasted image 20251005191819.png]]

5. <span style="font-weight:bold; color:rgb(161, 40, 226)">Writing the Code</span>:

Once saved the .ioc file. Timer2 will be initialized as it is going to be shown and we must start our PWM signal through the HAL command. 
``` C#
MX_TIM2_Init(); /* USER CODE BEGIN 2 */ 

HAL_TIM_PWM_Start(&htim2, TIM_CHANNEL_1); // Add this line! /* USER CODE END 2 */
```




