⚡ Smart Power Management Board (SPMB)
📌 Overview

The Smart Power Management Board is a power distribution and backup system designed to manage multiple power sources intelligently. It handles input protection, voltage regulation, battery charging, and automatic power switching between external supply and battery backup.

This project was developed as a PCB design exercise focused on power electronics, protection design, and embedded system integration.

🎯 Objectives
Design a safe DC power input stage with protection
Implement regulated 5V power rail using a buck converter
Integrate Li-ion battery charging system
Enable automatic power switching between supply and battery
Provide measurable and testable outputs for embedded monitoring
🧠 System Architecture
12V DC Input
   ↓
Fuse + Reverse Polarity Protection
   ↓
Buck Converter (12V → 5V)
   ↓
TP4056 Battery Charger
   ↓
18650 Li-ion Battery
   ↓
MOSFET Power Path Controller
   ↓
5V Output Rail (Load)
🔧 Key Features
🔌 Input Protection
Fuse (overcurrent protection)
P-MOSFET reverse polarity protection
⚡ Voltage Regulation
LM2596 buck converter (12V → 5V stable rail)
🔋 Battery Management
TP4056 Li-ion charging circuit
1-cell 18650 battery support
🔄 Power Path Switching
Automatic switching between adapter and battery
P-MOSFET-based high-side switching
📊 Monitoring Support
Voltage divider for ADC sensing
Test points for debugging
🧩 Main Components
Block	Component
Protection	Fuse, AO3401A MOSFET
Buck Converter	LM2596
Battery Charger	TP4056
Battery	18650 Li-ion cell
Switching	AO3401A MOSFETs
Sensing	Resistor voltage divider
⚙️ Design Highlights
🔐 Reverse Polarity Protection

P-MOSFET used to block incorrect input polarity while minimizing voltage drop.

🔋 Charging System

Battery is charged via regulated 5V rail from buck converter using TP4056.

🔄 Power Switching Logic
External power available → system powered by buck converter
External power lost → battery automatically takes over
📐 Voltage Monitoring

A resistor divider scales battery voltage for MCU ADC input.

⚠️ Known Limitations
TP4056 is not a full power-path management IC
No seamless simultaneous load + charging optimization
Future upgrade: dedicated power-path IC recommended
📁 Project Structure
SPMB/
├── schematic/
├── pcb/
├── fabrication/
├── docs/
│   └── README.md
└── images/
🚀 Future Improvements
Replace TP4056 with proper power-path IC (e.g. IP5306 or BQ series)
Add current sensing (INA219 or ACS712)
Add MCU (STM32 / ESP32) for smart monitoring
Add OLED display for real-time status
Upgrade to 4-layer PCB for better power integrity
🧠 What This Project Demonstrates
Power electronics design fundamentals
PCB-level protection strategies
Real-world battery integration
Analog + digital system interaction
Practical engineering tradeoffs
📌 Author Notes

This board is part of a progressive PCB engineering portfolio focused on moving from basic circuits to real embedded power systems design.
