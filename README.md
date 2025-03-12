Automated Parking Gate 

Overview

The Automated Parking Gate is a smart system designed to control vehicle access using an ultrasonic sensor and a servo motor. When a vehicle is detected within a specified range, the servo motor lifts the gate automatically. This project is ideal for use in parking lots, residential areas, or commercial buildings.

Features

 Ultrasonic Sensor-Based Detection – Detects vehicles approaching the gate.

 Servo Motor Control – Lifts and lowers the gate smoothly.

 Automated Operation – No manual intervention required.

 Serial Monitor Output – Displays distance measurements and gate status.

Components Used

Arduino Uno (or equivalent)

HC-SR04 Ultrasonic Sensor

SG90 Servo Motor

Jumper Wires

Power Supply (5V)

Circuit Diagram

(Include an image of your circuit wiring here)

Code

#include <Servo.h>

// Pin definitions
int triggerPin = 11;
int echoPin = 12;
int servoPin = 13;

// Distance measurement variables
long duration;
int distance;

// Servo object
Servo servo;

// Threshold distance (in cm)
int thresholdDistance = 20;

void setup() {
  Serial.begin(9600);
  servo.attach(servoPin);
  pinMode(triggerPin, OUTPUT);
  pinMode(echoPin, INPUT);
  servo.write(0); // Start position
  delay(1000);
}

void loop() {
  distance = measureDistance();
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < thresholdDistance && distance > 0) {
    servo.write(90);
    Serial.println("Vehicle detected! Gate opening.");
    delay(2000);
  } else {
    servo.write(0);
    Serial.println("No vehicle detected. Gate closed.");
    delay(1000);
  }
}

int measureDistance() {
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  return duration * 0.034 / 2;
}

Installation & Usage

Assemble the circuit as per the diagram.

Upload the code to your Arduino board.

Power the system and place an object (vehicle) in front of the sensor.

Observe the servo motor lifting the gate when an object is detected.

Troubleshooting

Servo not moving?

Ensure the servo is connected to a PWM pin.

Check power connections.

Use Serial.println() for debugging distance values.

Sensor not detecting?

Verify wiring and trigger/echo pin assignments.

Increase the detection threshold if needed.

Future Enhancements

 RFID Integration for authorized vehicle access.

 Mobile App Control for remote operation.

 Solar-Powered Option for energy efficiency.



Author

[Nicholas Dunwoody]
