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
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blynk LED Control with NodeMCU</title>
    <style>
        body { font-family: Arial, sans-serif; line-height: 1.6; margin: 20px; }
        code { background: #f4f4f4; padding: 5px; display: block; }
        pre { background: #f4f4f4; padding: 10px; }
    </style>
</head>
<body>
    <h1>🚀 Blynk LED Control with NodeMCU (ESP8266)</h1>
    <p>Follow these steps to control an LED using Blynk and a NodeMCU (ESP8266).</p>

    <h2>🌐 Step 1: Setup Blynk.Cloud</h2>
    <ol>
        <li>Go to <a href="https://blynk.cloud" target="_blank">Blynk Cloud</a> and register.</li>
        <li>Login and create a new template.</li>
        <li>Enter a template name (e.g., "Control LED").</li>
        <li>Select your device: <strong>ESP8266</strong>.</li>
        <li>Choose connection type: <strong>Wi-Fi</strong> and click <strong>Done</strong>.</li>
        <li>Go to <strong>Datastreams</strong> and select <strong>Digital</strong>.</li>
        <li>Enter a name, select pin as <strong>2 (D4)</strong>, and click <strong>Create</strong>.</li>
        <li>Go to <strong>Web Dashboard</strong>, add a <strong>Switch Widget</strong>, and link it to the datastream.</li>
        <li>Click <strong>Save</strong> and then <strong>Save</strong> again.</li>
        <li>Go to <strong>Search Page → Add a New Device → From Template</strong>.</li>
        <li>Enter the template name and click <strong>Create</strong>.</li>
        <li>Copy the <strong>Template ID</strong> and <strong>Auth Token</strong>.</li>
    </ol>

    <h2>📱 Step 2: Install & Configure Blynk Mobile App</h2>
    <ol>
        <li>Download and install the <strong>Blynk App</strong> from the Play Store/App Store.</li>
        <li>Login using the same credentials as Blynk Cloud.</li>
        <li>Select your <strong>"Control LED"</strong> template.</li>
        <li>Click on <strong>Setup Dashboard</strong> → Add <strong>Button Widget</strong>.</li>
        <li>Enter a name for the button, link it to the datastream, and set mode to <strong>Switch</strong>.</li>
    </ol>

    <h2>💻 Step 3: Upload Code to NodeMCU (ESP8266)</h2>
    <h3>1️⃣ Install Required Libraries</h3>
    <ul>
        <li>Open <strong>Arduino IDE</strong>.</li>
        <li>Go to <strong>Sketch → Include Library → Manage Libraries</strong>.</li>
        <li>Search for and install:
            <ul>
                <li><strong>Blynk</strong> by Volodymyr Shymanskyy</li>
                <li><strong>ESP8266WiFi</strong></li>
            </ul>
        </li>
    </ul>

    <h3>2️⃣ Upload This Code to ESP8266</h3>
    <pre><code>
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
    </code></pre>

    <h2>🚀 Step 4: Upload & Test</h2>
    <ol>
        <li>Open <strong>Arduino IDE</strong>.</li>
        <li>Go to <strong>Tools → Board</strong> → Select <strong>NodeMCU 1.0 (ESP-12E Module)</strong>.</li>
        <li>Select the correct <strong>Port</strong> (e.g., COM3, COM4, etc.).</li>
        <li>Click the <strong>Upload</strong> button.</li>
        <li>Open <strong>Serial Monitor</strong> (115200 Baud Rate) to check for "Device is Online" message.</li>
        <li>Go to <strong>Blynk Cloud</strong> to confirm the device is online.</li>
        <li>Use the <strong>Blynk App</strong> to control the LED.</li>
    </ol>

    <h2>🎉 Success!</h2>
    <p>Now you can turn your LED ON/OFF remotely using Blynk!</p>
</body>
</html>


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

