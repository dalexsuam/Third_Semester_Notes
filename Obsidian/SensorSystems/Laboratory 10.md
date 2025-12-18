
17/11/2025
***

# <span style="color:rgb(223, 109, 109)">Keyboard</span>

![[Pasted image 20251216152902.png]]
Today we will look briefly at its **electronics**. It is very simple and based entirely on **GPIOs**, but it will give you the foundation to interact with the keyboard and use it to input data.

In particular, we are talking about the **small keyboard next to the LCD**, which I am sure all of you have already noticed.


## <span style="color:rgb(239, 179, 1)">What is inside the keyboard?</span>

![[Pasted image 20251216152917.png]]

Internally, the keypad is nothing complicated: it is just a set of **push buttons**. From the schematic, you can see that there was the option to mount **two shift registers** and handle it in a way similar to the LED matrix. However, this design choice was not adopted. Instead, all the keypad connections are brought directly to the microcontroller pins and handled as **GPIOs**.

The keypad is organized as a **4×4 matrix**:
- 4 rows
- 4 columns

One set of lines is **driven** (outputs), while the other set is **read** (inputs).

## <span style="color:rgb(239, 179, 1)">Why rows and columns?</span>

This structure is used for the same reason as the LED matrix:  
we cannot afford to connect 16 individual buttons directly to 16 separate pins.

Instead:

- the **columns** are driven one at a time,
- the **rows** are read back.
    
In practice, four columns are connected on one side, and the four rows are connected on the other side. When we actively drive one column (for example, pulling it low), any button pressed in that column will pull the corresponding row line low as well. By reading the row pins, we can detect which button is pressed.

This means that, just like with the LED matrix, we must **multiplex the columns**:

- activate one column,
- read the rows,
- move to the next column,
- and repeat.
    
## <span style="color:rgb(239, 179, 1)">Button scanning and repeated presses</span>

If you implement only the most basic scanning code, you will immediately notice a problem. Since the keypad is continuously scanned, **a pressed button will be detected repeatedly** at the scanning frequency.

For example, if you press the key “A”, you may see “A” printed many times in a row. This is not the desired behavior.

The goal of the homework is to:

- keep scanning the keypad continuously,
- allow other keys to be detected,
- but **register a key press only once**, even if the button is held down.
    
You will need to design a simple and smart strategy to achieve this.

## <span style="color:rgb(239, 179, 1)">A special row and a hidden issue</span>

One of the rows in the keypad behaves slightly differently. You will notice that **key presses on that row take longer to be detected** compared to the others.

This is not a software bug. The reason is related to the **schematic**, and in particular to the **blue push button** connected on the board. You are expected to analyze the schematic and understand:

- why this row behaves differently,
- and why the response time is longer.
    

## <span style="color:rgb(239, 179, 1)">Debouncing considerations</span>

Finally, notice that **there is no hardware debouncing circuit** for the keypad buttons. This means that when a button is pressed, the signal may oscillate briefly before settling, which can cause multiple false detections if not handled correctly in software.

This is different from the blue push button on the board, which _does_ have hardware debouncing.

You should be aware of this issue. If you encounter problems due to bouncing:

- explain them clearly in your homework,
- describe **why** they occur,
- and discuss how they could be mitigated (even if you do not fully implement a solution).
    
Understanding and explaining these effects is part of the exercise.


![[Pasted image 20251216154949.png]]
As I was saying, the keypad uses **only four GPIO outputs and four GPIO inputs**. I listed them explicitly here just to make things easier for you, since they are spread across different pins.

Every time you want to use the keyboard, these pins must be configured correctly:

- the **columns** must be configured as outputs,
- the **rows** must be configured as inputs.
    
In other words, you will **drive the columns** and **read the rows** using GPIOs. Unlike the LED matrix, where data was sent through SPI, here we are directly reading the pin states.


![[Pasted image 20251216155012.png]]
Looking at the schematic again, you can see that there are **four transistors connected to the row lines**. These transistors are used to correctly pull one side of the button to ground when a column is activated. This allows us to detect a key press reliably.

The scanning mechanism works as follows:
- you activate one column at a time (by pulling it low),
- you read the row inputs,
- if a row goes from high to low, it means the corresponding key is pressed.
    
