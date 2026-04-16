# Button-Controlled LED with Serial Feedback

A beginner Arduino project that reads a push button, lights up an LED, and sends status messages to the Serial Monitor. This demonstrates **digital input**, **digital output**, **serial communication**, and **conditional logic** in one simple sketch.

## 📸 Demo Behavior
- **Button NOT pressed:** LED is OFF. Serial Monitor is quiet.
- **Button PRESSED:** LED turns ON. Serial Monitor prints `Button Pushed: 1` (or `0` depending on wiring).

## 🧰 Hardware Requirements
- Arduino Board (Uno, Nano, Mega, etc.)
- 1x Push Button
- 1x LED (Red used in sketch)
- 1x 220Ω Resistor (for LED)
- Jumper Wires
- Breadboard (optional but recommended)

## 🔌 Wiring Instructions

### Option A: Using Internal Pull-Up Resistor (Recommended)
*No external resistor needed for the button.*

| Component | Arduino Pin |
| :--- | :--- |
| Button Leg 1 | Digital Pin **12** |
| Button Leg 2 | **GND** |
| LED Anode (+) | 220Ω Resistor → Digital Pin **3** |
| LED Cathode (-) | **GND** |

### Option B: Using External Pull-Down Resistor
| Component | Arduino Pin |
| :--- | :--- |
| Button Leg 1 | **5V** |
| Button Leg 2 | Digital Pin **12** + 10kΩ Resistor to **GND** |
| LED Anode (+) | 220Ω Resistor → Digital Pin **3** |
| LED Cathode (-) | **GND** |

> ⚠️ **Important:** If using Option B, change `pinMode(pushButton, INPUT_PULLUP);` back to `pinMode(pushButton, INPUT);` in the code.

## 📂 Files in this Repository
- `button_led_serial.ino` – Main Arduino sketch
- `README.md` – This documentation

## 🚀 How to Use

1. **Install Arduino IDE**  
   Download from [arduino.cc](https://www.arduino.cc/en/software)

2. **Clone or Download this Repository**  
   ```bash
   git clone https://github.com/Abdelhakim-Baalla/DigitalReadSerial-Arduino-Button
   ```

3. **Open the Sketch**  
   Launch Arduino IDE and open `button_led_serial.ino`

4. **Configure Board & Port**  
   - `Tools > Board` → Select your Arduino model  
   - `Tools > Port` → Select the correct COM port

5. **Upload the Code**  
   Click the **Upload** button (right arrow icon)

6. **Open Serial Monitor**  
   - Go to `Tools > Serial Monitor`  
   - Set baud rate to **9600** (bottom right corner)

7. **Test It!**  
   Press the button. The LED should light up and a message should appear.

## 🧠 Code Walkthrough

```cpp
int pushButton = 12;   // Button connected to pin 12
int RedLED = 3;        // LED connected to pin 3

void setup() {
  Serial.begin(9600);                    // Start serial communication
  pinMode(pushButton, INPUT_PULLUP);     // Enable internal pull-up resistor
  pinMode(RedLED, OUTPUT);               // Set LED pin as output
}

void loop() {
  int buttonState = digitalRead(pushButton);  // Read button state

  if (buttonState == LOW) {                   // LOW = button pressed (with pull-up)
    digitalWrite(RedLED, HIGH);               // Turn LED ON
    Serial.print("Button Pushed: ");
    Serial.println(buttonState);              // Prints 0 when pressed
  } else {
    digitalWrite(RedLED, LOW);                // Turn LED OFF
  }

  delay(1);                                   // Small delay for stability
}
```

**Key Concepts Demonstrated:**
- `INPUT_PULLUP`: Uses Arduino's built-in resistor to prevent floating pin values.
- `digitalRead()`: Detects whether a pin is HIGH or LOW.
- `Serial.print()` / `println()`: Sends text and numbers to your computer for debugging.
- Conditional `if/else`: Makes decisions based on sensor input.

## 🔧 Troubleshooting

| Symptom | Likely Fix |
| :--- | :--- |
| LED flickers randomly | Button pin is floating. Use `INPUT_PULLUP` or add an external 10kΩ resistor. |
| No output in Serial Monitor | Check baud rate is set to 9600. Ensure correct Port is selected. |
| LED on when button NOT pressed | Your logic is reversed. Swap `LOW` and `HIGH` in the `if` statement. |

## 🎯 What's Next?

Once you've mastered this, try modifying the sketch to:
- Make the button **toggle** the LED (press once to turn on, press again to turn off)
- Add a second button to control a different LED
- Send analog sensor data (potentiometer) to the Serial Plotter

## 📄 License
This project is open-source and available under the MIT License. Feel free to use, modify, and learn from it.

---

*Built as part of an Arduino learning journey. Happy tinkering!*