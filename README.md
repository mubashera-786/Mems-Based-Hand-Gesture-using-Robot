# Mems-Based-Hand-Gesture-using-Robot
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
