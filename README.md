# 📻 RDA5807 FM Radio Kit — HU-017B

> A hands-on hardware project documenting the assembly, soldering, and software integration of an FM radio kit built around the **RDA5807MP** chip. Part of a broader journey into embedded systems and hardware-software co-design.

---

## 🧭 Overview

This project covers the complete lifecycle of building an FM radio from a PCB kit:

- Soldering ~30 through-hole and SMD-adjacent components
- Understanding the RDA5807MP's internal architecture
- Documenting the build process for reproducibility and learning
- *(Roadmap)* Integrating Arduino control via I2C to tune stations programmatically

**Kit:** Upgraded RDA5807 Radio Production Kit — HU-017B (FM Radio V3.0, 240806)  
**Chip:** RDA5807MP — single-chip broadcast FM radio tuner with RDS support  
**Interface:** I2C (TWI), 3-wire, and direct mode  
**Frequency Range:** 76–108 MHz  
**Power Supply:** USB / 3.3V–5V DC

---

## 🛠️ Soldering Station Setup

| Tool | Model |
|------|-------|
| Soldering Iron | Pine64 Pinecil V2 (smart, USB-C PD) |
| Stand | Pinecil Portable Mini Stand |
| Solder | SainSmart 63/37 Sn63Pb37, 0.6mm, flux rosin core |
| Flux | No-clean flux paste (10cc) |
| Desoldering | Solder wick braid |
| Work Surface | Silicone mat, heat resistant to 932°F |
| Tip Cleaner | Brass wool dry cleaner |
| Power Source | MacBook Pro USB-C PD charger (61W+) |

