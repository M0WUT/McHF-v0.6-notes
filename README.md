UI Board
========

Fit all components except:
* R11a 
* R30a 
* R31a 
* R32a 
* R33 
* R34 
* R42
* R43
* R43a 
* R47b 
* R47c 
* R47d 
* R47e 
* C1d 

The following are not on the BOM but should also not be fitted
* Y1
* C93
* C94

Also fit U7 which is a 24LC1026 as it saves the microcontroller wearing out its own internal FLASH. This is not on the BOM and not included but I have one spare for you. Prod me if I haven't given it to you.

Also fit a 2 pin 0.1" header into P6

Once just the UI board is built do the following:

You will need a Mini USB cable plugged into a computer (recommend not something nice as a precaution against bad soldering, maybe use a cheap USB hub?)

Bootloader loader software can be found [here](http://www.m0nka.co.uk/files/en.stsw-stm32080.zip)

Device bootloader can be found [here](http://www.m0nka.co.uk/wp-content/uploads/2014/02/mcHF_boot_0.0.0.14.zip)

To load the bootloader, follow instructions [here](http://www.m0nka.co.uk/wp-content/uploads/2016/03/Bootloader-Install.pdf) except ignore the section "How to put your device into DFU mode" (the first bit), replace that with:
* Short the P6 jumper
* Hold the BAND+ button down (S14, just above the LEDs)
* Plug in the Mini USB cable
* Count to 3 then release the BAND+ button.

The LCD backlight should be on.
Continue instructions from "After that start the DfuSe Demo..."

Remove the P6 jumper

Once the bootloader is installed, you need the firmware which can be found [here](http://www.m0nka.co.uk/wp-content/uploads/2016/03/mchf_firm_9_219_26_4.zip) and his firmware loader [here](http://www.m0nka.co.uk/files/mcHFManager_0.1.zip)

To load the firmware, put the device into bootloader mode:
* Unplug the Mini USB (if not already)
* Hold down the BAND- button (S4, just to the left of BAND+, above the holes for the ESP8266 option)
* Plug in the Mini USB cable
* Count to 3, then release the BAND- button

Now it gets a bit fun...

The mcHF will fail device driver installation. Go into Device Manager and manually update driver software, pointing it at the "driver" folder in the firmware loader folder you downloaded earlier (called mcHFManager_0.1)

This will almost certinaly fail as he didn't get his driver signed and Windows 10 forbids installation of unsigned drivers.

To force enable this, follow option two [here](https://www.howtogeek.com/167723/how-to-disable-driver-signature-verification-on-64-bit-windows-8.1-so-that-you-can-install-unsigned-drivers/), you will probably have to disconnect the mcHF and put it back into 
bootloader mode using my instructions above as the computer will probably kill power to the mcHF during reboot so it won't start with the BAND- button held down so won't be in bootloader mode.

Once the driver has been installed correctly, it shows up in Custom USB devices section as mcHF bootloader M0NKA, 2014
Now reboot your computer to take it out of "Allow unsigned drivers mode"

Now follow the instructions [here](http://www.m0nka.co.uk/wp-content/uploads/2016/03/Firmware-Upgrade.pdf) starting from below the section ("How to put your device into bootloader mode") as you have already done that using my
modified instructions above. so start from "Successful enter of bootloader mode is indicated by LCD backlight..." ignoring his crap about the LED pattern, mine goes alternate green / red flashing in bootloader mode but it is important the the backlight is turned off in this mode.

Once that's done, unplug the USB cable, plug it back in again and the mcHF should look radio-y.

Feel free to have a play, most menus are very sluggish as the microcontroller is failing to talk to stuff on the RF board so keep re-trying this. Hopefully mine will be built by then and I'll be able to report.

IMPORTANT
========
Once you are happy this is working do the following:
* Desolder R43b and clean up the pads
* Did you definetly remove it
* Are you sure?
* Check one last time for luck...
* Still don't belive you but whatever, if this is left on, there will be some SERIOUS magic smoke
* The mcHF is no longer able to run off USB power, the main voltage input is on the RF board so we shorted the USB 5V to the UI board 5V rail, if left shorted, R43b will short the mcHF 5V and the USB 5V, both of which will be power in normal operation.
 If you want to power if up for whatever reason, reshort the pads of R43b but REMOVE IT WHEN YOU ARE DONE!
* Pass me a beer :)

RF Board
========
Do not fit:
* R54
* C79
* RFC2
* RFC3
* D3
* D4

Don't wind transformers yet, there are many notes on what to do with them so take it easy for now and I'll work it out soon.






