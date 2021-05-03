# Tachometer

### Team members

Januška Tomáš
Klimeš Jiří
Mostecký Jan
Němec Petr

[Link to your GitHub project folder]( http://github.com/xxx)



-----------------------------------
### Project objectives

Console for bike
Hall sensor
Measuring - current speed
Measuring - how much distance was traveled
Measuring - time lenght of the travel

The goal of this project is to create Tachometer, that will work based on Hall senzor (based on Hall effect).
The Tachometer should (as mentioned above) measure time, lenght and velocity and all should be able to be displayed on a 7 segment display.

The code is written in VHDL.


-----------------------------------
## Hardware description

According to the assignment the code must be implementable on Arty A7 - 35T, or Arty A7 - 100T. We decided to choose Arty A7 - 35T.

Link to the Arty A7: Artix-7 FPGA Development Board:
https://store.digilentinc.com/arty-a7-artix-7-fpga-development-board/

All product support including documentation, projects, and the Digilent Forum can be accessed through the product resource center:
https://reference.digilentinc.com/reference/programmable-logic/arty-a7/start



But the most important are:

Reference Manual:
https://reference.digilentinc.com/reference/programmable-logic/arty-a7/reference-manual

Schematic:
https://reference.digilentinc.com/_media/reference/programmable-logic/arty-a7/arty_a7_sch.pdf



Arty A7-35T comes with several types of inputs or outputs, all can be seen on images below:

Board Image
![BoardImage](Images/Arty_A7_Board.png)

Board Description
![BoardDescription](Images/Board_Description.png)

Basic I/O
![BoardIO](Images/Basic_IO.PNG)



According to my basic VHDL and FPGA programming knowledge, the simplest way to operate this device that I could think of would be:
There will be 1 switch and 2 buttons.

- Switch: will have function of turning on/off the tachometer.

- First button:
The idea was to make this as FSM (finite state machine) whose states will change the displayed parameter.
All 3 measured parameters will be measured and calculated in parallel, but only one will be displayed at the time.
Hence the function of the first button, that is to change between the states, and thus change then displayed parameter.

- Second button:
The function of the second button is to simply reset the whole device.
Meaning, pressing the button should set the Distance, Time and Velocity to 0, and the counting will start over.



The 7 segment display:
The idea was to have 4 digit 7 segment display, to measure distance from 0 to 9999 metres.
That would also allow us to measure time from start (00:00) to maximum possible for 4 digit 7 seg. display (99:99), meaning 99 minutes and 99 seconds.
After that, the timer would reset and start over.
A better implementation would be with 6 digit 7 seg. display, that would allow us to measure (count) hours as well, extending the functionality of time measuring greatly.

Example of such display:
![BoardIO](Images/6Dig_7Seg_Display.PNG)

Available for example here:
https://www.aliexpress.com/i/32367486295.html

That display would include colon (double dot, ":") between hours, minutes and seconds.
And while measuring distance and velocity, colon wouldn't be displayed.




-----------------------------------
## VHDL modules description and simulations

Design modules






Testbench modules


-----------------------------------
## TOP module description and simulations

Write your text here.



-----------------------------------
## Video

*Write your text here*



-----------------------------------
## References

   1. Write your text here.
