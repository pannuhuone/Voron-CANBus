# Install Candlelight for U2C
## Steps for building software
* Assuming that you haven't build or install Candlelight before, meaning that you don't have file in your Raspberry for Candlelight. If you have, delete old files and directories.
* Connect to your Raspberry Pi with SSH
* STM chip on my U2C
![image](https://user-images.githubusercontent.com/5571703/210179779-565f5f4c-7649-409b-9c3b-3fdbac86b303.png)


* Install needed applications to Raspberry
```
sudo apt-get install cmake gcc-arm-none-eabi git
```
* Build software
```
cd ~
git clone https://github.com/bigtreetech/candleLight_fw
cd candleLight_fw
git checkout stm32g0_support
mkdir build
cd build
cmake .. -DCMAKE_TOOLCHAIN_FILE=../cmake/gcc-arm-none-eabi-8-2019-q3-update.cmake
make G0B1_U2C_fw
```
