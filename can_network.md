## Setup for Pi
*  Add file and following text to it
```
sudo nano /etc/network/interfaces.d/can0
```
```
allow-hotplug can0
iface can0 can static
 bitrate 750000
 up ifconfig $IFACE txqueuelen 256
 pre-up ip link set can0 type can bitrate 750000
 pre-up ip link set can0 txqueuelen 256
```
*  Reboot Raspberry
```
sudo reboot
```
## Test network
* After reboot, enter following command for check status for CAN network
```
ip -s link show can0
```
* You will see status for you network and main thing should be that network is UP

![image](https://user-images.githubusercontent.com/5571703/210180595-0690bb0d-23ce-46ba-a845-174b16eb1bfb.png)

## Troubleshoot
* [ ] To be added when errors occurs
