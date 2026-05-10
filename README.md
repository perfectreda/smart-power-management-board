<div align="center">

# ⚡ Smart Power Management Board
### `SPMB` — Intelligent Power Distribution & Battery Backup System

![PCB Design](https://img.shields.io/badge/PCB-Design-f5a623?style=for-the-badge&logo=altiumdesigner&logoColor=white)
![Power Electronics](https://img.shields.io/badge/Power-Electronics-3de8a0?style=for-the-badge)
![Li--ion](https://img.shields.io/badge/Battery-Li--ion_18650-5b8fff?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

*A power distribution and backup system designed to intelligently manage multiple power sources —  
handling input protection, voltage regulation, battery charging, and automatic power switching.*

</div>

---

## 📌 Overview

The **Smart Power Management Board (SPMB)** is a PCB-level power system that manages a 12V DC input, steps it down to a stable 5V rail, charges a Li-ion battery, and automatically switches between the external supply and battery backup when power is lost.

This project was developed as a **PCB design exercise** focused on power electronics, protection design, and embedded system integration.

---

## 🎯 Objectives

| # | Goal |
|---|------|
| 01 | Design a safe DC input stage with fuse and reverse-polarity protection |
| 02 | Implement a regulated **5V rail** using a buck converter |
| 03 | Integrate a **Li-ion battery charging** system via TP4056 |
| 04 | Enable **automatic power switching** between adapter and battery |
| 05 | Provide measurable outputs and test points for embedded monitoring |

---

## 🧠 System Architecture

```
┌─────────────────────────┐
│      12V DC Input       │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Fuse + Reverse Polarity │  ← P-MOSFET (AO3401A)
│      Protection          │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Buck Converter       │  ← LM2596 · 12V → 5V
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│   TP4056 Battery Charger │  ← CC/CV Li-ion charging
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    18650 Li-ion Battery  │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  MOSFET Power Path Ctrl  │  ← AO3401A high-side switch
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│    5V Output Rail (Load) │  ✅ Stable regulated output
└─────────────────────────┘
```

---

## 🔧 Key Features

### 🔌 Input Protection
- **Blade fuse** — overcurrent protection
- **P-MOSFET (AO3401A)** — reverse polarity protection with minimal voltage drop

### ⚡ Voltage Regulation
- **LM2596** buck converter stepping 12V down to a stable 5V rail

### 🔋 Battery Management
- **TP4056** — constant current / constant voltage Li-ion charging
- Single-cell **18650** battery support

### 🔄 Automatic Power Switching
- P-MOSFET-based high-side switching
- **Seamless fallback** to battery when adapter is removed

### 📊 Monitoring Support
- Resistor **voltage divider** for MCU ADC sensing
- Exposed **test points** across the board for debugging

---

## 🧩 Component List

| Block | Component | Description |
|-------|-----------|-------------|
| Input Protection | `Fuse` + `AO3401A` | Overcurrent + reverse polarity guard |
| Buck Converter | `LM2596` | Switching regulator, 12V → 5V |
| Battery Charger | `TP4056` | CC/CV Li-ion charging IC |
| Battery Cell | `18650 Li-ion` | Single cell, ~3.7V nominal |
| Power Switching | `AO3401A` | P-MOSFET high-side switch |
| Voltage Sensing | `R Divider` | Scales Vbatt for MCU ADC input |

---

## ⚙️ Design Highlights

<details>
<summary><strong>🔐 Reverse Polarity Protection</strong></summary>
<br>

A **P-MOSFET** is placed on the input stage to block incorrect polarity connections. Unlike a diode, the MOSFET's RDS(on) is very low — minimizing voltage drop under normal forward operation while still providing full protection.

</details>

<details>
<summary><strong>🔋 Charging System</strong></summary>
<br>

The **TP4056** is fed from the regulated 5V buck output, ensuring the battery always receives a clean, stable charge voltage regardless of input fluctuations. Charge current is set via a single resistor.

</details>

<details>
<summary><strong>🔄 Automatic Power Switching Logic</strong></summary>
<br>

| Condition | Behavior |
|-----------|----------|
| External adapter present | System powered by buck converter output |
| External adapter removed | Battery automatically takes over the load |

Gate logic on the P-MOSFET path handles switching passively — no firmware required.

</details>

<details>
<summary><strong>📐 Voltage Monitoring</strong></summary>
<br>

A precision resistor divider scales the 18650 voltage range **(0–4.2V → 0–3.3V)**, making it compatible with standard MCU ADC pins for real-time state-of-charge estimation.

</details>

---

## ⚠️ Known Limitations

> [!WARNING]
> **TP4056 is not a full power-path IC.** It cannot cleanly manage simultaneous charging and load driving, which may cause instability under heavy loads while charging.

- ❌ No seamless simultaneous load + charging optimization
- ❌ No built-in load-sharing arbitration logic
- ✅ **Recommended fix:** Replace TP4056 with a dedicated power-path IC such as **IP5306** or the **BQ series** (e.g. BQ24074)

---

## 📁 Project Structure

```
Smart_Power_Management_Board/
├── Block_Diagrame/     # System block diagrams
├── Hardware/           # Hardware design files, BOM
├── PCB/                # PCB layout pics
├── Schematic/          # KiCad / EasyEDA schematic pdf file
└── README.md
```

---

## 🚀 Future Improvements

- [ ] Replace TP4056 with proper power-path IC — **IP5306** or **BQ series**
- [ ] Add current sensing — **INA219** or **ACS712**
- [ ] Integrate MCU (**STM32 / ESP32**) for smart monitoring and logging
- [ ] Add **OLED display** for real-time voltage, current, and charge state
- [ ] Upgrade to **4-layer PCB** for better power integrity and reduced EMI

---

## 🧠 What This Project Demonstrates

- Power electronics design fundamentals
- PCB-level protection strategies
- Real-world Li-ion battery integration
- Analog + digital system interaction
- Practical engineering tradeoffs and component selection

---

## 👤 Author Notes

> This board is part of a **progressive PCB engineering portfolio** focused on moving from basic circuits to real embedded power systems design. Each iteration introduces more complexity — from passive protection circuits to active power management ICs and eventually MCU-controlled smart systems.

---

<div align="center">

**SPMB** · Smart Power Management Board · PCB Portfolio Project  
`12V Input` · `5V Regulated Output` · `18650 Li-ion` · `Auto Power Switch`

</div>
