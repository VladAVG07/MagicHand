Project Title: Magic Hand (Gesture-Controlled Turret)
1. General Description

The Magic Hand is a wireless tele-operation system that translates human hand gestures into mechanical movement. The system consists of a wearable glove equipped with flex sensors and an accelerometer (IMU). As the user moves their hand or flexes their fingers, an onboard microcontroller processes the analog data and transmits it wirelessly to a remote 2-axis turret.

For this specific iteration, the goal is to control a pan-tilt laser turret.

    Tilt (Up/Down): Controlled by flexing the index finger (or wrist pitch).

    Pan (Left/Right): Controlled by wrist rotation (IMU) or a second flex sensor.

    Action (Fire): Controlled by a specific gesture (e.g., making a fist or flexing the thumb).

2. Bill of Materials (BOM)
The Controller (The Glove)

    Microcontroller: ESP32 Development Board (Preferred for built-in wireless).

    Sensors:

        5x Flex Sensors (4.5 inch).

        1x IMU

    Components:

        Resistors

        Glove (fabric or worker's glove).

        Breadboard/Perfboard and Jumper wires.

The Receiver (The Turret)

    Microcontroller: ESP32 Development Board (or Arduino Uno if using external radio).

    Actuators:

        2x Servos

        1x Laser Diode module (5V).

    Structure: Pan/Tilt Servo Bracket Kit (3D printed or bought).

    Power: External 5V Power Supply (Batteries) for Servos.

5. Project Questions
Q1 - What is the system boundary?

The system boundary encompasses the Physical Glove, the Wireless Signal, and the Turret Mechanism.

    Input: The physical deformation of the sensors caused by the user's hand gestures.

    Output: The physical orientation of the turret and the state of the laser (On/Off).

    External Factors: The user's range of motion and ambient radio interference.

Q2 - Where does intelligence live?

The intelligence is distributed but edge-heavy on the Controller (Glove).

    Glove (Sender): Reads raw noisy analog signals, applies smoothing algorithms (like a moving average filter), creates the data packet, and handles the logic of "detecting a gesture."

    Turret (Receiver): Acts primarily as a "dumb" actuator that receives target angles and drives the motors to that position.

Q3 - What is the hardest technical problem?

Signal Noise and Mapping. Flex sensors are notoriously noisy and their resistance values drift. The hardest problem is writing software filters to stabilize the jitter so the turret moves smoothly rather than shaking uncontrollably. Additionally, mapping the non-linear resistance change of a flex sensor to the linear rotation of a servo requires careful calibration.
Q4 - What is the minimum demo?

A "Hello World" movement where flexing the index finger past a certain threshold moves the Turret Servo A from 0° to 90°, and straightening the finger returns it to 0°.
Q5 - Why is this not just a tutorial?

While the wiring implies a standard tutorial, this project involves systems integration. I am combining two distinct domains: wearable sensor technology and remote servo kinematics. I am writing custom code to handle the wireless protocol (ESP-NOW) and implementing a specific control scheme that translates flex intensity into velocity or position, which requires original logic not found in copy-paste tutorial code.
Do you need an ESP32?

YES. We need to buy two ESP32 boards.

    Why? The ESP32 has built-in Wi-Fi/Bluetooth. Using ESP-NOW allows the glove to talk to the turret with extremely low latency without needing complex external radio modules (like NRF24L01) or messy wiring. It is also small enough to fit comfortably on the back of the hand.
