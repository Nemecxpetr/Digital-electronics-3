# Lab_06: Driver for multiple seven-segment displays

## Domácí příprava

### Kód pro simulátor vln:

```vhdl
{
  signal:
  [
    ['Digit position',
      {name: 'Common anode: AN(3)', wave: 'xx01..01..01'},
      {name: 'AN(2)', wave: 'xx101..01..0'},
      {name: 'AN(1)', wave: 'xx1.01..01..'},
      {name: 'AN(0)', wave: 'xx1..01..01.'},
    ],
    ['Seven-segment data',
      {name: '4-digit value to display', wave: 'xx3333555599', data: ['3','1','4','2','3','1','4','2','3','1']},
      {name: 'Cathod A: CA', wave: 'xx01.0.1.0.1'},
      {name: 'CB', wave: 'xx0'},
      {name: 'CC', wave: 'xx0'},
      {name: 'CD', wave: 'xx0'},
      {name: 'CE', wave: 'xx1'},
      {name: 'CF', wave: 'xx1'},
      {name: 'CG', wave: 'xx0'},
    ],
    {name: 'Decimal point: DP', wave: 'xx01..01..01'},
  ],
  head:
  {
    text: '                    4ms   4ms   4ms   4ms   4ms   4ms   4ms   4ms   4ms   4ms',
  },
}
```

### Obrázek vln:

![screenshot](https://github.com/JanMostecky/Digital-electronics-1/blob/main/pictures/06%20vlna.JPG)

## Display driver

### p_mux kód:

```vhdl
p_mux : process(s_cnt, data0_i, data1_i, data2_i, data3_i, dp_i)          
begin                                                                     
    case s_cnt is                                                         
        when "11" =>                                                      
            s_hex <= data3_i;                                             
            dp_o  <= dp_i(3);                                             
            dig_o <= "0111";                                              
                                                                          
        when "10" =>                                                      
            -- WRITE YOUR CODE HERE                                       
            s_hex <= data2_i;                                             
            dp_o  <= dp_i(2);                                             
            dig_o <= "1011";                                              
                                                                          
                                                                          
        when "01" =>                                                      
            -- WRITE YOUR CODE HERE                                       
            s_hex <= data1_i;                                             
            dp_o  <= dp_i(1);                                             
            dig_o <= "1101";                                              
                                                                          
                                                                          
        when others =>                                                    
            -- WRITE YOUR CODE HERE                                       
            s_hex <= data0_i;                                             
            dp_o  <= dp_i(0);                                             
            dig_o <= "1110";                                              
                                                                          
    end case;                                                             
end process p_mux;                                                        
```


