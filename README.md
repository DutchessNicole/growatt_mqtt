# Growatt MQTT
Currently functional on a Growatt MIC 1500TL-X inverter 

Hardware:
- Wemos D1 mini (ESP-8266EX)
- UART 3.3v TTL to RS485 Converter
- Some wires and solder
- TX/Rx configuration is 13/12 (can be configured in the SoftwareSerial pin definition (SS_RX and SS_TX))

![Proto stage](/Images/Growatt_inverter.jpeg?raw=true)


Working registers:

- Inverter status (0 idle, 1 production, 3 error)
- Actual PV power (Watt) 
- PV Voltage (V)
- AC variables (V, I, P) 
- Energy generated daily and total (kWh)

MQTT updates 20-11-2021:

Changed MQTT_LOGTOPIC to MQTT_LOG_TOPIC
Added LWT topic to gracefully handle the end of the production day.

The topic structure is moved from the code to secrets.h
If you are updating an existing configuration, make sure to define the complete topic structure in the MQTT_TOPIC_BASE and MQTT_LWT_TOPIC

For example:

#define MQTT_TOPIC_BASE "domoticz/energy/pv1";

#define MQTT_LOG_TOPIC "log";

#define MQTT_LWT_TOPIC "domoticz/energy/pv1/LWT";

## References
Code structure based on: https://github.com/LukasdeBoer/esp8266-whr930-mqtt
