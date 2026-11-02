# 7. Build Sequence

---

## Step-by-Step Linear Implementation

Follow these 9 sequential steps in exact order. There are no branches or alternative paths.

```
 [Step 1: Procure BOM] ──────► [Step 2: Mechanical Assembly] ──► [Step 3: Power & Wiring]
                                                                        │
 [Step 6: Base Vision] ◄────── [Step 5: Base Station Rig]    ◄── [Step 4: Firmware & IMU]
         │
         ▼
 [Step 7: Telemetry Link] ───► [Step 8: Tethered Calibration] ──► [Step 9: Free Flight]
```

---

### Step 1: Procure the Exact Bill of Materials
Acquire the exact items specified in [03. Budget](03-Budget.md):
- 65mm polycarbonate Whoop frame with ducted propeller guards
- 4x 0802 19,000KV brushless motors (1.0mm shaft)
- 31mm 4-blade polycarbonate propellers (2 CW, 2 CCW)
- AIO Flight Controller (ESP32-S3 + ICM-42688 IMU + 5A 4-in-1 ESC)
- 2x 1S 300mAh LiHV batteries with BT2.0 / A30 connector
- 100µF 10V low-ESR ceramic capacitor
- OV9281 120 FPS USB monochrome global-shutter camera module
- 850nm optical bandpass filter film + 850nm IR LED board
- ESP32-S3 USB dev module (base-station radio transceiver)

---

### Step 2: Mechanical Assembly & Airframe Rigging
1. Invert the 65mm frame. Insert the four 0802 brushless motors into the motor wells.
2. Fasten each motor with two M1.4 $\times$ 3mm screws. Apply a dab of low-strength threadlocker (Loctite 222) to each screw.
3. Route the three-phase motor wires along the underside duct struts toward the center bay; secure them with strips of Kapton tape.
4. Press the 31mm 4-blade propellers onto the motor shafts:
   * Front-Left: Clockwise (CW)
   * Front-Right: Counter-Clockwise (CCW)
   * Rear-Left: Counter-Clockwise (CCW)
   * Rear-Right: Clockwise (CW)
5. Spin each blade by hand to verify a minimum $0.8\text{ mm}$ radial clearance between propeller blade tips and duct inner walls.

---

### Step 3: Power Distribution & Flight Electronics Wiring
1. Strip $2\text{ mm}$ of insulation from a BT2.0/A30 20AWG pigtail. Solder the red wire to `VBAT (+)` and the black wire to `GND (-)` on the AIO board.
2. Solder the $100\mu\text{F}$ 10V capacitor directly across the `VBAT` and `GND` pads on the AIO board to suppress motor switching transients.
3. Solder the three phase wires of each motor directly to the corresponding ESC solder pads on each corner of the AIO board.
4. Mount the AIO board onto the frame's center dampers using silicone rubber grommets. Ensure the arrow marked on the PCB points directly toward the front duct.
5. Measure resistance across the battery connector using a digital multimeter. Verify resistance is $>1\text{ k}\Omega$. A reading $<50\,\Omega$ indicates a solder bridge—clear before applying power.

---

### Step 4: Flash Firmware & Calibrate Attitude Loop
1. Connect the AIO board to your development PC via USB-C. Flash the ESP32-S3 using ESP-IDF with FreeRTOS enabled.
2. Configure SPI clock to the ICM-42688 IMU at $24\text{ MHz}$ with IMU sampling rate at $1\text{ kHz}$.
3. Set the flight control PID update rate to $500\text{ Hz}$ and motor output protocol to DShot300.
4. Place the assembled drone on a perfectly level surface. Run the calibration routine to store zero-rate gyro offsets and accelerometer gravity vector in flash memory.
5. Power the board with a 1S battery with propellers removed. Send test pulses to verify each motor spins in its designated direction.

---

