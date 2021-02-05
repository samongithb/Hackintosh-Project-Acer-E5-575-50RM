**_Hackintosh Big Sur guide for the Acer E5-575-50RM._**

**Specs**
1. Intel i5-7200U
2. IGPU: Intel UHD 620 (No dedicated 2GB Nvidia 940mx available in this variant)
3. Realtek ALC 255 (layout id: 3)
4. I2C touchpad with native apple gestures supported (Enable "Advanced" in touchpad section in BIOS).

As I am not sure how long I will maintain this repo so do update all your kexts.
Important ones are:
* [Lilu](https://github.com/acidanthera/Lilu)
* [WhateverGreen](https://github.com/acidanthera/whatevergreen/releases)
* [VirtualSMC](https://github.com/acidanthera/virtualsmc/releases)
  //Copy everything except SMC Dell sensors.kext and SMC light sensors.kext
* [VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2)
* [Voodoo I2C](https://github.com/VoodooI2C/VoodooI2C) //for gesture support

**Post Installation Guide**
* Dont bother fixing imessages and facetime. Every apple services except these works.
* Wifi and bluetooth(not in my case) does not work. So buy a wifi dongle separately. I recommend TP LINK WIFI Dongle as it is very compatible with mac.
  -TP Link officially does not support wifi drivers from mac 10.14+ so use this [BIG SUR OC WIFI ADAPTER](https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter) 
* for fixing the audio distortion and muffleness follow this [link](https://github.com/hackintosh-stuff/ComboJack)

**Error and fixing**
Please report any issues/things missing or possible improvements to the guide and I will try my best to fix them ASAP.
For full guide on doing it from scratch, follow: [This GUIDE](https://dortania.github.io/OpenCore-Install-Guide/)
Also I will be releasing a comprehensive guide to this from scratch.

**Thanks to**
Dortaina
RehabMan
InsanelyMac
for fixing all error encountered.

