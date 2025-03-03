# esphome-pipsolar-techfine
ESPHome component to monitor and control a pipsolar inverter via RS232

Supported devices
PIP4048 compatible PV Inverter

GD11048MH Solar Inverter

Requirements
ESPHome 2024.6.0 or higher.
One half of an ethernet cable with RJ45 connector
RS232-to-TTL module (MAX3232CSE f.e.)
Generic ESP32 or ESP8266 board

## Schematics

<a href="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/001.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/001.jpg" height="172">
</a>

<a href="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/002.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/002.jpg" height="172">
</a>

<a href="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/004.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/004.jpg" height="172">
</a>

<a href="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/005.jpg" target="_blank">
  <img src="https://raw.githubusercontent.com/syssi/esphome-pipsolar/main/images/005.jpg" height="172">
</a>

```
               RS232                     UART-TTL
┌──────────┐              ┌──────────┐                ┌─────────┐
│          │              │          │<----- RX ----->│         │
│          │<---- TX ---->│  RS232   │<----- TX ----->│ ESP32/  │
│   PIP    │<---- RX ---->│  to TTL  │<----- GND ---->│ ESP8266 │
│          │<---- GND --->│  module  │<-- 3.3V VCC -->│         │<--- VCC
│          │              │          │                │         │<--- GND
└──────────┘              └──────────┘                └─────────┘
```

### RJ45 connector

| Pin     | Purpose      | MAX3232 pin       | Color T-568B |
| :-----: | :----------- | :---------------- | :------------|
|    1    | TX           | P13 (RIN1)        | White-Orange |
|    2    | RX           | P14 (DOUT1)       | Orange       |
|    3    |              |                   |              |
|    4    | VCC 12V      | -                 | Blue         |
|    5    |              |                   |              |
|    6    |              |                   |              |
|    7    |              |                   |              |
|    8    | GND          | P15 (GND)         | Brown        |

Please be aware of the different RJ45 pinout colors ([T-568A vs. T-568B](images/rj45-colors-t568a-vs-t568.png)).

The inverter provides +12V on pin 4 or 7 depending on the model. You can use a cheap DC-DC converter to power the ESP with 3.3V.

The [source for the pinout is here](docs/HS_MS_MSX%20RS232%20Protocol.pdf).

### MAX3232

| Pin          | Label        | ESPHome     | ESP8266 example  | ESP32 example |
| :----------- | :----------- | :---------- | :--------------- | :------------ |
| P11 (DIN1)   | TXD          | `tx_pin`    | `GPIO4`          | `GPIO16`      |
| P12 (ROUT1)  | RXD          | `rx_pin`    | `GPIO5`          | `GPIO17`      |
| P16 (VCC)    | VCC          |             |                  |               |
| P15 (GND)    | GND          |             |                  |               |
