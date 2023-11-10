# Raspberry-Pi-4

- Install the Raspberry Pi Imager using Synaptic.
- Write the image to a microSD card - using a 64-bit Raspberry Pi OS lite image and include Wi-Fi and SSH settings.
- Connect using a cable, using ```ssh pi@raspberrypi.local``` and the SSH password set when creating the microSD card.
- ```sudo apt update``` and ```sudo apt full-upgrade``` to check for updates.
- To set the fan temperature, ```sudo raspi-config```, select ```performance``` and ```P3 Fan```.  Set the GPIO to 14 and the temperature to 80.  (https://www.raspberrypi.com/products/raspberry-pi-4-case-fan/)
- To set the Wi-Fi:
    ```nmcli dev wifi list``` to list networks
    ```sudo nmcli --ask dev wifi connect <example_ssid>``` to connect to a SSID
- To add a USB stick and automount it:

    ```sudo blkid``` to get the UUID.
  
    ```sudo mkdir /media/myUSB``` to create a mount point.
  
    ```sudo nano /etc/fstab``` and add the line ```UUID=[UUID of USB drive] /media/myUSB vfat uid=pi,gid=pi 0 2```

  Save and reboot Raspberry PI.  Running ```df -H``` should show the USB stick automounted.

- To install Microk8s:
  - ```sudo apt update``` and ```sudo apt install snapd```
  - ```sudo nano /boot/firmware/cmdline.txt``` and set the text to ```cgroup_enable=memory cgroup_memory=1 net.ifnames=0 dwc_otg.lpm_enable=0 console=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait```
  - ```sudo reboot```
  - ```sudo snap install microk8s --classic --channel=1.25```  (does it need --channel=1.25??)
  - ```grep mem /proc/cgroups | awk '{ print $4 }'``` should return ```1```
  - ```microk8s status --wait-ready``` should show that MicroK8s is ready.

- To install Docker:
  - ```curl -sSL get.docker.com | sh && sudo usermod pi -aG docker```
  
- To install Kubernetes dashboard:
  - ```sudo snap install kubectl --classic```
  - On laptop ```ssh -L 8001:localhost:8001 pi@raspberrypi.local```
  - On Raspberry Pi ```microk8s.kubectl proxy --accept-hosts=.\* --address=0.0.0.0```
  - On laptop http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#/login
  - On Raspberry Pi ```token=$(microk8s.kubectl -n kube-system get secret | grep default-token | cut -d " " -f1) microk8s.kubectl -n kube-system describe secret $token```
  - Copy and paste the token from the terminal into the prompt in Fx.

- To find the operating temperature:
  - ```sudo vcgencmd measure_temp```


- https://www.raspberrypi.com/documentation/computers/configuration.html#set-up-a-headless-raspberry-pi
- https://peppe8o.com/automount-usb-storage-with-raspberry-pi-os-lite-fstab-and-autofs/
- https://zenlot.medium.com/raspberry-pi-4-and-micro8ks-setup-4bc5ee6eb7d7
- https://gist.github.com/felipecruz91/e2414cd1ba76d71739cf0fc8302109da
- https://www.cyberciti.biz/faq/linux-find-out-raspberry-pi-gpu-and-arm-cpu-temperature-command/
