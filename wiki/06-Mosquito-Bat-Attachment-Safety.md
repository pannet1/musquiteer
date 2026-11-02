# 6. Neutralization & Safety

---

## 1. Why High-Voltage Meshes Were Eliminated

Mounting an energized mosquito racket grid onto a micro-drone creates three fatal engineering failure modes:

```
           +-------------------------------------------------------------+
           |       HAZARDS OF ENERGIZED HIGH-VOLTAGE MESH ON DRONE       |
           +-------------------------------------------------------------+

           [ 2,000V - 3,000V Spark Discharge ]
                           │
           ┌───────────────┴───────────────┐
           ▼                               ▼
    [ Severe RF/EMI ]              [ Aerodynamic Drag ]
    dI/dt pulse induces            Flat mesh acts as a sail;
    ground bounce; resets          destabilizes pitch axis;
    ESP32-S3 and latches IMU       blocks propeller downwash
```

1. **Broadband EMI & Microcontroller Latch-Up:**  
   When an electric arc discharges across a $2,000\text{V} - 3,000\text{V}$ spark gap, the nanosecond-scale current transient ($dI/dt$) generates intense electromagnetic radiation. This induces high-frequency transients onto the shared $3.3\text{V}$ logic plane, causing the flight controller to reset or latching the SPI bus to the IMU, resulting in immediate catastrophic flight loss.
2. **Aerodynamic Drag and Angular Inertia:**  
   A flat racket mesh acts as an aerodynamic sail. In forward translation, the incoming airflow exerts large pitching moments that easily overwhelm the control authority of micro-props. Furthermore, placing mass at the airframe perimeter dramatically increases rotational inertia ($I_{xx}, I_{yy}$), making PID stabilization sluggish and unstable.
3. **LiPo Fire Hazard:**  
   Lithium-Polymer batteries vent flammable electrolyte vapors if punctured or damaged during a crash. An active high-voltage spark source operating millimeters from a punctured 1S LiPo cell presents an unacceptable risk of fire.

---

## 2. The Selected Solution: Mechanical Propeller Ingestion

The engineered design uses the drone's existing propulsion system as the neutralization mechanism:

* **Blade Tip Velocity:** At $28,000\text{ RPM}$, the tips of the $31\text{mm}$ polycarbonate propellers travel at:
  $$v_{\text{tip}} = 2\pi \times \left(\frac{28000}{60}\right) \times 0.0155\text{ m} \approx 45.4\text{ m/s} \approx 163.6\text{ km/h}$$
* **Aerodynamic Inflow Funnel:** The ducted cowl creates a high-velocity low-pressure intake funnel. When the drone approaches within $3\text{ cm}$ of a mosquito, downwash suction pulls the insect into the spinning rotor disk.
* **Impact Neutralization:** The kinetic energy of rigid polycarbonate blades colliding at $>160\text{ km/h}$ instantly neutralizes the insect upon impact.
* **Key Advantages:**
  * **0 grams** added weight.
  * **0 Volts** electrical hazard.
  * **Zero EMI** generated.
  * Inherent human safety provided by the ducted perimeter rings.

---

## Related Pages

- [01. Project Goal](01-Project-Goal.md)
- [05. Prototype Capabilities](05-Prototype-Capabilities.md)
- [07. Build Sequence](07-Build-Sequence.md)
