A air quality sensor.

# BOM & Hardware Notes
- [ESP32 MCU (1)](https://www.amazon.com/gp/product/B09C5RDZ8G)
- [APC1, UART Version](https://octopart.com/search?q=APC1001U)
- An 8 pin JST GH connector & some leads for it

# Useful Links
- [Instructions for loading files with ampy](https://learn.adafruit.com/micropython-basics-load-files-and-run-code/file-operations)
- [Getting started guide with esp32 and micropython](https://docs.micropython.org/en/latest/esp32/tutorial/intro.html#esp32-intro)
- [Firmware downloads](https://micropython.org/download/esp32/) - this is using version esp32-20220618-v1.19.1.bin

# Misc. Notes

### Opportunities for performance improvement
- Read less often and put it into sleep.

### Misc. FW Notes
- enabling the watchdog creates problems when trying to push new firmware the watchdog resets it. 

# Command Reference
I don't use these commands often, so I'm including them here just so they're handy next time I need them. All are performed when connected to the ESP32 with USB.

##### To erase and install firmware

`esptool.py --port COM5 erase_flash`

`esptool.py --chip esp32 --port COM5 write_flash -z 0x1000 esp32-20220618-v1.19.1.bin`

##### To Run Code

`ampy -pCOM5 run main.py`

##### To Push Code

If code in a `main.py` file already running, stop it by connecting via serial and press Ctrl-A to stop code. Then run `ampy -pCOM5 rm main.py`

`ampy -pCOM5 put main.py`

Repeat for library files as required.

#### If Ampy Not Responding

First, make sure that the esp32 is booted correctly by opening the serial port with putty and making sure it's booted. See known issue about knob 2.

Then, see if the `main.py` needs to be stopped.