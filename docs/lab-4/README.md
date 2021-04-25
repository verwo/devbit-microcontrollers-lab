---
title: Lab 4
---

# Lab 4: A new Mbed

## Goal

1. Use timers
1. Explore interrupts

## Timer interrupt

Use a timer to toggle a LED, 3 seconds on and 1 second off using interrupts.

:::warning Assignment
Show the LEDs. What is frequency of the count signal?
:::

## External interrupt

:::warning Assignment
Toggle a LED using a button using the external interrupt rather than polling.
:::

:::warning Assignment
Show the flank of the input signal on a scope. What seems to be the problem?
:::

:::warning Assignment
Debounce the input signal using a timer interrupt.
:::

## Timer counter

Connect a button. Pressing the button starts a timer. Pressing it again, stops the timer and outputs the timer value. You may use the [Serial](https://os.mbed.com/docs/mbed-os/v5.15/apis/serial.html) class of the Mbed library to output the timer value. Pressing it again resets the timer to start over.

:::warning Assignment
Try to press twice to get as close to a period of 1 second as possible.
:::
