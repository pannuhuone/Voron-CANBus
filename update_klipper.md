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
* Stop the Klipper service
* Find UUID for CAN device
* 

## Updating Klipper on EBB36


[Back to main site](README.md)
