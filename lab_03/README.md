# Lab_03 Vivado

## VHDL code of 4 to 1 multiplexor

```vhdl
architecture Behavioral of mux_2bit_4to1 is
begin
      f_o <= a_i when (sel_i = "00") else 
             b_i when (sel_i = "01") else
             c_i when (sel_i = "10") else
             d_i;
    
end architecture Behavioral;
```

## VHDL code for testbench

```vhdl
 p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;

        s_d   <= "10"; s_c <= "00"; s_b <= "10"; s_a <= "11"; s_sel <= "00"; wait for 100 ns;
           
               
        s_sel <= "01"; wait for 100 ns;
        
        s_sel <= "10"; wait for 100 ns;
        
        s_sel <= "11"; wait for 100 ns;
        
        report "stimulus process finished" severity note;
        wait;
        
    end process p_stimulus;
   
   ```
   
   
  ## Sreenshot of behavioral simulation
    
  ![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/Lab_03_symulation.JPG)
    
## My tutorial for vivado project

Step 1: In order to create project in Vivado, you have to start your program. After the instalation there is no shortcut to open the program. Go to the vivado folder on your hard drive, opeN: yourlocation/vivado/2020.2/bin, and open vivado file. Dialog window shows up. Wait for few seconds and than the program will start. After that there should be shortcut file on your desktop. 

step 2: Click on start new project. click next, rename your project, click next, practicly every time click next, you can create all necesery files in the project. Just make sure that every time you can, you choose VHDL or the language you understand. Insted of parts choose on of the boards. And click finish. 

step 3: Create design file. Simply click on files -> create new file -> and then add design file. Follow the same procedure for tesbench file, only choose simulation file instead of design. 

Step 4: Start the simulation. Click on the button: run behavioral simulation. 

Step 5: Hope you have not messed up the code! It should be fine. 
