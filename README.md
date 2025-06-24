# Lightweight Hybrid Outboard Electric Assist System

## Objective

Design a **lightweight electric-assist system** to augment a **15hp 2-stroke gas outboard motor** with a **brushless DC motor (BLDC)** and a **capacitor bank**. The system is designed to provide additional **torque and horsepower for 5–6 seconds** during hole-shot acceleration to help a small boat get on plane faster. It should be **entirely self-contained**, relying on **onboard power generation only** — no external charging.

---

## System Overview

### ⚙️ Core Components

* **BLDC Motor**: Provides torque assist during planing, operating at engine shaft speeds.
  *Estimated weight: 4–6 kg*

* **Supercapacitor Bank**: Supplies high-current bursts for short durations.
  *Estimated weight: 4–5 kg*

* **Small Battery Pack**: Powers ESC logic, cap balancer, sensors, and control system.
  *Estimated weight: 0.5–1 kg*

* **Onboard Generator**: Taps engine shaft to recharge caps and maintain battery.
  *Estimated weight: 1–2 kg*

* **ESC (Electronic Speed Controller)**: Manages BLDC operation and energy draw.
  *Estimated weight: 0.3–0.6 kg*

* **Control Logic**: Manages boost timing via manual trigger or throttle-aware automation.
  *Estimated weight: 0.2–0.4 kg*

**Total estimated added weight**: \~10–15 kg

---

## Performance Targets

| Parameter        | Target Value                     |
| ---------------- | -------------------------------- |
| Assist Power     | 3.5–4.0 kW                       |
| Boost Duration   | 5–6 seconds                      |
| Cap Bank Voltage | 48–60 V                          |
| Motor RPM Range  | 5000–6000 RPM                    |
| Prop Shaft RPM   | \~3000–3200 RPM (2:1 gear ratio) |

---

## Capacitor Bank Design

### 🔋 Energy Requirement

* Target boost: **4 kW × 6 sec = 24,000 J (24 kJ)**

### 🧮 Capacitance Calculation (48V target)

```
C = 2E / V² = (2 × 24,000) / 48² ≈ 20.8 F
```

### 🔧 Recommended Configuration

* **18x 2.7 V, 3400 F supercapacitors in series**

  * Total voltage: 48.6 V
  * Effective capacitance: 94.4 F
  * Stored energy:

```
E = 0.5 × C × V² = 0.5 × 94.4 × 48^2 ≈ 109 kJ
```

* Provides \~4x required energy, reducing voltage sag and increasing reliability
* Must include:

  * Voltage balancing
  * Overvoltage protection
  * Safe venting and thermal dissipation

***Estimated capacitor bank weight: 4–5 kg***

---

## Motor Selection

### Required RPM

* Engine shaft RPM during hole shot: **5000–6000 RPM**
* BLDC motor must match or gear to this range

### Target Motor Specs

* KV Rating: **120–150 KV**
* Voltage: **48–60 V**
* Power: **4 kW continuous**
* Torque-capable at low-mid RPM

### Motor Types to Consider

* High-torque inrunner or outrunner motors used in:

  * Electric motorcycles
  * E-foil / electric surfboards
  * Light EV conversions

***Estimated motor weight: 4–6 kg***

---

## Mechanical Integration

* **Coupling Method**:

  * Direct coupling to engine crankshaft via clutch or splined shaft
  * Belt drive or chain reduction if KV is too high
* **Mounting Options**:

  * Inline with prop shaft
  * Side-mounted swing pod or bracket
* **Considerations**:

  * Water ingress protection
  * Vibration isolation
  * Quick-disengage or clutch system

***Estimated added mounting hardware weight: 1–2 kg***

---

## Charging System

### Generator Options

* Tap from outboard flywheel/alternator (if available)
* Add-on high-RPM DC generator linked to engine shaft

***Estimated generator weight: 1–2 kg***

### Charging Logic

* Charge caps between boost cycles with current-limited converter
* Include:

  * Buck converter with current limiting
  * Reverse current protection (diode or FET switch)
  * Capacitor voltage monitoring and cutoff
  * Trickle charge for battery pack

***Estimated power electronics weight: 0.5–1 kg (including ESC)***

---

## Control Logic

### Triggering Options

* Manual push button (on tiller or throttle control)
* Optional automation:

  * Based on throttle position
  * Based on GPS speed threshold

### Battery Pack

* Small 12V LiFePO₄ (\~50–100 Wh)

  * Powers ESC logic, sensors, relays, and controller
  * Charged from same onboard generator via buck converter

***Estimated battery weight: 0.5–1 kg***

---

## System Architecture Diagram

```
 [Gas Engine Shaft]
         │
         ├─────────────────────────────┐
         │                             │
     [DC Generator]              [Prop Shaft]
         │
         ▼
 [Charge Controller / Buck Converter]
         ├─────────────────────┐
         │                     │
 [Capacitor Bank (48V)]   [Battery Pack (12V)]
         │                     │
         └─────────────┐       │
                       ▼       ▼
                  [ESC / Motor Controller]
                       │
                  [BLDC Motor]
                       │
        [Inline Shaft Assist or Pod Propulsion]
```

---

## Next Steps

1. **Select Motor**: 120–150 KV, 48V, \~4 kW
2. **Select ESC**: 48V, 100A+, capacitor-compatible
3. **Build Cap Bank**: 18x 2.7V, 3400F supercaps with active balancing
4. **Design Charging System**: Buck converter with current limit and cutoff
5. **Design Mechanical Integration**: Shaft, pod, or belt mount
6. **Develop Control System**: Manual trigger, safety interlocks, logic control
7. **Waterproof & Test**: Full system validation in lab and then in water

---

## Considerations

* Ensure waterproofing and marine corrosion resistance
* Include thermal management for ESC and motor
* Protect against overvoltage, overcurrent, and heat
* Build diagnostics for voltage, current, and temp logging

---

## Summary

This hybrid electric assist system is designed to add a **short-duration torque burst** to a small outboard motor using an onboard-charged capacitor bank. By leveraging **supercapacitors for energy storage**, a **low-KV BLDC motor**, and **onboard generation**, the system enables **quick planing** while maintaining low weight and full self-sufficiency on the water.

**Total estimated system weight**: \~10–15 kg
