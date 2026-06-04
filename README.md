# UART Shell Project
This UART Shell project is a small, for fun project I did with the intention of reinforcing embedded systems concepts I learned in school. This project uses the UART communication protocol to send commands from my laptop to my STM32 NUCLEO-F411RE. These commands are simple, such as blinking an LED, however it establishes a foundation for future embedded work.

# What was done
1. Interrupt-driven RX
Interrupts were used to receive messages. This means that the CPU can process other tasks instead of busy waiting for a new message. To do this, the "HAL_UART_Receive_IT" and "HAL_UART_RxCpltCallback" functions were used to arm a byte for the interrupt, echo it, and then re-arm the byte again.
2. Ring Buffer
A ring buffer was introduced to manage incoming streams of data such that the ISR does not block it. This buffer is used for typing in the command prompt and stream of LED commands. The buffer sacrifices a slot to determine if it is full so that the head (transmit) does not overlap with the tail (receive). Also, the volatile keyword is used for head and tail variables because they are used for interrupts, and should not be cached / optimized by the compiler.
3. Line Parser
A line parser was made to accumulate user inputs into a buffer. This is used to trigger commands, such as turning an LED on.
4. Command Dispatcher
This command dispatcher compares inputs to commands in a state-machine fashion. For example, if the user types "led on" in the command prompt, the on-board LED will turn on. This has much more possibilities, such as commands to control output pins on the STM32 to turn on external devices, change brightness of an LED with PWM, turning on a fan, or typing and displaying to a LCD.

# What was learned overall  
This project reinforced and introduced topics related to embedded systems. This includes the difference between interrupt and polling, interrupt-driven UART RX, the purpose of a ring buffer, and implementing a line parser + command dispatcher.
