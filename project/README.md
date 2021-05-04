# Tachometer

### vypracovali:


Klimeš Jiří (),
Mostecký Jan (),
Němec Petr (),
Januška Tomáš ()

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

deska Arty A7-35T
![BoardImage](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Arty_A7_Board.PNG)

Popis desky
![BoardIO](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Board_Description.png)

Základní vstupy a výstupy
![BoardDescription](https://github.com/JanMostecky/Digital-electronics-1/blob/main/project/pictures/Basic_IO.PNG)


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
## Teoretický návrh tachometru

Pro zjednodušení implementace - vzhledem k našim začátečnických schopnostem ve VHDL - bylo rozhodnuto o ovládání tachometru jedním přepínačem a dvěma tlačítky. 

- Přepínač: zapínání a vypínání celého zařízení.

- Tlačítko A:
Přepínání zobrazených modulů na display. Pro tuto funkci byly navrženy dva různé moduly. První verze bylo použití stavového automatu, druhá verze za použití multiplexoru. 

- Tlačítko B:
Resetování celého zařízení, vynulování přičítání ujeté vzdálenosti. 

### Schéma top modulu




-----------------------------------
## VHDL moduly a jejich popis

### On_off modul

On_off modul slouží ke spouštění celého systému pomocí přepínače. 

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity on_off is
      Port (
            start_i : in  std_logic;     -- Input from Switch (0) to turn on/off the tachometer
            start_o : out std_logic     -- Output that starts other modules
            );
end on_off;

architecture Behavioral of on_off is

begin

      p_on_off : process(start_i)       -- When start_i changes ( we change the position of SW(0), the process is triggered)
         begin
            if (start_i = '1') then         -- Switch in position ON (or position 1)
                start_o <= '1';                 -- Output is 1
            else     -- Switch in position OFF (or 0)
                start_o <= '0';                 -- Output is 0
            end if;
         end process p_on_off;

end Behavioral;

```

```vhdl
library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;

entity tb_on_off is
--  Port ( );
end tb_on_off;

architecture Behavioral of tb_on_off is

        signal s_start_i      : std_logic;
        signal s_start_o      : std_logic;

begin
    uut_on_off : entity work.on_off
       
     port map(
            start_i  => s_start_i,
            start_o  => s_start_o
             );

    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        
        s_start_i     <= '0';
        wait for 100 ns;        
        s_start_i     <= '1';
        wait for 200 ns;        
        s_start_i     <= '0';
        wait for 20 ns;       
        s_start_i     <= '1';
        wait for 300 ns;        
        s_start_i     <= '0';
        wait for 200 ns;        
        s_start_i     <= '1';
        wait for 150 ns;

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end Behavioral;

```

### sensor modul


```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;


entity sensor is
  Port (
        input    : in  std_logic;
        en_i     : in  std_logic;
        reset    : in std_logic;
        
        revs_o   : out std_logic_vector(13 downto 0)
         );
end sensor;

architecture Behavioral of sensor is
    
    signal s_cnt_local : natural;
    
begin
    
    p_cnt_up_down : process(input, reset)
    begin
        
            if (reset = '1') then               -- Synchronous reset
                s_cnt_local <= 0;
            elsif (en_i = '1') then       -- Test if counter is enabled
                    -- TEST COUNTER DIRECTION HERE
                if rising_edge(input) then
                    if (s_cnt_local = 5000) then
                        s_cnt_local <=0;
                    else
                    s_cnt_local <= s_cnt_local + 1;
                    end if;
            end if;

        end if;
    end process p_cnt_up_down;

    revs_o <= std_logic_vector(to_unsigned(s_cnt_local, revs_o'length));

end Behavioral;

```

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;


entity tb_sensor is

end tb_sensor;

architecture Behavioral of tb_sensor is

        signal s_input      : std_logic;
        signal s_en_i       : std_logic;
        signal s_reset      : std_logic;
        signal s_revs       : std_logic_vector(13 downto 0);

begin
    uut_on_off : entity work.sensor

     port map(
            input  => s_input,
            en_i   => s_en_i,
            reset  => s_reset,
            revs_o   => s_revs
             );

    --------------------------------------------------------------------
    -- Reset generation process
    --------------------------------------------------------------------
    p_reset_gen : process
    begin
        s_reset <= '0';
        wait for 20 ns;
        
        -- Reset activated
        s_reset <= '0';
        wait for 30 ns;

        s_reset <= '0';
        wait for 700 ns;
        
        s_reset <= '0';
        wait for 70 ns;
        
        s_reset <= '0';
        
        wait;
    end process p_reset_gen;
    


    --------------------------------------------------------------------
    -- Data generation process
    --------------------------------------------------------------------
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        
        s_en_i     <= '1';
        
        s_input    <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;    
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';    
        wait for 10 ns;       
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;
        
        s_en_i      <='0';
        
        s_input    <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;        
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';    
        wait for 10 ns;       
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;
        
        
        s_en_i     <= '1';
        
        s_input    <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;        
        s_input     <= '0';
        wait for 10 ns;    
        s_en_i     <= '0';    
        s_input     <= '1';    
        wait for 10 ns;       
        s_input     <= '0';
        wait for 10 ns;    
        s_en_i     <= '1';    
        s_input     <= '1';
        wait for 10 ns;
        
        s_input    <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;        
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';    
        wait for 10 ns;       
        s_input     <= '0';
        wait for 10 ns;        
        s_input     <= '1';
        wait for 10 ns;
        
        
        s_input    <= '0';
        wait for 50 ns;        
        s_input     <= '1';
        wait for 40 ns;        
        s_input     <= '0';
        wait for 20 ns;        
        s_input     <= '1';    
        wait for 30 ns;       
        s_input     <= '0';
        wait for 70 ns;        
        s_input     <= '1';
        wait for 60 ns;
        
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end Behavioral;
```












### Testbench modules


-----------------------------------
## TOP module description and simulations

Write your text here.



-----------------------------------
## Video

*Write your text here*



-----------------------------------
## References

   1. Write your text here.
