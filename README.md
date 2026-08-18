# 🌿 Biodiesel Production via Transesterification — Steady-State Process Simulation

> A continuous biodiesel production process modelled in **Aspen PLUS V11**, implementing rigorous second-order reversible reaction kinetics for the base-catalyzed transesterification of waste cooking oil (WCO) to fatty acid methyl esters (FAME).

---

## 📌 Project Overview

This project presents a complete steady-state simulation of an industrial-scale biodiesel production plant built in Aspen PLUS V11. The simulation models the full process chain — from feed preparation through reaction, phase separation, methanol recovery, and final biodiesel purification — using the pseudo-homogeneous kinetic model of Vicente et al. (2005).

The process was designed around a target feedstock of **waste cooking oil (WCO)**, represented as triolein (C₅₇H₁₀₄O₆), reacting with methanol in the presence of a sodium hydroxide (NaOH) homogeneous catalyst.

---

## ⚙️ Simulation Environment

| Item | Detail |
|---|---|
| Software | Aspen PLUS V11 |
| Thermodynamic Model | NRTL (Non-Random Two Liquid) |
| Simulation Type | Continuous Steady-State |
| Reactor Type | CSTR (Continuous Stirred Tank Reactor) |
| Kinetic Model | Vicente et al. (2005) — pseudo-homogeneous, 2nd order reversible |

The NRTL activity coefficient model was selected for its suitability in handling the polar, non-ideal liquid mixtures present in this system — including methanol, glycerol, water, and fatty acid esters.

---

## 🏭 Process Description

The flowsheet is structured around four sequential sections:

### 1. Feed Preparation
- **WCO** (triolein) enters **MIXER2** directly
- **Methanol** and **NaOH catalyst** are first premixed in **MIXER1**, then combined with WCO and the **methanol recycle stream (METHREC)** in MIXER2
- The combined reactor feed exits MIXER2 as stream 2

### 2. Reaction
- The combined feed enters a single **CSTR** operating at 60°C and 101.325 kPa
- Three consecutive reversible transesterification reactions proceed within the reactor:
  - **Reaction 1:** Triolein + Methanol ⇌ Diglyceride + Methyl Oleate (FAME)
  - **Reaction 2:** Diglyceride + Methanol ⇌ Monoglyceride + Methyl Oleate (FAME)
  - **Reaction 3:** Monoglyceride + Methanol ⇌ Glycerol + Methyl Oleate (FAME)

### 3. Phase Separation
- The CSTR effluent enters a **three-phase decanter** at 60°C
- **LLD (light liquid phase):** FAME-rich stream → sent to methanol recovery column (B12)
- **HLD (heavy liquid phase):** Glycerol-rich stream → sent to glycerol recovery column (B6)

### 4. Purification & Methanol Recycle
- **B12 (RadFrac):** Recovers methanol overhead (METH2); biodiesel-rich bottoms proceed to water wash (B5)
- **B6 (RadFrac):** Recovers methanol overhead (METH1); glycerol exits as bottoms product
- **MIXER3** combines METH1 and METH2 into the **METHREC recycle stream**, returned to MIXER2
- **B5 (Water wash unit):** Removes residual catalyst and glycerol traces; purified biodiesel exits as **M-OLEATE**

### Process Flowsheet

![Aspen PLUS Flowsheet](flowsheet.png)

---

## 📥 Base-Case Feed Stream Specifications

| Stream | Component | Molar Flow (kgmol/hr) | Mass Flow (kg/hr) | Temperature (°C) | Pressure (kPa) |
|---|---|---|---|---|---|
| WCO | Triolein (C₅₇H₁₀₄O₆) | 1.00 | 885.43 | 25 | 101.325 |
| METHANOL | Methanol (CH₃OH) | 6.00 | 192.24 | 25 | 101.325 |
| NAOH | Sodium Hydroxide | 0.2214 | 8.856 | 25 | 101.325 |

**Methanol-to-oil molar ratio (base case):** 6:1

**Theoretical maximum FAME production:**
