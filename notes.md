# Links

- [Presentation](micropython-on-the-water.pdf)
- ![PILA Logo](saw64.png) [Pila - the Scons Tool](https://github.com/braiins/pila.git) - a free logo taken from https://pixabay.com/en/saw-tool-wood-carpentry-147284/

## The ECU board used

The ECU uses an open hardware flight controller - [Apogee](http://wiki.paparazziuav.org/wiki/Apogee/v1.00).

You can build it yourself or buy it from [alibaba](https://www.alibaba.com/product-detail/paparazzi-apogee-UAV-Flight-Control-ppz_60277228722.html). Technically any other flight controller with enough peripherals can be used.

## SConscript example using pila features
link to snippet https://paste.ubuntu.com/24802002/


# This talk is about how I
- (mis)used about 10 years of experience in embedded systems (experience shows that writing software for small devices is still very tedious on industry level and maintenance nightmare when not done right!)
- how I took micropython, freertos, linux kernel configuration management (Kconfig)
- for those not familiar with what micropython is... a 3.x implementation intended for bare-metal systems -> simple systems with 16+ kB SRAM and 64+ kB flash memory for program
- and used it out of pure passion to make my hobby advance a bit
- and the result is actually usable maybe on industry level?

# The demo is a proof of concept:

- that *business logic* and some non-realtime control processes can be moved to *Python* while the hard realtime is safely running in C with deadlines enforced by the realtime kernel
- uPy core can be isolated and used without its current complex HAL and drivers
- that scons can be used as powerful buildsystem in conjunction with configuration borowed from the Linux kernel

# The story

## What I don't like about uPy:
- a lot of duplicate code throughout all HALs/drivers
- provides complete reflection of the underlying hardware
- one can access every single pin -> not suitable for industry grade applications

## What I like about it:
- first implementation of Python 3.x standard that properly runs on bare metal


## What to do about it?
- take the uPy core only
- replace the build system
- write only thin HAL layer as python adapter for existing realtime HAL (braiins in house)
- integrate basic configuration options

Q: What should build micropython project?
A: Python!

## What is missing in embedded projects?
Flexible configuration management!

# Future
- real frozen modules/mpy cross compiler integration
- update for latest micropython
- integrate coroutines with RTOS -> RTOS aware async eventloop
- hal supports RX600 (Renesas), STM32


# TODO:
- async support in RT environment - RT aware eventloop
- mpy
