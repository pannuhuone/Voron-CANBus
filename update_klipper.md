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

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/586bc7c8-a2ea-4864-a270-434bfafd2593)

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/30434315-4a01-4f5e-955e-d21dcd71751b)

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/9a2e633c-230b-48f4-a551-1e3d5d756471)

* Flash new firmware to MCU with Kiauh

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/2d3a0b72-c13f-4659-a1f9-4a027fd5ef9b)

My choice was regular flashing method (1) via USB
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/9f4389fc-ffdf-4bbb-8d7e-7102f7133c84)

Then Kiauh handles the update process and everything went well
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/0bea56cc-2430-410e-85df-2e8466eee8bc)

And new firmware version can be seen also Mainsail
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/c2dace2f-a0ba-4b42-a4c8-cfac3d6a320a)


## Updating Klipper on EBB36

Current version for Klipper are following
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/25805933-4f16-4f03-b72d-dcb3f15f28b5)

* Configure Klipper
```
make menuconfig
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d18f6b6e-fa69-4471-9bad-2fef7b96c2f4)

* Build Klipper
```
make clean
make
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/7348d6d5-4906-4052-9e0b-227a13e010b7)


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
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/a31f4b49-be8e-48bd-9f02-2a9cd16e5dd3)

* Start Klipper service
```
sudo service klipper start
```

New version have been updated to EBB36
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/a4dea366-f1f7-44e7-8957-5f7541d48bd7)


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
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/0a8e0aff-3928-4fff-a568-689ff44df478)

Save configuration: Quit ```Q``` and Save Changes ```Y``` and exit.

* Compile Katapult
```
make clean
make
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/2ed0f09c-cb86-4240-94bb-487aa6d87864)

TBD

## Troubleshoot
> [!NOTE]
> CANbus query (below) doesn't show devices, because this shows only devices which are not yet initalized. ([information here](https://www.klipper3d.org/CANBUS.html#finding-the-canbus_uuid-for-new-micro-controllers))
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/b9558c90-6127-4a9a-9432-e3ece5314e03)


[Back to main site](README.md)
