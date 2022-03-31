---
title: Lab 4
---

# Lab 4: So long and thanks for all the Mbed

## Goal

1. Use timers
1. Explore interrupts

## Approach

Write a program for the assignments. Using both the [Mbed libraries](https://os.mbed.com/docs/mbed-os/v5.15/apis/drivers.html) and providing the low level code yourself.

1. Accept the [GitHub Classroom assignment](https://classroom.github.com/a/uh99BfFC)
1. Clone the GitHub Classroom repository
    ```bash
    git clone [[git URL]]
    ```
1. Make a branch per solution to the assignment
    ```bash
    git checkout -b [[branchname]]
    git checkout main
    ```
1. Push the results
    ```bash
    git push origin main
    ```

## Timer interrupt

Use a timer to toggle a LED, 3 seconds on and 1 second off using interrupts.

:::warning Assignment
Show the LEDs. What is frequency of the count signal?
:::

## External interrupt

:::warning Assignment
Toggle a LED using a button using the external interrupt rather than polling.
:::

## Timer counter

Connect a button. Pressing the button starts a timer. Pressing it again, stops the timer and outputs the timer value. Use *printf* to output the timer value. Pressing the button again resets the timer to start over.

:::warning Assignment
Try to press twice to get as close to a period of 1 second as possible.
:::
