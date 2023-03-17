# Nevermore Max PCB
[YouTube Video](soon_tm)
![Nevermore Max PCB](./Images/PCB.jpg)
A fan/LED controller PCB for Nevermore Max air filters. More information about the Nevermore Max can be found [here](https://github.com/nevermore3d/Nevermore_Max).

## Purchasing a PCB
Currently there are no known vendors selling assembled Nevermore Max PCBs. You can use the included gerber files to order your own from a PCB manufacturer like [PCBWay](https://www.pcbway.com/setinvite.aspx?inviteid=374841) or [JLCPCB](https://jlcpcb.com/).

This project is licensed under [GPL v3](./LICENSE), meaning vendors are allowed to sell PCBs without paying me. If you'd like to support the development of this and future projects please consider [sponsoring](https://github.com/sponsors/xbst) me on GitHub. You can also subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

## Features
- 1x 4-pin PWM fan connector with RPM monitoring
- 1x 3-pin fan connector with RPM monitoring (2-pin compatible)
- 2x I2C connectors for air quality monitor chips
- 1x Neopixel connector
- RP2040 MCU

## Instructions
### 1. PCB Tray
1. Print the ~~bottle opener~~ [Nevermore Max PCB tray](./Mounts/Nevermore-Max-PCB-Tray.stl) using the standard Voron print settings.
2. Remove the built-in supports.
3. Superglue 2 magnets. Pay attention to the polarities.
4. Mount the PCB. The plastic latches will keep the PCB in place, no screws needed. The USB/power side should be seated first.
![Instructions](./Images/PCB-Tray.png)
### 2. Wiring
1. All internal connectors and the power input connector are JST-XH. Use the diagram below to wire your fans/sensors/power.
![Pinout](./Images/Pinout.png)
### 3. Klipper Flashing
1. Connect the PCB to your Raspbery Pi while holding down the button on the PCB.
2. SSH into your Raspberry Pi.
3. Go to the Klipper directory
```
cd klipper
```
4. Clean remaining files from previous build.
```
make clean
```
5. Choose the options for the build.
```
make menuconfig
```
Use the following settings:
```
Micro-controller Architecture: Raspberry Pi RP2040
Communication inferface: USB
```
6. Build the firmware
```
make
```
7. Find the storage location of the RP2040. This will usually be sda1. Use this command one time with the PCB unplugged and one time with PCB plugged in (while holding down the button on the PCB) to verify.
```
ls /dev/
```
8. Flash the firmware.
```
sudo mount /dev/sda1 /mnt
sudo cp out/klipper.uf2 /mnt
sudo umount /mnt
```
### 4. Klipper Config
1. Download the [adxlmcu.cfg](./Firmware/nevermore.cfg) file from this repo and add it to your Klipper config directory.
2. Find your MCU address.
```
ls /dev/serial/by-id/*
```
3. Edit the nevermore.cfg file. Change the MCU serial address and edit the sensor/fan/RGB config to match your setup.
## YouTube

I am a YouTube content creator, and these projects were designed for my videos. If you want content about these projects & more, please consider [subscribing to my YouTube channel](https://www.youtube.com/channel/UClAWYmCkHjsbaX9Wz1df2mg).
<br>

If you feel like contributing to the development of this project and other projects like this you can sponsor me on [GitHub](https://github.com/sponsors/xbst), subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).

## Notes
- This readme file contains affiliate links. I make a comission on qualifying purchases.
- This project does not come with any warranty, if you choose to build/use a KUSBA, you are doing this at your own risk!
- If you want to sell PCBs, you are allowed to, and you will not owe me any royalties. **You cannot claim that I endorse the sale**. You can check the license file for more information. However, if you **wish** to give me a share you can sponsor me on [GitHub](https://github.com/sponsors/xbst), subscribe on [Patreon](https://l.isiks.tech/patreon) or [YouTube](https://l.isiks.tech/member).
