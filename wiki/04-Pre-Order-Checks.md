# 4. Pre-Order Checks

---

## Critical Component Verifications

Before placing orders with suppliers, confirm the following technical specifications to prevent incompatibility:

### 1. Motors and Propellers
- **Shaft Diameter:** Confirm the 0802 brushless motors have a **1.0mm shaft diameter**. (Some variants use 0.8mm or 1.5mm shafts, which will not fit standard 31mm 4-blade whoop props).
- **Connector Type:** Confirm whether the motor wires terminate in micro JST-1.25 plugs or bare enamel wire. Bare wire is preferred for direct soldering to save mass.

### 2. AIO Flight Controller
- **Motor Output Protocol:** Confirm the integrated ESC supports **DShot300 or DShot600**.
- **MCU & IMU:** Confirm the board features an **ESP32-S3** with exposed SPI bus to an **ICM-42688** or **BMI270** 6-DOF IMU.
- **RF Transceiver:** Confirm the ESP32-S3 has an onboard ceramic antenna or a 2.4GHz copper trace antenna.

### 3. Battery and Power Connectors
- **Connector Interface:** Strictly specify **BT2.0** or **A30** solid-pin connectors.
  * *Warning:* Avoid legacy PH2.0 rolled-sheet connectors. PH2.0 has a high contact resistance of $\approx 150\text{ m}\Omega$, causing severe voltage sag ($>0.4\text{V}$) during throttle bursts and triggering premature low-voltage cutoffs.
- **Battery Chemistry:** Select 1S **LiHV** ($4.35\text{V}$ cutoff) with $\ge 30\text{C}$ discharge rating.

### 4. Base-Station Camera Module
- **Sensor Type:** Confirm the camera uses an **OV9281** global-shutter monochrome sensor. (Avoid rolling-shutter sensors like OV2640 or OV5640).
- **Lens Mount:** Confirm an M12 lens mount with an unobstructed front thread to mount the $850\text{nm}$ bandpass filter film.

---

## Ordering Rule

Order all items according to the standardized Bill of Materials in [03. Budget](03-Budget.md). Do not purchase coreless brushed motors or add secondary onboard compute boards.

---

## Related Pages

- [02. Development Platform](02-Development-Platform.md)
- [03. Budget](03-Budget.md)
- [07. Build Sequence](07-Build-Sequence.md)
