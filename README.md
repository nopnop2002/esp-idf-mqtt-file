# esp-idf-mqtt-file
ESP-IDF example for sending and receiving files using MQTT.   
I found [this](http://www.steves-internet-guide.com/send-file-mqtt/) article.   
It's great to be able to exchange files using MQTT.   
Since the python code was publicly available, I ported it to esp-idf.   

# Software requirements
ESP-IDF V4.4/V5.x.   
ESP-IDF V5.0 is required when using ESP32-C2.   
ESP-IDF V5.1 is required when using ESP32-C6.   

# Installation

```Shell
git clone https://github.com/nopnop2002/esp-idf-mqtt-file
cd esp-idf-mqtt-file
idf.py set-target {esp32/esp32s2/esp32s3/esp32c2/esp32c3/esp32c6}
idf.py menuconfig
idf.py flash
```

# Configuration   

![config-top](https://github.com/nopnop2002/esp-idf-mqtt-file/assets/6020549/aea9bf86-d953-4cd2-bbb6-0d75081ef4e8)
![config-app](https://github.com/nopnop2002/esp-idf-mqtt-file/assets/6020549/d39d17ec-e6be-462b-95fb-1d69256fd4f0)

## WiFi Setting
Set the information of your access point.   
![config-wifi](https://github.com/nopnop2002/esp-idf-mqtt-file/assets/6020549/16363fe8-728d-45a9-b106-56c806dee257)

## Broker Setting

MQTT broker is specified by one of the following.
- IP address   
 ```192.168.10.20```   
- mDNS host name   
 ```mqtt-broker.local```   
- Fully Qualified Domain Name   
 ```broker.emqx.io```

You can download the MQTT broker from [here](https://github.com/nopnop2002/esp-idf-mqtt-broker).   

![config-broker-1](https://github.com/nopnop2002/esp-idf-mqtt-file/assets/6020549/5a603ac6-44e2-4efc-a8c5-ce12e94eb684)

Specifies the username and password if the server requires a password when connecting.   
[Here's](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-the-mosquitto-mqtt-messaging-broker-on-debian-10) how to install and secure the Mosquitto MQTT messaging broker on Debian 10.   

![config-broker-2](https://github.com/nopnop2002/esp-idf-mqtt-file/assets/6020549/7d9708d0-0127-4b18-bc7d-fd4cce81a5bb)

# How to use   

Run the following python script on the host side.
```
$ python3 -m pip install paho-mqtt

$ vi mqtt-file.py
Set the broker you will use.

$ python3 mqtt-file.py
usage python3 mqtt-file.py put path_to_host
usage python3 mqtt-file.py get path_to_spiffs
usage python3 mqtt-file.py list
usage python3 mqtt-file.py delete path_to_spiffs
```

Example of use.   
```
# Put README.md to SPIFFS
$ python3 mqtt-file.py put README.md

# SPIFFS file list
$ python3 mqtt-file.py list

$ mv README.md README.md.md

# Get README.md from SPIFFS
$ python3 mqtt-file.py get README.md

# Compare two files
$ diff README.md README.md.md

# Delete README.md from SPIFFS
$ python3 mqtt-file.py delete README.md
```

