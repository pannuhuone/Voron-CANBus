# Configuring Mainsail and Klipper
* I assume that you have already installed Mainsail image to Raspberry.

## Adding basic printer configuration for Mainsail
### 1. Initial printer.cfg
I copied initial printer.cfg from [Voron document site](https://docs.vorondesign.com/build/software/configuration.html), I choose V2 [Octopus printer.cfg](https://raw.githubusercontent.com/VoronDesign/Voron-2/Voron2.4/firmware/klipper_configurations/Octopus/Voron2_Octopus_Config.cfg).

### 2. Basic settings for printer.cfg
Changed needed properties from printer.cfg. Link for [instructions](https://docs.vorondesign.com/build/software/configuration.html).

### 3. Updating Octopus firmware
I had to update firmware on my Octopus, because Klipper wasn't able to connect mcu I had MARLIN text on my device identifier. [Instructions for updating klipper can be found from here](https://docs.vorondesign.com/build/software/octopus_klipper.html). I got following error

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

### 1. Add CAN Bus MCU configuration
```
[mcu can0]
canbus_uuid: YOUR_CAN_UUID
```
![image](https://user-images.githubusercontent.com/5571703/210330072-681cb399-c119-459c-9716-a238c92a0a3c.png)

### 2. Add EBB36 temperature
By adding following, you can see EBB36 temperature from Mainsail Dashboard view
```
[temperature_sensor EBB36]
sensor_type: temperature_mcu
sensor_mcu: can0
min_temp: 0
max_temp: 100
```
Then following will be seen on Dashboard

![image](https://user-images.githubusercontent.com/5571703/210348390-38ba1df8-edc8-40a0-a860-1678609e1e9f.png)

### 3. Add ADXL345 configuration
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

### 4. Hot end thermistor, change original setting from Extruder section point to EBB pin

Before this step, I removed the thermistor which I attached temporarily directly to Octopus.

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

### 5. Stealthburner fans

Changes to ```Fan control``` section

#### Extruder fan (4010)

Original:
```
##  Hotend Fan - FAN1
[heater_fan hotend_fan]
pin: PE5
max_power: 1.0
kick_start_time: 0.5
heater: extruder
heater_temp: 50.0
##  If you are experiencing back flow, you can reduce fan_speed
#fan_speed: 1.0
```

Changed:
```
## Stealthburner, Extruder fan
[heater_fan hotend_fan]
pin: can0: PA0
heater: extruder
max_power: 1.0
kick_start_time: 0.5
heater: extruder
heater_temp: 50.0
```

#### Part cooling fanm, blower (5015)

Original:
```
[fan]
pin: PA8
kick_start_time: 0.5
##  Depending on your fan, you may need to increase this value
##  if your fan will not start. Can change cycle_time (increase)
##  if your fan is not able to slow down effectively
off_below: 0.10
```

Changed:
```
##  Print Cooling Fan - FAN0
[fan]
pin: can0:PA1
kick_start_time: 0.5
##  Depending on your fan, you may need to increase this value
##  if your fan will not start. Can change cycle_time (increase)
##  if your fan is not able to slow down effectively
#off_below: 0.10
```

### 6. Extruder

Original:
```
#####################################################################
#   Extruder
#####################################################################

##  Connected to MOTOR_6
##  Heater - HE0
##  Thermistor - T0
[extruder]
step_pin: PE2
dir_pin: PE3
enable_pin: !PD4
##  Update value below when you perform extruder calibration
##  If you ask for 100mm of filament, but in reality it is 98mm:
##  rotation_distance = <previous_rotation_distance> * <actual_extrude_distance> / 100
##  22.6789511 is a good starting point
rotation_distance: 22.6789511   #Bondtech 5mm Drive Gears
##  Update Gear Ratio depending on your Extruder Type
##  Use 50:10 for Stealthburner/Clockwork 2
##  Use 50:17 for Afterburner/Clockwork (BMG Gear Ratio)
##  Use 80:20 for M4, M3.1
gear_ratio: 50:17               #BMG Gear Ratio
microsteps: 32
full_steps_per_rotation: 200    #200 for 1.8 degree, 400 for 0.9 degree
nozzle_diameter: 0.400
filament_diameter: 1.75
heater_pin: PA2
```
```
[tmc2209 extruder]
uart_pin: PE1
interpolate: false
run_current: 0.5
sense_resistor: 0.110
stealthchop_threshold: 0
```

Changed:
```
#####################################################################
#   Extruder
#####################################################################

##  Connected to MOTOR_6
##  Heater - HE0
##  Thermistor - T0
[extruder]
step_pin: can0:PD0
dir_pin: can0:PD1
enable_pin: !can0:PD2
##  Update value below when you perform extruder calibration
##  If you ask for 100mm of filament, but in reality it is 98mm:
##  rotation_distance = <previous_rotation_distance> * <actual_extrude_distance> / 100
##  22.6789511 is a good starting point
rotation_distance: 22.6789511   #Bondtech 5mm Drive Gears
##  Update Gear Ratio depending on your Extruder Type
##  Use 50:10 for Stealthburner/Clockwork 2
##  Use 50:17 for Afterburner/Clockwork (BMG Gear Ratio)
##  Use 80:20 for M4, M3.1
gear_ratio: 50:17               #BMG Gear Ratio
microsteps: 32
full_steps_per_rotation: 200    #200 for 1.8 degree, 400 for 0.9 degree
nozzle_diameter: 0.400
filament_diameter: 1.75
heater_pin: can0:PB13
```
```
[tmc2209 extruder]
uart_pin: can0:PA15
#interpolate: false
run_current: 0.5
sense_resistor: 0.110
stealthchop_threshold: 0
```

Testing extruder motor with following command
```
STEPPER_BUZZ STEPPER=extruder
```

Klipper shutdown and I got following error

![image](https://user-images.githubusercontent.com/5571703/210368643-b8e230ff-150f-4ea2-b021-540c8feeb57e.png)

Found out that I made an error for tmc_2209 extruder configuration. At first I entered uart_pin as ```uart_pin: can0:PE15``` and correct one is ```uart_pin: can0:PA15```

# Troubleshoot
### 1. Did have problem with Mainsail and no configuration files cannot be seen on ```Machine -> Config files``` -section

**Solution:** In this version, at least, there were problem with paths and following commands resolve this problem
```
cd ~/moonraker
git pull
./scripts/data-path-fix.sh
```

[Back to main site](README.md)