So, a key press is detected when the row signal becomes **logic 0**. This happens because one side of the button is forced to ground, and the input pin detects the transition from high to low.

Another important point is **bouncing**. You should carefully check the schematic to see:

- whether debouncing is present or not,
- how it differs from other inputs on the board,
- whether software debouncing is necessary in this case.
    
Try to understand this by looking closely at the circuit, because the behavior is different from other peripherals, such as a microphone.
# <span style="color:rgb(223, 109, 109)">Encoder</span>

Here is the same content rewritten as a **clear, structured textual explanation**, with smoother flow and correct terminology:
![[Pasted image 20251216161334.png]]

Now, regarding the theory part, we introduce the **encoder**. On the board, besides the potentiometer knob, you also have another rotary device, which is an encoder.

An **encoder** is a peripheral that provides information about **movement**, which can be linear or rotational. In our case, it is a **rotary encoder**. It allows us to determine:

- the **direction** in which the knob is being turned,
- and how **fast** the knob is being turned.
    
It does this by generating a series of electrical **pulses** as the knob rotates. Each rotation produces a sequence of square-wave signals. By counting these pulses, we can estimate the speed of rotation. The faster the pulses arrive, the faster the knob is being turned.

You can think of this signal as being similar to a **clock signal**. When we talk about clocks, timers immediately come to mind. In fact, this analogy is very useful, because timers can be configured to process exactly this kind of square-wave input.

There are two main types of encoders:

### <span style="color:rgb(161, 40, 226)">1. Single-channel encoder</span>

A single-channel encoder provides only one output signal. With this type, we can measure **speed**, because we can count how many pulses occur in a given time interval. However, we **cannot determine the direction of rotation**, since there is only one signal.

### <span style="color:rgb(161, 40, 226)">2. Quadrature (two-channel) encoder</span>

In a quadrature encoder, there are **two output channels**, typically called **A and B**, which are phase-shifted by **90 degrees** with respect to each other.

This phase difference allows us to determine the **direction of rotation**. By observing which signal’s rising edge occurs first, we can tell whether the knob is being turned clockwise or counterclockwise.

Once again, since the encoder outputs square-wave signals, we can connect these signals directly to a **timer peripheral**. The timer can be configured in encoder mode, allowing it to:

- count the incoming pulses,
- determine direction (in the quadrature case),
- and indirectly measure speed based on how frequently the pulses occur.
    

So, even though these signals are not clock signals in the strict sense, they behave like clocks from the timer’s point of view, and the timer can decode them efficiently.

This is the basic idea behind using an encoder and how it relates to timers in the microcontroller.

## <span style="color:rgb(239, 179, 1)">Encoder Modalities</span>

Here is an example of what was meant by **quadrature output**. In a quadrature encoder, there are **two signals**, usually called **channel A and channel B**, and they are **phase-shifted by 90 degrees** with respect to each other.

![[Pasted image 20251216163851.png]]
Because of this phase shift, the **relative timing of the edges** (rising or falling) on the two channels depends on the **direction of rotation**.

When the encoder is rotated in one direction (for example, clockwise), both signals may be high at some point, but the key observation is the **order in which the edges occur**. For instance:
- channel A may experience a falling edge while channel B is still high,
- then later channel B experiences its falling edge.

If the rotation direction is reversed (counterclockwise), the **order of these edges is reversed**:
- channel B changes first,
- followed by channel A.

By observing which channel changes state first, the system can determine the **direction of rotation**.

The microcontroller’s **timer peripheral** is able to decode this type of signal automatically. By monitoring the transitions on channels A and B and their relative order, the timer can:
- count movement,
- and determine whether the count should increase or decrease, corresponding to clockwise or counterclockwise rotation.
### <span style="color:rgb(161, 40, 226)">Three main counting modes</span>

Regarding the operating modes of the encoder interface, there are **three main counting modes**, depending on how many channels and edges are used:
![[Pasted image 20251216163945.png]]
1. **Mode using only channel A**  
   The timer counts transitions on channel A only.

![[Pasted image 20251216163955.png]]
1. **Mode using only channel B**  
   This works exactly the same way as the previous mode, but using channel B instead.

