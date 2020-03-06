---
title: lab-3
---

# Lab 3: Revenge of the Mbed

## Goal

1. Implement a binary counter, Gray code counter, and Snake counter on 4 leds  
1. Play a tune on the application board.
1. Setup TCP communication, between a client and a server


:::warning Assignment
This lab does not have any assignments and will not be graded. Enjoy!
:::

## LPC1768

1. Choose the [online](../lab-1/#mbed-blinky) or the [offline](../lab-1/#mbed-cli) Mbed development environment.
1. Select the [LPC1768](https://os.mbed.com/platforms/mbed-LPC1768/) as the target board.
    1. For the Mbed CLI compile with:
    ```bash
    mbed compile --target lpc1768 --toolchain GCC_ARM --flash
    ```

## Watch das blinking leds

![The LPC1768 board](./assets/mbed.png)

Figure 1: The LPC1768 board contains four leds.

1. Implement a binary counter on the four available leds (LED1, LED2, LED3 and LED4).
    1. Count from 0 to 15 in binary and start over again.
    1. LED1 represents the least significant bit, LED4 the most significant.
    1. For example: LED1 is ON, all other leds are OFF = '1', LED4 and LED1 are on, the other leds are off = '9'.
1. Implement a [Gray](https://en.wikipedia.org/wiki/Gray_code) code counter on the four available leds.
1. Implement a Snake counter on the four leds.
    |Decimal| 	Binary | Gray | Snake |
    | --- | --- |   --- |  --- |
    | 0 | 	0000 |	0000 | 0000 |
    | 1 | 	0001 | 	0001 | 0001 |
    | 2 | 	0010 |	0011 | 0011 |
    | 3 | 	0011 |	0010 | 0111 |
    | 4 | 	0100 |	0110 | 1111 |
    | 5 | 	0101 |	0111 | 1110 |
    | 6 | 	0110 |	0101 | 1100 |
    | 7 | 	0111 |	0100 | 1000 |
    | 8 | 	1000 |	1100 | 0000 |
    | 9 | 	1001 |	1101 | 0001 |
    | 10 | 	1010 |	1111 | 0011 |
    | 11 | 	1011 |	1110 | 0111 |
    | 12 | 	1100 |	1010 | 1111 |
    | 13 | 	1101 |	1011 | 1110 |
    | 14 | 	1110 |	1001 | 1100 |
    | 15 | 	1111 |	1000 | 1000 |

## Play a tune

1. Use the speaker on the [Mbed Application Board ](https://os.mbed.com/components/mbed-Application-Board/) to play the following tune. 
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

:::tip
Use three arrays: frequencies, lengths and delays
:::

## TCP communication

1. Use the Ethernet interface on the Mbed Application Board to set up [TCP communication](https://os.mbed.com/docs/mbed-os/v5.15/apis/network-socket.html) between a client and server. 
1. Work together and connect both boards (client & server) to a switch.
    ![Client and Server boards](./assets/client-server.png)

    Figure 2: The Client initiates communication with the Server, which listens and replies to the Client. Each have a unique IP address. The Server listens on a chosen port, while the client must connect to that port.

    :::danger Warning
    Choose unique IP addresses for each board in order to avoid conflicts.
    :::
1. Example Server code:
    ```cpp
    #include "mbed.h"
    #include "EthernetInterface.h"
    
    int main()
    {
        printf("Server example\n\r");
        
        EthernetInterface eth;

        //choose a unique IP address in the same network
        // set_network(HOST IP, SUBNET MASK, DEFAULT GATEWAY)
        eth.set_network("192.168.0.40","255.255.255.0","192.168.0.1");
        eth.connect();
        
        printf("The Server IP address is '%s'\n\r", eth.get_ip_address());
        
        TCPServer srv(&eth);  
        
        //choose a port to listen to
        srv.bind(4000);
        
        srv.listen();
        
        //server listens indefinitely
        while(true){
            TCPSocket client;
            SocketAddress client_addr;
            char *buffer = "Hello TCP client!\r\n";
            
            //setup connection
            srv.accept(&client, &client_addr);
            
            printf("Accepted %s:%d\n\r", client_addr.get_ip_address(), 
                        client_addr.get_port());
            
            // send reply to client            
            client.send(buffer, 256);
        
            client.close();
            
        }
    }
    ```
1. Example Client code:
    ```cpp
    #include "mbed.h"
    #include "EthernetInterface.h"

    int main()
    {
        printf("Client example\n\r");

        EthernetInterface eth;
        //choose a unique IP address in the same network
        // set_network(HOST IP, SUBNET MASK, DEFAULT GATEWAY)
        eth.set_network("192.168.0.39","255.255.255.0","192.168.0.1");
        eth.connect();

        printf("The client IP address is '%s'\n\r", eth.get_ip_address());

        TCPSocket socket;

        socket.open(&eth);
        //connect to server, use the server IP and chosen port
        socket.connect("192.168.0.40",4000);

        char rbuffer[64];

        //receive the data from the server
        int rcount = socket.recv(rbuffer, sizeof rbuffer);
        printf("received: %d\r\n", rcount);
        printf(rbuffer);

        socket.close();

    }
    ```

1. Expand the TCP examples: read the temperature sensor from the server and display the temperature on the client.  