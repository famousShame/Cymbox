## Instrument 2 Source Code

```
#include <Servo.h>
Servo myServo;


int angle;
int sensorValue;
int sensorLow = 1023;
int sensorHigh = 0;
const int ledPin = 13;


void setup() {
  myServo.attach(9);
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, HIGH);
  while (millis() < 5000) {
    sensorValue = analogRead(A0);
    if (sensorValue > sensorHigh) {
      sensorHigh = sensorValue;
    }
    if (sensorValue < sensorLow) {
      sensorLow = sensorValue;
    }
    digitalWrite(ledPin, LOW);
  }
}


void loop() {
  sensorValue = analogRead(A0);

  if(sensorValue < 500) {
    angle = 150;
  } else {
    angle = 30;
  }
  myServo.write(angle);
 Serial.print(angle);
  //Serial.println(sensorValue);
  delay(15);
}
```
