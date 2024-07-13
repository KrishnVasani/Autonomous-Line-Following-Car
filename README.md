# Autonomous-Line-Following-Car
Designed and built a Car to navigate a path using infrared sensors and control algorithms, exploring robotics and sensor integration


Explanation: 
            The code defines pins for the IR sensors, motor control pins, and motor speed.
            In the loop function, the code reads sensor values and compares them to predefined thresholds to determine if the line is detected.
            Based on the sensor readings, the code calls functions to move the car forward, turn left, or turn right.
            The moveForward, moveLeft, and moveRight functions control the motor direction and speed using the L298N motor driver.
