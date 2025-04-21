**DIP 3-Color RGB LED Module**. This module has **4 pins**:  
- **R (Red)**
- **G (Green)**
- **B (Blue)**
- **GND (Ground)**

---

## ✅ **1. Circuit Design (Wiring with Breadboard)**

### ➤ **Connections**

| RGB Module Pin | Connect To                 |
|----------------|----------------------------|
| R              | Arduino Digital Pin **9**  |
| G              | Arduino Digital Pin **10** |
| B              | Arduino Digital Pin **11** |
| GND            | Arduino **GND**            |

- Use **3 jumper wires** for signal pins and **1 for GND**.
- Place the RGB module on the **breadboard** and connect the pins accordingly.

💡 This module is **common cathode** (GND shared). So writing **HIGH = ON** won’t work. You’ll need to use **analogWrite** to control brightness (0 = off, 255 = full brightness).

---

## ✅ **2. Arduino Code (Fade and Static Colors)**

```cpp
// RGB pins
const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;

void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  // Static Colors
  setColor(255, 0, 0);   // Red
  delay(1000);
  setColor(0, 255, 0);   // Green
  delay(1000);
  setColor(0, 0, 255);   // Blue
  delay(1000);
  setColor(255, 255, 0); // Yellow
  delay(1000);
  setColor(80, 0, 80);   // Purple
  delay(1000);
  setColor(0, 255, 255); // Cyan
  delay(1000);
  setColor(255, 255, 255); // White
  delay(1000);
  setColor(0, 0, 0);     // Off
  delay(1000);

  // Fade effect
  for (int i = 0; i <= 255; i++) {
    setColor(i, 0, 255 - i); // fade between red and blue
    delay(10);
  }
}

void setColor(int red, int green, int blue) {
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}
```
