# EXP 1(E) CLOUD-BASED DEVICE CONTROL USING MQTT AND WI-FI COMMUNICATION

## Aim

To control an electrical device remotely through a cloud platform using MQTT communication and a Wi-Fi module.

# Hardware / Software Tools Required

- Arduino UNO / ESP32 / ESP8266 Wi-Fi Module
- USB Cable
- PC/Laptop
- Arduino IDE
- Wi-Fi Network
- Relay Module
- LED / DC Load
- Breadboard
- Jumper Wires
- Cloud Platform such as Blynk or ThingSpeak
- MQTT Broker / MQTT Service



# Procedure

## Step 1: Assemble the Circuit

1. Place the microcontroller board, Wi-Fi module, relay module, LED/load, and breadboard on the workbench.
2. Connect the required power supply and GND connections.
3. Ensure that the Wi-Fi module and controller operate at their specified voltage levels.

## Step 2: Connect the Relay Module

1. Connect the **VCC** of the relay module to the appropriate power supply.
2. Connect the **GND** of the relay module to **GND**.
3. Connect the relay input pin to a suitable digital output pin of the controller.
4. Connect the LED or other low-voltage load through the relay contacts.
5. Do not connect mains voltage directly during laboratory testing unless the setup is specifically designed and supervised for it.

## Step 3: Configure Wi-Fi Communication

1. Connect the Wi-Fi-enabled controller to the required Wi-Fi network.
2. Enter the Wi-Fi SSID and password in the program.
3. Verify that the device obtains an IP address.
4. Confirm that the controller can establish an Internet connection.

## Step 4: Configure the Cloud / MQTT Platform

1. Create an account on the selected cloud platform such as **Blynk** or **ThingSpeak**, as applicable.
2. Configure the required device, virtual control, channel, or dashboard.
3. Configure the MQTT broker/server details.
4. Set the MQTT topic used for ON/OFF control.
5. Define the payload values, for example:
   - `ON` – Switch device ON
   - `OFF` – Switch device OFF

## Step 5: Write and Upload the Program

1. Open the Arduino IDE.
2. Include the required Wi-Fi and MQTT libraries.
3. Enter the Wi-Fi credentials and MQTT broker details.
4. Configure the relay output pin.
5. Establish a connection with the Wi-Fi network.
6. Establish a connection with the MQTT broker.
7. Subscribe to the required MQTT topic.
8. Write the callback function to process ON/OFF commands.
9. Verify the program using the **Verify** button.
10. Upload the program to the controller.

## Step 6: Execute the Program

1. Power ON the controller and Wi-Fi module.
2. Open the configured cloud dashboard or MQTT client.
3. Send an **ON** command through the configured MQTT topic.
4. Observe that the relay activates and the connected device turns ON.
5. Send an **OFF** command.
6. Observe that the relay deactivates and the connected device turns OFF.
7. Monitor the Serial Monitor to verify MQTT connection and received commands.

## Step 7: Verify the Output

1. Check whether the controller successfully connects to Wi-Fi.
2. Verify the MQTT broker connection.
3. Send an ON command from the cloud platform.
4. Observe the device switching ON.
5. Send an OFF command from the cloud platform.
6. Observe the device switching OFF.
7. Record the commands and corresponding device states.

# Program
```
#include <WiFi.h>
  #include <PubSubClient.h>

  const char* ssid = "Wokwi-GUEST";   // Wokwi default WiFi
  const char* password = "";          // No password
  const char* mqtt_server = "broker.hivemq.com"; // Public MQTT broker

  WiFiClient espClient;
  PubSubClient client(espClient);

  const int ledPin = 2;

  void setup_wifi() {
       delay(10);
 WiFi.begin(ssid, password);
 while (WiFi.status() != WL_CONNECTED) {
delay(500);
 }
  }

  void callback(char* topic, byte* payload, unsigned int length) {
 if (payload[0] == '1') {
digitalWrite(ledPin, HIGH); // Turn LED ON
    } else {
digitalWrite(ledPin, LOW);  // Turn LED OFF
    }
  }

  void reconnect() {
     while (!client.connected()) {
      if (client.connect("ESP32Client")) {
        client.subscribe("iot/device/control"); // Subscribe to topic
      } else {
        delay(5000);
      }
          }
  }

  void setup() {
    pinMode(ledPin, OUTPUT);
       setup_wifi();
    client.setServer(mqtt_server, 1883);
    client.setCallback(callback);
  }

  void loop() {
    if (!client.connected()) {
      reconnect();
 }
    client.loop();
     }
```


> **Note:** The above program is written for an **ESP32** using the `WiFi.h` library. Replace the Wi-Fi credentials, MQTT broker address, and MQTT topic with the values used in the laboratory setup.

# Observation

<img width="1535" height="733" alt="image" src="https://github.com/user-attachments/assets/23442659-31d9-4bfb-b0f9-aadd2153424b" />
<img width="731" height="1600" alt="WhatsApp Image 2026-09-26 at 10 44 37 AM" src="https://github.com/user-attachments/assets/09baeb3b-d112-4319-9186-4e7713e2df0d" />

# Result

The **cloud-based device control system was successfully implemented using MQTT and Wi-Fi communication**. The device was remotely controlled by sending ON/OFF commands through the MQTT communication channel. The experiment demonstrated the use of **IoT cloud connectivity, MQTT messaging, Wi-Fi communication, and remote device control**.
