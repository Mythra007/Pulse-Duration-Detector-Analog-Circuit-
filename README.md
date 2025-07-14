# Pulse-Duration-Detector-Analog-Circuit-
Designed a fully analog system using op-amps, RC timing, and MOSFET discharge logic to detect valid HIGH pulses by duration and drive an LED output without digital components.
# Pulse Duration Detector (Analog Circuit Design)

This project implements a **non-periodic pulse duration detection circuit** using only analog components — op-amps, resistors, capacitors, and a MOSFET. The system turns ON an LED **only if the input pulse remains HIGH for a predefined minimum duration**, and resets immediately when the pulse ends. Short spikes or brief noise pulses are ignored.

---

## Objective

Design a low-power, precision analog system to:
- Detect if a digital input pulse lasts longer than a minimum duration
- Ignore short pulses (noise immunity)
- Turn ON an LED **only during valid pulses**
- Automatically reset when the pulse ends
- Use **only analog components** (no timers, MCUs, or digital logic)

---

## Components Used

| Component      | Purpose                                                                 |
|----------------|-------------------------------------------------------------------------|
| **LT1363 Op-Amp** | Acts as a high-speed comparator and LED driver                        |
| **RC Network** | Integrates input signal over time to evaluate pulse duration             |
| **IRFZ44N MOSFET** | Rapidly discharges capacitor to reset system after pulse              |
| **Vishay VS-E5PX3012 LED** | Output indicator, driven directly by op-amp                   |
| **Potentiometer (optional)** | Dynamically adjusts threshold voltage (i.e., pulse duration sensitivity) |

---

## Design Breakdown

### Comparator Stage
- **Configured as a non-inverting comparator**
- Uses **LT1363** op-amp for its **±50mA output** (sufficient to directly drive LED)
- Reference threshold voltage set via voltage divider

### RC Integrator
- Integrates the input HIGH pulse to build voltage across a capacitor
- If duration is long enough, comparator triggers LED ON
- **Short pulses don't cross threshold → LED remains OFF**

### MOSFET Discharge Circuit
- **N-Channel IRFZ44N** discharges capacitor quickly after pulse ends
- Controlled via inverting op-amp stage

### Feedback (Hysteresis)
- Positive feedback resistor adds hysteresis
- Improves noise immunity and comparator switching stability

---

## Design Highlights

- ✅ **No microcontroller** used
- ✅ **No digital logic** — purely analog
- ✅ **No transistor needed for LED drive** (op-amp output sufficient)
- ✅ **Fully resettable, supports continuous operation**
- ✅ **Dual ±12V power only**

---

## Simulation Behavior

- Simulated in **LTspice**
- Uses controlled waveforms with valid and invalid pulses
- Shows:
  - LED turns ON only for pulses > threshold duration
  - Capacitor resets instantly via MOSFET after each pulse

---

## Threshold Tuning (Potentiometer)

- Adjusting potentiometer changes comparator reference voltage
- Allows **dynamic tuning of required pulse length**
- Bonus feature for flexible duration detection

---

## Visuals (To Add)
- Circuit schematic
- Waveforms (Input vs Capacitor vs LED)
- LTspice simulation screenshot

---

## Applications

- Pulse qualification circuits (debouncing, edge filters)
- Digital signal validation for industrial sensors
- Analog watchdog systems
- Timing-based access control (e.g., button held down long enough)

---

## Future Extensions

- Replace LED with opto-isolator or relay
- Use LM393 comparator IC for faster switching
- Add audio buzzer for visual + audio indication
- Combine with a microcontroller to log valid events
