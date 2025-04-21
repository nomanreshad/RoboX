## 🔵 **1.5. Bluetooth Module (HC-05)**

### 🔌 **Circuit Diagram Connection (with Arduino UNO)**

| **HC-05 Pin** | **Connect to Arduino UNO** |
|---------------|-----------------------------|
| VCC           | 5V                          |
| GND           | GND                         |
| TXD           | **Pin 10 (RX)**             |
| RXD           | **Pin 11 (TX)** *(via voltage divider)*  
| EN (optional) | Leave open or 3.3V (for AT mode) |

---

### ⚠️ **Important Note:**
The **HC-05 Bluetooth module's RX pin** (which receives data) **only supports 3.3V**.  
But the **Arduino UNO TX pin** sends data at **5V**, which can damage the HC-05 RX pin over time.

---

### ✅ **Solution: Use a Voltage Divider**

To safely reduce 5V (from Arduino TX) to around 3.3V (for HC-05 RX), we use **two resistors** to make a **voltage divider**.

### ⚡ Voltage Divider Formula:

```
            R2
V out = ----------- X V in
          R1 + R2
```

Where:
- `V_in` = input voltage (here it's 5V from Arduino TX)
- `V_out` = the reduced voltage (what HC-05 receives)
- `R1` = the resistor connected to the **signal source** (Arduino TX) → here it's **1kΩ**
- `R2` = the resistor connected to **GND** → here it's **2kΩ**

---

### 🧠 In this case:

-  R1 = 1kΩ
- R2 = 2kΩ
- V in = 5V

Plug into the formula:

```
             2kΩ               
V out = ------------- X 5V 
          1kΩ + 2kΩ

          2
      = ----- X 5V ≈ 3.3V
          3            
```

So the TX voltage from Arduino is safely stepped down to ~3.3V before going into the HC-05 RX pin.

---

### 🔧 How to Make It:

Connect two resistors like this:
- One **1kΩ resistor** from **Arduino TX** to a **middle point**.
- One **2kΩ resistor** from the **middle point** to **GND**.
- Then connect the **middle point** to **HC-05 RX pin**.

---

### 🟡 What is the "Middle Point"?

The **middle point** is simply the **junction** where the two resistors are connected together.

---

Here’s how the full connection works step by step:

### 🧩 Components:
- **1kΩ resistor** (R1)
- **2kΩ resistor** (R2)

---

### 🔌 Step-by-Step Wiring:
1. **Connect one end of the 1kΩ resistor (R1)** to **Arduino TX pin**.
2. **Connect one end of the 2kΩ resistor (R2)** to **GND (ground)**.
3. **Connect the other ends of R1 and R2 together** — this junction is the **middle point**.
4. Connect the **middle point to the HC-05 RX pin**.

---

### 🔌 Diagram:

```
    Arduino TX
        |
       R1 (1kΩ)
        |
     [Middle Point] ---> goes to HC-05 RX
        |
       R2 (2kΩ)
        |
       GND
```

---

### 🧠 **Code (Using SoftwareSerial)**

```cpp
#include <SoftwareSerial.h>

SoftwareSerial BT(10, 11); // RX, TX

void setup() {
  Serial.begin(9600);
  BT.begin(9600); // Default baud rate of HC-05
  Serial.println("Bluetooth Ready");
}

void loop() {
  if (BT.available()) {
    char c = BT.read();     // Receive from phone
    Serial.print(c);        // Show on Serial Monitor
  }

  if (Serial.available()) {
    char c = Serial.read(); // Send from computer
    BT.print(c);            // Send to Bluetooth
  }
}
```

---

### 📱 **Test via Android App**
You can use:
- **Bluetooth Terminal HC-05 or Arduino Bluetooth Controler** (Google Play)
- Or any custom app that supports HC-05

---

### 📌 Use Cases in Your Robot:
- Receive commands like: `'F'` (forward), `'B'` (back), `'L'` (left), `'R'` (right), `'S'` (stop)
- Also voice command (with Android voice to text + send via Bluetooth)
