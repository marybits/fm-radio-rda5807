# 📻 RDA5807 FM Radio Kit — HU-017B

![Final assembled radio](docs/photos/11_final_assembled_front.jpg)

> A hands-on hardware project documenting the assembly and soldering of an FM radio kit built around the **RDA5807MP** chip. Part of a broader journey into embedded systems and hardware fundamentals.

---

## Overview

This project covers the complete lifecycle of building an FM radio from a PCB kit:

- Soldering ~30 through-hole components
- Understanding the RDA5807MP's internal architecture
- Documenting the build process for reproducibility and learning

**Kit:** Upgraded RDA5807 Radio Production Kit — HU-017B (FM Radio V5.0, 240806)  
**Chip:** RDA5807MP — single-chip broadcast FM radio tuner with RDS support  
**Interface:** I2C (TWI), 3-wire, and direct mode  
**Frequency Range:** 76–108 MHz  
**Power Supply:** USB / 3.3V–5V DC

---

## Soldering Station Setup

### Iron & Power
| Tool | Model | Notes |
|------|-------|-------|
| Soldering Iron | Pine64 Pinecil V2 (smart, USB-C PD) | Open-source firmware [IronOS](https://github.com/Ralim/IronOS) |
| Stand | Pinecil Portable Mini Stand | Brass wool tip cleaner |
| Power Source | MacBook Pro USB-C PD charger (61W+) | Reaches working temp in ~7 seconds |
| Cable | Anker USB-C 240W (3ft) | Dedicated to soldering station |

### Consumables
| Tool | Model | Notes |
|------|-------|-------|
| Solder | SainSmart 63/37 Sn63Pb37, 0.6mm | Eutectic alloy |
| Flux | No-clean flux paste (10cc) | For rework and fine joints |
| Desoldering | Solder wick braid | No-clean formula |
| Tip Cleaner | Brass wool dry cleaner | Dome-shaped, non-slip base |

### Hand Tools
| Tool | Model | Notes |
|------|-------|-------|
| Wire Stripper / Cutter | WGGE WG-015 8-inch | Multi-function: strip, cut, crimp |
| Flush Cutter | VCELINK 5-inch | For trimming component leads flush to PCB |
| Tweezers | MMOBIEL ESD 7-piece set | Anti-static, multiple tip shapes |
| Helping Hands | Stanz with 2.5X magnifier | Dual adjustable alligator clips, heavy base |

### Work Surface
| Tool | Model | Notes |
|------|-------|-------|
| Silicone Mat | 13.8 × 9.8 inch | Heat resistant to 932°F |

---

## Key Components

| Component | Ref | Role |
|-----------|-----|------|
| RDA5807MP module | U1 | FM tuner chip — receives and processes FM radio signals |
| STC8G1K17 | U2 | Microcontroller — manages buttons, display, station memory |
| TDA2822 | U9 | Audio amplifier — drives the speaker |
| AMS1117-3.3V | U10 | Voltage regulator — steps down to 3.3V for RDA5807 |
| 4-digit 7-segment display | U7 | Shows current frequency |
| Potentiometer 200K | R1 | Analog volume control |
| Electrolytic capacitors 100μF ×4 | C4,C5,C7,C8 | Power filtering |
| Push buttons ×4 | S1-S4 | V+, V-, F-, F+ controls |

> Full BOM available in the [kit instruction sheet](docs/schematic.pdf).

---

## System Architecture

```text
Antenna
   ↓
RDA5807MP (FM tuner)
   ↓
STC8G1K17 (microcontroller)
   ↓
TDA2822 (audio amplifier)
   ↓
Speaker / Audio Jack
```

---

## Chip Deep Dive — RDA5807MP

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


---

## Build Log

Full step-by-step build documentation with photos available in [`docs/build-log.md`](docs/build-log.md).

---

## 📁 Repository Structure

```
rda5807-fm-radio-kit/
├── README.md                  # This file
└── docs/
    ├── build-log.md           # Detailed build diary with photos
    ├── schematic.pdf          # Kit schematic & component map
    └── photos/                # Build process photos
```

---

## 🧠 What I Learned

- **Through-hole soldering fundamentals** — component orientation, heat transfer, solder flow
- **Reading datasheets** — extracting register maps, electrical characteristics, timing diagrams
- **Voltage regulation** — role of AMS1117 in stepping down to 3.3V for the RDA5807
- **Audio amplification** — how the TDA2822 drives the speaker from the FM demodulated signal
- **Firmware behavior** — how the STC8G1K17 manages station memory and button mapping

---

## 👤 Author

**Mary Araujo**  
Computer Engineering Student — University of Ottawa (2nd year)  

---
