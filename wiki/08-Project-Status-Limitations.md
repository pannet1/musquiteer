# 8. Project Status & Limitations

---

## 1. Project Engineering Status

The project architecture has completed first-principles engineering review and is locked into a **single linear execution plan**. 

| Phase | Milestone | Status |
|---|---|---|
| **Architecture** | Physics, payload, and power tree validation | **Complete** (Single-path locked) |
| **BOM Definition** | Component selection and budget optimization | **Complete** (₹9,300 total) |
| **Hardware Build** | Mechanical assembly and flight electronics wiring | Ready to execute (Step 1–3) |
| **Firmware & Control** | ESP-IDF attitude loop and DShot configuration | Ready to execute (Step 4) |
| **Base Station** | 120 FPS NIR optical tracking & ESP-NOW link | Ready to execute (Step 5–7) |
| **Flight Interception** | Tethered validation and free-flight engagement | Ready to execute (Step 8–9) |

---

## 2. Operational Limitations & Bounds

To ensure dependable operation within the defined hardware envelope, adhere to these operational bounds:

1. **Flight Volume:**  
   A single stationary OV9281 wide-angle camera covers an effective operational volume of approximately **$3.0\text{m} \times 3.0\text{m} \times 2.5\text{m}$**. Beyond this range, target pixel resolution drops below 2 pixels.
2. **Flight Endurance:**  
   The 1S 300mAh LiHV battery delivers **3.5 to 4.5 minutes** of sustained flight. Keep spare batteries charged on an external 1S LiHV balance charger.
3. **Ambient Light Isolation:**  
   The $850\text{nm}$ bandpass filter rejects domestic fluorescent, incandescent, and LED room lighting. However, direct outdoor sunlight through open windows contains strong NIR spectral power and should be shaded during tracking trials.
4. **Indoor Air Currents:**  
   Turn off high-speed ceiling fans during interception operations to prevent turbulent air currents that exceed the drone's attitude authority.

---

## Related Pages

- [01. Project Goal](01-Project-Goal.md)
- [05. Prototype Capabilities](05-Prototype-Capabilities.md)
- [07. Build Sequence](07-Build-Sequence.md)
