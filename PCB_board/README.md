# Adjustable Dual-Rail Linear Power Supply




## Overview

This PCB implements a transformer-based adjustable symmetric linear power supply using LM317 (positive rail) and LM337 (negative rail).  
The design is intended for analog laboratory and audio applications requiring adjustable dual-rail voltage.

The supply includes current-boosting pass transistors, output protection, auxiliary regulation for panel electronics, and standard stability and protection elements as recommended in the regulator datasheets.

---

### 3D Model:
<img width="1206" height="652" alt="image" src="https://github.com/user-attachments/assets/1e88aec4-d3cf-4337-9dc5-bc78ac05fb59" />

### Scheamtic:
<img width="1734" height="1191" alt="image" src="https://github.com/user-attachments/assets/934c705e-9a38-4ae2-ae31-69d0edb05fc9" />

---

## Input Stage

The power supply is driven from a transformer providing:

- 2 × 32 VAC
- Maximum current for each: 5 A

Rectification is implemented using a dual-diode full-wave configuration.  
After rectification:

Each rail includes two 4700 µF bulk capacitors (4.7 mF per capacitor).  
Due to the relatively moderate bulk capacitance and high load capability, ripple voltage increases under heavy load conditions.

---

## Regulation Stage

Voltage regulation is implemented using:

- LM317 (positive rail)
- LM337 (negative rail)

Both regulators are adjustable via external multi-turn potentiometers mounted off-board (front panel configuration).
For additional flexibility, THT footprints for potentiometers are included on the PCB.  
These can be used if the user needs or prefers the connstant output voltage.
<img width="408" height="153" alt="image" src="https://github.com/user-attachments/assets/947a3696-673c-44f5-ad98-845b30751597" />


Each regulator includes:

- 100 nF input capacitor
- 1 µF output capacitor
- Protection diodes to prevent reverse discharge during power-down
- Startup bias implementation for controlled initial behavior

---

## Current Boost Stage

To extend output current beyond the 1.5 A limit of LM317/LM337, one external TIP-series pass transistor is used per rail.

This allows the supply to deliver higher output current, while the regulators control the reference and stability.

The output rails are protected by:

- 4 A fuse per rail

The design assumes a maximum intended continuous output current of approximately 4 A.

---

## Maximum Output Voltage

Although the transformer provides 2 × 32 VAC, the maximum guaranteed regulated output voltage is approximately:

±28 V DC

This limitation is caused by cumulative voltage drops across:

- Rectifier diodes
- Series resistances
- Regulator dropout voltage
- V_BE drop of the TIP pass transistors

These drops ensure stable regulation but reduce the theoretical maximum voltage available at the output.

---

## Thermal Considerations

Due to the high rectified input voltage, substantial power dissipation occurs when the output voltage is set significantly lower than the input voltage.

Power dissipation can be approximated by:

P ≈ (Vin - Vout) × Iout

This results in considerable heat generation in:

- LM317 / LM337 regulators
- TIP pass transistors

To manage thermal conditions, the PCB includes heatsinks rated approximately for passive cooling using radiators:

- LM317 / LM337: up to ~10 W
- TIP pass transistors: up to ~17 W

These values assume adequate airflow and proper mechanical mounting.  
Under sustained high-current operation at low output voltage, additional cooling or forced airflow may be required.

---

## Auxiliary Supply

An additional LM7818 linear regulator branch provides:

- Supply for digital panel meters
- Power LED indicator

<img width="259" height="248" alt="image" src="https://github.com/user-attachments/assets/1b0e8e8a-f235-46d7-a66c-f4c8405376f1" />

---

## Design Notes & Limitations

The design was developed based on a 2 × 32 V transformer, primarily because it was readily available.  
However, for most practical applications, a lower secondary voltage (e.g., 2 × 16–18 V) would be more appropriate.

In my use cases, the maximum required output voltage is ±12 V. Therefore, a 32 V transformer is overkill and results in significant voltage drop across the regulators. This leads to increased power dissipation and substantial heat generation.

In the future, the transformer will likely be replaced with a lower-voltage unit better matched to the intended output range. For now, all testing is performed using the existing transformer, without applying heavy loads.

Additionally, mounting holes for THT potentiometers are included on the PCB to increase flexibility. This allows the board to be used either with panel-mounted multi-turn potentiometers or with onboard adjustment, enabling configuration as a fixed or adjustable voltage source.

Each output rail includes two screw-terminal connectors to improve usability and versatility, allowing multiple connections and easier integration into laboratory setups.
