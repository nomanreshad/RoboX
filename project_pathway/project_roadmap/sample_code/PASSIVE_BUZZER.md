### 🔌 **Circuit Connection (Breadboard)**

| Buzzer Pin | Connect To     |
|------------|----------------|
| **Positive (+)** | Arduino Digital Pin **8** |
| **Negative (-)** | GND on Arduino |

> 📌 You **don't need any resistor** for this buzzer when using with Arduino.

---

### 🧠 **Arduino Code – Playing Different Frequencies**

```cpp
int buzzerPin = 8;

void setup() {
  // No setup needed for tone
}

void loop() {
  // Play a low frequency
  tone(buzzerPin, 500); // 500 Hz
  delay(1000);

  // Play a mid frequency
  tone(buzzerPin, 1000); // 1 kHz
  delay(1000);

  // Play a high frequency
  tone(buzzerPin, 2000); // 2 kHz
  delay(1000);

  // Stop sound
  noTone(buzzerPin);
  delay(1000);
}
```

---

### 🧠 Code: Melody

```cpp
int buzzerPin = 8;

void setup() {
  // Play a simple melody on startup
  playMelody();
}

void loop() {
  // Do nothing in loop
}

void playMelody() {
  tone(buzzerPin, 262); // C4
  delay(300);
  tone(buzzerPin, 294); // D4
  delay(300);
  tone(buzzerPin, 330); // E4
  delay(300);
  tone(buzzerPin, 349); // F4
  delay(300);
  tone(buzzerPin, 392); // G4
  delay(300);
  noTone(buzzerPin);
}
```

---

## 🚨 2. **Obstacle Warning Tone Example**

When the object is too close (e.g., less than 10cm), a warning tone plays for a short time.

### ✅ Circuit Update:
- Use **HC-SR04** with:
  - **Trig → pin 9**
  - **Echo → pin 10**

### 🧠 Code: Obstacle + Warning Tone

```cpp
#define trigPin 9
#define echoPin 10
#define buzzerPin 8

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.println(distance);

  if (distance < 10) {
    // Play warning tone
    tone(buzzerPin, 1000); // 1kHz warning
    delay(300);
    noTone(buzzerPin);
    delay(200);
  } else {
    noTone(buzzerPin);
  }

  delay(200);
}
```

---

### 🧠 **Code: Mario Theme on Passive Buzzer**

This is a short but recognizable part of the Mario tune:

```cpp
#define buzzer 8

void setup() {
  // Play Mario theme once on startup
  playMario();
}

void loop() {
  // Nothing here
}

void beep(int note, int duration) {
  tone(buzzer, note, duration);
  delay(duration * 1.3);
  noTone(buzzer);
}

void playMario() {
  beep(660, 100); delay(100);
  beep(660, 100); delay(300);
  beep(660, 100); delay(300);
  beep(510, 100); delay(100);
  beep(660, 100); delay(300);
  beep(770, 100); delay(550);
  beep(380, 100); delay(575);

  beep(510, 100); delay(450);
  beep(380, 100); delay(400);
  beep(320, 100); delay(500);
  beep(440, 100); delay(300);
  beep(480, 80);  delay(330);
  beep(450, 100); delay(150);
  beep(430, 100); delay(300);

  beep(380, 100); delay(200);
  beep(660, 80);  delay(200);
  beep(760, 50);  delay(150);
  beep(860, 100); delay(300);
  beep(700, 80);  delay(150);
  beep(760, 50);  delay(350);
  beep(660, 80);  delay(300);
  beep(520, 80);  delay(150);
  beep(580, 80);  delay(150);
  beep(480, 80);  delay(500);
}
```
