**_Hackintosh Big Sur guide for the Acer E5-575-50RM._**

**IMPORTANT**
**Hackintosh Build is not 1/2 hour work it requires you to research about your hardware and its compatibility. Start this project only when you have ample amount of time and patience**

**Specs**
1. Intel i5-7200U(kabylake)
2. IGPU: Intel UHD 620 (No dedicated 2GB Nvidia 940mx available in this variant)
3. Realtek ALC 255 (layout id: 3)
4. I2C touchpad with native apple gestures supported (Enable "Advanced" in touchpad section in BIOS).
5. Audio: Realtek ALC 255 with layout id: 3

**Step 1: Downloading MAC OS BIG SUR**
* Follow this [Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos) to download the MacOS, follow that guide only upto downloading part. For setting up of EFI files refer to this guide.

**Step 2: Gathering Files**
* Make a new folder _ACPI_ and download these files and place it there
  * [SSDT-PLUG](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PLUG-DRTNIA.aml)
  * [SSDT-EC-USBX](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-LAPTOP.aml)
  * [SSDT-XOSI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)
  * [SSDT-PNLF](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)

* Now make a folder _Kexts_ and download these files and place it there 
  
  * [Lilu](https://github.com/acidanthera/Lilu)
  * [WhateverGreen](https://github.com/acidanthera/whatevergreen/releases)
  * [VirtualSMC](https://github.com/acidanthera/virtualsmc/releases)
  //Copy everything except SMC Dell sensors.kext and SMC light sensors.kext
  * [VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2)
  * [Voodoo I2C](https://github.com/VoodooI2C/VoodooI2C) //for gesture support
  * [Apple ALC](https://github.com/acidanthera/AppleALC) //for audio
  * [USBInjectAll](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/) //sometimes usb ports doesn't work so this is required sometimes
 
**Step 3: Combining Files**
* Now download Latest [opencore](https://github.com/acidanthera/OpenCorePkg) release.
* Extract the zip file and copy _EFI_ folder from _X64_ to any convenient place.
* Head to _OC_ folder and there in _ACPI_ folder, paste all the files we downloaded and placed in our ACPI folder. 
* Now in _OC_ folder, head to Drivers and delete everything except _HfsPlus.efi_ and _OpenRuntime.efi_
* Again in OC folder, head to _kexts_ folder and paste all the files we downloaded in our kexts folder.
* Now in _Resources_ folder delete everything but keep the folder.
* Same goes for _Tools_ folder.

**Step 4: Editing Config.plist**
* I have provided a sample plist so you can edit that or use the sample plist provided in opencore release docs. It's upto you.
* You need to download two files
  * [ProperTree](https://github.com/corpnewt/ProperTree)
  * [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
* Use GenSMBIOS to generate your serial number. Remember while generating serial keys use _MacBookPro 14,1_ as it is most compatible with this system.
* Now download the config.plist file given here. and place it in _OC_ folder.
* Now Launch ProperTree and open config the plist you just copied to _EFI/OC/_
* Go to file->OC Snapshot and select _EFI/OC/_
* Now expand ACPI section and go to the section where it says _SSDT_XOSI.AML_. This is required for native apple gestures support. Check if following values are there or not. if not add them. For people editing sample plist from opencore docs you can also add this:

| Comment | String | Change _OSI to XOSI |
|---------|--------|---------------------|
| Count   | Number | 0                   |
| Limit   | Number | 0                   |
| Find    | Data   | 5F4F5349            |
| Replace | Data   | 584F5349            |

* Now head over to Device properties->Add.
* Check if present or not:

| PciRoot(0x0)/Pci(0x1b,0x0) | Dictionary | 1 key/value pair |
|----------------------------|------------|------------------|

* and under this, check if this is present or not:

| device-id | Data | 16590000 |
|-----------|------|----------|

* if not present add them as it is necessary for Intel UHD 620 graphics to work.
* Now head over to PlatformInfo -> Generic
  * In _SystemProductname_ add MacBookPro 14,1.
  * In _SystemSerialNumber_ add _serial_ number you generated from GenSMBIOS
  * In _In SystemUUID_ add _SmUUID_ value
  * In _MLB_ add _Board Serial_ Value
* Save the Config.plist file  
* To check if something is missing head over to [sanity checker](https://opencore.slowgeek.com)
* Your EFI file is ready, now if you have followed the guide carefully then you must have your MacOS ready to install. 
**IMPORTANT: YOU NEED TO CLEAN FLASH THE MAC OS i.e. YOU NEED TO FORMAT YOUR SSD/HDD WHILE INSTALLING MAC OS SO MAKE SURE YOU HAVE BACKED UP YOUR FILES**

**BIOS OPTIONS**
  * Make sure secure boot is turned off and F12 boot is enabled
**Post Installation Guide**
* Install open core configurator and mount EFI partiton on your device and copy EFI files from your USB to your laptop EFI partition.
* Dont bother fixing imessages and facetime. Every apple services except these works.
* for fixing the audio distortion and muffleness follow this [link](https://github.com/hackintosh-stuff/ComboJack)

**Error and fixing**
Please report any issues/things missing or possible improvements to the guide and I will try my best to fix them ASAP.
For full guide on doing it from scratch, follow: [This GUIDE](https://dortania.github.io/OpenCore-Install-Guide/)

**Thanks to**
* Dortaina
* RehabMan
* InsanelyMac
for fixing all error encountered.

