## Instrument 2 Source Code


[Back](https://famousshame.github.io/Cymbox/instrument-2)


[Home](https://famousshame.github.io/Cymbox)




```
/*
	Seamus Tynan -- Instrument #2
    Copyright (C) <2021>  <Seamus Tynan>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
*/
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
