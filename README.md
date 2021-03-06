# LG Thinq MQTT Proxy

This application can connect to LG Thinq infrastructure and register for the updates coming from smart LG devices. Received messages are converted into JSON payload and sent to your private MQTT server. This way you can enhance your home automation (like OpenHab or HomeAssistant) thanks to received notifications from your fridge or washing machine.

## Credits

This application is based on the code written by `dcmeglio` at https://github.com/dcmeglio/hubitat-thinq .
He made a great job by finding all the details necessary to connect to the LG's MQTT servers and register for the messages coming from the LG's appliances.

I have asked him if he doesn't have any objection with adaptation of his work and renaming the project to “Thinq MQTT Proxy”. 
His answer was
> No objections at all. Good luck!


My goal was to keep the code as close to the original one, to make any updates with upstream easier.
I have implemented a thin layer which is providing necessary infrastructure for this code to work as standalone application.

## Prerequisites

1. Java 8
1. Apache Maven 3.6.3

## Building

```shell
mvn clean package
```

## First run

Copy `state-example.json` to `state.json` and correct your language, region and local MQTT server settings.

```
java -jar ./target/thinq-mqtt-proxy.jar init
```

## Running

### For the first time

Check if application works correctly when running it from command line
```shell
java -jar ./target/thinq-mqtt-proxy.jar run
```

### As a service

If previous step was successful, run 
```shell
sudo ./install.sh
```

It should create and start `thinq-mqtt-proxy` service. You can verify if works correctly by inspecting `thinq-mqtt-proxy.log` or by issuing command
```shell
sudo systemctl status thinq-mqtt-proxy.service
```

## Items to do

1. [x] MQTT reconnects
1. [ ] Error handling   
1. [x] Easier setup
1. [x] Better format of the messages after conversion
1. [x] Provide documentation on how to run it as service
1. [x] Friendly names for the MQTT topic (i.e. `washer` instead of long id string) 
  
   Instead of using cryptic uuid of the device as the topic name, by default is it generated from the device type in lower case (ie. "refrigerator"). 
   This name is persisted into the configuration file and can be modified if different name is needed.
1. [ ] Code cleanup and hardening
1. [ ] Tests
1. [x] Better logging

## Disclaimer

* As I have only `v2` devices, I have not corrected the code to handle `v1` ones. Original code is written to handle them, so adding support should be doable.
* I have tested only washer and fridge, because I don't have more Thinq enabled devices. There might be some fixes necessary for other devices.
* This application is a hobby project for other hobbyists, provided as-is. I am not responsible for any issues caused by its use.

## Discussion

https://community.openhab.org/t/lg-smart-thinq/38818