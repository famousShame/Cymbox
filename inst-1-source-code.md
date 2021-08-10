## Instrument 1 Source Code


[Back](https://famousshame.github.io/Cymbox/instrument-1)


[Home](https://famousshame.github.io/Cymbox/)




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
    
    [GNU Public License](https://www.gnu.org/licenses/gpl-3.0.html)
*/
const int controlPin1 = 2;
const int controlPin2 = 3;
const int enablePin = 9;
const int directionSwitchPin = 4;
const int onOffSwitchStatePin = 5;
const int potPin = A0;
int onOffSwitchState = 0;
int previousOnOffSwitchState = 0;
int directionSwitchState = 0;
int previousDirectionSwitchState = 0;
int motorEnabled = 0;
int motorSpeed = 0;
int motorDirection = 1;


void setup() {
  pinMode(directionSwitchPin, INPUT);
  pinMode(onOffSwitchStatePin, INPUT);
  pinMode(controlPin1, OUTPUT);
  pinMode(controlPin2, OUTPUT);
  pinMode(enablePin, OUTPUT);
  digitalWrite(enablePin, LOW);

}

void loop() {
  onOffSwitchState = digitalRead(onOffSwitchStatePin);
  delay(1);
  directionSwitchState = digitalRead(directionSwitchPin);
  motorSpeed = analogRead(potPin)/10;
  if (onOffSwitchState != previousOnOffSwitchState) {
    if(onOffSwitchState == HIGH){
      motorEnabled = ! motorEnabled; 
    }
  }
  if (directionSwitchState != previousDirectionSwitchState){
    if(directionSwitchState == HIGH) {
      motorDirection = ! motorDirection;
    }
  }
  if(motorDirection == 1){
    digitalWrite(controlPin1, HIGH);
    digitalWrite(controlPin2, LOW);
  }else{
    digitalWrite(controlPin1, LOW);
    digitalWrite(controlPin2, HIGH);
  }
  if(motorEnabled == 1) {
    analogWrite(enablePin, motorSpeed);
  }else{
    analogWrite(enablePin, 0);
  }
  previousDirectionSwitchState = directionSwitchState;
  previousOnOffSwitchState = onOffSwitchState;
  
}
```
