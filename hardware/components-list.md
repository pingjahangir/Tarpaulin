# ✅ **`hardware/components-list.md` — Components Used in the Tarpaulin Automation Prototype**

# **Hardware Components List**

### *Automated Tarpaulin Protection System Prototype*

**Author:** Mohammed Jahangir (GitHub: *pingjahangir*)

This document contains the complete set of electrical, electronic, mechanical, and structural components used in building the automated tarpaulin system prototype.

---

# 🧰 **1. Electronic Components**

### **1.1 Microcontroller**

| Component             | Quantity | Purpose                                                            |
| --------------------- | -------- | ------------------------------------------------------------------ |
| **Arduino Mega 2560** | 1        | Reads switch inputs, controls stepper drivers, drives servo motors |

---

### **1.2 Stepper Motors**

| Component                                    | Quantity | Specs                          | Purpose                                        |
| -------------------------------------------- | -------- | ------------------------------ | ---------------------------------------------- |
| **NEMA 17 Stepper Motor (4.2 kg-cm torque)** | 2        | 200 steps/rev, 1.8° step angle | Moves the tarpaulin along the lead screw rails |

The NEMA 17 motors provide high torque required for moving the tarp smoothly.

---

### **1.3 Stepper Motor Drivers**

| Component                 | Quantity | Specs                               | Purpose                                  |
| ------------------------- | -------- | ----------------------------------- | ---------------------------------------- |
| **TB6560 Stepper Driver** | 2        | Microstepping capability, 3A output | Powers and controls each NEMA 17 stepper |

Parameters configured during development:

* Microstepping: **Full step mode**
* Current limit adjusted using DIP switches
* ENA/DIR/STEP controlled by Arduino Mega

---

### **1.4 Servo Motors**

| Component                   | Quantity | Specs                         | Purpose                                             |
| --------------------------- | -------- | ----------------------------- | --------------------------------------------------- |
| **MG995 High-Torque Servo** | 2        | 9 kg-cm torque, 180° rotation | Responsible for rolling and unrolling the tarpaulin |

These were used to rotate the metal shaft that rolls the tarp.

---

### **1.5 Switches**

| Component                           | Quantity | Purpose                                                  |
| ----------------------------------- | -------- | -------------------------------------------------------- |
| **Tactile Switches / Push Buttons** | 2        | One controls opening, other controls closing of the tarp |

Functions:

* Switch 1 → Start opening movement
* Switch 2 → Start closing movement
* If both are pressed → **error mode**

---

### **1.6 Power Supplies**

| Component             | Quantity | Purpose                               |
| --------------------- | -------- | ------------------------------------- |
| 12V DC Battery Packs  | 2        | Power for TB6560 drivers and steppers |
| 5V Servo Power Source | 1        | Power for MG995 servos                |
| Arduino USB/5V        | 1        | Arduino logic supply                  |

⚠️ All grounds were connected together (common ground).

---

# 🔧 **2. Mechanical Components**

### **2.1 Lead Screw Assembly**

| Component                           | Quantity | Purpose                                 |
| ----------------------------------- | -------- | --------------------------------------- |
| **Lead Screws (length ~600–800mm)** | 2        | Linear motion track for tarp movement   |
| **Lead Screw Nuts**                 | 2        | Coupled to the moving platform          |
| **Motor Couplers**                  | 2        | Connect NEMA17 shaft to the lead screws |

---

### **2.2 Frame & Mounts**

All custom-designed and 3D-printed.

| Component                             | Quantity | Purpose                              |
| ------------------------------------- | -------- | ------------------------------------ |
| **Stepper Motor Mounts (3D-printed)** | 2        | Hold motors firmly on wooden base    |
| **Support Blocks (3D-printed)**       | 2        | Lead screw alignment                 |
| **Sliding Platform Connectors**       | 2        | Hold the tarp on the moving carriage |
| **Servo Mounts**                      | 2        | Align MG995 with tarp shaft          |

Material used: **PLA 3D-printed parts**

---

### **2.3 Tarpaulin System**

| Component                     | Quantity | Purpose                              |
| ----------------------------- | -------- | ------------------------------------ |
| **Green Tarpaulin Sheet**     | 1        | Simulates the real truck tarp        |
| **Rolling Shaft (metal rod)** | 1        | Servo rotates the rod to roll/unroll |

---

### **2.4 Wooden Base**

| Component        | Quantity | Purpose                                             |
| ---------------- | -------- | --------------------------------------------------- |
| **Wooden Board** | 1        | Entire prototype mounted on this board for rigidity |

Approx size: 2–3 feet.

---

# 🔌 **3. Electrical Wiring Summary**

* Arduino Mega connected to step/direction pins:

  * `dirPin1 = 24`, `stepPin1 = 25`
  * `dirPin2 = 26`, `stepPin2 = 27`
* Switch inputs:

  * `switch1Pin = 22`
  * `switch2Pin = 23`
* Servo outputs on PWM:

  * `servo1 = Pin 9`
  * `servo2 = Pin 10`
* External power for steppers: 12V
* External power for servos: 5V
* Arduino powered via USB
* **Common ground** used everywhere (mandatory)

---

# 🧪 **4. Tools Used**

* 3D Printer (FDM – PLA)
* Soldering iron + solder wire
* Hot glue gun (for reinforcement)
* Wire cutter + stripper
* Mini screwdriver set
* CAD software (for designing brackets)
* Multimeter (for measuring stepper driver pins)

---

# 📦 **5. Consumables**

* Jumper wires (M–M, M–F, F–F)
* PLA filament
* Hot glue sticks
* M3 screws and nuts
* Electrical tape
* Zip ties
* Bearings (optional)

---

# 🧤 **6. Summary**

This components list covers the entire bill of materials used to build the tarpaulin automation prototype from scratch.
It reflects research, electrical understanding, mechanical design, and hands-on fabrication done by **Mohammed Jahangir (pingjahangir)** during the project.
