# Biodiesel Production via Transesterification — Steady-State Process Simulation

> A continuous biodiesel production process modelled in Aspen PLUS V11, implementing rigorous second-order reversible reaction kinetics for the base-catalyzed transesterification of waste cooking oil (WCO) to fatty acid methyl esters (FAME).

---

## Project Overview

This project presents a complete steady-state simulation of an industrial-scale biodiesel production plant built in Aspen PLUS V11. The simulation models the full process chain from feed preparation through reaction, phase separation, methanol recovery, and final biodiesel purification using the pseudo-homogeneous kinetic model of Vicente et al. (2005).

The process was designed around a target feedstock of waste cooking oil (WCO), represented as triolein (C₅₇H₁₀₄O₆), reacting with methanol in the presence of a sodium hydroxide (NaOH) homogeneous catalyst.

---

## Simulation Environment

| Item | Detail |
|---|---|
| Software | Aspen PLUS V11 |
| Thermodynamic Model | NRTL (Non-Random Two Liquid) |
| Simulation Type | Continuous Steady-State |
| Reactor Type | CSTR (Continuous Stirred Tank Reactor) |
| Kinetic Model | Vicente et al. (2005) — pseudo-homogeneous, 2nd order reversible |

The NRTL activity coefficient model was selected for its suitability in handling the polar, non-ideal liquid mixtures present in this system — including methanol, glycerol, water, and fatty acid esters.

---

## Process Description

The flowsheet is structured around four sequential sections:

### 1. Feed Preparation
- **WCO** (triolein) enters the mixer directly
- **Methanol** and **NaOH catalyst** are first premixed, then combined with WCO and the **methanol recycle stream

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
- **Distillation Column:** Recovers methanol overhead; biodiesel-rich bottoms proceed to water wash (B5)
- **Two-phase separator:** Recovers methanol overhead; glycerol exits as bottoms product
- **Water wash unit:** Removes residual catalyst and glycerol traces; purified biodiesel exits as **M-OLEATE**

### Process Flowsheet

![Aspen PLUS Flowsheet](AspenPLUS.png)

---

## Base-Case Feed Stream Specifications

| Stream | Component | Molar Flow (kgmol/hr) | Mass Flow (kg/hr) | Temperature (°C) | Pressure (kPa) |
|---|---|---|---|---|---|
| WCO | Triolein (C₅₇H₁₀₄O₆) | 1.00 | 885.43 | 25 | 101.325 |
| METHANOL | Methanol (CH₃OH) | 6.00 | 192.24 | 25 | 101.325 |
| NAOH | Sodium Hydroxide | 0.2214 | 8.856 | 25 | 101.325 |

**Methanol-to-oil molar ratio (base case):** 6:1

---

## Reaction Kinetics — Vicente et al. (2005)

The transesterification reaction was modelled as three consecutive reversible reactions, each second-order overall (first order with respect to each reactant), using the kinetic parameters of Vicente et al. (2005) for NaOH-catalyzed transesterification at 60°C.

### Kinetic Parameters

| Reaction Step | Direction | Rate Constant k (L/mol·min) | Activation Energy Eₐ (cal/mol) |
|---|---|---|---|
| TG → DG + FAME | Forward (k₁) | 0.0510 | 7,566 |
| DG + FAME → TG | Reverse (k₂) | 0.3983 | 7,413 |
| DG → MG + FAME | Forward (k₃) | 0.5417 | 9,931 |
| MG + FAME → DG | Reverse (k₄) | 0.9583 | 9,823 |
| MG → GL + FAME | Forward (k₅) | 0.0090 | 1,423 |
| GL + FAME → MG | Reverse (k₆) | 0.000015 | — |

---

## 🔧 CSTR Operating Conditions

| Parameter | Value |
|---|---|
| Temperature | 60°C |
| Pressure | 101.325 kPa |
| Base-case residence time | 0.5 hr |
| Reactor specification type | Residence time |

---

## Key Simulation Result

FAME yield at base-case conditions:

$$\text{FAME Yield} = \frac{\text{FAME mass flow (kg/hr)}}{889.47 \text{ kg/hr}} \times 100 = \mathbf{100.0\%}$$

The high yield is consistent with the strong forward rate constants of the Vicente et al. (2005) kinetic model under NaOH catalysis at 60°C, which drives the three-step reaction system to thermodynamic equilibrium within the base-case residence time of 0.5 hours.

---

This simulation was developed as part of a B.Eng thesis in Chemical Engineering at the **University of Port Harcourt**, under the supervision of **Prof. Koyejo M. Oduola**. The full thesis extends this flowsheet with a structured **One-At-A-Time (OAT) sensitivity analysis** of four process variables (methanol-to-oil ratio, catalyst concentration, temperature, and residence time) on FAME yield 