In these single-channel modes, each **mechanical step** of the encoder results in a change of **±2 counts**. For the encoder on the board, one full mechanical rotation corresponds to **24 counts**. Therefore, when the counter reaches +24 (or −24), it means that one full revolution has been completed.

At this point, it is important to consider what happens when the timer counter reaches its maximum value and **overflows**. If the knob continues to rotate, the counter will wrap around, and this behavior must be handled correctly in the software.

![[Pasted image 20251216164006.png]]

3. **Mode using both channels A and B**  
   When both channels are used, the timer counts **more edges per mechanical step**, effectively increasing the resolution. Since both rising and falling edges on both channels are taken into account, the number of counts per revolution is doubled.

In this case, instead of counting up to 24 for one full rotation, the counter must reach **48 counts** to represent a complete turn. This higher count provides **better resolution**, meaning finer detection of angular movement.

In summary, the encoder interface is fundamentally based on **counting signal transitions**. By choosing how many channels and edges to count, we can trade off simplicity versus resolution, while the timer hardware takes care of direction decoding and counting automatically.


![[Pasted image 20251216164044.png]]

These are the pins to which the **rotary encoder** is connected. In particular, the two encoder channels are connected to **PC6 and PC7**. On this board, these pins are internally mapped to **Timer 3**, meaning that only **TIM3** can be used to interface with the encoder.

For this reason, **Timer 3 must be configured in encoder mode**. In this mode, the timer hardware automatically processes the two quadrature signals coming from the encoder and updates its counter accordingly, taking care of both counting and direction detection.

An important aspect to note is that **there is no hardware debouncing** on the encoder. Electrically, the encoder is equivalent to **two mechanical switches**, and like any mechanical contact, it introduces **bouncing**. Bouncing causes rapid, unwanted transitions on the signal lines, which appear as noise and can lead to incorrect counting if not handled properly.

To address this issue, we will make use of the **digital input filtering** that is built into the timer’s encoder interface. This hardware filter allows us to suppress short, spurious transitions caused by bouncing **without writing any additional software**. By configuring the timer’s digital filter parameters appropriately, only stable transitions are counted, resulting in reliable encoder readings.


## <span style="color:rgb(239, 179, 1)">Bouncing!</span>

This figure is an example meant to illustrate **what happens when a mechanical switch bounces** during a transition, in this case when the signal goes from logic **1 to 0**.

![[Pasted image 20251216164536.png]]
Ideally, when the switch is pressed or released, we would like the signal to change cleanly from 1 to 0 (or from 0 to 1). However, because the switch is mechanical, the contacts physically vibrate for a short time. As a result, instead of a single clean falling edge, the signal oscillates between 0 and 1 several times before stabilizing.

From the point of view of the microcontroller, this is a problem. The input logic will see:

- One falling edge,
- then one or more rising edges,
- then more falling edges,  
    all with **different pulse widths**.
    
Some of these pulses are very short, others are longer. If the software (or hardware) reacts to every edge it detects, the system may **count multiple transitions instead of just one**, leading to errors. For example, an encoder could increment or decrement several times even though the knob moved only one step.

To avoid this problem, we use **digital filtering**, also called **debouncing**.

Instead of reacting immediately to a single edge, the digital filter works by **sampling the signal at a fixed frequency** and checking its value **multiple times** before deciding that the signal has actually changed.

For example, suppose we configure the filter to require **two consecutive samples** after a falling edge:

- The first sample might read `0`
- The second sample might read `1`
    

Since the two samples are not equal, the filter **rejects the change** and waits longer. It then takes two new samples:

- If both samples read `0`, the filter now considers the signal stable
- Only at this point does the system accept that the signal has transitioned to `0`
    

In other words, the signal must remain consistently high or low for a certain amount of time before the state is updated.

![[Pasted image 20251216164718.png]]

In our microcontroller, this digital filtering is **fully configurable in hardware** (inside the timer peripheral). We can adjust two main parameters:

1. **Sampling frequency**  
    This is derived from the internal timer clock divided by a selectable prescaler.  
    The division factor can range from no division up to a division by 32.  
    A larger division means the samples are taken **more slowly and further apart in time**.
    
2. **Number of samples required**  
    We can choose how many consecutive samples must have the same value before the signal is considered stable.  
    This number can range from **1 up to 8 samples**.
    

