# PID-DC-Motor-Speed-Controller Diagram + the code

The wiring Diagram

![Uploading Screenshot 2026-11-26 at 2.35.16 pm.png…]()




The code:

```cpp
#include <SPI.h>
#include <MFRC522.h>
#include <ESP32Servo.h>

// Complete project code
const int ENA = D5;
const int IN1 = D2;
const int IN2 = D3;

const int encoderA = D8;
const int encoderB = D7;
const int potPin = A2;

volatile long encoderCount = 0;

// Encoder counts per output shaft revolution
const float CPR = 600.0;
const float MAX_RPM = 100.0;

// Initial PID tuning values
float Kp = 2.0;
float Ki = 0.5;
float Kd = 0.1;

float integral = 0;
float previousError = 0;

unsigned long previousTime = 0;

void encoderISR() {
  if (digitalRead(encoderA) == digitalRead(encoderB)) {
    encoderCount++;
  } else {
    encoderCount--;
  }
}

void setup() {
  Serial.begin(115200);

  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  pinMode(encoderA, INPUT_PULLUP);
  pinMode(encoderB, INPUT_PULLUP);

  analogReadResolution(12);
  analogWriteResolution(8);

  attachInterrupt(
    digitalPinToInterrupt(encoderA),
    encoderISR,
    CHANGE
  );

  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  analogWrite(ENA, 0);

  previousTime = millis();
}

void loop() {
  unsigned long currentTime = millis();

  if (currentTime - previousTime >= 100) {

    float dt = (currentTime - previousTime) / 1000.0;
    previousTime = currentTime;

    noInterrupts();
    long counts = encoderCount;
    encoderCount = 0;
    interrupts();

    // Calculate actual motor speed
    float actualRPM = abs(counts) * 60.0 / (CPR * dt);

    // Read desired motor speed
    int potValue = analogRead(potPin);
    float targetRPM = potValue * MAX_RPM / 4095.0;

    float error = targetRPM - actualRPM;
    float derivative = (error - previousError) / dt;

    // PID control
    float candidateIntegral = integral + error * dt;

    float output = Kp * error
                 + Ki * candidateIntegral
                 + Kd * derivative;

    // Prevent integral windup
    if ((output >= 0 && output <= 255) ||
        (output > 255 && error < 0) ||
        (output < 0 && error > 0)) {
      integral = candidateIntegral;
    }

    int pwm = constrain((int)output, 0, 255);

    if (targetRPM < 1.0) {
      pwm = 0;
      integral = 0;
    }

    analogWrite(ENA, pwm);
    previousError = error;

    // Serial Plotter output
    Serial.print("Target_RPM:");
    Serial.print(targetRPM);

    Serial.print("\tActual_RPM:");
    Serial.print(actualRPM);

    Serial.print("\tPWM:");
    Serial.println(pwm);
  }
}
