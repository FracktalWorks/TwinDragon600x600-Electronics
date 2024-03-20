# TwinDragon600x600-Electronics
Electronic description, pinout and manuals for the electronics used in Twin Dragon 600x600x600 (Enhanced Size)

### For the Combination of BTT Manta M8P V2.0 + RPi CM4 + RP2040 based toolboard

Pin Configurations, jumper selection, CanBus and multi-MCU wiring to RPi CM4 embedded onto BTT Manta M8P V2.0 for Twin Dragon 600x600x600

Components used:
1. BTT Manta M8P V2.0 - 1
2. RPi CM4 (embed onto BTT Manta M8P V2.0) - 1
3. RP2040 based Can Module/Toolboard - 2
4. TMC5160 Stepper drivers - 4
5. TMC5160T Plus Z driver - 1
6. TMC2209 stepper drivers - 2 (External) + 2 (Present on the Toolboards)
7. BTT HDMI5 Touch Display

## Setting up BTT Manta M8P V2.0 + RPi CM4 + RP2040 based toolboard

After powering on the M8P, the LED on the bottom left corner will light up to indicate normal power supply. The VUSB jumper in the center is for selecting power - it should only be shorted when powering the board via USB or supplying power out via USB.

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/a958c1ba-796f-418f-ada7-2db6b0ebb668)

### Other Initial preparation and setting up jumpers

#### TMC Driver SPI Mode

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/3333b970-bcab-4d4b-b9cb-f18ed82d6cfc)

The first row are the defined pin for the drivers, which are either high or low when shorted or unshorted to establish different mode of communication. The second row are defined with the SPI modes, with the namings of 'MISO', 'CS', 'SCK' and 'MOSI' when read from left to right. Since we use the TMC5160 driver, it specifically operates only on the SPI mode. Insert the jumpers corresponding to its parallel pins only on the 1st and the 2nd row as shown in the image.

#### TMC Driver UART Mode

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/1110018c-07fe-482e-8d79-761831509141)

The given set of pin to short is the CS pin that enables only the uart mode.

#### Driver Voltage selection

For High Voltage selection(48V):

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/bf3a8896-4cff-40da-9098-789842d58acb)

Since the TMC5160 operates only on SPI mode, which is specifically for achieving faster communication and higher speeds, it needs an operating voltage of around 48V. The manta M8P has seperte pins for regular voltage of 24V and high voltage of 48V, that is to be jumped to the common pin of voltage supply to the drivers. We jump the HV pin in the left to the middle pin of supply in order to provide 48V to the drivers, as shown in the image above.

For normal Voltage selection (24V):

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/f2a6d8c0-dbdb-4a7c-89c2-14ec335743cc)

This voltage selection can be used when using a regular TMC2209 on the UART mode

#### Setting up jumper for probe activation

![BTT Manta M8P V2 0 ABL Connections](https://github.com/FracktalWorks/TwinDragon600x600-Electronics/assets/80109965/196da29f-d003-4410-bdbf-421b9a2d7515)


The pin for probe used here is the IND-probe pin on Manta M8P V2.0, and the jumpers are placed on the two pins beside the probe pins, and other three perpendicular pins to its right, where the top two are to jumped together to activate the probe pin, as shown in the image above, to enable 24V/5V supply to the ABL board. The three columns of the pins starting from the top are 5V, 12V, 24V Respectively.

#### Setting up Jumper for CANBUS communication

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/a540b422-52cb-41cc-b6a8-25c727c4f089)

At the left of the CAN pin, a small jumper is to be placed on the pins that mention '120R' depicting the 120 ohms resistance that is applied on the CAN Low and High communication pins. This is a crucial pin for the setting up of the CAN communication of the motherboard and toolboard.

## Wiring and Connections

![Twin Dragon 600 CM4 M8P V2 0 - Wiring](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/78dbc25f-ff8f-4533-9c9d-a62a0f82dd5e)

The overall connections of all the Electrical and Electronic components are present in the image above

### BTT Manta M8P V2.0 Pin connections

![Twin Dragon 600x600 with M8P V2 0 Wiring](https://github.com/FracktalWorks/TwinDragon600x600-Electronics/assets/80109965/7eced48d-cfc8-49cb-b144-970571d24fa0)


## Dragon ToolBoard Pinout Mappings

![WhatsApp Image 2024-03-20 at 14 31 21](https://github.com/FracktalWorks/TwinDragon600x600-Electronics/assets/80109965/88b125b5-2338-4aa1-831f-7f72e4ff2525)


![WhatsApp Image 2024-03-20 at 14 31 21 (1)](https://github.com/FracktalWorks/TwinDragon600x600-Electronics/assets/80109965/39d8fcf0-845f-4c06-a3fb-4be4854f6058)


## To setup Raspeberry Pi camera Rev 1.3, interfaced with RPi CM4 and BTT Manta M8P/M5P

In order to interface the Pi camera Rev 1.3 with the RPi CM4 and BTT Manta M8P/M5P, flip the board and check for a CSI1 camera slot, which should look like the image below

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/de2eb324-dc58-4c48-af00-7386afde8c35)

Instructions to attach the camera in BTT Manta M8P V2.0

![image](https://github.com/FracktalWorks/TwinDragon600-Electronics/assets/80109965/1bc509c2-2984-46af-a074-268701a05b0c)


Instructions to attach the camera in BTT Manta M8P V2.0

1. Now, boot up the board (including CM4), SSH into the CM4 and open the terminal
2. We will have to download a bin file into the boot folder of the CM4, below is the command to enter into the terminal.

`sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-cam1.bin -O /boot/dt-blob.bin`

If the above command does not work, try the following command:

`sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-cam1.bin -O /boot/firmware/dt-blob.bin`

3. Now, in the terminal, enter `sudo raspi-config` and select the option '3 Interface Options    Configure connections to peripherals'. Now select the first option 'P1 Camera      Enable/disable connection to the Raspberry Pi Camera'. A pop-up would appear where it asks to enable the camera. Make sure to select <yes> and exit the portal.

4. Now, in the terminal, type in `sudo nano /boot/config.txt` and make sure the settings are enabled

   `start_x=1
   gpu_mem=128`

   Note: make sure `#camera_auto_select=1` is commented out, or else it will not work.

For more clarifications, check out 'Julia TouchUI documentation' for more settings on Pi-camera
