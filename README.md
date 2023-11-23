# Solar-powerObjectives :

Real-Time Monitoring: Objective: Provide real-time visibility into the performance of solar panels and the overall solar power system. Benefits: Enables immediate detection of issues, optimization of energy production, and timely decision-making. 
• Fault Detection and Diagnostics: Objective: Detect and diagnose faults or anomalies in the solar power system. Benefits: Reduces downtime by allowing prompt identification and resolution of issues, improving overall system reliability. • Dust or Soiling Sensors: Optical sensors that can detect the amount of dust or soiling on the surface of the solar panels. • Remote Monitoring and Control: Remote Access: Enable remote monitoring and control of solar energy systems, allowing operators to manage and optimize performance from anywhere.
• Alerts and Notifications: Provide automated alerts and notifications for system issues or deviations from expected performance, facilitating timely response. • User Interface: Provide a user-friendly interface for system operators and end-users to monitor and understand the performance of the solar energy system.

FEATURES:-

• The ESP32 typically comes with a dual-core processor, allowing for efficient multitasking and performance.

• Integrated Wi-Fi module enables wireless communication, making it suitable for IoT (Internet of Things) applications.

• The ESP32 is designed to operate with low power consumption, making it suitable for battery-powered devices and applications where power efficiency is crucial.

• Supports various Wi-Fi protocols (802.11 b/g/n) for wireless communication and Bluetooth protocols for short-range communication.

• Specifies the range of voltages that the sensor can accurately measure. It's important to choose a module that suits the voltage levels you expect in your application.

• Specifies the range of current levels that the sensor can accurately measure. It's important to choose a sensor that suits the current levels expected in your application.

• Servo motors are known for their precise positional control. They can maintain and control their position accurately.

• Specifies the range of particle sizes that the sensor can detect. Dust sensors may be optimized for specific particle size ranges, such as PM1, PM2.5, or PM10.

• Indicates how closely the sensor's measurements correspond to the actual particle concentrations. Accuracy is often given as a percentage.

• The primary feature of a photoresistor is its ability to change resistance in response to changes in illumination. As light intensity increases, the resistance decreases, and vice versa.

• The primary feature of an LDR is its ability to change resistance based on the intensity of incident light. As the light intensity increases, the resistance decreases, and vice versa.

• Relays have different contact configurations, including normally open (NO), normally closed (NC), and changeover (CO) or double-throw contacts. These configurations determine how the relay behaves in its normal state and when activated.

MIND MAP :-

