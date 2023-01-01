# BIGTREETECH EBB36 v1.2 
## IMPORTANT INFORMATION
* **THE BOOT PIN IS PULLED HIGH DURING DFU MODE THIS PIN IS SHARED WITH THE HEATER AND WILL CAUSE YOUR HEATER TO HEAT - REMOVE 24V POWER WHEN ENTERING DFU MODE**
* **Before proceeding it is critical that your CAN network is configured for your printer, failure to setup the network will cause a problem when you try to connect devices. [Click here for installing the network.](can_network.md)**

## Installing CANboot
* Chip on EBB board
![image](https://user-images.githubusercontent.com/5571703/210181066-093cb59a-13f4-43e1-a7fb-6ce9342ede84.png)

### Generate CANBoot configuration and compile firmware
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

* Save configuration: Quit ```Q``` and Save Changes ```Y``` and exit.

3. Compile the firmware
```
make clean
make
```

![image](https://user-images.githubusercontent.com/5571703/210181767-25d94f9c-9fa8-422e-8ac5-367635dd05c8.png)

### Install the firmware to the board
1. Install jumper to following pins on the board (image have been copied from EBB36 manual from Bigthreetech repository, [link here](https://github.com/bigtreetech/EBB))
* The jumper will be needed that board can be powered with USB cable.
 
![image](https://user-images.githubusercontent.com/5571703/210182028-49adecd6-33d7-4e7c-9d56-28c77542c465.png)

2. Connect your EBB36 with Raspberry using USB cable.

3. Hold RESET and BOOT buttons on your board and release after a while.

4. Check that your board in DFU mode with command in Raspberry ```lsusb```

* Now you should see that board is in DFU mode and something like below should be listed (**Please not that ID might be different in your case!**)

```Bus 001 Device 005: ID 0483:df11 STMicroelectronics STM Device in DFU Mode```

5. Erase and install CANBoot firmware to the board. **Please not that you need to use correct ID which is shown to you in step 4!!!** In this example same ID have been used which is shown to me in step 4.

```sudo dfu-util -a 0 -D ~/CanBoot/out/canboot.bin --dfuse-address 0x08000000:force:mass-erase:leave -d 0483:df11```

![image](https://user-images.githubusercontent.com/5571703/210182509-e74b02b5-1b81-4bc0-80a8-e63da294e10b.png)

# If you haven't yet installed CAN network, this is time to do so.
* [ ] Check formatting for this reminder!

6. Remove USB cable from the board

7. Remove jumper from the board

8. Insert CANbus cable (4-pin)
* Please check couple of times that your cable pins that those are 

9. Power up your printer

10. Wait until your devices are up and running and check that you CAN network is up and you can see the devices
* [ ] commands and outcomes here!

[Next step: Install Klipper to EBB36]()
* [ ] Add page for this

### Troubleshoot
1. When installing the firmware, last information is ```dfu-util: Error during download get_status```, see picture below

![image](https://user-images.githubusercontent.com/5571703/210182451-2c7b4501-dd6b-4198-b02a-13cd018ca4a2.png)

**Solution:** If line before the error is shown ```File downloaded successfully```, this error can be ignored.

[Back to main site](README.md)
