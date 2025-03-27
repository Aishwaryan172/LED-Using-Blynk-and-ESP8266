# IoT LED Control Using Blynk and ESP8266

## Introduction
This project demonstrates the power and versatility of the Internet of Things (IoT) by enabling remote control of an LED using the **Blynk platform** and an **ESP8266 Wi-Fi module**. With this project, you can toggle an LED on/off from anywhere in the world using a smartphone or any internet-connected device. It introduces key IoT concepts and explores Blynk's user-friendly interface for creating custom dashboards.

---

## Objectives
1. **Remote Control**: Control an LED from a smartphone or other devices over the internet.
2. **IoT Familiarization**: Understand how IoT devices communicate and exchange data.
3. **Explore Blynk**: Learn to use the Blynk platform for building IoT applications.
4. **Real-Time Feedback**: Monitor the LED's status through the Blynk app.
5. **Code Implementation**: Develop skills in programming ESP8266 using Arduino IDE.
6. **Troubleshooting**: Gain hands-on experience solving hardware and software issues.

---

## Features
- Remote LED control using a smartphone.
- Real-time status updates of the LED.
- Customizable interface via the Blynk app.
- Compact and cost-effective IoT solution.

---

## Hardware Components
- **NodeMCU (ESP8266)**: The main microcontroller with built-in Wi-Fi capabilities.
- **LED**: The indicator controlled remotely.
- **Jumper Wires**: Connect the components on the breadboard.
- **Breadboard**: For prototyping the circuit.
- **Connecting cable**: Connecting cables are used to supply VCC (power) and GND (ground).

---

## Software Components
1. **Arduino IDE**: For writing and uploading code to the ESP8266.
2. **ESP8266 Library**: To enable programming the NodeMCU in Arduino IDE.
3. **Blynk App**: To create a user-friendly interface for controlling the LED.

---

## Circuit Diagram
![Circuit Diagram](https://github.com/Aishwaryan172/LED-Using-Blynk-and-ESP8266/blob/main/Circuit%20Diagram(LED)..png)
*Fig 1: Circuit diagram for LED control using ESP8266*

---

## Setup Instructions
### Prerequisites
- Install [Arduino IDE](https://www.arduino.cc/en/software).
- Download and install the **ESP8266** library in Arduino IDE.
- Install the Blynk app on your smartphone (available on [Android](https://play.google.com) and [iOS](https://apps.apple.com)).

### Steps
1. **Hardware Setup**:
   - Connect the LED to the NodeMCU as per the circuit diagram.
   - LED Positive (Anode) → D4 (GPIO2) on NodeMCU
   - LED Negative (Cathode) → GND on NodeMCU
   - connecting cable is connected to cpu and node mcu
   - Use a suitable resistor with the LED to prevent damage.
   
2. **Blynk Configuration**:
   # 🚀 Blynk LED Control with NodeMCU (ESP8266)

   Follow these steps to control an LED using Blynk and a NodeMCU (ESP8266).

   ## 🌐 Step 1: Setup Blynk.Cloud
   1. Go to [Blynk Cloud](https://blynk.cloud) and register.
   2. Login and create a new template.
   3. Enter a template name (e.g., "Control LED").
   4. Select your device: **ESP8266**.
   5. Choose connection type: **Wi-Fi** and click **Done**.
   6. Go to **Datastreams** and select **Digital**.
   7. Enter a name, select pin as **2 (D4)**, and click **Create**.
   8. Go to **Web Dashboard**, add a **Switch Widget**, and link it to the datastream.
   9. Click **Save** and then **Save** again.
   10. Go to **Search Page → Add a New Device → From Template**.
   11. Enter the template name and click **Create**.
   12. Copy the **Template ID** and **Auth Token**.

   ## 📱 Step 2: Install & Configure Blynk Mobile App
   1. Download and install the **Blynk App** from the Play Store/App Store.
   2. Login using the same credentials as Blynk Cloud.
   3. Select your **"Control LED"** template.
   4. Click on **Setup Dashboard** → Add **Button Widget**.
   5. Enter a name for the button, link it to the datastream, and set mode to **Switch**.

   ## 💻 Step 3: Upload Code to NodeMCU (ESP8266)

   ### 1️⃣ Install Required Libraries
   - Open **Arduino IDE**.
   - Go to **Sketch → Include Library → Manage Libraries**.
   - Search for and install:
     - **Blynk** by Volodymyr Shymanskyy
     - **ESP8266WiFi**

   ### 2️⃣ Upload This Code to ESP8266
   ```cpp
   #define BLYNK_PRINT Serial
   #include <ESP8266WiFi.h>
   #include <BlynkSimpleEsp8266.h>
   
   #define relay1 D0
   #define relay2 D1
   
   char auth[] = "Your_Blynk_Auth_Token"; // Replace with your Auth Token
   char ssid[] = "Your_SSID";             // Replace with your Wi-Fi name
   char pass[] = "Your_Password";         // Replace with your Wi-Fi password
   
   BLYNK_WRITE(V0) {
     bool value1 = param.asInt();
     digitalWrite(relay1, value1 ? LOW : HIGH);
   }
   
   BLYNK_WRITE(V1) {
     bool value2 = param.asInt();
     digitalWrite(relay2, value2 ? LOW : HIGH);
   }
   
   void setup() {
     pinMode(relay1, OUTPUT);
     pinMode(relay2, OUTPUT);
     digitalWrite(relay1, HIGH);
     digitalWrite(relay2, HIGH);
     Blynk.begin(auth, ssid, pass);
   }
   
   void loop() {
     Blynk.run();
   }

   ## 🚀 Step 4: Upload & Test
   1. Open **Arduino IDE**.
   2. Go to **Tools → Board** → Select **NodeMCU 1.0 (ESP-12E Module)**.
   3. Select the correct **Port** (e.g., COM3, COM4, etc.).
   4. Click the **Upload** button.
   5. Open **Serial Monitor** (115200 Baud Rate) to check for "Device is Online" message.
   6. Go to **Blynk Cloud** to confirm the device is online.
   7. Use the **Blynk App** to control the LED.
   
   ## 🎉 Success!
   Now you can turn your LED ON/OFF remotely using Blynk!




4. **Code**:
   - Open Arduino IDE.
   - Include the necessary libraries: `ESP8266WiFi.h` and `BlynkSimpleEsp8266.h`.
   - Replace the placeholder values in the code:
     - `ssid`: Your Wi-Fi name.
     - `pass`: Your Wi-Fi password.
     - `auth`: Your Blynk Auth Token.
   - Upload the code to your NodeMCU.

5. **Run the Project**:
   - Power the NodeMCU and connect it to Wi-Fi.
   - Open the Blynk app, and control the LED using the configured buttons.

---

## Code
Here’s the sample code used in this project:

```cpp
#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

#define relay1 D0
#define relay2 D1

char auth[] = "Your_Blynk_Auth_Token"; // Replace with your Auth Token
char ssid[] = "Your_SSID";             // Replace with your Wi-Fi name
char pass[] = "Your_Password";         // Replace with your Wi-Fi password

BLYNK_WRITE(V0) {
  bool value1 = param.asInt();
  digitalWrite(relay1, value1 ? LOW : HIGH);
}

BLYNK_WRITE(V1) {
  bool value2 = param.asInt();
  digitalWrite(relay2, value2 ? LOW : HIGH);
}

void setup() {
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);
  digitalWrite(relay1, HIGH);
  digitalWrite(relay2, HIGH);
  Blynk.begin(auth, ssid, pass);
}

void loop() {
  Blynk.run();
}