![WhatsApp Image 2023-11-17 at 11 19 58_d0ef5a5e](https://github.com/KavyaGC1/Solar-power/assets/149661780/c895346b-fab0-43f5-bca1-2a5760c12453)

WORKING :-

A solar power monitoring system is designed to efficiently track and manage the performance of a solar power installation. The system employs advanced technologies, including real-time monitoring through the integration of Blynk IoT and ESP32 microcontroller. ESP32, a powerful and versatile microcontroller, serves as the brain of the system. It interfaces with the solar panels, inverters, and other relevant components to collect data on parameters such as solar irradiance, temperature, voltage, and current.

The Blynk IoT platform acts as the bridge between the ESP32 and the user interface, enabling real-time visualization and control. Through the Blynk mobile app or web interface, users can monitor the solar power system remotely and receive instant updates on its performance. The system allows users to track energy production, identify potential issues, and optimize the efficiency of the solar installation.

Real-time monitoring is crucial for identifying fluctuations in energy production, detecting faults or malfunctions promptly, and ensuring optimal energy utilization. The ESP32 continuously gathers data from various sensors deployed in the solar power system and transmits this information to the Blynk cloud server. Users can access this data in a user-friendly interface, where customizable widgets display relevant metrics, charts, and graphs.

The integration of Blynk IoT with ESP32 not only enhances real-time monitoring capabilities but also enables remote control and automation features. Users can remotely adjust parameters, such as tilt angles of solar panels or turn on/off specific components, to optimize energy generation based on prevailing conditions. Additionally, the system can send alerts and notifications in case of anomalies, ensuring a proactive approach to maintenance and troubleshooting.

In conclusion, the solar power monitoring system with real-time monitoring using Blynk IoT and ESP32 is a sophisticated solution that empowers users to make informed decisions, maximize energy efficiency, and ensure the longevity of their solar power installations. Through seamless integration and intuitive interfaces, this system contributes to the advancement of sustainable energy practices by providing a comprehensive and user-friendly approach to solar power management.


FLOW CHART:-


![WhatsApp Image 2023-11-17 at 11 00 44_de08fcf4](https://github.com/KavyaGC1/Solar-power/assets/149661780/20ced412-dfeb-40ea-b96f-570c4197233d)
ALGORITHM:-

![ALGO SOLAR](https://github.com/KavyaGC1/Solar-power/assets/149661780/c3aed5fd-3714-4734-a8bc-828032ca718a)

CIRCUIT BLOCK DIAGRAM:-

![SOLAR CIRCUIT](https://github.com/KavyaGC1/Solar-power/assets/149661780/685a96c7-acd5-44d6-a85f-285948ae3659)

CODE : -

#include "BlynkEdgent.h" #include <Deneyap_Servo.h> int ldr1 = A0; int ldr2 = A1; int pos; int voltage1 = 12; int voltage2 = 11; Servo myservo;

void servo_ldr() { int ldr1_read = analogRead(ldr1); int ldr2_read = analogRead(ldr2); Serial.print("light1 = "); Serial.println(ldr1_read); Serial.print("light2 = "); Serial.println(ldr2_read); int map1 = map(ldr1_read,0,8191,52,0); int map2 = map(ldr2_read,0,8191,53,105); if(ldr1_read>=ldr2_read) { myservo.write(map1); delay(30); } else { myservo.write(map2); delay(30); } } /*BLYNK_WRITE(V0) { int pinValue = param.asInt(); digitalWrite(42,pinValue);

} BLYNK_WRITE(V1) { int pinValue = param.asInt(); digitalWrite(5,pinValue);

} BLYNK_WRITE(V2) { int pinValue = param.asInt(); digitalWrite(6,pinValue);

}*/

void setup() { WiFi.begin(ssid,pass); pinMode(ldr1,INPUT); pinMode(ldr2,INPUT); pinMode(voltage1,INPUT); pinMode(voltage2,INPUT); Serial.begin(9600); myservo.attach(9); delay(100);

BlynkEdgent.begin(); }

void loop() { for(i=0;i<50;i++) { servo_ldr(); float volt1 = analogRead(voltage1);

float volt2 = analogRead(voltage2);

float vout_solar = (volt1/15500)*25; float vout_battery = (volt2/15500)*25;

Serial.print("solar voltage = "); Serial.println(vout_solar); Serial.print("battery voltage = "); Serial.println(vout_battery);

float map_volt1 = map(vout_battery,3.3,4.2,0,100);

Blynk.virtualWrite(V0, vout_solar); Blynk.virtualWrite(V1,vout_battery); Blynk.virtualWrite(V2, mapping);

//Blynk.virtualWrite(V4, millis() / 1000); delay(2000); BlynkEdgent.run(); } }

![pro1](https://github.com/KavyaGC1/Solar-power/assets/149661780/545311b2-428c-48a6-b673-1011a95bbc4e)

![pro2](https://github.com/KavyaGC1/Solar-power/assets/149661780/3bfce0ea-cce2-4e22-b029-6aec68920515)

![pro3](https://github.com/KavyaGC1/Solar-power/assets/149661780/836e41df-e0e5-451b-ad40-60ce66999ffd)

https://user-images.githubusercontent.com/109717277/285266649-081893ee-a9f6-4c46-a034-cc75fde29293.mp4

