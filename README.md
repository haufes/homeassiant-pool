# Home Assistant config for pool control

This repository contains the config files for my Home Assiant installation as well as the wiring and part details. 

## Features 
- Control the weekday schedual of the pool pump and heat pump via the UI (Hydro off peak hours)
- Control whether the pump and heat pump are following their scheduals or on manual control
- Monitor the temperature of the water and air
- Monitor the water presure at the filter
- Warn if the pump is running, but there is no water presure
- Monitor if the heat pump is running based on temperature increase of the water


![UI](https://lh3.googleusercontent.com/bh4MtPjBncF-adeGD4bfPDaWAAlPDlH3qpJCK8XQa2-XUYUpdRn6QAPsC8mUuM3jmWnTPGO2fbyvdCzQvwz3KISJVSdbpSBATFoEVtHP5atw4mNS3kBz0JXPJb_2VblFy4hK2IadFxCQJflW3N6unxs2x7CwSqPSjAIPp0F1gqPCSJSB1n4EnE7XgXxm4h2QoROAwF0hNys0OF3jeCqSwJC6GTA1SHHZUlRkXr9W2J2DDJBsFBJkX5HUdZQIwfip6i_jPsxvlk8UYJlDNrdWkMLwp_1Qko6PnaSOgzS-HSEtnD4_YWmQ4B4BLCf9dTQr4UIKz7rPhmvoJQUtbBECPtc5Pkqp0Y-GN_6iRADbIvgvz9V6ksumIJUrDllPbwffkOgbCbjWadHaGJUslLbX72cWxMaQ9FIbURfcB3PvXY2gM29Y3RW0kWSkM5-r3SRWjCda4VrQxV4a30kKRW9KtEZ-eodmGDrUZ7r5Qo9JzmBKZxRP0ZkLOgYJnXYU64rUvFRk8CVtsGe1KRg9997Ty1K5wNOl370_5GiWKVT6eib1MlGREAPXpVgmruYFf0bqpnEuJECMMA5RG1eBB_8e3B2_KSYqH05xL2DjZyTnYh2zYf4P4qOT-vYoGad-cS0uhnkRAqeGeQQLHCTpn6uvFdzTxQGJoSeIpnbKxvR-VFLF5_mBTdjQgOc4-BRwHLxAGBZWDtwD3ZeAMz_f_kxKETpG=w886-h625-no)


Changed from a MCP3008 to MCP3304 to get a better resolution of the pressure sensor.

## Hardware
 - [Raspberry Pi 3](https://www.amazon.ca/gp/product/B01CCF9BYG/ref=oh_aui_detailpage_o09_s00?ie=UTF8&psc=1)
 - [8 Channel DC 5V Relay](https://www.amazon.ca/gp/product/B06XCN5JNH/ref=oh_aui_detailpage_o09_s00?ie=UTF8&psc=1)
 - [Waterproof Digital Temperature Temp Sensor Probe DS18b20](https://www.amazon.ca/gp/product/B00KUNKR3M/ref=oh_aui_detailpage_o06_s00?ie=UTF8&psc=1)
 - [Pressure Transducer Sensor](https://www.amazon.ca/gp/product/B01HZ3ZZOA/ref=oh_aui_detailpage_o05_s00?ie=UTF8&psc=1)
 - ~~[MCP3008](https://www.arrow.com/en/products/mcp3008-isl/microchip-technology)~~
 - [MCP3304](https://www.arrow.com/en/products/mcp3304-cip/microchip-technology) Better resolution than the MCP3008
 

 ## Wiring diagram
 Replace MCP3008 with MCP3304
 ![Wiring diagram](https://raw.githubusercontent.com/haufes/home-assistant-pool/master/project_resorces/Pool%20Controler_schem.png)
 
 ## References
 - [Multiple DS18B20 temperature sensors - Raspberry Pi Forums](https://www.raspberrypi.org/forums/viewtopic.php?t=167896)
 - [Reading from a MCP3002 analog-to-digital converter](http://raspberry.io/projects/view/reading-from-a-mcp3002-analog-to-digital-converter/)
 - [Python code to use the MCP3008 analog to digital converter with a Raspberry Pi or BeagleBone black.](https://github.com/adafruit/Adafruit_Python_MCP3008)
 - [Raspberry Pi Analog Water Sensor Tutorial | Rototron](https://www.rototron.info/raspberry-pi-analog-water-sensor-tutorial/)
 - [Install docker] (https://howchoo.com/g/nmrlzmq1ymn/how-to-install-docker-on-your-raspberry-pi)
## Install

Install the docker home assistant container

sudo docker run --restart always --init -d --name="homeassistant" --cap-add ALL -v /lib/modules:/lib/modules -v /sys:/sys --device /dev/ttyAMA0:/dev/ttyAMA0 --device /dev/mem:/dev/mem --privileged -v /home/pi/homeassiant-pool:/config -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/raspberrypi3-homeassistant

Install gpiozero into the container
sudo docker exec -it homeassistant pip install gpiozero

run in container
sudo docker exec -it homeassistant /bin/bash

restart
sudo docker restart homeassistant


Clone this repo into it's config folder. /home/homeassistant/docker

Add a secrets.yaml file after cloning. Contains the login and email details for gmail and recipients
