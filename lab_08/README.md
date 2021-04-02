# LAB_08_Traffic_ligts

## Domácí příprava:

| **Input P** | `0` | `0` | `1` | `1` | `0` | `1` | `0` | `1` | `1` | `1` | `1` | `0` | `0` | `1` | `1` | `1` |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **Clock** | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) | ![rising](https://raw.githubusercontent.com/SimonCieslar/Digital-electronics-1/main/Labs/08-traffic_lights/Images/eq_uparrow.png) |
| **State** | A | A | B | C | C | D | A | B | C | D | B | B | B | C | D | B |
| **Output R** | `0` | `0` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `0` | `1` | `0` |



| **RGB LED** | **Artix-7 pin names** | **Red** | **Yellow** | **Green** |
| :-: | :-: | :-: | :-: | :-: |
| LD16 | N15, M16, R12 | `1,0,0` | `1,1,0` | `0,1,0` |
| LD17 | N16, R11, G14 | `1,0,0` | `1,1,0` | `0,1,0` |


