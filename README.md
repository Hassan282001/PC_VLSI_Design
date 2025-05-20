# 8-Bit Program Counter Schematic Design

## 📖 Overview

This project implements a transistor-level, static-CMOS 8-bit Program Counter (PC) that either increments by 1 on each clock edge or jumps to a branch target address (PC+1 + offset) under control of a branch signal. All sub-modules (2:1 multiplexer, ripple-carry full-adder, and master-slave flip-flop register) are designed from scratch, analyzed for timing using logical-effort and RC models, and validated through simulation.

---

## ⚙️ Design Components

1. **2:1 Transmission-Gate Multiplexer**  
   - Pass‐gate implementation for full‐swing outputs  
   - Compact: 2 transistors per bit + inverter  
   - Delay: ~127 ps  

2. **8-Bit Ripple-Carry Full Adder**  
   - Eight cascaded 1-bit cells (28 transistors/bit)  
   - Simple, low-area solution for small bit-width  
   - Worst-case delay: ~250 ps  

3. **8-Bit Edge-Triggered Register**  
   - Master-slave flip-flop with fast clock buffer  
   - Ensures clean setup/hold timing  
   - CLK-to-Q delay: ~50 ps  

4. **Top-Level PC Module**  
   - Data path when branching:  
     1. PC → adder1 (PC+1)  
     2. → adder2 (+ offset)  
     3. → MUX → register  
   - Critical path delay: ~350 ps → max clock ≈ 2.86 GHz  
   - Power: sub-mW at 1 GHz  

---

## 📊 Results

| Module                  | Delay (ps) |  
| ----------------------- | ---------- |  
| 2:1 MUX                 | 127        |  
| 8-bit Ripple-Carry Adder| 250        |  
| Register (8-bit FF)     | 173        |  
| **Total (critical path)** | **350**  |  

---

## 🔍 Potential Improvements

- **Single-stage addition:** Merge PC+1 and offset addition into one adder to cut logic depth.  
- **Faster adder architecture:** Implement carry-lookahead or carry-skip to reduce worst-case delay.  
- **Clock gating & sizing:** Add clock gating for power savings and transistor-sizing optimizations on critical nodes.

---

## 📂 Repository Contents

- **`schematic/`** – Cadence netlists & layouts for each module  
- **`symbol/`** – Cadence symbol files  
- **`maestro/`** – Simulation setups & logs  
- **`report/`** – Full written report with figures, waveforms, and tables  
