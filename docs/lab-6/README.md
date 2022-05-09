---
title: lab-6
---

# Lab 6: And another Mbed...

## Goal

1. Set up Ethernet communication with the FRDM-K64F board using the Mbed libraries

## FRDM-K64F

As the Nucleo-L476RG does not support Ethernet, in this lab the [FRDM-K64F](https://os.mbed.com/platforms/FRDM-K64F/) is used.

:::tip
As this is a different microcontroller, you will need to change the target of the build command.
:::

## TCP communication

1. Use the Ethernet interface to set up [TCP communication](https://os.mbed.com/docs/mbed-os/v5.15/apis/network-socket.html) between a client and server.

* Use the examples TCPServer and TCPClient (work together):
    * Example [TCP Server](https://os.mbed.com/users/pcordemans/code/tcp-server/)
    * Example [TCP Client](https://os.mbed.com/users/pcordemans/code/tcp-client/)
* Accept the [GitHub Classroom](https://classroom.github.com/a/OcHniFYw) assignment.
* Commit and push your results to the repository

:::warning Assignment
Expand the TCP examples: read the potentiometer values from the client and change the color of the LED of the server accordingly. 
:::

:::tip string is not a char array
One of the easiest ways to manipulate strings is to use the C++ [string](http://www.cplusplus.com/reference/string/string/) class. However a C++ **string** is not an array of characters. The *send* and *recv* methods expect a **char** array so a **string** needs to be converted. The **string** class has a method *c_str* which returns the **char** array equivalent of the **string**.
:::
