# Raspberry-Pi-4

- Write the image to microSD card - used 64-bit Raspberry Pi OS lite image
- Use the Raspberry Pi Imager (install using Synaptic)
- Remember to add WiFi and SSH settings

- To access the Raspberry Pi, ```ssh pi@raspberrypi.local``` and use the SSH password set when creating the microSD card.
- To set the temperature for the fan, ```sudo nano /boot/config.txt``` and add ```dtoverlay=gpio-fan,gpiopin=18,temp=80000``` at the end of the file.  80000 is 80*C, the point at which the processor will throttle if too warm.
- https://www.raspberrypi.com/documentation/computers/configuration.html#set-up-a-headless-raspberry-pi
