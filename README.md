# MSI-Prestige-15
- Model A10SC-213RU

# Hardware
|Specifications | Description|
|-|-|
|CPU       | Intel i5-10210U|
|IGPU      | Intel Graphics UHD 620|
|GPU       | Nvidia GTX1650 Max-Q
|Display   | CMN N156HCE-EN1 FHD
|RAM       | 16GB (8x2) Corsair Vengeance 2400|
|ROM       | Samsung 970 EVO 512GB|
|Audio     | Realtek ACL298|
|Wireless  | Intel AX201|

# Tested System Configuration
- <img src="https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/Screenshot.png/" width=512>
- OpenCore: v0.8.0
- MacOS: Monterey 12.6.8
- SMBIOS: MacBook Pro 16.3
- Config: [In repository](/OpenCore/config.plist)
  - If use SAMSUNG SSD: Set Config.plist->Kernel->Quirks->SetApfsTrimTimeout = 4294967295

- Required efi drivers
  - OpenHfsPlus
  - OpenRuntime
  - OpenCanopy
  - AudioDxe
 
# ACPI Tables
- [In repository](/ACPI/patched)

# Required kexts (tested)
- Lilu : https://github.com/acidanthera/Lilu/releases (1.8.4)
- WhateverGreen : https://github.com/acidanthera/WhateverGreen/releases (1.6.6)
- VirtualSMC : https://github.com/acidanthera/VirtualSMC/releases (1.3.2)
  - SMCBatteryManager
  - SMCLightSensor
  - SMCProcessor
  - SMCSuperIO
- AppleALC : https://github.com/acidanthera/AppleALC/releases (1.8.4)
- NVMeFix : https://github.com/acidanthera/NVMeFix/releases (1.1.1)
- NoTouchID : https://github.com/al3xtjames/NoTouchID/releases (1.0.3)
- USBPorts.kext [from repository](/Kexts)
- Voodool2C : https://github.com/VoodooI2C/VoodooI2C/releases (2.8)
  - Voodool2CHID
- VoodooPS2Controller : https://github.com/acidanthera/VoodooPS2/releases (2.3.5)
- itlwm : https://github.com/OpenIntelWireless/itlwm/releases (2.2.0)
- IntelBluetoothFirmware : https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases (2.3.0)
- BlueToolFixup.kext : https://github.com/acidanthera/BrcmPatchRAM/releases (2.6.8)
- CPUFriend : https://github.com/acidanthera/CPUFriend/releases (1.2.7)
  - CPUFriendDataProvider [from repository](/Kexts)

# Pre-Install
- Make bootable USB Drive with OpenCore and Mac OS Monterey
  - OpenCore - https://github.com/acidanthera/OpenCorePkg/releases
  - OpenCore Resources - https://github.com/acidanthera/OcBinaryData
  
- Installation requires an internet connection, you have two options:
  - 1. Use usb WI-FI dongle OR usb ethernet adapter
  - 2. Fill your WI-FI SSID and password in itlwm.kext/Contents/Info.plist "WiFiConfig" section

- In BIOS
  - Turn off Secure Boot
  - Press L-ALT + R-CTRL + R-SHIFT + F2 or (fn + F2) for see hidden feature
  - Go to Advanced->Power & Performance->CPU - Power Management Control->CPU lock Configuration->CFG lock = **Disabled**

# Installation
- Install

# Post-Install
- Disable Force Click in trackpad settings for normal left click
- In Terminal
  - sudo pmset powernap 0
  - sudo pmset proximitywake 0
  - sudo pmset standby 0
  - sudo pmset tcpkeepalive 0
- Install HeliPort.app to work with internal Wi-Fi \- https://github.com/OpenIntelWireless/HeliPort/releases

# Working
- CPU (800 MHz - 4.20 GHz | 35W | Speed Shift)
- IGPU Intel UHD 620
- WI-FI (HeliPort)
- Bluetooth
- Keyboard (backlight, volume +/-/mute, brightness +/-)
- Trackpad (gestures)
- Audio (AppleALC layout=22 or 29)
  - Stereo microphones [**(Bug 1)**](#Bugs)
  - Audio speakers
  - Combined audio jack (Audio+Mic)
- Screen brightness
- Sleep (hibernatemode 3)
- USB 3.2 XHCI Host Controller 
  - Left side 2x USB3.2 Type-C Gen1
  - Right side 2x USB3.2 Gen1
- WebCamera
- Battery indication
- HDMI (Video+Audio)
- External monitor (Video+Audio) via Type-C to HDMI adapter  

# Bugs
- Bug 1: Inverted channels
- Bug 2: When you reboot from Windows to MacOS, the sound amplifier will not turn on. Use shutdown not reboot.

# Does not work
- Card Reader Realtek RTS5250 PCI-E
- Fingerprint Reader Synaptics WBDI
- Nvidia GTX1650 Max-Q (Disabled via SSDT)

# Addition
It was helpful:
- https://dortania.github.io/getting-started/
- https://github.com/ErrorErrorError/msi-gs65-gs75-hackintosh#fix-sleep-and-prevent-ddgpu-turning-back-on-after-sleep
- https://github.com/hla63/Msi-modern-15-Hackintosh
- https://github.com/vomesk fix HDMI
