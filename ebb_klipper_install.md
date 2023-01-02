# Install Klipper to EBB36
## Make configuration and compile
1. Assuming that steps before this one has been succesfully and you find can_uuid for EBB CanBoot.
2. Make configuration
```
cd ~/klipper
make menuconfig
```
Enter following options
* Use same communication interface than before
* Use same CAN Bus speed than you entered earlier steps

![image](https://user-images.githubusercontent.com/5571703/210255352-24327954-f7b8-464e-9f4e-cb01da81ab29.png)

Save configuration by selecting ```Q``` and then ```Y```

3. Compile Klipper

![image](https://user-images.githubusercontent.com/5571703/210255622-81607732-689a-4543-819f-19d4520336cd.png)

## Install Klipper to EBB36

4. Install Klipper with following command

```
python3 ~/CanBoot/scripts/flash_can.py -i can0 -f ~/klipper/out/klipper.bin -u YOUR_UUID
```
**Please use correct UUID in your case** You were able to check correct UUID with following command
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```
![image](https://user-images.githubusercontent.com/5571703/210256353-1a323157-7b9f-443b-9f45-b54154266357.png)

Assuming that everything went well, you are now able query CANBus UUID for Klipper with following command
```
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0

```
And you should see following
```
Found canbus_uuid=YOUR_UUID, Application: Klipper
```

![image](https://user-images.githubusercontent.com/5571703/210256643-dbd12ca6-d579-44a6-b5c3-35625a29bf84.png)

# Troubleshoot
* [ ] Will be added when facing problems

[Back to main site](README.md)
