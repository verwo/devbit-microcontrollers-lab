---
title: lab 3
---

# Lab 3: Mostly Mbed

## Goal

1. Assemble the protoshield.
1. Write low-level code to control the GPIO peripheral.
    1. Configure a digital output
    1. Read from a digital input

## GitHub Classroom

1. Follow the [Classroom URL](https://classroom.github.com/a/f2Uqq7sV), accept the assignment with your name and link your GitHub account.
1. Clone the repository.
1. Follow the instructions in the README.md to build the project.

## Adafruit protoshield

Follow the [instructions](https://learn.adafruit.com/adafruit-proto-shield-arduino/solder-it) to assemble the Adafruit Protoshield.

:::warning Assignment
Show your assembled protoshield.
:::

## Low level GPIO

For the following assignments you may not use **mbed.h**.

:::tip
To solve the assignments you may not use **mbed.h**. However if you want to test the hardware, you may use the Mbed library.
:::

Connect the green led and red led to a pin of your choice. 

Use the [example project](https://microcontrollers.netlify.app/digital-io/#gpio) to write the following program.

The green led blinks at a frequency of 2 Hz.
The red led blinks at a frequency of 1 Hz.

:::warning Assignment
Show the blinking leds. Add the schematic of your Protoshield to the REPORT.md
:::

Change the wait function so the parameter indicates microseconds instead of milliseconds.

:::warning Assignment
Use the oscilloscope to measure a 200 µs delay. Generate a square wave on a pin with a period of 200µs. Add the scope image to REPORT.md.
:::

Connect a push button to a pin. Read the value of the push button.

:::warning Assignment
If the value of the push button is '0' turn on the green led, if it is '1' turn on the red led.
:::

## Extra

Build a binary counter using the green led, red led and LD2 of the Nucleo. The green led is the MSB and LD2 the LSB.

:::warning Assignment
Make the counter count at a speed of 1 Hz.
:::

:::warning Assignment
Start the binary counter when pressing the button. Stop the binary counter when pressing the button again.
:::
