# Plan for CANBus

## Big shout and credits for following persons
* Maz0r for instructions which have been applied in here also. [Link here](https://github.com/maz0r/klipper_canbus)

## Goals
* Remove X and Y drag chains -> less wires which can be broken and less weight on gantry.
* Using Bigthree U2C.
* Using CANBoot for easier updates in the future.
* Stealthburner with EBB36 with cover.
* [ ] Link to KEJAR31 repository

## Hardware
* [ ] Enter used hardware

## Wiring for CAN
![image](https://user-images.githubusercontent.com/5571703/210214738-20594a0c-377b-4b67-9f57-dd373c3f51c8.png)

## Setup phases
1. Physical setups.
* [ ] Stealthburner setups.
* [ ] Electronic comparement setups.
2. [Install Candlelight for U2C](candlelight.md) 
* This will done only if you need to update Candlelight or your board doesn't have one.
* I ordered U2C board from Biqu ([link](https://biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device?_pos=1&_sid=f0f8330af&_ss=r&variant=39762747949154)) and it has Candlelight factory installed.
3. [Install CAN network](can_network.md)
4. [Install CANboot for EBB36](ebb36.md)
