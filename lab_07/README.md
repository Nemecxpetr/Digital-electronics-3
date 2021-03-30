# Lab 7: Latches and Flip-flops

## Preparation task

### D latch

 | **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | no change |
   | 0 | 1 | 0 |  change |
   | 1 | 1 | 1 | no change |
   | 1 | 0 | 1 |  change |
   
   q(n+1) = d
   
### JK flip-flop

   | **J** | **K** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | 0 | No change |
   | 0 | 0 | 1 | 1 | No change |
   | 0 | 1 | 0 | 0 | reset |
   | 0 | 1 | 1 | 0 | reset |
   | 1 | 0 | 0 | 1 | set |
   | 1 | 0 | 1 | 1 | set |
   | 1 | 1 | 0 | 1 | toggle |
   | 1 | 1 | 1 | 0 | toggle |
   
   q(n+1) = j*q(n)! + k!*q(n)
   
### T flip-flop

   | **T** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | no change |
   | 0 | 1 | 1 | no change |
   | 1 | 0 | 1 | invert |
   | 1 | 1 | 0 | invert |
   
   q(n+1) = t*q(n)! + t!*q(n)

## D latch

### VHLD code process p_d_latch

```vhdl
p_d_latch : process (d, arst, en)
begin
    if (arst = '1') then
        q     <= '0';
        q_bar <= '1';
    elsif  (en = '1') then
        q <= d;
        q_bar <= not d;        
    end if;
end process p_d_latch;
```

### VHDL code tb_d_latch

```vhdl
p_reset_gen : process
    begin
        s_arst <= '0';
        wait for 28 ns;
        
        -- Reset activated
        s_arst <= '1';
        wait for 53 ns;

        -- Reset deactivated
        s_arst <= '0';

        wait;
    end process p_reset_gen;
    
    p_stimulus  : process
```

### Tb screenshot

## Flip-flops

### p_d_ff_arst

```vhdl
p_ff_arst : process (clk, arst)             
begin                                         
    if (arst = '1') then                      
        q     <= '0';                         
        q_bar <= '1';
                                
    elsif  rising_edge(clk) then                    
        q <= d;                               
        q_bar <= not d;                       
    end if;                                   
end process p_ff_arst;                 
```

### p_jk_ff_rst

```vhdl
p_jk_ff_rst : process (clk)             
begin                                         
  if rising_edge(clk) then 
       if (rst = '1') then
          s_q <= '0';
      else
          if (j = '0' and k = '0') then
              s_q <= s_q;
          elsif (j = '0' and k = '1') then
              s_q <= '0';
          elsif (j = '1' and k = '0') then
              s_q <= '1';
          elsif (j = '1' and k = '0') then                   
              s_q <= not s_q;  
          end if; 
        end if;                   
    end if;                                   
end process p_jk_ff_rst;       

  q <= s_q;
  q <= not s_q;

end Behavioral;
```

