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
    
  ![screenshot]https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/Lab_03_symulation.JPG
    
