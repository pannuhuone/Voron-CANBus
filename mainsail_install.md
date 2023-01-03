# Configuring Mainsail and Klipper
* I assume that you have already installed Mainsail image to Raspberry.

## Adding basic printer configuration for Mainsail
1. I copied initial printer.cfg from [Voron document site](https://docs.vorondesign.com/build/software/configuration.html), I choose V2 [Octopus printer.cfg](https://raw.githubusercontent.com/VoronDesign/Voron-2/Voron2.4/firmware/klipper_configurations/Octopus/Voron2_Octopus_Config.cfg).
2. Changed needed properties from printer.cfg. Link for [instructions](https://docs.vorondesign.com/build/software/configuration.html).
3. I had to update firmware on my Octopus, because Klipper wasn't able to connect mcu I had MARLIN text on my device identifier. [Instructions for updating klipper can be found from here](https://docs.vorondesign.com/build/software/octopus_klipper.html). I got following error

![image](https://user-images.githubusercontent.com/5571703/210272179-771dc049-b240-41fd-b52c-f3db2bf7e580.png)

I have following chip on my Octopus

![image](https://user-images.githubusercontent.com/5571703/210272408-613216e9-11b3-4948-afc2-0cda6e36a134.png)

So, configured Klipper as following settings

![image](https://user-images.githubusercontent.com/5571703/210272445-bb050fe6-3bbb-4373-8d6b-636fd0722d7a.png)

Built the Klipper

![image](https://user-images.githubusercontent.com/5571703/210272561-6ddaf716-697a-4d2a-a7c7-dbc94b2bd8f6.png)

And followed rest of the instructions for updating the Octopus.

Make sure that you have bed and hot end termistors connected, otherwise you will get error about those. I added separate thermistor directly to Octopus before I had hot end thermistor connected and configure to EBB36. Otherwise you should get following error

![image](https://user-images.githubusercontent.com/5571703/210335096-581216b9-b2ee-41f5-9c6d-811022cde0ea.png)

## CAN related configurations to printer.cfg
* Sample configurations for EBB36 v1.2 can be found from Bigthreetech Github site, [link here](https://github.com/bigtreetech/EBB/blob/master/EBB%20CAN%20V1.1%20(STM32G0B1)/sample-bigtreetech-ebb-canbus-v1.2.cfg).

1. Add CAN Bus MCU configuration
```
[mcu can0]
canbus_uuid: YOUR_CAN_UUID
```
![image](https://user-images.githubusercontent.com/5571703/210330072-681cb399-c119-459c-9716-a238c92a0a3c.png)

2. Add ADXL345 configuration
```
[adxl345]
cs_pin: can0: PB12
spi_software_sclk_pin: can0: PB10
spi_software_mosi_pin: can0: PB11
spi_software_miso_pin: can0: PB2
axes_map: x,y,z

[resonance_tester]
accel_chip: adxl345
probe_points:
    150, 150, 20
```

3. Hot end thermistor, change original setting from Extruder section point to EBB pin

Original:
```
## Check what thermistor type you have. See https://www.klipper3d.org/Config_Reference.html#common-thermistors for common thermistor types.
## Use "Generic 3950" for NTC 100k 3950 thermistors
sensor_type: Generic 3950
sensor_pin: PF4
```
Changed:
```
## Check what thermistor type you have. See https://www.klipper3d.org/Config_Reference.html#common-thermistors for common thermistor types.
## Use "Generic 3950" for NTC 100k 3950 thermistors
sensor_type: Generic 3950
#sensor_pin: PF4
sensor_pin: can0: PA3
```

# Troubleshoot
### 1. Did have problem with Mainsail and no configuration files cannot be seen on ```Machine -> Config files``` -section

**Solution:** In this version, at least, there were problem with paths and following commands resolve this problem
```
cd ~/moonraker
git pull
./scripts/data-path-fix.sh
```

[Back to main site](README.md)
