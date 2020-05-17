---
title: lab 4
---

# Lab 4: The last Mbed

## Goal

1. Write low-level code to control the GPIO peripheral.
1. Configure a digital output
1. Read from a digital input

## NUCLEO-L476RG

Based on the [low-level blinky example](https://microcontrollers.netlify.app/digital-io/#example) write code for the following scenario's:

1. PB10 outputs high for 5 ms and outputs low for 2 ms. This behavior loops forever.
1. PC1 outputs a square wave with a period starting at 1 ms, incrementing the period with 1 ms every cycle. When 500 ms is reached start over.
1. PA0 samples the value on its pin every 20 ms. Gather 100 samples.  

Submit the 3 programs in the assignment on Toledo.
