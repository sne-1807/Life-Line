# Life Line: Technology Integrated Rescue Gear

## Why Life Line?
- Life-Line is an advanced rescue gear system designed to assist citizens and streamline rescue effort for rescue teams during flood relief operations. 
- Built as an electronic upgrade to existing life jackets, the device enables real-time location tracking, hazard detection, and environmental monitoring.
- By integrating sensors to report real-time data to make accurate location based weather prediction using ML model, and LoRa communication to ensure communication without cellular network or WiFi.

## Tech Stack
### Microcontroller: 
- **ESP32**: Embedded board managing all operations
### Sensors:
- **GPS Module**: real-time location tracking for rescue coordination
- **DHT11 Sensor**: Monitors temperature and humidity, data of which will be sent to ML models in backend for weather prediction
- **BMP180 Sensor**: Measures air pressure, required for weather prediction ML model
- **Conductivity Sensor**: Can be inserted into water before entering to detect electric currents 
### Communication: 
- **LoRa Protocol**: offers long-range, lower-power wireless data transfer independent of cellular/WiFi/BT
### Power System:
- **Rechargeable batter with BMS**
### User Interfaces and Alerts:
- **OLED Display and Buzzer**: Displays/sounds notifications and alerts
- **LED Torch**
### Machine Learning Backend:
- Real-time data from IoT sensors sent to a cloud server
- ML model predicts imminent weather changes particular to the location of the jacket user and delivers actionable alerts to both victims and rescue teams

## Current Status/Prototype:
- As of now, the *GPS tracking* and *sensor integration (DHT11 and BMP180)* was done, with real-time data communication tested between two ESP32's communicating with LoRa communication protocol
-  Machine learning model created and tested separately


