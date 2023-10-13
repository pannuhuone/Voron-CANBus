## Sections
* [Updating MCU](https://github.com/pannuhuone/Voron-CANBus/blob/main/update_klipper.md#updating-mcu)
* [Updating the Katapult (CANboot)[(https://github.com/pannuhuone/Voron-CANBus/blob/main/update_klipper.md#updating-the-katapult-formerly-know-as-canboot)
* [Updating Klipper on EBB36]()

## Updating MCU

> [!NOTE]
> I have [BIGTREETECH Octopus V1.1 Control Board](https://biqu.equipment/products/bigtreetech-octopus-v1-1) as MCU and following is based on that
> It might be that some part will be different if another board is used!

> [!WARNING]
> This section (update MCU) is work in progress. I haven't done the update yet and I need to verify the flow and commands.

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
* Find UUID for CAN device
* 

## Updating Klipper on EBB36

> [!WARNING]
> This section (update Klipper) is work in progress. I haven't done the update yet and I need to verify the flow and commands.

Current version for Klipper are following
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d66d3fa0-e8f8-49cc-a02b-f6194b3a1be5)

* Configure Klipper
```
make menuconfig
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d79732e7-8869-4630-9721-517c23dcbe7b)

* Build Klipper

![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/6c860873-b5f8-4d66-ae15-b904544e081f)

* Upload Klipper to EBB36 board
```
python3 ~/CanBoot/scripts/flash_can.py -i can0 -f ~/klipper/out/klipper.bin -u YOUR_UUID
```
> [!IMPORTANT]
> Replace YOUR_UUID from the UUID from your printer.cfg.

## Troubleshoot
> [!NOTE]
> CANbus query (below) doesn't show devices, because this shows only devices which are not yet initalized. ([information here](https://www.klipper3d.org/CANBUS.html#finding-the-canbus_uuid-for-new-micro-controllers))
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/15eefd85-8d34-4e89-b59b-f395182181b8)


[Back to main site](README.md)
