# HUMAN-FOLLOWING-ROBOT-CAR-USING-ARDUINO

**Project summary**
An Arduino Uno robot that follows a human/object using an ultrasonic distance sensor for range and two IR sensors for angular direction. Motors are driven by an L298N module. When the ultrasonic reports an object within the set range and the IR sensors detect the target, the car moves forward/left/right; if no target is found it stops.

**Components & roles**

Arduino Uno — main controller running the logic.

Ultrasonic sensor (e.g., HC-SR04) — measures distance to object (used to decide if the car should follow).

2 × IR sensors (left & right) — simple line/proximity detectors used to decide steering (left/right/forward).

L298N motor driver — drives two DC motors (H-bridge); PWM pins control speed.

DC motors + chassis + power supply — propulsion and mechanical platform.


**What’s good in your design**

Clear separation of sensor reading and movement functions (getDistance(), forward(), left(), right(), stopCar()).

Use of PWM for motor speed control (analogWrite on enable pins).

Serial debug prints make testing easier.


**Important technical issues & realistic limits**

1. 20 meters detection is unrealistic for common ultrasonic modules.
Typical hobby ultrasonic sensors (HC-SR04 family) reliably measure up to about 3–4 meters (≈300–400 cm) in ideal conditions. Claiming 20 m (2000 cm) is not achievable with standard modules — the hardware and beam spread make that impossible. Keep your DETECT_DISTANCE realistic (see suggestions).


2. pulseIn timeout set to 120000 µs matches the 20 m target (sound round-trip for 20 m is ≈117600 µs) but sensors won’t return accurate readings that far. Using such a long blocking timeout will stall your loop if no echo is received. Prefer shorter, realistic timeouts.


3. IR sensor logic depends on sensor type. Many IR modules output LOW when they detect something; confirm your sensors’ truth table. Your code assumes LOW == detected — that’s fine if tested, but document it.


4. Delay(100) in loop adds 100 ms latency. That’s usually fine but consider non-blocking timing (millis()) for more responsive control and sensor fusion.



**Practical wiring (pin map from your code)**

IR_LEFT → digital pin 2 (INPUT)

IR_RIGHT → digital pin 3 (INPUT)

Ultrasonic TRIG → digital pin 11 (OUTPUT)

Ultrasonic ECHO → digital pin 12 (INPUT)

L298N IN1/IN2 left → left1 (9), left2 (10)

L298N IN3/IN4 right → right1 (7), right2 (8)

L298N ENA → enLeft (5 PWM)

L298N ENB → enRight (6 PWM)
(Also connect grounds together: Arduino GND, motor battery negative, L298N GND.)

**Conclusion:**
The Human/Object Following Car project successfully demonstrates how Arduino can be used to build an intelligent robotic system that detects and follows a moving target using sensors. By integrating an Ultrasonic sensor for distance measurement, IR sensors for direction control, and an L298N motor driver for motor operation, the car achieves autonomous movement and obstacle response. Although the theoretical range of 20 meters exceeds the practical limits of common ultrasonic sensors, the project effectively shows real-time sensing, decision-making, and motor control principles. It provides a strong foundation for learning embedded systems, robotics, and sensor interfacing, and can be further improved by using advanced sensors, adding wireless control, or implementing algorithms for smoother navigation and enhanced accuracy.








Which of those would you like next?
