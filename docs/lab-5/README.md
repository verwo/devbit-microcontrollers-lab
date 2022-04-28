---
title: lab-5
---

# Lab 5: Life, the Universe and Mbed

## Goal

1. Explore PWM
1. Explore ADC
1. Explore UART

## Prelude

1. Create a new project named **lab5** with mbed OS version 6.15.1

    ```bash
    mbed new lab5
    ```

1. Create a **main.cpp** file:

    ```cpp
    #include "mbed.h"

    int main(){
        printf(
            "Mbed OS version %d.%d.%d\n",
            MBED_MAJOR_VERSION,
            MBED_MINOR_VERSION,
            MBED_PATCH_VERSION
        );
        while(true);
    }
    ```

1. Compile and flash

    ```bash
    mbed compile -f
    ```

:::warning Assignment

1. Use a serial terminal to check the mbed version:

    ```bash
    mbed sterm
    ```

:::

1. Accept the [GitHub classroom](https://classroom.github.com/a/wlKwOVUg) assignment.
1. Add the GitHub repository created by GitHub Classroom as the remote of your lab5 repository

    ```bash
    git remote add origin git@github.com:microcontrollers-2122/lab5-microcontrollers-<your username here>.git
    ```

1. Add a .gitignore file containing:

    ```text
    BUILD
    __pycache__
    ```

1. Add to the git staging area:

    ```bash
    git add .
    ```

1. Commit:

    ```bash
    git commit -m"initial commit of lab 5"
    ```

1. Push:

    ```bash
    git push origin main
    ```

## PWM

1. Use the speaker on the [Mbed Application Shield](https://os.mbed.com/components/mbed-Application-Shield/) to play the following tune.
    1. Frequency is selected by period = 1.0  / frequency.
    1. Length is selected by setting PWM out at 0.5 and waiting the indicated number of milliseconds.
    1. Delay is selected by setting PWM out at 0 and waiting the indicated number of milliseconds.
        |Note| 	Frequency (Hz) | Length (ms) | Delay (ms) |
        | --- | --- |   --- |  --- |
        | 0 | 	110 |	480 | 100 |
        | 1 | 	110 | 	480 | 100 |
        | 2 | 	110 |	480 | 100 |
        | 3 | 	98 |	360 | 75 |
        | 4 | 	130 |	120 | 100 |
        | 5 | 	110 |	480 | 100 |
        | 6 | 	98 |	360 | 75 |
        | 7 | 	130 |	120 | 100 |
        | 8 | 	110 |	960 | 100 |
        | 9 | 	165 |	480 | 100 |
        | 10 | 	165 |	480 | 100 |
        | 11 | 	165 |	480 | 100 |
        | 12 | 	175 |	360 | 75 |
        | 13 | 	130 |	120 | 100 |
        | 14 | 	104 |	480 | 100 |
        | 15 | 	98 |	360 | 75 |
        | 16 | 	130 |	120 | 100 |
        | 17 | 	98 |	960 | 75 |

This is the initial code to play a note on the speaker of the Mbed Application Shield 

```cpp
#include "mbed.h"
#include "platform/mbed_thread.h"

DigitalIn fire(D4);
PwmOut spkr(D6);

void play_note(float frequency, uint32_t length);

int main()
{
    while (true)
    {
        while (!fire)
        {
        }
        
        play_note(110, 480);       
    }   
}

void play_note(float frequency, uint32_t length)
{
    spkr.period(1.0 / frequency);
    spkr = 0.5;

    thread_sleep_for(length);

    spkr = 0.0;
}
```

:::tip
Use three arrays: frequencies, lengths and delays
:::

:::warning Assignment
Play the tune on the speaker. Make a new branch, commit and push your code to GitHub.
:::

## ADC

On the Mbed Application Shield two potentiometers are connected respectively to pins A0 and A1. Also an RGB LED is connected to D5, D8 and D9 for respectively R, G and B.

The AnalogIN class provides an ADC, while the brightness (and therefore color) of the RGB can be controlled with PWM.

:::warning Assignment
Control R and B with the potentiometers.
:::

## LM75B

The LM75B is a digital temperature sensor.

Import the LM75B library:

```bash
mbed add http://os.mbed.com/users/chris/code/LM75B/
```

Example code for reading the temperature every second and send it to the UART:

```cpp
#include "mbed.h"
#include "platform/mbed_thread.h"
#include "LM75B.h"

const uint8_t MAXIMUM_BUFFER_SIZE = 32;

LM75B sensor(D14, D15);

int main()
{
    char buffer[MAXIMUM_BUFFER_SIZE] = {0};
    

    while (true)
    {
        int temp = sensor.read();
        uint8_t length = sprintf(buffer, "%s %d\n", "Temp = ", temp);
        printf(buffer, length);
        thread_sleep_for(1000);
    }   
}
```

:::warning Assignment
Rather than sending the temperature every second. Calculate the moving average every 5 seconds and round to the nearest integer value. Send this value to the pc when the button is pressed. Also change the color of the RGB LED to reflect the current temperature.
:::

## MMA7660 accellerometer (extra)

Use the [MMA7660 accellerometer](https://os.mbed.com/users/Sissors/code/MMA7660/) to control the behavior of the RGB LED. Note that the library uses the deprecated wait function. Wait accepts a float parameter representing a value in seconds. The function supported by Mbed OS6 thread_sleep_for accepts an integer parameter representing a value in milliseconds. You'll need to convert all waits into a thread_sleep_for.