The most conservative (and safest) configuration is:

- Clock divided by 32 (slow sampling)
- 8 consecutive identical samples required
    

This configuration provides the strongest debouncing, because it is very unlikely that bouncing noise will satisfy all those conditions. However, it also introduces the **longest delay** before a transition is recognized.

Conversely:

- No clock division
- Only 1 or 2 samples
    

This is the fastest response but also the **least robust** against bouncing.

In our case, even the slowest configuration corresponds to a delay of only about **12.2 microseconds**, which is negligible for human interaction (such as turning a knob or pressing a key). However, in high-speed or time-critical applications, such a delay might be unacceptable, so the filter parameters must always be chosen based on the specific use case.

## <span style="color:rgb(239, 179, 1)">IOC window</span>

![[Pasted image 20251216165918.png]]
Here is a screenshot of the **IOC (CubeMX) window** you will see when configuring a timer in **encoder mode**. As shown, the two timer channels are combined to operate as an encoder interface. In this configuration, you must correctly set several parameters, in particular the **encoder mode**, which defines which edges are counted and how the channels are interpreted.

This configuration should already be correctly set in the project template. However, if you encounter any issues, please let me know.

The objective of this exercise is to **read the encoder position** and send the information to the computer, including the **rotation speed in revolutions per minute (RPM)**.

To compute the speed, you need to know how many **counts correspond to one full rotation** of the encoder. This depends on the selected encoder mode:

- Using **TI1 only** → 24 counts per revolution
- Using **TI2 only** → 24 counts per revolution
- Using **TI1 + TI2** → 48 counts per revolution
    
You will also need a **timer as a time base** to measure how many counts occur within a known time interval. The data can then be transmitted to the PC, for example using **DMA**.

Some additional tips:


~~~c#
HAL_TIM_Encoder_Start(TIM_HandleTypeDef *htim, uint32_t Channel);

__HAL_TIM_GET_COUNTER(TIM_HandleTypeDef *htim);

~~~

- The encoder interface allows you to determine both **rotation direction** and **speed**. You can choose whether to represent the direction as a positive or negative value.
- To start the encoder, you must use the dedicated HAL function:

- `HAL_TIM_Encoder_Start()`
    instead of the standard `HAL_TIM_Base_Start()` or `HAL_TIM_Base_Start_IT()`.
    
- When starting the encoder, you must specify **which channels are enabled**, depending on the encoder mode you selected.
    
To read the encoder position, you can use the function that returns the **timer counter value**. This counter represents the current position of the encoder. You can:

- Start counting from zero and allow the value to increase or decrease, or
- Start from a midpoint value and count up or down from there.
    

You will need to decide which approach is more convenient for your implementation.

Be careful: the **timer counter can overflow or underflow**. You must consider whether this can happen in your application and how to handle it correctly.

For example, if the counter starts at zero and you rotate the encoder in the negative direction, the counter will underflow and jump to a very large value (e.g., from 0 to 65,535 for a 16-bit counter). If you directly compute speed from this difference, you may obtain incorrect RPM values. Therefore, you must explicitly handle **overflow and underflow cases** when computing speed and direction.

Finally, remember that the number of counts per full rotation depends on the encoder mode you selected, as explained earlier.
***
****
***
***
***
# <span style="color:rgb(223, 109, 109)">Homework 10a: scan each column on the keyboard, of course using a timer interrupt</span>


### Homework description

This is essentially your homework for next week.

Your task is to:

- scan each column of the keyboard,
- use a **timer interrupt** to perform the scanning,
- configure the GPIO pins correctly for rows and columns,
- detect key presses reliably.

There were two main constraints in this exercise:

1. **Each key press must be transmitted only once**.  
    When a button is pressed, the corresponding value should be sent a single time, not repeatedly every time the columns are multiplexed. Since column multiplexing is required for scanning the matrix, you must ensure that the transmission is triggered only on a _new_ key press.
    
2. **Handling multiple key presses**.  
    In principle, the matrix scanning approach allows detection of multiple simultaneous key presses. Your implementation should not inherently prevent this, even if you decide to process only one key at a time.
    
