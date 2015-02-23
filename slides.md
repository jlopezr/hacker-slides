# Internet of Things
## Introduction
---
## Course Information
* 11 Hours of class
* Theory
* Practical
    * Contiki project (6 weeks after last class)  

---
## Internet of Things

* It is a concept that has attracted much rhetoric, misconception and confusion as to what it means and its implications in a social context

* First proposed by [MIT Auto-ID Center](http://autoidlabs.org/) and intimately linked to [RFID](http://en.wikipedia.org/wiki/Radio-frequency_identification) and electronic product code ([EPC](http://www.gs1.org/barcodes))

* <em>... all about physical items talking to each other...</em>

---
## Internet of Things

* Refers to a network between objects, usually it  will be wireless and self-configuring, such as household appliances. <!-- .element: class="fragment" -->

* Has come to describe a number of technologies and research disciplines that enable the Internet to reach out into the real world of physical objects. <!-- .element: class="fragment" -->

---
## Dimensions
![iot axis](iot-axis.png) <!-- .element: class="stretch" -->

---
## Why?

* Dynamic control of industry and daily life
* Improve the resource utilization ratio 
* Better relationship between human and nature
* Act as a technology integrator

---
## Enabling technologies

* `RFID`: To identify and track the data of things 

* `Sensors`: To collect and process the data to detect the changes in the physical status of things

* `Networks`: To enhance the power of the network by transferring processing capabilities to different part of the network.

* `Nano Tech`: To make the smaller and smaller things have the ability to connect and interact.

---
### Applications. Intelligent Home
![intelligent-home](smart-home.jpg)

---
### Applications. Intelligent Home 2
![intelligent-home](smart-home-2.jpg)

---
### Applications. Smart Grid
![smart-grid](smart-grid.jpg)

---
### Applications. Shopping
![shopping](shopping.jpg)

---
### Applications. Health care
![smart-health](smart-health.jpg)

---
### Applications. Transportation
![shopping](transportation.jpg)

---
### Applications. Manufacturing
![shopping](smart-manufacturing.jpg)

---
### Applications. Farming
![shopping](smart-farming.jpeg)

---
### Applications. Logistics
![shopping](smart-logistics.jpg)

---
## State of the Art
![iot soa](iot-soa.png)

---
## Challenges

- Technological Standardization in most areas are still remain fragmented.
- Managing and fostering rapid innovation is a challenge for governments 
- Privacy and security
- Absence of governance

---
## Examples
The tado° smart thermostat and intelligent heating system

![](tado-box-570.jpg)

---
## Examples
The LIFX WiFi light bulb

![](lifx-570.png)

---
## Examples
Watteco IP Sensors

![](watteco-ipsensor.png)

---
## Examples
Zolertia Zoundtracker. Noise monitoring system

![](zolertia-zoundtracker-570.jpg)

---
### Some inspiration...

<a href="http://www.youtube.com/watch?feature=player_embedded&v=ozLaklIFWUI
" target="_blank"><img src="http://img.youtube.com/vi/ozLaklIFWUI/0.jpg" 
alt="IMAGE ALT TEXT HERE" border="10" /></a>

---
# Contiki

#### An Operating System 
#### for the Internet of things

---
## Installation

- Download [Instant Contiki](http://sourceforge.net/projects/contiki/files/Instant%20Contiki/)
- Download [Virtual Box](http://www.vmware.com/go/downloadplayer/)
- Follow [this](http://www.contiki-os.org/start.html) instructions

---
## Setup suggestions

* Spanish keyboard 
    * System Settings > Keyboard Layout > Layouts > Spanish
    
* Add include directories to Eclipse
    * /usr/local/avr/include
    * /home/user/CodeSourcery/SourceryG++Lite/arm-none-eabi/include

---
## Contiki

- Contiki – pioneering open source operating
system for sensor networks
    - <u>IP networking</u>
    - Hybrid threading model, <u>protothreads</u>
    - Dynamic loading
    - Power profiling
    - Network shell
- Small memory footprint
- Designed for portability
    - 14 platforms, 5 CPUs

---
## Name

The [Kon-Tiki raft](http://en.wikipedia.org/wiki/Kon-Tiki) sailed across the Pacific Ocean with minimal resources

![Kon-Tiki](Kon-Tiki.jpg)

## Targets

- Small embedded processors with
networking
    - Sensor networks, <b>smart objects</b> ...
- 98% of all microprocessors go into
embedded systems
- 50% of all processors are 8-bit
    - MSP430, AVR, ARM7, 6502, ...

---
## Background: uIP

- uIP – micro IP
- Open source
- ~5k code, ~2k RAM
    - Smallest configuration ~3k code, ~128 bytes
RAM
- RFC compliant
    - Order of magnitude smaller than previous stacks
- Bottom-up design
    - Single-packet buffer
    - <u>Event-driven</u> API

---
## uIP: API

- Two APIs
    - The “raw” uIP event-driven API
    - Protosockets, sockets-like programming based on protothreads
    
- Event-driven API works well for small programs
    - Explicit state machines

- Protosockets work better for larger programs
    - Sequential code

---
## Example

````
int smtp_protothread(struct psock *s)
{
    PSOCK_BEGIN(s);
    PSOCK_READTO(s, '\n');
    if(strncmp(inputbuffer, “220”, 3) != 0) {
    PSOCK_CLOSE(s);
    PSOCK_EXIT(s);
}

PSOCK_SEND(s, “HELO ”, 5);
PSOCK_SEND(s, hostname, strlen(hostname));
PSOCK_SEND(s, “\r\n”, 2);
PSOCK_READTO(s, '\n');
if(inputbuffer[0] != '2') {
    PSOCK_CLOSE(s);
    PSOCK_EXIT(s);
}
```

note: Not sure if this is needed

---
## Processes

* The Contiki kernel is event-based
    * Invokes processes whenever something
happens
        * Sensor events
        * Processes starting, exiting
* Process invocations must not block
* Protothreads provide sequential flow of
control in Contiki processes

[More info](https://github.com/contiki-os/contiki/wiki/Processes)

---
## Event driven

* Event-driven vs multithreaded
    * Event-driven requires less memory
    * Multithreading requires per-thread stacks

---
## Timers
[More info](https://github.com/contiki-os/contiki/wiki/Timers)

---
## Hello World

```
/* Declare the process */
PROCESS(hello_world_process, “Hello world”);
/* Make the process start when the module is loaded */
AUTOSTART_PROCESSES(&hello_world);

/* Define the process code */
PROCESS_THREAD(hello_world_process, ev, data) {
    PROCESS_BEGIN(); /* Must always come first */
    
    printf(“Hello, world!\n”); /* Initialization code goes here *
    while(1) { /* Loop for ever */
        PROCESS_WAIT_EVENT(); /* Wait for something to happen */
    }
    
    PROCESS_END(); /* Must always come last */
}
```
---
## More slides I

Building the Internet of Things

[Day 1 part 1](http://www.slideshare.net/ADunkels/building-the-internet-of-things-with-thingsquare-and-contiki-day-1-part-1)

[Day 1 part 2](http://www.slideshare.net/ADunkels/building-the-internet-of-things-with-thingsquare-and-contiki-day-1-part-2)

[Day 1 part 3](http://www.slideshare.net/ADunkels/building-day-1-upload-3)

[Day 2 part 1](http://www.slideshare.net/ADunkels/building-day-2-upload-1)

[Day 2 part 2](http://www.slideshare.net/ADunkels/building-the-internet-of-things-with-thingsquare-and-contiki-day-2-part-2)

[Day 2 part 3](http://www.slideshare.net/ADunkels/building-day-2-upload-building-the-internet-of-things-with-thingsquare-and-contiki-day-2-part-3)

---
## More slides II

Advanced IoT Firmware Engineering

[Day 1 part 1](http://www.slideshare.net/ADunkels/advanced-internet-of-things-firmware-engineering-with-thingsquare-and-contiki-day-1-part-1)

[Day 1 part 2](http://www.slideshare.net/ADunkels/advanced-internet-of-things-firmware-engineering-with-thingsquare-and-contiki-day-1-part-2)

[Day 1 part 3](http://www.slideshare.net/ADunkels/advanced-internet-of-things-firmware-engineering-with-thingsquare-and-contiki-day-1-part-3)


Other stuff

[6lowpan Book Exercises](http://www.slideshare.net/techdude/6lowpan-book-course-exercises-ppt)

[libellium smart world](http://www.libelium.com/wp-content/themes/libelium/images/content/applications/libelium_smart_world_infographic_big.png)

---
## Table Example
| Tables        | Are           | Cool  |
| ------------- |---------------| ----- |
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |