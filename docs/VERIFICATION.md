# Verification record

Final automated checks were run on 2026-11-09 with KiCad 10.0.8.

| Check | Result |
|---|---|
| Native KiCad ERC | 0 errors, 0 warnings |
| KiCad-agentic ERC | 0 errors, 0 warnings |
| KiCad-agentic filtered DRC | 0 active violations; 0 unconnected items |
| Native KiCad CLI DRC | 323 geometric rule findings; 0 unconnected items; 152 schematic/PCB field-parity findings when parity checking is enabled |
| PCB connectivity | 0 unrouted connections |
| Copper layers | 4 (`F.Cu`, `In1.Cu`, `In2.Cu`, `B.Cu`) |
| Inner-plane continuity | 0 signal tracks on In1.Cu/In2.Cu; uninterrupted GND and 3.3 V planes |
| Board outline | 85 × 55 mm, closed rounded outline |
| Sensor peninsula | Only `+3V3`, `GND`, `I2C_SDA`, `I2C_SCL`; no vias |
| ESP32 antenna keepout | No routed copper items in the keepout |
| BOM coverage | 31 active BOM lines; 31/31 with MPN and datasheet URL |

The PCB was also rendered successfully with KiCad's 3D renderer for mechanical/placement inspection. All requested controls and the USB-C receptacle are accessible from the board edges/top side. Production release still requires selecting a fabricator stackup, reconciling the native CLI findings with that fabricator's rules, and building a first article.

The native CLI findings are dominated by 0.15 mm routed neck-downs against the current 0.20 mm project minimum, clearance and hole constraints, connector-edge geometry, and missing footprint-side metadata fields. They are retained here as explicit release limitations; no PCB geometry or project rules were changed during repository publication.

The conservative EMC heuristic still reports some F.Cu↔B.Cu USB/LED transitions without a GND via inside its strict 1.0 mm radius. Dedicated GND stitching was added at the USBLC6 return and around the Type-C fanout, while In1.Cu remains a continuous reference plane. The residual `USB_RXLED_N`/`USB_TXLED_N` findings concern low-speed LED sink nets despite their names. These are pre-compliance review notes, not KiCad DRC failures; first-article USB and radiated-emissions testing remains required.
