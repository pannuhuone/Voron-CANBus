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

Make sure that you have bed and hot end termistors connected, otherwise you will get error about those.

## CAN configurations to printer.cfg
1. Add CAN Bus MCU configuration
```
[mcu can0]
canbus_uuid: YOUR_CAN_UUID
```


# Troubleshoot
1. Did have problem with Mainsail and no configuration files cannot be seen on ```Machine -> Config files``` -section

**Solution:** In this version, at least, there were problem with paths and following commands resolve this problem
```
cd ~/moonraker
git pull
./scripts/data-path-fix.sh
```
