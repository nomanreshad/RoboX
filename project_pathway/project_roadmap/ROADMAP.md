# 🛠️ Updated Project Roadmap – Step-by-Step  

### ✅ Step 1: **Hardware – Build the Circuit Diagram**
- ✅ **1.1. Power Supply + Arduino Setup**  
  🔹 Connect battery/power source to Arduino and modules safely

- ✅ **1.2. Motor Driver (L298N) + DC Motors** - [Sample Code](sample_code/MOTOR.md)  
  🔹 Connect DC motors for movement and rotation  
  🔹 Connect to Arduino for direction/speed control

- ✅ **1.3. Extras**  
  🔹 RGB LED for status indication - [Sample Code](sample_code/RGB_LED.md)  
  🔹 Buzzer for obstacle alert - [Sample Code](sample_code/BUZZER.md)  

- ✅ **1.4. Ultrasonic Sensors (HC-SR04)** - [Sample Code](sample_code/HC-SR04_SENSOR.md)  
  🔹 Mount fixed in front  
  🔹 Robot rotates to check different directions

- ✅ **1.5. Bluetooth Module (HC-05)** - [Sample Code](sample_code/HC-05_BLUETOOTH_MODULE.md)  
  🔹 TX/RX to Arduino (Serial Communication)  
  🔹 Pair with Android app for manual/voice control

---

### ✅ Step 2: **Software – Write Arduino Code Step-by-Step**
- ✅ **2.1. Movement Logic (Basic Controls)**  
  🔹 Move: forward, backward, left, right, rotate  
  🔹 Rotate in place (left/right) to scan environment

- ✅ **2.2. Ultrasonic Sensor Logic**  
  🔹 Move forward until object detected  
  🔹 Rotate left/right to scan  
  🔹 Decide the best path (least distance)

- ✅ **2.3. Bluetooth Command Handling**  
  🔹 Receive commands from app  
  🔹 Convert to movement, stop, or rotate

- ✅ **2.4. Voice Command Integration**  
  🔹 App converts voice to text → sends via Bluetooth  
  🔹 Arduino parses and acts (e.g., “go forward”, “rotate left”)
