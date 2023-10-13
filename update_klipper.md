## Sections
* [Updating MCU](https://github.com/pannuhuone/Voron-CANBus/blob/main/update_klipper.md#updating-mcu)
* [Updating Klipper on EBB36](https://github.com/pannuhuone/Voron-CANBus/blob/main/update_klipper.md#updating-klipper-on-ebb36)
* [Updating the Katapult (CANboot)](https://github.com/pannuhuone/Voron-CANBus/blob/main/update_klipper.md#updating-the-katapult-formerly-know-as-canboot)

## Updating MCU

> [!NOTE]
> I have [BIGTREETECH Octopus V1.1 Control Board](https://biqu.equipment/products/bigtreetech-octopus-v1-1) as MCU and following is based on that
> It might be that some part will be different if another board is used!

You can update Klipper to MCU by using Kiauh. You can find instructions for installing Kiauh from [Github](https://github.com/dw-0/kiauh).

* Build Klipper with Kiauh
> [!NOTE]
> You need information what chip is used on your board. I'm using STM32F446ZET6, so I'm using following configuration

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/900fb218-2ddc-4731-bc59-964d49948b49)

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/cfb108b6-6975-475a-b454-a7da9f9230c7)

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/e9a0a78d-0956-40c4-87c2-dd8cd9bd30ae)

* Flash new firmware to MCU with Kiauh

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/df9f4936-8aa8-4855-a4c0-c0825979f476)

My choice was regular flashing method (1) via USB
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/a0bed4a7-d17d-4928-aaf0-3bb5cc4c6dcb)

Then Kiauh handles the update process and everything went well
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/ee7441f9-3a67-44ce-920c-ea17e10575e7)

And new firmware version can be seen also Mainsail
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/66296397-6566-469d-b493-12ed0cf3b120)


## Updating Klipper on EBB36

> [!WARNING]
> This section (update Klipper) is work in progress. I haven't done the update yet and I need to verify the flow and commands.

Current version for Klipper are following
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/5b39526e-780c-4cbe-a0e8-6b237d65aa4a)

* Configure Klipper
```
make menuconfig
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d79732e7-8869-4630-9721-517c23dcbe7b)

* Build Klipper
```
make clean
make
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/6c860873-b5f8-4d66-ae15-b904544e081f)


* At first stop Klipper service
```
sudo service klipper stop
```

* Upload new Klipper version to EBB36
> [!IMPORTANT]
> Replace YOUR_UUID from the UUID from your printer.cfg.

> [!NOTE]
> Following commands for uploading the firmware to EBB36 applies when CANboot have been replaced by Katalpult.

```
python3 ~/katapult/scripts/flashtool.py -i can0 -f ~/klipper/out/klipper.bin -u YOUR_UUID
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/647e8205-af98-497e-99b5-7e04744bde84)

* Start Klipper service
```
sudo service klipper start
```

New version have been updated for EBB36
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/f279cfb4-46c1-4d59-958b-c9e9ec0fe906)


## Updating the Katapult (formerly know as CANboot)

> [!WARNING]
> This section (update Katapult) is work in progress. I haven't done the update yet and I need to verify the flow and commands.

* It might be that this won't be needed. Klipper can be updated without updating the Katapult.
* Github repository for Katapult: [https://github.com/Arksine/katapult](https://github.com/Arksine/katapult).

### Steps for the update
* Fetch Katapult software
```
git clone https://github.com/Arksine/katapult
cd katapult
```
* Configure Katapult
```
make menuconfig
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d0dc06a0-2192-4867-a1de-2c40f6f98c81)

Save configuration: Quit ```Q``` and Save Changes ```Y``` and exit.

* Compile Katapult
```
make clean
make
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/6a7dc8e8-7132-4c7c-9915-ed932d8a945a)

* Stop the Klipper service
```
sudo service klipper stop
```

* Upload new version to EBB36
> [!IMPORTANT]
> Replace YOUR_UUID from the UUID for CAN device (EBB36) from your printer.cfg.

```

```


* Start Klipper service
```
sudo service klipper start
```

## Troubleshoot
> [!NOTE]
> CANbus query (below) doesn't show devices, because this shows only devices which are not yet initalized. ([information here](https://www.klipper3d.org/CANBUS.html#finding-the-canbus_uuid-for-new-micro-controllers))
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/15eefd85-8d34-4e89-b59b-f395182181b8)


[Back to main site](README.md)