![[Pasted image 20251216171835.png]]
Regarding the **IOC configuration**, there is not much to add, since the pin assignments were already suggested. You had several GPIO inputs and outputs to configure. However, you should have noticed that **one of the rows is connected to pin PC13**, which is configured as an input. This pin is read by the microcontroller to receive data from the matrix.

PC13 is special because it is also connected to another component we have used in previous laboratories: the **blue user button**. In addition, you may have noticed that the **key matrix itself does not include a hardware debouncing circuit**, meaning that software debouncing is required.

However, unlike the other rows, **PC13 does have a hardware debouncing circuit** (from the blue button). This difference can lead to inconsistent behavior across rows if not handled carefully. You will later see that this issue can be addressed simply by **executing operations in the correct order**, without adding complex extra code. If the commands are not ordered properly, unexpected behavior may occur.

This issue is fundamentally related to the **hardware schematic**. One specific row (PC13) will behave differently, and potentially other rows as well, because the STM32F401 has a limited number of pins. As a result, some pins are shared across multiple peripherals. This can lead to side effects such as LEDs turning on unexpectedly or signals interfering with each other, due to interconnections or mild crosstalk.

For this reason, **PC13 requires special attention**, and you must explicitly handle this behavior in your code. Again, this does not require additional logic, but rather a correct sequencing of operations.

Apart from this, there are no major complications.

![[Pasted image 20251216185113.png]]
![[Pasted image 20251216185054.png]]

![[Pasted image 20251216185142.png]]
A key component of this implementation is the **timer**. In this case, **Timer 10** was chosen and configured in **interrupt mode** with a period of **4 milliseconds**, the same value used for the LED matrix scanning. This allows reuse of the same scanning frequency.

A 4 ms period is **much faster than human reaction time**, so the scanning of the key matrix will feel instantaneous to the user. In practice, although there is a small delay between pressing a button and detecting it, it is fast enough that it will not be perceived.

~~~~c#
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
~~~~
We do something similar to what you did with the encoder.
* The digital filter samples for a certain number of times the signal and checks if these are the same. 
* Otherwise it checks again.
We're going to do something like this. So every time we scan the column, we're going to see which buttons are pressed and which are not. And we want these buttons to stay pressed for at least a certain number of cycles.
* In this case, I chose 2. So if the button is pressed / released for two consecutive cycles, that means that the button is pressed or released. 
* If it stays up or down for one single cycle, it means it was probably noise. It was not an actual signal.

I chose 2 out of the fact that I have 4ms x 4 columns x 2 cycles should be 32 ms, which are enough for the bouncing 
==Of course, the longer the bounce time, the longer the reaction time of the button. So if you do one second, it's going to be a delay of maximum one second from when you press to when it is shown==

~~~~c#
// Keyboard character map - maps physical key positions to ASCII characters
// Layout: column-major order: [column0_row0, column0_row1, column0_row2, column0_row3, column1_row0, column1_row1, ...]
char map[16] = "FB73EA62D951C840";  // F, B, 7, 3, E, A, 6, 2, D, 9, 5, 1, C, 8, 4, 0

// Array to track how long each key has been pressed (in timer cycles)
uint32_t keypress[16];  
// Array to track if a key press has been acknowledged/sent already
uint32_t ack[16];       

// Current column being scanned (0-3)
int column_index = 0;
~~~~
I want to check if the key has already been pressed. And second of all, which is going to be useful, why to do the debouncing? And second of all, I have an acknowledgement. Why the acknowledgement? It's going to tell me if I've already sent the letter or not. If I've already sent it and that letter is pressed again at this next cycle, I'm not going to send it again. Okay. It's just two checks that I do. So there are flags, yes, but I have one flag for each letter. Why? Because this is useful for sending multiple letters

~~~~c#
// Main initialization - start the timer in interrupt mode
HAL_TIM_Base_Start_IT(&htim10);  // Timer 10 runs at 4ms period (250Hz)
~~~~

Starting from my main, I don't do anything but starting the timer, interrupt mode, and everything is going to happen inside of the interrupt. 

