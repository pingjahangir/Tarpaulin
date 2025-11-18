
# **Challenges Faced & How We Solved Them**

### *Automated Tarpaulin Protection System Prototype*

**By Mohammed Jahangir (GitHub: pingjahangir)**

This document highlights all major issues encountered during the development of the prototype and the engineering decisions taken to overcome them.

---

# 🧩 **1. Synchronizing Both NEMA17 Stepper Motors**

### **Challenge:**

Both stepper motors must rotate *exactly at the same speed* and *same timing*, or the tarpaulin will tilt or jam on the lead screws.

### **Solution:**

* We used **one shared step pulse loop** to step both motors simultaneously
* Both TB6560 drivers receive identical HIGH/LOW pulses
* Direction pins are controlled together
* This ensured perfect synchronization

```cpp
digitalWrite(stepPin1, HIGH);
digitalWrite(stepPin2, HIGH);
delayMicroseconds(stepInterval);
digitalWrite(stepPin1, LOW);
digitalWrite(stepPin2, LOW);
```

This solved the alignment and movement smoothness issue.

---

# 🧩 **2. TB6560 Configuration Confusion**

### **Challenge:**

TB6560 has DIP switches for current, microstepping, and decay modes.
Incorrect settings cause:

* Motor vibrations
* Missed steps
* Overheating

### **Solution:**

We went through datasheets and tested combinations until achieving stable behavior:

* Microstepping: **Full step**
* Current limit: Configured for NEMA17 rated current
* Proper wiring of ENA, DIR, and STEP pins

After correct configuration, motor noise reduced drastically.

---

# 🧩 **3. Servo Motors Not Providing Enough Torque During Roll/Unroll**

### **Challenge:**

MG995 servos initially struggled to roll/unroll the heavy tarpaulin sheet.

### **Solution:**

* Improved mechanical leverage by repositioning servo horns
* Reduced friction via sanding and alignment
* Balanced the tarp on both sides
* Tuned servo angles in code (0° ↔ 180°)

After this, the rolling mechanism became smooth and consistent.

---

# 🧩 **4. Lead Screw Alignment Issues**

### **Challenge:**

If the lead screws are even slightly misaligned, the moving platform gets stuck.

### **Solutions Implemented:**

* Re-measured spacing between mounts
* Adjusted 3D-printed brackets
* Realigned couplers
* Ensured equal tension across sliding platform

This improved motion stability significantly.

---

# 🧩 **5. Both Switches Pressed at Once → Motors Fighting Each Other**

### **Challenge:**

When both switches were pressed accidentally, motors tried to move in opposite directions.

### **Solution:**

Added logic to detect this condition and immediately stop all motors:

```cpp
if (switch1State == LOW && switch2State == LOW) {
  Serial.println("Error: Both switches are pressed. Motors will not move.");
  stopAllMotors();
}
```

This introduced **safety control** to protect motors and driver hardware.

---

# 🧩 **6. Tarpaulin Slipping or Folding Incorrectly**

### **Challenge:**

The tarp sheet occasionally bunched up or slipped while rolling.

### **Solutions:**

* Adjusted tension
* Ensured equal pull from both sides
* Added roughness to servo shaft for grip
* Reduced speed occasionally to prevent jerks

This made the unrolling much smoother.

---

# 🧩 **7. Power Supply Instability**

### **Challenge:**

NEMA17 motors and MG995 servos draw significant current.
Power fluctuations caused:

* servo jitter
* stepper skipping
* Arduino resets

### **Solution:**

* Separated servo power from stepper power
* Used dedicated 12V battery pack for steppers
* Used 5V external supply for servos
* Common ground maintained

After power separation, stability improved greatly.

---

# 🧩 **8. Mechanical Vibrations on Wooden Base**

### **Challenge:**

The wooden base → vibrations → inaccurate movement.

### **Solution:**

* Added rubber padding under the base
* Tightened mount screws
* Added hot glue on joints for damping
* Reinforced servo and motor mounts

Vibration was nearly eliminated.

---

# 🧩 **9. 3D Printed Parts Not Matching Perfect Dimensions**

### **Challenge:**

Some parts required post-processing because of:

* Slight warping
* Tight tolerances
* Layer shifting

### **Solution:**

* Sanded the shafts and holes
* Filed 3D-printed slots
* Reprinted a few parts with better infill
* Used M3 screws to clamp loose areas

This made the mechanical assembly precise.

---

# 🧩 **10. Understanding TB6560 Timing**

### **Challenge:**

TB6560 requires precise **pulse width** and **delay** for reliable stepping.

### **Solution:**

Experimented with pulse delays and found:

```
stepInterval = 290 microseconds
```

This gave:

* Smooth movement
* No dropped steps
* Perfect servo synchronization

---

# ✨ **Summary**

This project required combining **mechanical engineering**, **embedded programming**, **CAD design**, **3D printing**, and **electrical knowledge**.

Through trial, testing, and iteration, each challenge was carefully solved, resulting in a fully working tarpaulin automation prototype built from scratch.

---

# 👤 **Author**

**Mohammed Jahangir**
GitHub: [@pingjahangir](https://github.com/pingjahangir)
Trainee Engineer — Guidsoft Technologies Pvt. Ltd.

I will prepare **docs/build-steps.md** — the full detailed step-by-step build guide for the tarpaulin project, similar to what we built for the robotic hand.

