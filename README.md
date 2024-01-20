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


## WiFi Setting
Set the information of your access point.
![config-wifi](https://github.com/nopnop2002/esp-idf-adc2mqtt/assets/6020549/2774c6c5-1c9b-468f-9116-4c146fb0cd77)


## Broker Setting

## Broker Setting

MQTT broker is specified by one of the following.
- IP address   
 ```192.168.10.20```   
- mDNS host name   
 ```mqtt-broker.local```   
- Fully Qualified Domain Name   
 ```broker.emqx.io```

You can download the MQTT broker from [here](https://github.com/nopnop2002/esp-idf-mqtt-broker).   

![config-broker-1](https://github.com/nopnop2002/esp-idf-adc2mqtt/assets/6020549/6c356b93-c032-4c50-8965-dc31a78bcfcc)

Specifies the username and password if the server requires a password when connecting.   
[Here's](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-the-mosquitto-mqtt-messaging-broker-on-debian-10) how to install and secure the Mosquitto MQTT messaging broker on Debian 10.   

![config-broker-2](https://github.com/nopnop2002/esp-idf-adc2mqtt/assets/6020549/14d93639-4132-43b7-8a20-c68fd17179d1)


# How to use   

Run the following python script on the host side.
```
$ python3 mqtt-file.py
usage python3 mqtt-file.py put path_to_host
usage python3 mqtt-file.py get path_to_spiffs
usage python3 mqtt-file.py list
usage python3 mqtt-file.py delete path_to_spiffs
```

Example of use.   
```
$ python3 mqtt-file.py put README.md
$ python3 mqtt-file.py list
$ mv README.md README.md.md
$ python3 mqtt-file.py get README.md
$ diff README.md README.md.md
$ python3 mqtt-file.py delete README.md
```

