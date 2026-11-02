# 5. Prototype Capabilities

---

## System Performance Specifications

| Parameter | Performance Bound | Verification Method |
|---|---|---|
| **All-Up Flight Weight** | $32.0\text{ g}$ (drone + battery) | Precision digital laboratory balance |
| **Peak Total Thrust** | $140\text{ g}$ | Static inverted load-cell thrust bench |
| **Thrust-to-Weight Ratio** | **4.38 : 1** | Ratio of peak thrust to AUW |
| **Hover Throttle Level** | $\approx 38 - 42\%$ | Current draw and PWM telemetry at hover |
| **Max Flight Speed** | $8.0\text{ m/s}$ ($28.8\text{ km/h}$) | Optical ground-station trajectory derivation |
| **Max Angular Rate** | $1,200^\circ/\text{s}$ | Gyroscope saturation threshold |
| **Optical Frame Rate** | $120\text{ FPS}$ | Base camera USB 3.0 stream |
| **Shutter Exposure Time** | $1.5\text{ ms}$ ($1/660\text{ s}$) | Global-shutter register configuration |
| **Telemetry Update Rate** | $100\text{ Hz}$ | ESP-NOW packet interval |
| **Guidance Latency** | $<2.0\text{ ms}$ (RF transmission) | Host TX to drone RX timestamp differential |
| **Flight Endurance** | 3.5 to 4.5 minutes | Sustained hover on 1S 300mAh LiHV |
| **Neutralization Mode** | Mechanical ingestion (28,000 RPM blades) | Ducted intake propeller impact |

---

## Deliberately Excluded Items

To guarantee flight stability and safety, the following items are **strictly excluded**:
- **No Onboard Camera:** Vision processing is conducted offboard on the base station.
- **No High-Voltage Grid:** No Cockcroft-Walton multipliers, spark gaps, or exposed electrified meshes are mounted on the drone.
- **No Flat Racket Mesh:** No planar aerodynamic surfaces are mounted to the frame.

---

## Related Pages

- [01. Project Goal](01-Project-Goal.md)
- [06. Neutralization & Safety](06-Mosquito-Bat-Attachment-Safety.md)
- [08. Project Status & Limitations](08-Project-Status-Limitations.md)
