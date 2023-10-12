## Updating the Katapult (formerly know as CANboot)
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
Current version for Klipper are following
![image](https://github.com/pannuhuone/Voron-CANBus/assets/5571703/d66d3fa0-e8f8-49cc-a02b-f6194b3a1be5)

[Back to main site](README.md)
