Perfect! If you're switching to a **2-pin switch for only power ON/OFF**, it simplifies things a lot.

Here’s your updated section for the **2-pin power switch**, replacing the 4-pin version:

---

#### 🔘 **3. Power Switch (2-Pin Metal Push Button – Latching Type)**  
- Mount the **switch after the fuse** to control entire power flow.  
- Use a **latching switch** (press once = ON, press again = OFF).  
- This switch simply opens/closes the power line — no signal pin involved.

| Pin Type         | Connects To                            |
|------------------|----------------------------------------|
| **Pin 1**        | **Battery Positive** (after **Fuse**)  |
| **Pin 2**        | **Input of Schottky Diode**            |

> This way, the switch cuts or passes the positive voltage from the battery.

---

### ⚠️ **Important Notes**
- This setup controls **power only**, not any software function.
- If you need to detect button presses for software (like mode changes), you’ll still need a **separate push button** wired to a digital pin.
- Always use a **latching switch** for this, so it stays ON or OFF after being pressed.

---

Would you like me to now update your full power flow diagram to reflect this 2-pin switch version?