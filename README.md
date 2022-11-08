# MacOS Monterey on Asus X555LJ Laptop.
Based on Opencore.
Light install and update.

![alt text](https://github.com/Vejtarn/Screenshots/blob/master/Asus%20x555lj/Monterey.png?raw=true)

In this thread you will find a fully working version of the Openkore loader with Mac OS Monterey for the Asus x555lj laptop

# Description of laptop:
- Intel® Core™ i5-5200U - 5th generation Intel ® Core ™ i5 processors - Broadwell
- Intel® HD Graphics 5500 - 2048 Mb
- BCM4352 802.11ac Wireless Network Adapter + Bluetooth 4,0 - based on BCM94352HMB
- Realtek RTL8168GU/8111GU PCI Express Gigabit Ethernet
- Generic AHCI Controller: SSD ADATA SU800 - 1,02 Tb
                           HDD Hitachi Travelstar 5K1000 - 1Tb
- Wildcat Point-LP High Definition Audio Controller - based on Realtek ALC233
- Nvidia GeForce 930M - disabled

# BIOS 604 2019/06/04 setting
- Advansed:
_Internal Pointer Devise [Enabled]_;
_Wake On Lid Open [Enabled]_;
_Power Off Energy Saving [Enabled]_;
_Intel Virtualization Technology [Enabled]_;
_Intel AES-NI [Enabled]_;
_VT-d [Enabled]_;
_SATA Configuration - SATA Mode Selection [AHCI]_ ;
_Graphics Configuration - DVMT Pre-Allocated [128M]_;
_Smart Settings - SMART Self Test [Enabled]_;
_Network Stack Configuration - Network Stack [Disabled]_; 
_USB Configuration - Legasy USB Support [Enabled];
                   - XHCI Pre-Boot Mode [Enabled];
                   - USB Mass Storage Driver Support [Enabled]_;
- Boot:
_Fast Boot [Disabled]_;
_Launch CSM [Disabled]_;

- Security:
_Secure Boot Control [Disabled]_;

![alt text](https://github.com/Vejtarn/Screenshots/blob/master/Asus%20x555lj/X555LJ%20Monterey.png?raw=true)

# What doesn't work
- Brightness display
- Brightness, sleep, and flight mode function buttons
- Cardreader
- Geforce 930M

# What work
All other devices are up and running. The battery is working - there is a display of the status and time of use.
- Battery life indicator
- Intel HD 5500
- Sound
- Jack
- Keyboard
- Touchpad
- WiFi & Bluetooth
- Webcam
- Ethernet
- iCloud
- USBs - All USBs work fine in Big Sur and Monterey


# How did I do it.
This is a completely rethought build, based on an earlier one.

The necessary SSDTs have been added to the ACPI folder:
- add SSDT-EC
- add SSDT-HPET (added, but not used)
- add NVIDIAOFF (Disables the wrong video card NVIDIA)
- add SSDT-PLUG
- add SSDT-PNLF (I still have hopes to solve the problem with adjusting the brightness of the screen)
- add SSDT-SBUS-MCHC (added the necessary device MCHC and fixed the path to SMBUS)

Of the patches:
In ACPI:
- Rename EHC1 to EH01
- Rename EHC2 to EH02 
- Rename EC0 to EC 
- Rename HECI to IMEI 
- Rename SAT0 to SATA
- HPET _CRS to XCRS Rename
- RTC IRQ 8 Patch
- TIMR IRQ 0 Patch

In Kernel:
- Enable TRIM for SSD

All other necessary settings were taken from the OpenCore-Install-Guide:
https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/broadwell.html

PS.
This build has been tested in:
- all version MacOS Big sur 
- all version MacOS Monterey

PPS.
Before using this build to install MACOS on a similar laptop, I strongly recommend editing the list of devices in:
- "DeviseProperties -> Add ->", 
since only my ASUS x555lj laptop devices are registered there, in which some factory components have been replaced.
