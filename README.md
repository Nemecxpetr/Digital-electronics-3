# 01 Gates

Úkol z prvního cvičení na počítači.

odkaz na můj GitHub: https://github.com/JanMostecky

## Ověření De Morganova zákona:
ukázka kódu

```vhdl
architecture dataflow of gates is
begin
    for_o <= (not (b_i) and a_i) or (not (c_i) and not (b_i));

    fand_o <= not(not(not b_i and a_i) and not(not c_i and not b_i));

    fnor_o <= not(b_i or not a_i) or not( c_i or b_i);

end architecture dataflow;
```

### Tabulka hodnot
| **c** | **b** |**a** | **f(c,b,a)** | **fand(c,b,a)** | **fnor(c,b,a)** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 1 | 1 | 1 |
| 0 | 0 | 1 | 1 | 1 | 1 |
| 0 | 1 | 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 | 1 | 1 |
| 1 | 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 | 0 |

### odkaz na VHDL kód:
https://www.edaplayground.com/x/A5JW

### screenshot fungování funkce
![screenshot](/pictures/screenshot_3.JPG)

## Ověření zákona o distribuci
