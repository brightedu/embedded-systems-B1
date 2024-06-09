# PROJECTNAME :Decoding of an IR Signal Receiver with Arduino

1. [Introduction](#introduction)
2. [Hardware Requirements](#hardware-requirements)
3. [Software Requirements](#software-requirements)
4. [Wiring Diagram](#wiring-diagram)
5. [Code Explanation](#code-explanation)
6. [Installation](#installation)
7. [Usage](#usage)

   ## Introduction

This project demonstrates how to decode signals from an Infrared (IR) remote control using an Arduino. IR remote controls are widely used in various devices such as TVs, air conditioners, and audio systems. This guide will help you understand how to receive and decode these IR signals with an Arduino, allowing you to use an IR remote to control your own Arduino projects.

## Hardware Requirements

- Arduino Uno (or any compatible Arduino board)
- IR receiver module (e.g., VS1838B or similar)
- Jumper wires
- Breadboard
- IR remote control

## Software Requirements

- Arduino IDE (latest version)
- IRremote library for Arduino

## Wiring Diagram

Connect the IR receiver module to the Arduino as follows:

- *IR Receiver Module Pinout*:
  - VCC: Connect to 5V on the Arduino
  - GND: Connect to GND on the Arduino
  - OUT: Connect to digital pin 11 on the Arduino (or any other digital pin if you modify the code accordingly)


    IR Receiver Pin       Arduino Pin
    --------------        -----------
    VCC                  5V
    GND                  GND
    OUT                  Digital Pin 11


## Code Explanation

The code provided decodes the IR signal received by the IR receiver module and prints the decoded value to the Serial Monitor. This can be used to identify the signals sent by different buttons on an IR remote control.

### Code

cpp
#include <IRremote.h>

// Define the digital pin for the IR receiver
const int RECV_PIN = 11;

IRrecv irrecv(RECV_PIN);
decode_results results;

void setup() {
  Serial.begin(9600);  // Start the Serial Monitor
  irrecv.enableIRIn(); // Start the receiver
}

void loop() {
  if (irrecv.decode(&results)) {
    Serial.println(results.value, HEX); // Print the decoded value in HEX format
    irrecv.resume(); // Receive the next value
  }
}


### Explanation

1. *Include the IRremote Library*: The IRremote library is essential for decoding IR signals.
2. *Define the Pin*: The RECV_PIN constant defines the digital pin connected to the IR receiver's OUT pin.
3. *Initialize the IR Receiver*: The irrecv object is created to handle IR signals received on the defined pin.
4. *Setup Function*:
   - Serial.begin(9600): Initializes the serial communication at a baud rate of 9600.
   - irrecv.enableIRIn(): Starts the IR receiver.
5. *Loop Function*:
   - Checks if an IR signal has been received using irrecv.decode(&results).
   - Prints the decoded value to the Serial Monitor in hexadecimal format.
   - Resumes the receiver for the next signal with irrecv.resume().

## Installation

1. *Install the Arduino IDE*: Download and install the Arduino IDE from the [official website](https://www.arduino.cc/en/software).
2. *Install the IRremote Library*:
   - Open the Arduino IDE.
   - Go to Sketch > Include Library > Manage Libraries.
   - In the Library Manager, search for "IRremote" and install the latest version by shirriff.

## Usage

1. *Connect the Hardware*: Follow the wiring diagram to connect the IR receiver to the Arduino.
2. *Upload the Code*: Open the provided code in the Arduino IDE and upload it to your Arduino board.
3. *Open the Serial Monitor*: Go to Tools > Serial Monitor in the Arduino IDE.
4. *Press Buttons on the IR Remote*: Point your IR remote towards the receiver and press buttons. The decoded values will be displayed on the Serial Monitor.