~~~c#
// Timer interrupt callback function - called every 4ms (when Timer 10 overflows)
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim) {
    // Check if this interrupt is from Timer 10
    if (htim == &htim10) {
        // ==============================================
        // STEP 1: READ CURRENT COLUMN'S ROWS
        // ==============================================
        // Scan all 4 rows for the currently active column
        // Note: Active-low logic: GPIO_PIN_SET = not pressed, GPIO_PIN_RESET = pressed
        
        // Check Row 0 for current column
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
        // ==============================================
        // STEP 2: ADVANCE TO NEXT COLUMN
        // ==============================================

        column_index = (++column_index) % 4;  // Cycle through columns 0→1→2→3→0...        
        // Activate only the current column (active-high drive)
        // Only one column is active at a time to prevent ghosting
        HAL_GPIO_WritePin(PIN_C0, (column_index == 0) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C1, (column_index == 1) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C2, (column_index == 2) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        HAL_GPIO_WritePin(PIN_C3, (column_index == 3) ? GPIO_PIN_SET : GPIO_PIN_RESET);
        
        // ==============================================
        // STEP 3: CHECK FOR DEBOUNCED KEY PRESSES
        // ==============================================
        // Scan through all 16 keys to check for valid presses
        for (int i = 0; i < 16; i++) {
            // Check if key has been pressed for more than DEBOUNCE_TIME cycles
            if (keypress[i] > DEBOUNCE_TIME) {
                // Key is validly pressed (debounced)
                if (ack[i] == 0) {
                    // First time detecting this debounced press - send character
                    HAL_UART_Transmit_DMA(&huart2, &map[i], 1);  // Send via UART2
                    ack[i] = 1;  // Mark as acknowledged
                }
            } else {
                // Key is not pressed (or not yet debounced)
                ack[i] = 0;  // Reset acknowledgement for next press
            }
        }
    }
}
~~~

## Key Concepts Explained:
1. **Matrix Scanning**:
    - Only one column is activated at a time
    - All rows are read for that column        
    - This prevents "ghosting" (false key detections)
2. **Debouncing Logic**:
    - Each key has a counter (`keypress[i]`) that increments while pressed
    - Only when counter exceeds `DEBOUNCE_TIME` (2 cycles = 8ms) is it considered a valid press
    - This filters out mechanical switch bounce (rapid on/off transitions)
3. **Acknowledgment System**:
    - `ack[i]` prevents repeated sending of the same key press
    - Only sends character when key is first debounced
    - Resets when key is released
4. **Timing**:
    - Full matrix scan: 4 columns × 4ms = 16ms
    - Debounce time: 2 cycles × 4ms = 8ms minimum
    - Max response time: 16ms (scan) + 8ms (debounce) = 24ms

The implementation efficiently scans a 4×4 keypad with debouncing and prevents key repeat until the key is released and pressed again.
# <span style="color:rgb(223, 109, 109)">Homework 10b: Read the encoder position and send to the PC the rotation speed in rpm</span> 

What you need to do is **enable both encoder channels**, because we want to detect rotation in **both directions**. The direction (positive or negative count) is determined by **comparing the two channels**, which are phase-shifted with respect to each other.
![[Pasted image 20251216211657.png]]
You can choose different **encoder modes** that define how the microcontroller reads these channels. In particular, you can select:

- **T1 mode**
- **T2 mode**
- **T1 and T2 combined mode**
    

The main difference between these modes is the **counting resolution**:
- In **T1 or T2 mode**, one mechanical revolution corresponds to **24 counts**
- In **T1 + T2 mode**, one mechanical revolution corresponds to **48 counts**
    
Because of this, you must be careful when computing position or speed and divide by **24 or 48**, depending on the selected mode.

You should also pay attention to **which edges are counted** (rising, falling, or both). This choice affects how the ticks are generated and how the direction is detected.

To clarify the difference between the modes:

- In **T1 or T2 mode**, the timer uses **both channels to determine direction**, but it **counts ticks from only one channel**
    
- In **T1 + T2 mode**, the timer still uses both channels for direction, but it **counts ticks from both channels**, effectively doubling the resolution
    
In our specific case, we are **forced to use Timer 3 in encoder mode**, because the encoder channels are physically connected to that timer. Both timer channels must be enabled to read channels A and B of the encoder.

==The **digital input filter** was also enabled, as discussed previously, to handle **mechanical bouncing** of the encoder. Without filtering, the bouncing would introduce noise and lead to incorrect counts.==

![[Pasted image 20251216211738.png]]
In addition, another timer was enabled and used as a **time base**. This timer reads the encoder count **once per second**, allowing us to determine how many ticks occur in one second. From this value, we can compute the **rotational speed in revolutions per minute (RPM)**.

To summarize:

- There are **three valid encoder configurations**    
- None of them is wrong
- The important points are:
    - Correct edge selection
    - Correct division factor (24 or 48)
    - Proper handling of direction
    - Use of input filtering
    
Beyond that, the implementation is straightforward.

### <span style="color:rgb(161, 40, 226)">For communication and don't forget interrupts</span>

![[Pasted image 20251216211759.png]]

![[Pasted image 20251216211822.png]]

### <span style="color:rgb(161, 40, 226)">For the code</span> 

As for the **code**, it is relatively straightforward. In `main.c`, I start **two timers**:

- **Timer 3** is configured in **encoder mode**. All encoder channels are enabled so that the timer can detect both the **rotation direction** and the **count increments or decrements**.
    
- **Timer 2 is configured in **interrupt mode**. Inside its interrupt callback, I read the encoder counter value from **Timer 3**.
    
~~~~c#
uint16_t oldcounts;
uint16_t counts = 0;
uint16_t delta;
char string[100];
~~~~

Even though Timer 3 itself is not configured to generate interrupts, it is still good practice to **check which peripheral triggered the interrupt**, since multiple timers are enabled. This avoids unexpected behavior and makes the code more robust.
~~~c#
	HAL_TIM_Encoder_Start(&htim3, TIM_CHANNEL_ALL);
	HAL_TIM_Base_Start_IT(&htim2);
~~~


Inside the Timer 2 interrupt, I implement a structure similar to what we used in the very first homework with `HAL_GetTick()` for data balancing. The idea is the following:
~~~~c#
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim){
	if(htim==&htim2){
		oldcounts = counts;
		counts = __HAL_TIM_GET_COUNTER(&htim3);
		delta = counts - oldcounts;
		float rpms = (delta/24.0)*60.0;
		int length = snprintf(string, sizeof(string), "Value %d \r\nDelta %d \r\nRPM %.2f\r\n", counts, delta, rpms);
		HAL_UART_Transmit_DMA(&huart2, string, length);
	}
}
~~~~
- I keep a variable called `old_counts`, which stores the **encoder count from the previous timer cycle**
- At each Timer 3 interrupt, I read the **current encoder count** using  
    `__HAL_TIM_GET_COUNTER(&htim3)`
