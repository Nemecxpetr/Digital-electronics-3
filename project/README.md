# Tachometer

### vypracovali:

Januška Tomáš (),
Klimeš Jiří (),
Mostecký Jan (),
Němec Petr ()

[Github project folder]( https://github.com/JanMostecky/Digital-electronics-1/tree/main/project)



-----------------------------------
## Cíl projektu

Cílem projektu bylo navrhnout a realizovat pomocí jazyku VHDL cyklo-tachometr. Následně výsledek projektu zpracovat do README.md souboru a videoprezentace. 

Funkce tachometru: měření rychlosti, Měření ujeté vzdálenosti.


-----------------------------------
## Použitý Hardware

Vytvořený kód měl být implementovatelný na desky Arty A7 - 35T, or Arty A7 - 100T. Pro tento projek byla zvolena deska Arty A7 - 35T.

Odkaz na stránky výrobce desky: Artix-7 FPGA Development Board:
https://store.digilentinc.com/arty-a7-artix-7-fpga-development-board/

Technická dokumentace desky, uživatelské fórum: 
https://reference.digilentinc.com/reference/programmable-logic/arty-a7/start

Manuál:
https://reference.digilentinc.com/reference/programmable-logic/arty-a7/reference-manual

Schéma:
https://reference.digilentinc.com/_media/reference/programmable-logic/arty-a7/arty_a7_sch.pdf


### Vstupy a výstupy desky Arty A7-35T:

Board Image
![BoardImage](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Arty_A7_Board.PNG)

Board Description
![BoardDescription](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Basic_IO.PNG)

Basic I/O
![BoardIO](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Board_Description.png)



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
