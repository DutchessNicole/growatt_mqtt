# Growatt MQTT
Currently functional on a Growatt MIC 1500TL-X inverter 

Hardware:
Wemos D1 
UART TTL to RS485 Converter (Works at 3.3v TTL)

Working registers:

Inverter status (0 idle, 1 active, 3 error)
Actual PV power (Watt) 
PV voltage 
AC variables (V, I, P) 
Energy generated daily and total

## References
Code structure based on: https://github.com/LukasdeBoer/esp8266-whr930-mqtt
