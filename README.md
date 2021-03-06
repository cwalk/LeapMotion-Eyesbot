## Introduction

Leap Motion projects with Eyesbot robot

## YouTube

YouTube: https://www.youtube.com/watch?v=p1Aup4VvjZU

## Summary

Eyesbot is a robot engineered by a very intelligent coworker of mine. It is mainly made out of 3D printed material, with silicon molded grip attached to 2 rear wheels. The front has a ball on the underside to allow it to roll smoothly. The electronics consist of a custom PCB using Bluetooth to connect to a smart device (like an iPod or iPhone) which the robot uses to communicate to a backend service. The device's front facing camera can be used for navigation, or taking pictures. The front of the robot also has 2 LEDs for headlights.

## Code Setup

Make sure you have nodejs and npm installed.

Install cylonjs, a robotics javascript framework. More info here: https://cylonjs.com

For more info on Leap Motion, check out: http://cylonjs.com/documentation/drivers/leapmotion/

Clone the directory: `git clone https://github.com/cwalk/LeapMotion-Eyesbot`

Navigate to the directory and do an `npm install` and you should have cylon and cylon-leapmotion.

## Robot Setup

First, make sure the robot is turned on. Turn on your iDevice, and strap it in to the robot. Make sure you device has bluetooth turned on, and switch the bluetooth connector on the robot on. Once the device and the robot connect, we can use the device to connect to the backend service. Once that is connected, we can run the node script to control the robot through the Leap Motion.

## Usage

Run the files by using the command `node Eyesbot.js`

This allows us to send commands through HTTP GETS to the backend service, depending on where our hand is over the Leap Motion. 

## Control

Currently the code allows the user to drive the robot as follows in the diagram below. You can change the values to speed up/slow down the robot if you wish.

If your hand is above a value of 200 on the Y axis, as percieved by the Leap Motion, the code automatically send the speeds "0.0" to both the left and right wheels, essentially stopping the robot. If you ever want to stop the robot, just move your hand higher on the Y axis until the robot stops moving.

If you wish to move forward, you must put your hand past at least a value of -30 in the Z axis. If the X axis is detected greater than 50, you will move forward right, or less than -50 forward left. If X axis is between -50 and 50, you will move straight forward.

Similarly, if you wish to move backwards, you must put your hand at least a value of 30 in the Z axis. If the X axis is detected greater than 50, you will move backward right, or less than -50 backward left. If X axis is between -50 and 50, you will move straight backward.

![Movement Diagram](/Movement Diagram.jpg?raw=true "Movement Diagram")

Here is a diagram of the axis for the Leap Motion as reference (I know, it's confusing why the Z axis is reversed, oh well. I accounted for that in the code, so your movements should be natural, and the robot will mimic your hand over the Leap Motion).

![Leap Motion Axes Diagram](/Leap Motion Axes.png?raw=true "Leap Motion Axes Diagram")

## Gesture Support

The code currently supports 2 gestures; keyTap and screenTap

- **keyTap**: Perform a keyTap gesture over the Leap Motion to turn on the Eyesbot's headlights. Doing it a 2nd time will turn them off.

- **screenTap**: Perform a screenTap gesture over the Leap Motion to take a picture with the iDevice's front facing camera. You can later access this in the camera roll of the Photos application. 
