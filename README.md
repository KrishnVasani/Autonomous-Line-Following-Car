# Autonomous-Line-Following-Car
Designed and built a Car to navigate a path using infrared sensors and control algorithms, exploring robotics and sensor integration

#define leftSensorPin  2  // Analog pin connected to left IR sensor
#define rightSensorPin 3  // Analog pin connected to right IR sensor
#define motorSpeed     150 // Speed of the motors (adjust as needed)

// Motor control pins connected to L298N
int in1 = 5;
int in2 = 4;
int in3 = 9;
int in4 = 8;

void setup() {
  pinMode(leftSensorPin, INPUT);
  pinMode(rightSensorPin, INPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
}

void loop() {
  int leftSensorValue = analogRead(leftSensorPin);
  int rightSensorValue = analogRead(rightSensorPin);

  // Define thresholds for black and white lines (adjust as needed)
  int blackThreshold = 700;
  int whiteThreshold = 300;

  // Control car movement based on sensor readings
  if (leftSensorValue < blackThreshold && rightSensorValue < blackThreshold) {
    // Both sensors on black (line lost) - move forward slowly
    moveForward(motorSpeed / 2);
  } else if (leftSensorValue < blackThreshold) {
    // Left sensor on black, right sensor on white - turn right
    moveRight(motorSpeed, motorSpeed / 2);
  } else if (rightSensorValue < blackThreshold) {
    // Right sensor on black, left sensor on white - turn left
    moveLeft(motorSpeed, motorSpeed / 2);
  } else {
    // Both sensors on white (on track) - move forward
    moveForward(motorSpeed);
  }
}

void moveForward(int speed) {
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
  analogWrite(5, speed);  // Adjust speed pin based on your motor driver
  analogWrite(9, speed);  // Adjust speed pin based on your motor driver
}

void moveLeft(int leftSpeed, int rightSpeed) {
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
  analogWrite(5, leftSpeed);  // Adjust speed pin based on your motor driver
  analogWrite(9, rightSpeed);  // Adjust speed pin based on your motor driver
}

void moveRight(int leftSpeed, int rightSpeed) {
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
  analogWrite(5, leftSpeed);  // Adjust speed pin based on your motor driver
  analogWrite(9, rightSpeed);  // Adjust speed pin based on your motor driver
}
