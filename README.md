# PID-DC-Motor-Speed-Controller Diagram + the code

The wiring Diagram

<img width="948" height="630" alt="image" src="https://github.com/user-attachments/assets/9a6eda00-6de8-4ec5-91b3-1f6bec1051f4" />



The code:

```cpp
#include <InterruptEncoder.h>

InterruptEncoder encoder;

const int motorForward = D5;
const int motorBackward = D3;
const int potPin = A2;

const float COUNTS_PER_REV = 600.0;

long lastCount = 0;
unsigned long lastTime = 0;

float rpm = 0;
String direction = "stop";

void setup() {
  Serial.begin(115200);

  encoder.attach(D8, D7);

  pinMode(motorForward, OUTPUT);
  pinMode(motorBackward, OUTPUT);
  pinMode(potPin, INPUT);

  analogReadResolution(12);
  analogWriteResolution(8);

  analogWrite(motorForward, 0);
  analogWrite(motorBackward, 0);

  lastCount = encoder.read();
  lastTime = millis();

  Serial.println("Motor Controller Ready");
  Serial.println("Commands: forward, backward, stop");
}

void loop() {

  // Read potentiometer
  int potValue = analogRead(potPin);

  // Convert potentiometer reading to voltage
  float voltage = potValue * 3.3 / 4095.0;

  // Convert potentiometer reading to PWM
  int pwm = map(potValue, 0, 4095, 0, 255);

  // Calculate speed percentage
  float speedPercentage = pwm * 100.0 / 255.0;

  // Read direction commands
  if (Serial.available() > 0) {

    String command = Serial.readStringUntil('\n');

    command.trim();
    command.toLowerCase();

    if (command == "forward") {
      direction = "forward";
    }

    else if (command == "backward" ||
             command == "backwards") {
      direction = "backward";
    }

    else if (command == "stop") {
      direction = "stop";
    }
  }

  // Motor direction and speed control
  if (direction == "forward") {
    analogWrite(motorBackward, 0);
    analogWrite(motorForward, pwm);
  }

  else if (direction == "backward") {
    analogWrite(motorForward, 0);
    analogWrite(motorBackward, pwm);
  }

  else {
    analogWrite(motorForward, 0);
    analogWrite(motorBackward, 0);
  }

  // Calculate RPM every 100 milliseconds
  unsigned long currentTime = millis();

  if (currentTime - lastTime >= 100) {

    long currentCount = encoder.read();
    long countDifference = currentCount - lastCount;

    float elapsedTime =
        (currentTime - lastTime) / 1000.0;

    rpm = (abs(countDifference) / COUNTS_PER_REV)
          * (60.0 / elapsedTime);

    lastCount = currentCount;
    lastTime = currentTime;

    // Display results
    Serial.print("Direction: ");
    Serial.print(direction);

    Serial.print(" | Voltage: ");
    Serial.print(voltage, 2);

    Serial.print(" V | PWM: ");
    Serial.print(pwm);

    Serial.print(" | Speed: ");
    Serial.print(speedPercentage, 1);

    Serial.print("% | RPM: ");
    Serial.println(rpm, 2);
  }
}
