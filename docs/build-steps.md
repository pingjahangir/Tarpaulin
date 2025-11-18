# **Build Steps – Automated Tarpaulin Protection System Prototype**

### *Documented by Mohammed Jahangir (GitHub: pingjahangir)*

Trainee Engineer – Guidsoft Technologies Pvt. Ltd.

This guide documents the full step-by-step process followed to design, fabricate, assemble, and test the tarpaulin automation prototype.

---

# 🧭 **1. Research & Planning**

### **1.1 Understanding the Real-World Problem**

We studied how material theft occurs during truck transportation:

* Drivers or helpers partially open the tarp mid-route
* Material is removed discreetly
* There is no tracking or alert mechanism
* Losses cost companies large amounts daily

We set out to design a system that makes tarpaulin access:

* Secure
* Controlled
* Trackable
* Automatable

### **1.2 Mechanical Study**

We evaluated:

* Lead screw mechanisms
* Stepper motor torque requirements
* Servo-based rolling systems
* 3D-printed bracket design
* Mounting structure feasibility

### **1.3 Electronics Study**

Researched each component:

* TB6560 stepper drivers
* NEMA17 motors
* MG995 servo motors
* Arduino Mega control logic
* Switch input handling

---

# 🛠️ **2. Mechanical Fabrication**

### **2.1 Building the Frame**

* Used a wooden baseboard as the main platform
* Marked alignment lines for lead screw placement
* Ensured both lead screws were parallel to avoid jamming

### **2.2 Installing Lead Screws**

* Mounted two metal lead screws (~600–800 mm long)
* Attached lead screw nuts to sliding carriage plate
* Connected each lead screw to a NEMA17 motor via couplers

### **2.3 Creating the Sliding Carriage**

* 3D-printed a rectangular carriage plate
* Attached the plate firmly to both lead screw nuts
* Ensured smooth sliding with minimal friction

### **2.4 Servo-Based Rolling System**

* Mounted a metal rod for tarpaulin rolling
* Attached two MG995 servos on either side
* Connected servo horns to the rod using custom 3D-printed clamps
* Ensured servos rotated the rod synchronously

### **2.5 Tarpaulin Attachment**

* Cut a green tarpaulin sheet
* Mounted one end tightly to the rolling shaft
* Attached the other end to the sliding plate
* Ensured even tension and alignment

---

# 🔌 **3. Electronics Assembly**

### **3.1 Wiring Stepper Motors and TB6560 Drivers**

Each stepper wired to its TB6560:

* **STEP → Arduino pin**
* **DIR → Arduino pin**
* **ENA left floating** (or tied high based on version)
* **Motor coil pairs wired correctly**
* **12V supply connected**

### **3.2 Wiring the Control Switches**

Two switches were connected using:

* INPUT_PULLUP mode
* One switch for opening
* One switch for closing

### **3.3 Wiring the Servo Motors**

MG995 servos wired to:

* Pin 9 (servo1)
* Pin 10 (servo2)
  Powered via external 5V supply.

### **3.4 Power Topology**

To ensure stability:

* Steppers → powered by 12V battery
* Servos → powered by 5V external supply
* Arduino → USB/5V
* **All grounds tied together**

---

# 💻 **4. Software Development**

### **4.1 Writing the Control Logic**

We developed a simple but effective Arduino program that:

* Reads switch states
* Moves NEMA17 stepper motors based on switch input
* Rotates servos in corresponding direction
* Prevents both switches from running motors at once
* Uses blocking step loops for synchronized movement

### **4.2 Switch Logic**

* **Switch 1 ON → Open tarpaulin**

  * NEMA motors clockwise
  * servo1 clockwise
  * servo2 counterclockwise

* **Switch 2 ON → Close tarpaulin**

  * NEMA motors counterclockwise
  * servo1 counterclockwise
  * servo2 clockwise

* **Both ON → Safety stop**

### **4.3 Step Pulse Timing**

Used:

```
stepInterval = 290 microseconds
```

This gave:

* Smooth motion
* No skipped steps
* Good servo-sync timing

### **4.4 Servo Control**

Servos move instantly to:

* 0° or 180° during operation
* 90° neutral when stopped

---

# 🧪 **5. Testing & Calibration**

### **5.1 Motor Direction Test**

* Verified clockwise and counterclockwise direction
* Adjusted DIR pin wiring where required

### **5.2 Lead Screw Alignment Test**

* Moved carriage full length
* Identified jamming points
* Re-aligned screw spacing

### **5.3 Servo Synchronization Test**

* Ensured both servos rotate simultaneously
* Checked rolling smoothness

### **5.4 Switch Debouncing**

* Verified that INPUT_PULLUP works reliably
* No false triggers

### **5.5 Full Prototype Trial**

* Pressed OPEN → tarp unrolled and carriage moved forward
* Pressed CLOSE → tarp rolled and carriage returned
* Tested emergency stop by pressing both switches

---

# 🧩 **6. Integration Issues Resolved**

Refer to `challenges-and-solutions.md` for detailed problem-solving logs.

Key solved issues:

* Stepper synchronization
* Servo torque problems
* TB6560 DIP configuration
* Frame alignment
* Power instability
* Tarpaulin slipping

---

# ⭐ **7. Completed Prototype**

The final prototype successfully demonstrates:

✔ A functional mechanical system
✔ Accurate motor control
✔ Rolling/unrolling automation
✔ Synchronized dual-stepper operation
✔ Switch-based safety logic
✔ Fully integrated hardware + software

This validates the feasibility of building a fully automated tarpaulin security system for heavy transport trucks.

---

# 👤 **8. Author**

**Mohammed Jahangir**
GitHub: [@pingjahangir](https://github.com/pingjahangir)
Trainee Engineer — Guidsoft Technologies Pvt. Ltd.

Tell me which direction you want!