> **Note on the Pinecil:** The Pinecil runs [IronOS](https://github.com/Ralim/IronOS) open-source firmware and negotiates USB PD for optimal wattage. Paired with a MacBook charger it reaches working temperature in ~7 seconds.

---

## 📦 Bill of Materials (BOM)

| # | Name | Component | Ref | Qty |
|---|------|-----------|-----|-----|
| 1 | Digital Tube | — | U7 | 1 |
| 2 | Direct insertion resistor 10K | R2, R3, R4, R5, R6 | — | 5 |
| 3 | Direct insertion resistor 1K | R1, R12, R13, R14 | — | 4 |
| 4 | Direct insertion resistor 510 | R10 | — | 1 |
| 5 | USB Socket | — | — | 1 |
| 6 | Toggle Switch | — | P5 | 1 |
| 7 | M2 antenna | — | DC | 1 |
| 8 | M2 screw | — | — | 4 |
| 9 | Audio Jack | — | U6 | 1 |
| 10 | 6×6×12.5 Key | — | S1, S2, S3, S4 | 4 |
| 11 | STC89C17 module | — | U4 | 1 |
| 12 | Electrolytic capacitor 100μF | — | C4, C5, C6, C7, C8 | 5 |
| 13 | Electrolytic capacitor 1μF | — | C1, C2, C3, C9 | 4 (opt.) |
| 14 | TDA2822 | — | U8 | 1 |
| 15 | RDA5807 module | — | U1 | 1 |
| 16 | Potentiometer 200K | — | R1 | 1 |
| 17 | Capacitor ceramic 104 | — | — | — |
| 18 | Red LED | — | D1 | 1 |
| 19 | RDA5807 module | — | U9 | 1 |
| 20 | Capacitor ceramic 104 | — | — | — |
| 21 | 4P receptacle | — | — | 1 |
| 22 | AMS1117-3.3V | — | U10 | 1 |
| 23 | AMS1117-3.3V | — | U2 | 1 |
| 24 | 8P IC socket | — | — | 1 |
| 25 | 16P IC socket | — | — | 1 |
| 26 | 8P speaker | — | — | 1 |
| 27 | Capacitor 104 | — | — | — |
| 28 | PCB | — | — | 1 |
| 29 | 4P red and black wire | Power | — | 1 |
| 30 | Battery shroud | — | — | 1 |
| 31 | Screw pack | — | — | 1 |
| 32 | Housing | — | — | 1 |
| 33 | Instruction | — | — | 1 |

---

## 🔬 Chip Deep Dive — RDA5807MP

The **RDA5807MP** is a fully integrated single-chip FM stereo radio tuner IC.

### Key Features
- FM frequency range: **76–108 MHz** (worldwide band support)
- **RDS/RBDS** decoder built-in
- **SNR:** 71 dB typical
- **I2C interface** at address `0x10` (sequential mode) or `0x11` (random access)
- Automatic Frequency Control (AFC)
- Automatic Gain Control (AGC)
- Bass boost, soft mute, high-cut filter
- On-chip oscillator — no external crystal needed
- 3.3V supply voltage

### Register Map (key registers)
| Register | Address | Description |
|----------|---------|-------------|
| CHIP_ID | 0x00 | Chip ID (should return 0x58) |
| CTRL | 0x02 | Enable, RDS, new method, soft reset |
| TUNE | 0x03 | Channel + TUNE bit + Band + Space |
| RSSI | 0x0B | Signal strength (RSSI) |

> Full register map: [RDA5807MP datasheet (PDF)](https://cdn-shop.adafruit.com/product-files/4663/RDA5807MP_datasheet_v1.pdf)

---

## 📸 Build Log

> *Photos will be added as the build progresses.*

### Stage 1 — Component Inventory
- [ ] Verify all BOM components against kit contents
- [ ] Take photos of all components laid out

### Stage 2 — Resistors & Capacitors
- [ ] Solder all resistors (check color bands against BOM)
- [ ] Solder ceramic capacitors
- [ ] Solder electrolytic capacitors (mind polarity)

### Stage 3 — ICs & Modules
- [ ] Place IC sockets (do NOT solder ICs directly)
- [ ] Solder TDA2822 amplifier socket
- [ ] Insert RDA5807 module
- [ ] Insert STC89C17 microcontroller module

### Stage 4 — Connectors & Controls
- [ ] Solder USB socket
- [ ] Solder audio jack
- [ ] Solder push buttons (×4)
- [ ] Solder toggle switch
- [ ] Solder potentiometer

### Stage 5 — Power & LEDs
- [ ] Solder AMS1117 voltage regulators
- [ ] Solder LED (check polarity — anode to +)

### Stage 6 — Final Assembly
- [ ] Attach digital tube display
- [ ] Test power-on (LED should light)
- [ ] Tune to a known strong station
- [ ] Verify audio output through jack

---

## ⚠️ Lessons Learned

> *To be updated during the build.*

- ...

---

## 🗺️ Roadmap — Arduino I2C Integration

The RDA5807MP exposes a full I2C control interface, which means it's possible to control the radio programmatically — tune to a specific frequency, read RSSI signal strength, enable RDS decoding — all from an Arduino.

### Planned features
- [ ] Wire RDA5807 SDA/SCL pins to Arduino Uno
- [ ] Write I2C initialization sequence (soft reset → enable → set band)
- [ ] Implement `setFrequency(float mhz)` function
- [ ] Read and display RSSI from register `0x0B`
- [ ] Serial monitor interface to type frequency and tune
- [ ] *(Stretch)* RDS station name decoding

### Wiring plan (Arduino Uno)
```
RDA5807  →  Arduino Uno
VCC      →  3.3V
GND      →  GND
SDA      →  A4
SCL      →  A5
```

### I2C initialization sequence (pseudocode)
```cpp
// Write to register 0x02 to enable the chip
Wire.beginTransmission(0x10);
Wire.write(0x02);             // Register address
Wire.write(0b11000001);       // DHIZ | DMUTE | ENABLE
Wire.write(0b00000000);
Wire.endTransmission();

// Set frequency: channel = (freq*10 - 870) / 1  [for 100kHz spacing, 87MHz band]
// Example: 101.1 MHz → channel = (1011 - 870) = 141 = 0x8D
```

> Full Arduino sketch will be added to `/arduino/` once hardware testing is complete.

---

## 📁 Repository Structure

```
fm-radio-rda5807/
├── README.md                  # This file
├── docs/
│   ├── build-log.md           # Detailed build diary
│   ├── schematic.pdf          # Kit schematic & component map
│   ├── RDA5807MP_datasheet.pdf
│   └── photos/
│       ├── 01_components.jpg
│       ├── 02_resistors_done.jpg
│       ├── 03_ics_placed.jpg
│       ├── 04_final_assembly.jpg
│       └── 05_working.jpg
└── arduino/
    ├── rda5807_i2c_basic/
    │   └── rda5807_i2c_basic.ino
    └── rda5807_serial_tuner/
        └── rda5807_serial_tuner.ino
```

---

## 🧠 What I Learned

- **Through-hole soldering fundamentals** — component orientation, heat transfer, solder flow
- **Reading datasheets** — extracting register maps, electrical characteristics, timing diagrams
- **I2C protocol** — address modes, read/write sequences, 7-bit addressing
- **Voltage regulation** — role of AMS1117 in stepping down to 3.3V for the RDA5807
- **Audio amplification** — how the TDA2822 drives the speaker from the FM demodulated signal

---

## 👤 Author

**Mary Araujo**  
Computer Engineering Student — University of Ottawa (2nd year)  
[github.com/yourusername](https://github.com/marybits) · [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)

---

## 📄 License

MIT — feel free to use this documentation as a reference for your own build.
