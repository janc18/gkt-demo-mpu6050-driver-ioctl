# Gtk Demo Application with MPU6050

This is a demo application to learn about kernel module to create a driver for linux.
I tested this using a Raspberry Pi Zero.
The Application is a GUI made with gtk3 than read the values of the MPU6050 using IOCTL commands.

## GUI components

- 6 Level Bars to view a visual representation of the raw values
- 6 Labels who display in text the raw values

## Hardware requirements

- SBC (Raspberry Pi Zero)
- MPU6050
- LCD Screen (tested with a HDMI 5in display)

## Software requirements

- xorg
- cmake
- gcc
- make
- libgtk-3-0
- libgtk-3-dev

## Steps to configure the screen suspension

If you don't have a Windows manager do the following:

1. Add the following line to this file **/etc/.rc.local**

```sh

export DISPLAY=:0 

```
2. Add the following lines to **/etc/X11/xorg.conf** to disable the screen suspension

```sh
Section "ServerFlags"
    Option "BlankTime" "0"
    Option "StandbyTime" "0"
    Option "SuspendTime" "0"
    Option "OffTime" "0"
EndSection
```
If you have a Desktop environment, use your GUI to change the screen suspension time

## Steps to build the app and kernel module

### Gtk application build steps
```sh
mkdir build
cd build
cmake ..
make
```
### Kernel module build steps
```sh
cd i2c_mpu6050
make
```

## Steps to run the application

1. Load kernel module
```sh
cd i2c_mpu6050
sudo insmod i2c_mpu6050.c
```
2. Run the Gtk application

If you don't have a Desktop environment
```sh
cd build
sudo startx ./executable
```
If you have a Desktop environment
```sh
cd build
./executable
```
