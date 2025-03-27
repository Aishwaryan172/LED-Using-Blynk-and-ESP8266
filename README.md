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
- **Resistor (220Ω - 330Ω)**: Prevents excessive current through the LED.
- **USB Cable**: Used to connect the NodeMCU to the computer for programming.
- **Power Supply**: 5V USB adapter or power bank (optional).

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
  
---

## Hardware Connection
1. **Connect the LED to NodeMCU**:
   - LED **Positive (Anode)** → **D4 (GPIO2)** on NodeMCU
   - LED **Negative (Cathode)** → **GND** on NodeMCU
   - **Resistor (220Ω - 330Ω)** in series with the LED anode.
2. **Connect NodeMCU to Power**:
   - Use a **USB cable** to connect NodeMCU to a computer for programming.
   - After programming, use a **5V USB adapter or power bank** to power it independently.

---

### Step 1: Setup Blynk Cloud
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

### Step 2: Install & Configure Blynk Mobile App
1. Download and install the **Blynk App** from the Play Store/App Store.
2. Login using the same credentials as Blynk Cloud.
3. Select your **"Control LED"** template.
4. Click on **Setup Dashboard** → Add **Button Widget**.
5. Enter a name for the button, link it to the datastream, and set mode to **Switch**.

### Step 3: Upload Code to NodeMCU
1. Open Arduino IDE.
2. Include the necessary libraries: `ESP8266WiFi.h` and `BlynkSimpleEsp8266.h`.
3. Replace the placeholder values in the code:
   - `ssid`: Your Wi-Fi name.
   - `pass`: Your Wi-Fi password.
   - `auth`: Your Blynk Auth Token.
4. Upload the code to your NodeMCU.

### Step 4: Run the Project
1. Power the NodeMCU and connect it to Wi-Fi.
2. Open the Blynk app and control the LED using the configured buttons.
3. Verify that the device is online in Blynk Cloud.

---

## Code
Here’s the sample code used in this project:

```cpp
#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

#define LED_PIN D4

char auth[] = "Your_Blynk_Auth_Token"; // Replace with your Auth Token
char ssid[] = "Your_SSID";             // Replace with your Wi-Fi name
char pass[] = "Your_Password";         // Replace with your Wi-Fi password

BLYNK_WRITE(V0) {
  int value = param.asInt();
  digitalWrite(LED_PIN, value);
}

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Blynk.begin(auth, ssid, pass);
}

void loop() {
  Blynk.run();
}
```

---

## 🚀 Success!
Now you can turn your LED ON/OFF remotely using Blynk!
