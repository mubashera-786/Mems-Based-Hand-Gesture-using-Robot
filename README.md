MEMS-Based Hand Gesture Controlled Robot (IoT Project)
This project demonstrates the use of MEMS (Micro-Electro-Mechanical Systems) technology to control a robot using hand gestures. The robot moves in response to the tilt of your hand, detected using an ADXL345 accelerometer. The project incorporates an ESP8266 Wi-Fi module, allowing it to be controlled wirelessly. The motors are controlled by an L298N motor driver.

Features
Hand gesture-controlled robot using a MEMS accelerometer (ADXL345).
Wireless communication using ESP8266.
Ability to move forward, backward, left, right, or stop based on hand gestures.
Real-time gesture detection and motor control.

Components
ESP8266: Wi-Fi module for IoT integration.
ADXL345: 3-axis MEMS accelerometer for gesture recognition.
L298N: Motor driver to control the robot's motors.
Motors: Two DC motors for movement.
Power Supply: For powering the ESP8266, ADXL345, and motors.
Wires and Breadboard: For connections.

Hardware Setup
ADXL345 Sensor: Connect to the ESP8266 using I2C (SDA and SCL lines).
L298N Motor Driver: Connect to the ESP8266 to control the motors.

ESP8266 Pins:
D3 → Motor 1 (Forward)
D4 → Motor 1 (Backward)
D5 → Motor 2 (Forward)
D6 → Motor 2 (Backward)
Power Supply: Ensure a stable power source for the motors and ESP8266.

Software Setup
Install the following libraries in the Arduino IDE:
Adafruit Unified Sensor: For interfacing with the ADXL345.
Adafruit ADXL345 Library: For reading acceleration data from the sensor.
Program the ESP8266 with the code provided.

How It Works
The ADXL345 accelerometer measures the hand's tilt in three axes: X, Y, and Z.
The ESP8266 reads the sensor data and interprets hand gestures.
Tilting forward: Robot moves forward.
Tilting backward: Robot moves backward.
Tilting left or right: Robot turns left or right.
No tilt: Robot stops.

Circuit Diagram
Add a simple schematic illustrating connections between:

ESP8266
ADXL345
L298N Motor Driver
Motors
Installation
Clone this repository or download the code.
Open the code in the Arduino IDE.
Connect your ESP8266, upload the code, and power on the setup.
Usage
Power on the robot.
Use hand gestures to control the robot:
Forward Gesture: Tilt your hand forward.
Backward Gesture: Tilt your hand backward.
Left Gesture: Tilt your hand left.
Right Gesture: Tilt your hand right.
Stop Gesture: Keep your hand flat.

Code
The following is the main code controlling the robot's movement based on the hand gesture:
#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_ADXL345_U.h>
#define m1 D3
#define m11 D4
#define m2 D5
#define m22 D6

/* Assign a unique ID to this sensor at the same time */
Adafruit_ADXL345_Unified accel = Adafruit_ADXL345_Unified(12345);

void setup() {
  Serial.begin(9600);
  // Initialize ADXL345
  if (!accel.begin()) {
    Serial.println("Ooops, no ADXL345 detected ... Check your wiring!");
    while (1);
  }
  accel.setRange(ADXL345_RANGE_16_G);
  
  pinMode(m1, OUTPUT);
  pinMode(m11, OUTPUT);
  pinMode(m2, OUTPUT);
  pinMode(m22, OUTPUT);
}

void loop() {
  sensors_event_t event;
  accel.getEvent(&event);
  float x = event.acceleration.x;
  float y = event.acceleration.y;
  
  if (y < -7) forward();
  else if (y > 7) back();
  else if (x < -7) right();
  else if (x > 7) left();
  else stop1();
}

void forward() {
  digitalWrite(m1, HIGH);
  digitalWrite(m11, LOW);
  digitalWrite(m2, HIGH);
  digitalWrite(m22, LOW);
}

void back() {
  digitalWrite(m1, LOW);
  digitalWrite(m11, HIGH);
  digitalWrite(m2, LOW);
  digitalWrite(m22, HIGH);
}

void left() {
  digitalWrite(m1, LOW);
  digitalWrite(m11, HIGH);
  digitalWrite(m2, HIGH);
  digitalWrite(m22, LOW);
}

void right() {
  digitalWrite(m1, HIGH);
  digitalWrite(m11, LOW);
  digitalWrite(m2, LOW);
  digitalWrite(m22, HIGH);
}

void stop1() {
  digitalWrite(m1, LOW);
  digitalWrite(m11, LOW);
  digitalWrite(m2, LOW);
  digitalWrite(m22, LOW);
}

License
This project is open-source and free to use under the MIT License.
