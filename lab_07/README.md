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
    begin
    report "Stimulus process started" severity note;
    s_d  <= '0';
    s_en <= '0';
    
    assert(s_q = '0')
    report "Error" severity error;
    
    --d sekv
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    --/d sekv
    
    assert(s_q = '0' and s_q_bar = '1')
    report "Error" severity error;
    
    s_en <= '1';
    
    --d sekv
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_en  <= '0';  -- en to 0
    wait for 200 ns;
    s_d  <= '0';    
    --/d sekv
    
    --d sekv
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    --/d sekv
    
    --d sekv
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    wait for 10 ns;
    s_d  <= '1';
    wait for 10 ns;
    s_d  <= '0';
    --/d sekv
    
    report "Stimulus process finished" severity note;
    wait;
    end process p_stimulus;
```

### Tb screenshot

![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/lab_07_tbdlatch.JPG)

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


### p_d_ff_rst

```vhdl
p_ff_rst : process (clk)             
begin                                         
    if rising_edge(clk) then
      if (rst = '1') then               
         q <= '0';
         q_bar <= '1';
      else                           
         q <= d;
         q_bar <= not d;
      end if;
   end if;             
end process p_ff_rst;   
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

### p_t_ff_rst
```vhdl
p_t_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                s_q     <= '0';
                s_q_bar <= '1';
            else
                if (t = '0') then
                    s_q     <= s_q;
                    s_q_bar <= s_q_bar;
                else
                    s_q     <= not s_q;
                    s_q_bar <= not s_q_bar;
                end if;    
            end if;
        end if;
    end process p_t_ff_rst;
    
    q     <= s_q;
    q_bar <= s_q_bar;
```

## Testbenches

### tb_p_d_ff_arst

```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk <= '0';
            wait for c_clk_PERIOD / 2;
            s_clk <= '1';
            wait for c_clk_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
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
    
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_d <= '0';
        
        --d sekv
        wait for 14 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        
       
        wait for 4 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';   
        --/d sekv
        
        --d sekv
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';   
        --/d sekv
        
    report "Stimulus process finished" severity note;
    wait;
    end process p_stimulus;
```

### tb_p_d_ff_rst

```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk <= '0';
            wait for c_clk_PERIOD / 2;
            s_clk <= '1';
            wait for c_clk_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
 p_reset_gen : process
    begin
        s_rst <= '0';
        wait for 28 ns;
        
        -- Reset activated
        s_rst <= '1';
        wait for 53 ns;

        -- Reset deactivated
        s_rst <= '0';

        wait;
    end process p_reset_gen;
    
 p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_d <= '1';
        
        --d sekv
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';        
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        
        assert(s_q = '0' and s_q_bar = '1')
        report "Error - Failed" severity error;
        
        wait for 20 ns;
        s_d  <= '1';
        wait for 25 ns;
        
        assert(s_q = '1' and s_q_bar = '0')
        report "Error - Failed" severity error;
        --/d sekv
        
        --d sekv
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';
        wait for 10 ns;
        s_d  <= '0';
        wait for 10 ns;
        s_d  <= '1';   
        --/d sekv
        
    report "Stimulus process finished" severity note;
    wait;
    end process p_stimulus;
```

### tb_jk_ff_rst

```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk <= '0';
            wait for c_CLK_PERIOD / 2;
            s_clk <= '1';
            wait for c_CLK_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    
    p_reset_gen : process
    begin
        s_rst <= '0';
        wait for 28 ns;
        
        -- Reset activated
        s_rst <= '1';
        wait for 53 ns;

        -- Reset deactivated
        s_rst <= '0';

        wait;
    end process p_reset_gen;
    
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_j <= '0';
        s_k <= '0';
        
        --d sekv
        wait for 37 ns;
        s_j <= '0';
        s_k <= '0';        
        wait for 3 ns;
        s_j <= '1';
        s_k <= '0';                       
        wait for 7 ns;
        s_j <= '0';
        s_k <= '1';        
        wait for 14 ns;
        s_j <= '1';
        s_k <= '0';       
        wait for 7 ns;
        s_j <= '1';
        s_k <= '1';
        --/d sekv
        
        --d sekv
        wait for 7 ns;
        s_j <= '0';
        s_k <= '0';             
        wait for 7 ns;
        s_j <= '0';
        s_k <= '1';     
        wait for 7 ns;
        s_j <= '1';
        s_k <= '0';     
        wait for 7 ns;
        s_j <= '1';
        s_k <= '1';
        --/d sekv

        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```