- The encoder counter may have increased or decreased depending on the rotation direction
    
I then compute the **difference (delta)** between the current count and the previous count. This delta represents how many encoder ticks occurred during the last time interval (one second in this case).

To compute the **rotational speed in RPM**, I proceed as follows:

- I divide the delta by **24**, because I selected **T1 encoder mode**, which produces 24 counts per mechanical revolution
- I then multiply the result by **60**, to convert revolutions per second into **revolutions per minute**
    
This gives me the RPM value.
### Overflow and Underflow Handling

One important issue, which I already mentioned last time, is **counter overflow and underflow**.

This problem can be solved very simply by storing the counter values in a **signed 16-bit integer (`int16_t`) instead of an unsigned integer**.

Why does this work?

With an **unsigned integer**, if the counter underflows (for example, when rotating in the negative direction past zero), the value wraps around to something close to $2^{16}$. This would produce a very large delta value, which is physically impossible in one second and would result in an incorrect RPM calculation.

With a **signed integer**, overflow and underflow are handled naturally through **two’s complement representation**. When the counter wraps around, the sign bit changes, and the difference between the two values still yields the **correct delta**.

For example:

- Instead of going from `2` to a very large unsigned value
- The signed integer representation correctly produces a small negative delta
    
This approach automatically fixes both **overflow and underflow**, without requiring any additional conditional checks in the code.

Of course, you could also handle overflow and underflow manually with explicit checks, but using a signed integer is simpler and more elegant.

I strongly recommend trying this approach yourself if you did not discover it on your own. At first, it may seem unintuitive, but once you understand it, it becomes very clear—and it is also easy to explain during an exam.