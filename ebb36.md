## BIGTREETECH EBB36 v1.2 
### IMPORTANT INFORMATION
* **THE BOOT PIN IS PULLED HIGH DURING DFU MODE THIS PIN IS SHARED WITH THE HEATER AND WILL CAUSE YOUR HEATER TO HEAT - REMOVE 24V POWER WHEN ENTERING DFU MODE**
* **Before proceeding it is critical that your CAN network is configured for your printer, failure to setup the network will cause a problem when you try to connect devices. [Click here for installing the network.](can_network.md)**

### Installing CANboot
* Chip on EBB board
![image](https://user-images.githubusercontent.com/5571703/210181066-093cb59a-13f4-43e1-a7fb-6ce9342ede84.png)
1. Clone CANboot repository to your Raspberry and move to the directory
```
cd ~/
git clone https://github.com/Arksine/CanBoot
cd CanBoot
```
2. Configure Makefile
```
make menuconfig
```
* Select correct values for board with chip **STM32G0B1**
* Remember to enter same bus speed than you entered for U2C (network setup)!

![image](https://user-images.githubusercontent.com/5571703/210181316-fa95f903-4438-48a8-a8a1-6a1f32ddc0c9.png)

* [ ] How to choose correct communication interface?

[Back to main site](README.md)
