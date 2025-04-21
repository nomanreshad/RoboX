# 🤖 Circular 2-Wheel Differential Drive Robot

## 🧱 1. Chassis Design

- **Shape**: Circular  
- **Wheel Setup**:
  - **2x Big Wheels** (Left & Right side)
  - **2x Ball Caster Wheels** (placed diagonally for stability)
- **Movement**: Controlled using only wheels (no body rotation motor needed)

---

## ⚙️ 2. Components Required

| Component | Quantity | Notes |
|----------|----------|-------|
| 🔌 DC Gear Motor | 2 | N20 or high-torque TT motors |
| 🔌 L298N Motor Driver | 1 | To control motor direction/speed |
| ⚙️ Big Wheels | 2 | Compatible with motors |
| ⚪ Ball Caster Wheels | 2 | For balance |
| 🔋 Lithium-ion Battery (7.4V or 12V) | 1 | Power source |
| 🧠 Arduino Uno | 1 | Microcontroller |
| 🔌 Jumper Wires (Male-Male) | ~10 | For basic connections |
| 🔌 Jumper Wires (Male-Female) | ~10 | For power/motor/breadboard |
| 🔲 Breadboard | 1 | For prototyping (optional) |
| 🔧 Chassis | 1 | Circular, DIY or store-bought |

---

## 🔋 3. Power Supply

- **Battery Options**:
  - ✅ 7.4V Li-ion Battery Pack (Recommended)
  - ✅ 12V Li-ion Battery (for higher torque)
- **Regulation (Optional)**:
  - Use a 7805 voltage regulator to power sensors safely
- **Charger**:
  - 🔌 Use 2S Li-ion/LiPo charger (e.g., TP4056, Imax B3)

---

## 🔌 4. Complete Wiring Guide: Arduino + L298N + DC Motors

### 🧰 Required Items

- ✅ Arduino UNO/Nano  
- ✅ L298N Motor Driver Module  
- ✅ 2x DC Motors  
- ✅ Breadboard  
- ✅ Jumper Wires  
- ✅ Battery (7.4V/12V)

---

### 🔋 A. Power Setup

| From | To |
|------|----|
| Battery (+) | `L298N VCC` |
| Battery (–) | `L298N GND` |
| Arduino GND | `L298N GND` |
| L298N 5V (with jumper) | `Arduino 5V` (⚠️ Only if jumper enabled) |

> 📝 **Note**: If battery >12V, disconnect `L298N 5V` from Arduino and use a regulator.

---

### ⚙️ B. Motor Connections

| L298N Pins | Motor |
|------------|-------|
| OUT1, OUT2 | Left Motor (Motor A) |
| OUT3, OUT4 | Right Motor (Motor B) |

---

### 🔧 C. Arduino to L298N

| L298N Pin | Arduino Pin | Description |
|----------|--------------|-------------|
| IN1 | D8 | Left Motor Direction 1 |
| IN2 | D7 | Left Motor Direction 2 |
| IN3 | D6 | Right Motor Direction 1 |
| IN4 | D5 | Right Motor Direction 2 |
| ENA | D9 | Left Motor Speed (PWM) |
| ENB | D10 | Right Motor Speed (PWM) |

> 📝 **Tip**: Connect ENA/ENB to **5V** if you don’t need PWM speed control.

---

## 🔁 Movement Types (Differential Drive Table)

| Left Motor | Right Motor | Movement |
|------------|-------------|----------|
| Forward    | Forward     | Move Forward |
| Backward   | Backward    | Move Backward |
| Forward    | Stop        | Curve Right |
| Stop       | Forward     | Curve Left |
| Forward    | Backward    | Rotate Clockwise |
| Backward   | Forward     | Rotate Counter-Clockwise |

---

## 🚗 Robot Movement Logic:

### ✅ **Move Forward**  
- **Left Motor:** Forward  
- **Right Motor:** Forward  

```cpp
IN1 = HIGH, IN2 = LOW   → Left motor moves forward  
IN3 = HIGH, IN4 = LOW   → Right motor moves forward  
```

---

### ✅ **Move Backward**  
- **Left Motor:** Backward  
- **Right Motor:** Backward  

```cpp
IN1 = LOW, IN2 = HIGH   → Left motor moves backward  
IN3 = LOW, IN4 = HIGH   → Right motor moves backward  
```

---

### 🔄 **Turn Left (Normal Left Turn)**  
👉 The robot **moves forward** while gradually turning left (like a car).  
- **Left Motor: Slower or Stop**  
- **Right Motor: Forward**

```cpp
IN1 = LOW; IN2 = LOW;    → Left motor OFF or slow
IN3 = HIGH; IN4 = LOW;   → Right motor forward
```

---

### 🔁 **Rotate Left In-Place (Spin Left)**  
👉 The robot **stays in the same spot** and spins to the left.  
- **Left Motor: Backward**  
- **Right Motor: Forward**

```cpp
IN1 = LOW; IN2 = HIGH;   → Left motor backward
IN3 = HIGH; IN4 = LOW;   → Right motor forward
```

---

### 🔄 **Turn Right**
- **Left Motor: Forward**  
- **Right Motor: Slower or Stop**

```cpp
IN1 = HIGH; IN2 = LOW;   → Left motor forward
IN3 = LOW; IN4 = LOW;    → Right motor OFF or slow
```

---

### 🔁 **Rotate Right In-Place**
- **Left Motor: Forward**  
- **Right Motor: Backward**

```cpp
IN1 = HIGH; IN2 = LOW;   → Left motor forward
IN3 = LOW; IN4 = HIGH;   → Right motor backward
```

---

### ✅ **Stop the Robot**  
- Both motors are turned off (or PWM set to 0):

```cpp
ENA = 0  
ENB = 0  
```

---

## 💻 Arduino Code (Basic Motor Rotation Example)

```cpp
#define ENA 9
#define IN1 8
#define IN2 7
#define ENB 10
#define IN3 6
#define IN4 5

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
}

void loop() {
  // Rotate robot to the right
  digitalWrite(IN1, HIGH); // Left motor forward
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);  // Right motor backward
  digitalWrite(IN4, HIGH);
  analogWrite(ENA, 150);   // Speed control (0-255)
  analogWrite(ENB, 150);
  delay(1000);             // Rotate for 1 second

  // Stop motors
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
  delay(1000);
}
```
