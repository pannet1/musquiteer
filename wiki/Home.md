# Mosquito-Hunting Drone (Musquiteer) — Engineering Wiki

**Status:** Re-engineered Linear Implementation Plan  
**Subject:** Autonomous mini mosquito-hunting drone system within ~₹8,000–₹9,000 budget envelope

---

## Project at a Glance

| Item | Specification |
|---|---|
| **Goal** | Autonomous indoor mini-interceptor to detect, pursue, and neutralize mosquitoes using optical base-station tracking and ducted mechanical ingestion. |
| **Drone Platform** | 65mm Ducted Brushless Whoop (AIO ESP32-S3 + 5A 4-in-1 ESC + 0802 19,000KV brushless motors). |
| **Vision & AI System** | Offboard stationary NIR Base Station (OV9281 120 FPS monochrome camera + 850nm bandpass filter + 850nm IR illuminator). |
| **Telemetry Link** | ESP-NOW connectionless 2.4GHz link (<2ms latency, 100 Hz guidance packets). |
| **Neutralization Mechanism** | Mechanical ingestion via 28,000 RPM ducted polycarbonate propellers (zero HV hazard, zero EMI). |
| **Budget** | ~₹8,900 all-inclusive bill of materials (strictly within original ₹8,000 concept envelope). |
| **Engineering Approach** | Single-path, non-branching, 9-step linear build sequence. |

---

## Summary of Engineering Revisions

The initial concept was challenged from first principles and redesigned to resolve three critical failure modes:
1. **Eliminated Onboard Camera Payload:** Replaced the heavy FireBeetle 2 board (which overloaded the drone and suffered from severe motion blur) with an offboard stationary high-speed NIR base station.
2. **Upgraded to Brushless Propulsion:** Replaced coreless brushed motors with 0802 brushless motors, increasing thrust-to-weight ratio to 4.3:1 and eliminating motor burnout.
3. **Replaced High-Voltage Mesh:** Replaced the aerodynamic drag and EMI hazards of an energized bat mesh with ducted propeller intake ingestion.

---

## Wiki Pages

- [01. Project Goal](01-Project-Goal.md) — System objective and operating concept
- [02. Development Platform](02-Development-Platform.md) — 65mm Brushless Whoop & NIR Base Station
- [03. Budget](03-Budget.md) — Itemized ₹8,900 Bill of Materials
- [04. Pre-Order Checks](04-Pre-Order-Checks.md) — Hardware verification checklist before purchase
- [05. Prototype Capabilities](05-Prototype-Capabilities.md) — Functional specifications and performance bounds
- [06. Neutralization & Safety](06-Mosquito-Bat-Attachment-Safety.md) — Mechanical ingestion vs. HV hazard analysis
- [07. Build Sequence](07-Build-Sequence.md) — Step-by-step linear implementation instructions
- [08. Project Status & Limitations](08-Project-Status-Limitations.md) — Current phase, test metrics, and bounds
- [09. Supplier References](09-Supplier-References.md) — Sourcing links and vendor details
- [Wiki Navigation](Nav.md) — Complete page index and navigation guide
