# 2. Development Platform

---

## 1. Interceptor Drone: 65mm Brushless Whoop

The flying platform is an ultra-lightweight, high-thrust **65mm ducted brushless micro-drone** utilizing an integrated All-In-One (AIO) flight controller.

| Subsystem | Component | Specification |
|---|---|---|
| **Frame** | 65mm Whoop Frame | Polycarbonate ducted frame with integrated propeller guards (weight: 3.2g) |
| **Motors** | 4x 0802 Brushless Motors | 19,000 KV, 1.0mm shaft diameter, micro JST-1.25 or direct solder |
| **Propellers** | 31mm 4-Blade Props | Polycarbonate, 1.0mm center bore (2 CW, 2 CCW) |
| **Flight Controller** | AIO ESP32-S3 Board | Integrated ESP32-S3 MCU + 6-DOF IMU (ICM-42688) + 5A 4-in-1 DShot300 ESC |
| **Battery** | 1S LiHV 300mAh | 3.8V nominal (4.35V peak), 30C continuous / 60C burst, BT2.0 or A30 connector |
| **All-Up Weight** | Fully Assembled | **32.0 grams** (including battery) |
| **Total Thrust** | 4 Motors @ 100% | **140 grams** (Thrust-to-weight ratio = **4.38 : 1**) |

---

## 2. Stationary Base Station: Optical Tracking

Rather than flying a heavy camera and compute board, vision and tracking are handled by a stationary ground unit connected to a host laptop.

| Subsystem | Component | Specification |
|---|---|---|
| **Camera Module** | OV9281 Monochrome USB | Global shutter, 120 FPS at $1280 \times 800$, M12 $120^\circ$ wide-angle lens |
| **Optical Filter** | 850nm Narrowband Film | Blocks visible ambient room lighting; isolates active NIR scatter |
| **Illuminator** | 850nm IR LED Array | Circular array of 850nm high-power infrared LEDs surrounding camera lens |
| **Radio Link** | ESP32-S3 USB Dongle | Connected to host laptop via USB; transmits ESP-NOW packets at 100 Hz |

---

## 3. Why the FireBeetle 2 Board Was Eliminated

1. **Mass Penalty:** The FireBeetle 2 board with camera lens and mounting hardware weighs ~18–22g. On a 35g drone, this is a 60% mass increase, causing immediate motor saturation and battery voltage collapse.
2. **Silicon Redundancy:** The drone flight controller already features an ESP32-S3. Carrying two identical MCUs doubles power regulators and passive losses needlessly.
3. **Severe Motion Blur:** The OV2640 rolling-shutter sensor indoor exposure time (1/30s) smears a 2 m/s mosquito across 40–50 pixels.
4. **Latency Bottleneck:** Running TinyML object detection on an ESP32-S3 achieves only 3–5 FPS with 200ms latency, making real-time interception impossible.

---

## Related Pages

- [01. Project Goal](01-Project-Goal.md)
- [03. Budget](03-Budget.md)
- [07. Build Sequence](07-Build-Sequence.md)