### Step 5: Assemble the Stationary NIR Optical Base Station
1. Screw a $120^\circ$ wide-angle lens onto the OV9281 camera module. Affix the $850\text{nm}$ bandpass filter film directly in front of the lens using optical adhesive rings.
2. Align the circular $850\text{nm}$ IR LED array concentrically around the camera lens.
3. Mount the camera assembly on a stationary tripod positioned in the corner of the room, looking downward into the flight volume at a $30^\circ$ tilt angle.
4. Plug the camera into the laptop's USB 3.0 port. Plug the second ESP32-S3 module (radio transmitter) into another USB port.

---

### Step 6: Deploy Base-Station Target Tracking Software
1. Configure the OV9281 to stream monochrome video at $1280 \times 800$ resolution at $100\text{ FPS}$ with exposure locked to $1.5\text{ ms}$.
2. For each frame $I_t$, compute absolute difference against previous frame: $D_t = |I_t - I_{t-1}|$. Static objects produce values near zero; moving retro-reflective insects appear as bright point clusters.
3. Apply binary threshold $T=30$ to $D_t$, followed by a $3 \times 3$ morphological open operation to eliminate sensor shot noise.
4. Compute centroid coordinates $(u_t, v_t)$ of any cluster measuring between 2 and 15 pixels.
5. Feed $(u_t, v_t)$ into a 4-state Linear Kalman Filter $[x, y, v_x, v_y]^T$ to produce smoothed target positions and instantaneous heading vectors.

---

### Step 7: Configure Low-Latency Telemetry Link
1. Configure the host ESP32-S3 and the drone AIO board on ESP-NOW channel 6 with zero-encryption mode for minimum latency.
2. Transmit this 12-byte packed guidance payload from host to drone at $100\text{ Hz}$:
   ```c
   struct __attribute__((packed)) {
       uint8_t  header;       // 0xAA
       int16_t  target_x;     // mm relative to room origin
       int16_t  target_y;     // mm relative to room origin
       int16_t  target_z;     // mm relative to room origin
       int16_t  target_yaw;   // target bearing in milliradians
       uint8_t  state_flags;  // Bit 0: Hover, Bit 1: Intercept, Bit 2: Abort
       uint8_t  checksum;     // XOR of bytes 0..10
   } CommandPacket;
   ```
3. On the drone's Core 0, an interrupt handler receives the packet, validates the checksum, and writes the target vector into a thread-safe atomic buffer for the Core 1 flight controller.

---

### Step 8: Calibration & Tethered Interception Test
1. Place four small IR retro-reflective markers on the floor at known dimensions ($1\text{m} \times 1\text{m}$ square). Compute perspective transform matrix from camera pixel space to real-world ground coordinates $(X, Y, Z)$.
2. Suspend the drone from the ceiling using a $1.5\text{m}$ braided line attached through the center-of-gravity loop on top of the frame.
3. Using an IR LED attached to a thin rod, move a test target across the camera's field of view.
4. Confirm the tethered drone yaw-aligns toward the target within $100\text{ ms}$ and tilts its pitch/roll axes to track the target without hunting or oscillating.

---

### Step 9: Live Flight Engagement & Mechanical Ingestion
1. Connect battery. Verify voltage is $4.30\text{V} - 4.35\text{V}$ per cell.
2. Send `state_flags = 0x01` (Hover mode). The drone ascends to $1.0\text{ meter}$ and maintains position via base-station optical feedback.
3. When the base station detects a valid mosquito profile ($500\text{ Hz}$ motion cadence + size 2–10 pixels):
   * State switches to `0x02` (Intercept).
   * Base station extrapolates target trajectory $200\text{ ms}$ forward.
   * Drone accelerates along the interception vector at $1.5\text{ m/s}$.
4. As the ducted front cowl reaches within $3\text{ cm}$ of the mosquito, low-pressure propeller downwash sucks the insect into the intake; high-speed polycarbonate blades rotating at $28,000\text{ RPM}$ mechanically neutralize the target upon impact.
5. Drone returns to default $1.0\text{m}$ hover center and awaits next target acquisition.

---

## Related Pages

- [03. Budget](03-Budget.md)
- [04. Pre-Order Checks](04-Pre-Order-Checks.md)
- [06. Neutralization & Safety](06-Mosquito-Bat-Attachment-Safety.md)
