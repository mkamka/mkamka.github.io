# Android Bluetooth Project Documentation

This documentation describes the assignment and creation of an Android app that uses Bluetooth to communicate with a Bluno Beetle Bluetooth Arduino device. The Beetle is connected to a 3d-printed camera stand prototype that has two servos connected to be able to rotate the stand both horizontally and vertically. The main purpose of the app is to send commands through Bt to control the stands rotation via servos.

## Prequisites
  * DfRobot [Bluno Beetle](http://https://www.dfrobot.com/product-1259.html.com)
  * Camera stand
  * Android phone, i got my hands on a LG leon with Android 6.0.
  * Power supplies & jumpercables & connectors

## The Android Application

The Android application is based on DfRobot's [BlunoBasicDemo](https://github.com/DFRobot/BlunoBasicDemo)- demo app.

## The Arduino Application

The app uses servo.h library for Arduino to connect to and control the servos. Otherwise it is a very simple implementation. The basic idea is that it reads character from serial connection and moves the servos based on the char it receives.

## Bluno Beetle

The Beetle is connected is connected to servos from pins A0 and A1. It can be programmed using The Arduino IDE though its usb micro connector.

## Camera stand
I received the stand readymade, only needing a power supply and other cable connections.

## The Flow
User opens the Android app. User searches for available devices. The App will only connect to Bluno devices. When a device is found and the connection is made, user has access to a view where he can control the stand rotation. User can then disconnect from the device, and after he is routed to the same search view he was in first.
