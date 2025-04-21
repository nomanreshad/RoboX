## 🔌 **Ultrasonic Sensor HC-SR04 – Wiring with Arduino (Breadboard)**

### 🟦 **Sensor Pins**:
- **VCC** – Power (+5V)
- **Trig** – Trigger input (from Arduino)
- **Echo** – Echo output (to Arduino)
- **GND** – Ground

### 🧠 **Breadboard Connections**:

| HC-SR04 Pin | Connects To         |
|-------------|----------------------|
| VCC         | 5V on Arduino        |
| GND         | GND on Arduino       |
| Trig        | Pin **9** on Arduino |
| Echo        | Pin **10** on Arduino|

> ✅ Use male-to-male jumper wires. Insert sensor into the breadboard, connect each pin as listed.

---

## 🧾 **Sample Arduino Code (Obstacle Detection)**

This code checks the distance and prints it in the Serial Monitor.

```cpp
#define trigPin 9
#define echoPin 10

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  // Send trigger pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read echo
  duration = pulseIn(echoPin, HIGH);

  // Calculate distance (in cm)
  distance = duration * 0.034 / 2;

  // Print distance
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  delay(500);
}
```

---

## ✅ What It Does:
- Sends a 10µs pulse to the **Trig** pin.
- Waits for the **Echo** signal and measures how long it took to return.
- Calculates the distance using the speed of sound.
- Displays the result in centimeters.

---

### 📏 **"Calculates the distance using the speed of sound"**

The **HC-SR04 Ultrasonic Sensor** works by sending a **sound wave** (inaudible to us) from the **Trig pin**, and then waiting to **receive the echo** on the **Echo pin**.

So basically:

1. It sends out a sound pulse.
2. The sound hits an object and **bounces back**.
3. The sensor measures how long that bounce took (round trip).
4. Since we know the **speed of sound is about 343 meters per second (or 0.0343 cm/µs)**, we can calculate how far away the object is.

---

### 🧮 **Distance formula**:
```cpp
distance = (duration × speed of sound) / 2
```

In our Arduino code:
```cpp
distance = duration * 0.034 / 2;
```

- `duration` = time (in microseconds) it took for the sound to go to the object and back.
- `0.034` = speed of sound in cm/µs.
- Divide by 2 because the sound travels to the object **and then back**.
