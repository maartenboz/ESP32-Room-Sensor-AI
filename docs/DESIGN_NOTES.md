# ESP32 Room Sensor & Control Board — design notes

## Architecture

The controller is an `ESP32-S3-WROOM-1-N8` module. USB-C is implemented as a USB 2.0 full-speed device connection to an `FT231XS-R`; the ESP32 native USB pins are deliberately unused. FT231X DTR/RTS signals drive the standard cross-coupled two-NPN automatic download/reset circuit, while dedicated BOOT and RESET switches remain available.

The FT231X factory CBUS functions provide real hardware activity indication: CBUS1 is `RXLED#` and CBUS2 is `TXLED#`. The FT231X MTP should be programmed for a 500 mA bus-powered configuration before relying on the full board current budget.

## Power tree

`VBUS` passes through a Littelfuse `1206L050/16WR` resettable fuse to `+5V_USB`. A Nexperia `PESD5V0S1UL` protects VBUS, and an ST `USBLC6-2SC6` protects D+/D−. The `AP63203WU-7` synchronous buck converts 5 V to 3.3 V with a 4.7 µH Coilcraft XAL4020 inductor, 10 µF plus 100 nF input bypassing, a 100 nF bootstrap capacitor, and 2 × 22 µF output capacitance. Additional 22 µF and 100 nF capacitors are placed at the ESP32 module.

The design target is approximately 450–500 mA worst-case USB input current during Wi-Fi transients. The 2 A regulator rating supplies transient and thermal margin; it does not imply that the USB host is asked to deliver 2 A. The SHT40 heater is intended only for brief firmware-controlled use.

## Sensor layout

The `SHT40-AD1B-R2` is mounted at the lower board edge on a milled peninsula. Two slots, a narrow FR-4 neck, a copper-pour/via keepout and distance from the ESP32 and buck regulator reduce conducted heat. Exactly four nets enter the peninsula (`+3V3`, `GND`, `I2C_SDA`, `I2C_SCL`), and there are no vias or plane fills beneath the sensor area.

## PCB construction

- Board: 85 × 55 mm, 4 mm corner radius.
- Mounting: four symmetric 3.2 mm NPTH holes for M3 hardware.
- Copper: four layers — F.Cu signals/components, In1.Cu uninterrupted ground reference, In2.Cu uninterrupted 3.3 V distribution, B.Cu secondary routing and ground pour. All routed signal tracks are confined to F.Cu and B.Cu.
- Overall thickness: 1.6 mm nominal FR-4; final dielectric thicknesses must be selected from the fabricator's current four-layer stackup.
- General routed clearance is 0.20 mm where space permits; the verified absolute minimum is 0.15 mm in the USB-C fine-pitch breakout.
- General signals use 0.20 mm tracks. USB uses 0.18 mm. Standard vias are 0.60/0.30 mm; four local USB-C breakout vias use 0.40/0.20 mm.
- USB D+/D− run over a continuous In1.Cu reference plane. Total routed lengths are about 44.7 mm (D+) and 38.9 mm (D−); the approximately 5.8 mm skew corresponds to only tens of picoseconds and is electrically negligible at USB full-speed, but the final 90 Ω differential geometry must be recalculated against the chosen production stackup.
- The ESP32 antenna is at the top board edge. Its footprint keepout is preserved on all copper layers; the final board contains no tracks or vias in that keepout.
- Isolated copper texts `L1`, `L2`, `L3`, `L4` are present on F.Cu, In1.Cu, In2.Cu and B.Cu respectively.

## Firmware and production notes

- User buttons are active-low.
- User LEDs are active-high; RX/TX activity LEDs are active-low FT231X CBUS loads.
- Potentiometers use ADC1 channels so Wi-Fi does not disable the ADC inputs.
- The optional 47 pF USB shunt footprints C15/C16 are marked DNP; populate only after signal-integrity/EMI measurement shows a need.
- Do not run the SHT40 heater continuously; that would invalidate ambient-temperature readings.
- Electrical validation does not replace first-article USB, RF, current-transient and sensor-offset measurements.
