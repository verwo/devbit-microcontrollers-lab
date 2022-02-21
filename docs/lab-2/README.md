---
title: Lab-2
---

# Lab 2: Mbed at the end of the universe

## Goal

1. Write C++ code to manipulate bits
1. Learn using pointers in C++ code

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

1. For the following assignments, accept the GitHub Classroom repository associated with lab 2.
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
Write a function *mirrornibble* which mirrors the lower nibble in a byte to the upper nibble of that byte.

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
