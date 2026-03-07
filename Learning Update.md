# Learning Update S1P

## Software: Control Logic

The Raspberry Pi should be the main driver of the rovers control system. Focusing, solely on high-level logic rather than low-level timing-sensitive controls. The Pi will be used to handle the web UI, camera streaming, decision-making, and communication between systems. The ESP32 should be the used for all real-time control tasks.

Servo control design should be done through a small state machine with defined positions under movement limits to ensure safe motions. For example, idle, lower, scoop, lift, dump, and reset. This allows for more predictable controls and is much easier to debug.

## Hardware: Components, Power Distribution, and Wiring

**Components**

Cytron 3A 16V dual channel motor driver - Controls the 2 DC drive motors through ESP32 PWM and is powered by the battery.
DC-DC Convertor - Takes input voltage from battery and converts to a lower voltage acceptable for other components (Pi & servos)
35 Kg servo (180 degree) - High torque servo motor that rotates between 0 and 180 degrees. Able to lift, hold, or push with high torque. 
25 Kg servo (180 degree) - Lower torque servo motor that rotates between 0 and 180 degrees. Used for dumping or low torque position control.
3s Li-Po battery - 3 Cells connected in series and powers the whole system.
Fuses - Used for safety when too much current flows, the fuse blows and disconnects power. Protects wiring from overheating, electronics damage, and battery from fault current.

**Power Distribution**

Power needs to be distributed across different power rails to avoid voltage drops, electrical noise, and resets. Even with separate power rails all the main components need to share a common ground to close the circuit preventing floating voltages (0V reference point). A Fuse should be placed around the main battery, the motor driver branch, servo branch, and Pi/logic branch. If any short happens throughout the rover all components are protected. 

**Wiring**

The breadboard is best used for low-power connections like the ESP32 and sensors. Wires must be plugged into the + and - rail on the board and next to the corresponding ground and 3.3V pin on the ESP32 for proper power. The same goes for the sensors, but they also need to be wired to the ESP32 SDA and SCL pins from its own SDA and SCL pins. On the rover, the use of WAGO lever nuts allows for a secure way to join and distribute power lines between the components as well as serve as a common ground connector.