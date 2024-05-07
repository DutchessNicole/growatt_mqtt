# Growatt Solar Inverter parameters to MQTT topics
Currently functional on a Growatt MIC 1500TL-X inverter and MOD 9000TL3-X

**Hardware:**
- Wemos D1 mini (ESP-8266EX)
- UART 3.3v TTL to RS485 Converter
- Some wires and solder
- TX/Rx configuration is 13/12 (can be configured in the SoftwareSerial pin definition (SS_RX and SS_TX))
- Most inverters provide 5v on the USB port when the inverter is online. If that does not work, 12v power supply from the inverter can be used, else you need an external power supply.

![Proto stage](/Images/Growatt_inverter.jpeg?raw=true)


**Working registers:**

- Inverter status (0 idle, 1 production, 3 error)
- Actual PV power (Watt) 
- PV Voltage (V)
- AC variables (V, I, P) 
- Energy generated daily and total (kWh)

**Register read updates 06-02-2024**

Added 2nd and 3rd phase Voltage & power registers  (comment out if you have a single phase inverter)
Changed PV and AC total power register
Added 2nd string registers (comment out if you have a single phase inverter)
Removed current registers
Minor tidying up

**MQTT updates 20-11-2021:**

Changed MQTT_LOGTOPIC to MQTT_LOG_TOPIC
Added LWT topic to gracefully handle the end of the production day.

The topic structure is moved from the code to secrets.h
If you are updating an existing configuration, make sure to define the complete topic structure in the MQTT_TOPIC_BASE and MQTT_LWT_TOPIC

For example:

#define MQTT_TOPIC_BASE "solar";

#define MQTT_LOG_TOPIC "solar/log";

#define MQTT_LWT_TOPIC "solar/LWT";

**Home assistant custom sensor:**

Adapt the state_topic of both sensors to match your MQTT_TOPIC_BASE configuration.

Paste into the configuration.yaml

	mqtt:
		sensor:
 			- name: "Solar PvP"  
				state_topic: "solar/PacT"
   				state_class: "measurement"
   				unit_of_measurement: "W"
   	 			device_class: "power"
			- name: "Solar1 Eactotal"
  				state_topic: "solar/Eactotal"
				state_class: "total"
   				unit_of_measurement: "kWh"
   				device_class: "energy"
   

## References
Code structure based on: https://github.com/LukasdeBoer/esp8266-whr930-mqtt
