# Plan for CANBus
## Goals
* Remove X and Y drag chains -> leass wires.
* Using U2C.
* Using CANBoot for easier updates.
* Stealthburner with EBB36 with cover.

## Wiring for CAN
![voron_canbus_wiring](https://user-images.githubusercontent.com/5571703/210175147-d069ec34-d23b-4c70-a096-16d26bb934da.jpg)

## Setup phases
1. Physical setups.
* [ ] Stealthburner setups.
* [ ] Electronic comparement setups.
2. [Install Candlelight for U2C](candlelight.md) 
* This will done only if you need to update Candlelight or your board doesn't have one.
* I ordered U2C board from Biqu ([link](https://biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device?_pos=1&_sid=f0f8330af&_ss=r&variant=39762747949154)) and it has Candlelight factory installed.
3. [Install CAN network](can_network.md)
4. 
