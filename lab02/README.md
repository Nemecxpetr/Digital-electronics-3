# Lab 02: Cinbinational logic

## Truth Table:

| **Dec. equivalent** | **B[1:0]** | **A[1:0]** | **B is greater than A** | **B equals A** | **B is less than A** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 0 | 0 0 | 0 | 1 | 0 |
| 1 | 0 0 | 0 1 | 0 | 0 | 1 |
| 2 | 0 0 | 1 0 | 0 | 0 | 1 |
| 3 | 0 0 | 1 1 | 0 | 0 | 1 |
| 4 | 0 1 | 0 0 | 1 | 0 | 0 |
| 5 | 0 1 | 0 1 | 0 | 1 | 0 |
| 6 | 0 1 | 1 0 | 0 | 0 | 1 |
| 7 | 0 1 | 1 1 | 0 | 0 | 1 |
| 8 | 1 0 | 0 0 | 1 | 0 | 0 |
| 9 | 1 0 | 0 1 | 1 | 0 | 0 |
| 10 | 1 0 | 1 0 | 0 | 1 | 0 |
| 11 | 1 0 | 1 1 | 0 | 0 | 1 |
| 12 | 1 1 | 0 0 | 1 | 0 | 0 |
| 13 | 1 1 | 0 1 | 1 | 0 | 0 |
| 14 | 1 1 | 1 0 | 1 | 0 | 0 |
| 15 | 1 1 | 1 1 | 0 | 1 | 0 |

## Karnaugh maps: 
### B>A
![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/K-map%20SoP.JPG)

y(B1, B0, A1, A0) = B1 * !A1 + B0 * !A1 * !A0 + B1 * B0 * !A0

### B<A
![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/K-map%20PoS.JPG)

y(B1, B0, A1, A0) = (A1 + A0) * (!B1 + !B0) * (!B1 + A1) * (!B1 + A0) * (!B1 + A1)

### B=A
![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/K-map%20B%3DA.JPG)

## 2-bit comparator

### Eda playground link : 

https://www.edaplayground.com/x/fFGz

## 4-bit comparator

### Listing of VHDL Architecture
```vhdl
architecture Behavioral of comparator_4bit is
begin
    B_less_A_o     <= '1' when (b_i < a_i) else '0';
    B_greater_A_o  <= '1' when (b_i > a_i) else '0';
    B_equals_A_o   <= '1' when (b_i = a_i) else '0';
  

end architecture Behavioral;
```
### Listing of VHDL stimulus process

```vhdl
p_stimulus : process
    begin
        
        report "Stimulus process started" severity note;


        
        s_b <= "1111"; s_a <= "1000"; wait for 100 ns;
       
        assert ((s_B_greater_A = '1') and (s_B_equals_A = '0') and (s_B_less_A = '0'))
     
        report "Test failed for input combination: 1111, 1000" severity error;
        
                
		s_b <= "1010"; s_a <= "0101"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
        report "Test failed for input combination: 1010, 0101" severity error;
        
        s_b <= "1010"; s_a <= "1010"; wait for 100 ns;
        assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
        report "Test failed for input combination: 1010, 1010" severity error;
       
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
   
   ```

### Test Output

analyze design.vhd

analyze testbench.vhd

elaborate tb_comparator_4bit

testbench.vhd:42:9:@0ms:(report note): Stimulus process started

testbench.vhd:56:9:@200ns:(assertion error): Test failed for input combination: 1010, 0101

testbench.vhd:63:9:@300ns:(report note): Stimulus process finished

Finding VCD file...

./dump.vcd

### Edaplaygroung link
https://www.edaplayground.com/x/fQY4

