# Android Bluetooth Project Documentation

This documentation describes the assignment and creation of an Android app that uses Bluetooth to communicate with a Bluno Beetle Bluetooth Arduino device. The Beetle is connected to a 3d-printed camera stand prototype that has two servos connected to be able to rotate the stand both horizontally and vertically. The main purpose of the app is to send commands through Bt to control the stands rotation via servos.

## Prequisites
  * DfRobot [Bluno Beetle](http://https://www.dfrobot.com/product-1259.html.com)
  * Camera stand
  * Android phone, i got my hands on a LG leon with Android 6.0.
  * Power supplies & jumpercables & connectors

## The Android Application

The Android application is based on DfRobot's [BlunoBasicDemo](https://github.com/DFRobot/BlunoBasicDemo)- demo app.

### The Source
[github](https://github.com/mkamka/CameraBlunoApp)

## The Arduino Application

The app uses servo.h library for Arduino to connect to and control the servos. Otherwise it is a very simple implementation. The basic idea is that it reads character from serial connection and moves the servos based on the char it receives.
#### The Source
```c
#include <Servo.h>

Servo servoHorizontal;
Servo servoVertical;

int horPos = 0;
int verPos = 0;

void setup() {
   pinMode(A0, OUTPUT);
   pinMode(A1, OUTPUT);
   servoHorizontal.attach(A0); //analog pin 0
   servoHorizontal.write(horPos);

  servoVertical.attach(A1); //analog pin 1
  servoVertical.write(verPos);
  Serial.begin(115200);  //initial the Serial
}

void loop() {
  if (Serial.available())  {
    int lastCmd;
    char command = Serial.read();
    switch (command) {
      case 'u':
        lastCmd = servoVertical.read();
        if(lastCmd <= 175) {
          servoVertical.write(lastCmd + 5);
          delay(30);
          Serial.println(lastCmd + 5);
        } else {
          Serial.println("Yläpäässä");
        }
        break;
      case 'd':
        lastCmd = servoVertical.read();
        if(lastCmd >= 5) {
          servoVertical.write(lastCmd - 5);
          delay(30);
          Serial.println(lastCmd - 5);
        } else {
          Serial.println("Alapäässä");
        }
        break;
      case 'l':
        lastCmd = servoHorizontal.read();
        if(lastCmd >= 5) {
          servoHorizontal.write(lastCmd - 5);
          delay(30);
          Serial.println(lastCmd - 5);
        } else {
          Serial.println("Vasemmalla");
        }
        break;
      case 'r':
        lastCmd = servoHorizontal.read();
        if(lastCmd <= 175) {
          servoHorizontal.write(lastCmd + 5);
          delay(30);
          Serial.println(lastCmd + 5);
        } else {
          Serial.println("Oikealla");
        }
        break;
       case 'i':
          servoHorizontal.write(0);
          servoVertical.write(0);
          delay(1500);
          Serial.println("initialize");
        break;
      }
  }
}
```

## Bluno Beetle

The Beetle is connected to the servos from pins A0 and A1. It can be programmed using The Arduino IDE though its usb micro connector.

## Camera stand
I received the stand readymade, only needing a power supply and other cable connections.

## The Flow
User opens the Android app. User searches for available devices. The App will only connect to Bluno devices. When a device is found and the connection is made, user has access to a view where he can control the stand rotation. User can then disconnect from the device, and after he is routed to the same search view he was in first.
