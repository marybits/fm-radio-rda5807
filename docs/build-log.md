# Build Log — RDA5807 FM Radio Kit HU-017B

A detailed diary of the complete assembly and debugging process.

---

## Session 1 — May 15, 2026

**Duration:** ~4 hours  
**Status:** 🔧 In progress  
**Tools used:** Pinecil V2, Stanz helping hands, ESD tweezers, flux paste, solder wick, 63/37 solder wire

---

### Stage 1 — Soldering Station Setup

Before touching the kit, the full soldering station was assembled and verified.

📸 `photos/01_station_setup.jpg`

**Station components laid out:**
- Pine64 Pinecil V2 (USB-C PD, IronOS firmware)
- Pinecil mini stand with brass wool cleaner
- SainSmart 63/37 Sn63Pb37 solder wire, 0.6mm
- TOWOT no-clean flux paste + solder wick
- Stanz helping hands with 2.5X magnifier
- Silicone heat-resistant mat (13.8 × 9.8 inch)
- ESD tweezers (MMOBIEL 7-piece set)
- VCELINK flush cutters

**Power source:** MacBook Pro USB-C PD charger. The Pinecil negotiates USB PD and reaches 300°C in ~7 seconds.

---

### Stage 2 — Component Inventory

All components were laid out on the silicone mat and verified against the BOM before soldering.

📸 `photos/02_components_inventory.jpg`

**Components identified:**
- 4× electrolytic capacitors (100μF) — C4, C5, C7, C8
- 4× ceramic capacitors (104) — C1, C2, C6, C9
- 1× electrolytic capacitor (1μF) — C3
- 5× resistors 1K — R2-R5
- 8× resistors 510R — R7-R14
- 1× resistor 10K — R16
- 1× red LED — D1
- 4× tactile push buttons — S1-S4
- 4× black key caps
- 1× RDA5807 FM module (green PCB) — U1
- 1× TDA2822 audio amplifier IC — U9
- 1× STC8G1K17 microcontroller — U2
- 1× AMS1117-3.3V voltage regulator — U10
- 1× 3362P 200K trimmer potentiometer — R1
- 1× 4-digit 7-segment display — U7
- 1× USB socket, 1× audio jack (pink), 1× toggle switch
- 1× speaker, 1× radio antenna
- Clear acrylic case + screws + red/black speaker wire

> **Note:** The kit uses STC**8**G1K17 microcontroller, not the STC89C17 listed in some versions of the BOM. This is an upgraded MCU with a different firmware and button mapping.

---

### Stage 3 — PCB Assembly

The PCB was mounted in the Stanz helping hands and assembly began following the manufacturer's graphical instructions.

📸 `photos/03_pcb_in_helping_hands.jpg`  
📸 `photos/04_pcb_resistors_soldered.jpg`  
📸 `photos/05_pcb_mid_assembly_front.jpg`  

**Soldering order followed:**
1. Resistors (lowest profile first)
2. Ceramic capacitors
3. LED (polarity verified — long leg to + pad)
4. Electrolytic capacitors (polarity verified)
5. IC sockets (TDA2822 8-pin, STC8G1K17 16-pin)
6. RDA5807 module
7. USB socket, audio jack, toggle switch
8. Push buttons
9. Trimmer potentiometer R1
10. 7-segment display

**Pinecil settings:** 300°C throughout. 63/37 eutectic solder flows cleanly at this temperature.

---

### Stage 4 — PCB Inspection (front and back)

📸 `photos/06_pcb_complete_front.jpg`  
📸 `photos/07_pcb_complete_back.jpg`

Back of the board inspected under the Stanz 2.5X magnifier. All joints appear shiny and well-formed. No obvious solder bridges detected under magnification.

---

### Stage 5 — ICs and Final Components

📸 `photos/08_pcb_with_ics.jpg`

- TDA2822 inserted into 8-pin DIP socket (notch aligned per schematic)
- STC8G1K17 inserted into 16-pin DIP socket
- Antenna attached to U6 connector
- Speaker wired with red/black wire to Speaker pads

---

### Stage 6 — First Power-On ✅

📸 `photos/10_first_power_on.jpg`  

**USB connected → immediate results:**
- ✅ Red LED (D1) lit up
- ✅ 7-segment display shows **107.3 MHz** (default frequency)
- ✅ Microcontroller (STC8G1K17) booted successfully
- ✅ AMS1117 3.3V regulator confirmed working
- ✅ Static audio confirmed on speaker — analog audio path operational

---

### Stage 7 — Case Assembly

📸 `photos/09_case_back_with_speaker.jpg`  
📸 `photos/11_final_assembled_front.jpg`  
📸 `photos/12_final_assembled_back.jpg`

PCB mounted into transparent acrylic case. Speaker secured with self-tapping screws. Antenna extended through top slot. M2 screws used to close the case.

---

## Current Functional Status

| Feature | Status | Notes |
|---------|--------|-------|
| Power on | ✅ Working | LED + display boot correctly |
| Display | ✅ Working | Shows 107.3 MHz |
| Volume control | ✅ Working | V+ / V- respond (0-15 levels) |
| Audio output | ✅ Working | Static confirmed — RF signal received |
| Setup mode | ✅ Working | Sn / Po / dP menus accessible |
| Frequency navigation | 🔧 In progress | Currently locked to 107.3 MHz |

---

## Lessons Learned

| # | Lesson | Context |
|---|--------|---------|
| 1 | 63/37 eutectic solder at 300°C flows cleanly for through-hole work | No cold joints in initial build |
| 2 | Read firmware documentation before assuming hardware failure | F+/F- behavior is firmware-controlled, not pure hardware |
| 3 | Static = success — RF noise confirms the entire analog chain works | RDA5807 → TDA2822 → speaker all functional |
| 4 | The STC8G1K17 has different firmware than older STC89C17 versions | Button mapping and menu system differ from some online guides |

---

## Pending Tasks

- [ ] Complete frequency navigation setup
- [ ] Document final working state with audio on a live station

## ⚠️ Debugging Notes

During the first power-on test, the radio appeared locked at 107.3 MHz and the F+/F- buttons were initially unresponsive. After reviewing the firmware behavior and setup menus, it became clear that the issue was firmware-related rather than a soldering or hardware fault.

This highlighted the importance of validating firmware configuration before assuming PCB assembly errors.
