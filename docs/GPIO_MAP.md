# ESP32 Room Sensor — GPIO map

| ESP32-S3 pin | Board function | Electrical notes |
|---|---|---|
| GPIO0 | BOOT / automatic download | 10 kΩ pull-up; BOOT switch to GND; driven by the FT231X DTR/RTS transistor network |
| GPIO4 / ADC1_CH3 | POT1 | 10 kΩ potentiometer; 1 kΩ series resistor and 100 nF ADC filter |
| GPIO5 / ADC1_CH4 | POT2 | 10 kΩ potentiometer; 1 kΩ series resistor and 100 nF ADC filter |
| GPIO6 | USER_BTN1 | Active-low; external 10 kΩ pull-up |
| GPIO7 | USER_BTN2 | Active-low; external 10 kΩ pull-up |
| GPIO8 | I2C_SDA | SHT40 data; 4.7 kΩ pull-up to 3.3 V |
| GPIO9 | I2C_SCL | SHT40 clock; 4.7 kΩ pull-up to 3.3 V |
| GPIO10 | USER_LED1 | Active-high red LED through 2.2 kΩ |
| GPIO11 | USER_LED2 | Active-high yellow LED through 2.2 kΩ |
| GPIO43 / U0TXD | USB-UART TX | ESP32 TX to FT231X RXD |
| GPIO44 / U0RXD | USB-UART RX | FT231X TXD to ESP32 RX |
| EN | RESET / automatic reset | 10 kΩ pull-up, 1 µF to GND, RESET switch and auto-program transistor network |
| GPIO19 / USB_D− | Not connected | Native USB intentionally unused |
| GPIO20 / USB_D+ | Not connected | Native USB intentionally unused |

GPIO3, GPIO45 and GPIO46 are intentionally unused because of ESP32-S3 strapping/input restrictions. All other unused module pins are explicitly marked no-connect in the schematic.
