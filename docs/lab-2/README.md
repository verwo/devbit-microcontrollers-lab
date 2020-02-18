---
title: Lab-2
---

# Lab 2: Attack of the Mbeds

## Goal

1. Install the build tools for C++ on host
1. Write C++ code to manipulate bits
1. Learn using pointers in C++ code

## Build tools

1. Install gcc, g++ and make, choose your OS:
    1. On Windows:
        1. Enable the feature Windows Subsystem for Linux, open Powershell as an Administrator:
            ```bash
            Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
            ```
        1. Restart when prompted
        1. Go to the Microsoft store, install Ubuntu
        1. Launch Ubuntu and follow the Ubuntu instructions     
    1. On Ubuntu:
        1. Update your package lists 
            ```bash
            sudo apt-get update
            ```
        1. Install g++
            ```bash
            sudo apt-get install g++
            ```
    1. On Mac OS X:
        1. Experimental: Try installing XCode. Inform me if it worked.

    ::: tip

    Windows Subsystem for Linux (WSL) is a lightweight Virtual Machine to run Linux (development) tools. It is not a complete Virtual Machine and is not intended for production purposes, like running an Apache webserver. 

    While in the Microsoft Store, install the Windows Terminal app. This terminal allows you to run Powershell, WSL and CMD and provide a nice interface to these shells. Did you know [a terminal is not a shell](https://www.hanselman.com/blog/WhatsTheDifferenceBetweenAConsoleATerminalAndAShell.aspx)?

    More information on [WSL](https://www.hanselman.com/blog/CoolWSLWindowsSubsystemForLinuxTipsAndTricksYouOrIDidntKnowWerePossible.aspx) and [Windows Terminal](https://www.hanselman.com/blog/ItsTimeForYouToInstallWindowsTerminal.aspx). 

    :::

1. Write a Hello World program in a file called **hello.cpp**.
    ```cpp
    #include <iostream>
    using namespace std;
    
    int main() 
    {

        cout << "Hello World! \n"; 
        return 0;
    }
    ```
1. Locate the file **hello.cpp** and run:
    ```bash
    g++ hello.cpp
    ```
    ::: tip
    If you are using WSL, your Windows file system can be found at ```/mnt```, for example: ```/mnt/c/```
    :::
1. Run the binary
    ```bash
    .\a.out
    ```
::: warning Assignment
Write a program which displays *Hello [insert your name here]!*
:::

## Bit manipulation

1. Write a function *bitset* which sets a bit at a given position in a word. 
    ```cpp
    #include <iostream>
    #include "stdint.h"

    using namespace std;

    /**
    * Sets a bit at word at a given position
    * @param word as a reference
    * @param position of the bit to be set
    **/
    void bitset(uint32_t &word, uint8_t position)
    {
        // write your bitset implementation here
    }

    int main()
    {
        uint32_t x = 0xF0;
        // The hex streaming function sets the output formatting 
        // of numbers in the stream to hex 
        // it should be called only once
        cout << "Value x: " << hex << x << "\n";

        bitset(x, 2);
        
        cout << "Set bit 2 of x: " << x << "\n";
        return 0;
    }
    ```

1. The *bitset* function:
    1. Create the correct mask by shifting a single bit to the correct position:<br> ```uint32_t mask = 1 << position;```
    1. **OR** the mask with  ```uint32_t result = word | mask;```
    1. Assign the mask to word ```word = result;```
1. Or do it in a single statement:
    ```cpp
    /**
    * Sets a bit at word at a given position
    * @param word as a reference
    * @param position of the bit to be set 
    **/
    void bitset(uint32_t &word, uint8_t position){
        word |= (1 << position); 
    }
    ```

1. For the following assignments, clone the [test-bit-manipulations](https://github.com/pcordemans/test-bit-manipulations) repository.
1. To build the project and run the tests
    ```bash
    make
    ```
1. Edit the code in **bitmanipulator.cpp**

::: warning Assignment
Write a function *bittoggle* to toggle a bit at a given position in a word.
:::

::: warning Assignment
Write a function *bitclear* to clear a bit at a given position in a word.
:::

::: warning Assignment
Write a function *swapnibble* which swaps the upper with the lower nibble in a byte. 

For example:
Input: 0xA5
Output: 0x5A
:::

::: warning Assignment
Write a function *mirrornibble* which mirrors the lower nibble in a word in the upper nibble of a byte. 

For example:
Input: 0x05
Output: 0xA5
:::

::: warning Assignment
Write a function *ASCIItoBCD* which converts two [ASCII](https://www.asciitable.com/) characters of numbers to a single [Binary Coded Decimal](https://en.wikipedia.org/wiki/Binary-coded_decimal) (BCD).

For example:
Input (ASCII): upper = 0x31, lower = 0x32
Output (BCD): 0x12
:::

::: warning Assignment
Write a function *compactbytes* which retrieves four bytes from a byte array and puts these in a single word LSB first.

For example:
Input (array A): A[0] = 0x2, A[1] = 0xB, A[2] = 0x10, A[3] = 0xF0 
Output: 0xF010 0B02
:::

## Extra

1. Write a function *swaphalfword* which swaps the upper and the lower halfword in a word.
1. Write a function *mirrorhalfword* which mirrors the upper and the lower halfword in a word.
1. Write a function *compactbytesM* which retrieves four bytes from a byte array and puts these in a single word MSB first.
1. Write a function *expandBytes* which expands a word into an array of bytes LSB at position 0.
