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
   - first go to the blyn.cloud website and register to website and login
   - go to the templete page click on new template button and enter any name also select your device name (ESP8266)
   - select connection type it is WI-FI and click done
   - then go to datastreams and select digital give name select pin as 2 then click create
   - then go to web dashboard drag and drop the switch widget then go to settings select datastream and click save and again click save
   - then go to the search page select add a new device and select from template and entire template name then click criate
   - now we will get template id and authotication taken copy that one and paste in our program
   - then go to tools select board as node mcu and select port click arrow button run the program
   - then go to wesit now the device shows is online
   - Create a new project in the Blynk app.
   - Add a button widget and link it to **Virtual Pins V0** and **V1**.
   - Obtain the **Auth Token** for the project.

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

