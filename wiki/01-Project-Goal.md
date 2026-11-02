# 1. Project Goal

---

## Objective

Develop a high-agility, autonomous micro-drone system named **Musquiteer** to detect, pursue, and neutralize mosquitoes indoors.

---

## Operating Concept

Mosquitoes (*Aedes* / *Culex*) fly erratically at $1.2 - 2.5\text{ m/s}$ with accelerations exceeding $1.5\text{ g}$. An effective interception system requires high thrust-to-weight ratio ($>3:1$), high-framerate optical tracking ($\ge 100\text{ FPS}$), and zero parasitic aerodynamic drag.

The system is partitioned into two specialized nodes:

1. **Stationary Optical Base Station:**
   * High-framerate ($120\text{ FPS}$) Near-Infrared (NIR) camera with $850\text{nm}$ bandpass filter and active $850\text{nm}$ illumination.
   * Tracks insect centroids via temporal differencing and predicts flight trajectories using a 4-state Kalman filter.
   * Sends real-time guidance setpoints to the drone at $100\text{ Hz}$ over ESP-NOW ($<2\text{ms}$ latency).

2. **Agile Micro-Interceptor Drone:**
   * 65mm ducted brushless Whoop ($32\text{g}$ All-Up Weight).
   * High thrust-to-weight ratio ($4.3:1$) powered by 0802 19,000KV brushless motors.
   * Hard real-time $500\text{ Hz}$ attitude control on an integrated ESP32-S3 All-In-One (AIO) flight controller.
   * **Kinetic Ingestion Neutralization:** Ducted propellers spinning at $28,000\text{ RPM}$ create an intake suction funnel that mechanically neutralizes mosquitoes upon contact—eliminating high-voltage hazards and EMI completely.

---

## Why the Initial Wiki Concept Was Challenged

| Old Initial Concept | Failure Mode Identified | Corrected Single-Path Design |
|---|---|---|
| LiteWing Coreless Brushed Motors | Motor burnout, voltage sag, unable to lift camera | 0802 Brushless Motors (4.3:1 thrust-to-weight ratio) |
| Onboard FireBeetle 2 Camera | Motion blur at 1/30s exposure, 3-5 FPS inference latency | Offboard Stationary 120 FPS Global-Shutter NIR Camera |
| Flat Mosquito-Bat Mesh | High aerodynamic drag, severe pitching moments, inertia | Ingestion inside Ducted Propeller Cowl (0g added weight) |
| Energized High Voltage Grid | Arc EMI resets flight controller, fire hazard near LiPo | Pure Mechanical Blade Neutralization (Zero HV, Zero EMI) |

---

## Related Pages

- [02. Development Platform](02-Development-Platform.md)
- [05. Prototype Capabilities](05-Prototype-Capabilities.md)
- [07. Build Sequence](07-Build-Sequence.md)
