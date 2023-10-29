# Raspberry-Pi-4

- Install the Raspberry Pi Imager using Synaptic.
- Write the image to microSD card - using 64-bit Raspberry Pi OS lite image and include Wi-Fi and SSH settings.
- Connect using a cable, using ```ssh pi@raspberrypi.local``` and the SSH password set when creating the microSD card.
- ```sudo apt update``` and ```sudo apt full-upgrade``` to check for updates.
- To set the fan temperature, ```sudo raspi-config```, select ```performance``` and ```P3 Fan```.  Set the GPIO to 14 and the temperature to 80.  (https://www.raspberrypi.com/products/raspberry-pi-4-case-fan/)
- To set the Wi-Fi:
    ```nmcli dev wifi list``` to list networks
    ```sudo nmcli --ask dev wifi connect <example_ssid>``` to connect to a SSID

- https://www.raspberrypi.com/documentation/computers/configuration.html#set-up-a-headless-raspberry-pi
