# AMD-3900x_MSI-Unify-X570_AMD-X5700XT

EFI for my Hackintosh based on OpenCore



Hello.



Based on some sources in the internet 

[Hackintosh-Forum](https://www.hackintosh-forum.de)

[AMD-OSX](https://forum.amd-osx.com/index.php)

[Dortania.Github.io](https://dortania.github.io/OpenCore-Desktop-Guide/AMD/zen.html)

i was able to get my Hardware working with macOS. I want to share this with you and maybe we can optimize it together a bit more.

**Attention**: This EFI is uploaded without SMBIOS settings (serialnumber, etc.). After downloading the EFI you have to change it [this way](https://dortania.github.io/OpenCore-Desktop-Guide/AMD/zen.html#platforminfo).





So let`s start:

## Bios Settings:

##### Enabled:

- EHCI/XHCI Hand-off

- Above 4G decoding



##### Disabled:

- CSM



## <u>Hardware</u>

CPU: AMD Ryzen 9 3900X 3.8 GHz 12-Core

Motherboard: MEG MSI X570 Unify

Video Card: 8GB Sapphire RX 5700 XT Nitro+

<u>Software</u>

OpenCore: 0.5.9

MacOS Catalina: 10.15.5



## **<u>Kexts</u>:**



[SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor/blob/master/README.md) - XNU kernel extension for power management and monitoring of AMD processors.

[AppleALC](https://github.com/acidanthera/AppleALC/releases) - An open source kernel extension enabling native macOS HD audio for not officially supported codecs without any filesystem modifications.

[HibernationFixup](https://github.com/acidanthera/HibernationFixup) - An open source kernel extension providing a sync between RTC variables and NVRAM. In the config.plist the parameter "hbfx-disable-patch-pci" is set in the section NVRAM -> boot-args.

[Lilu](https://github.com/acidanthera/lilu/releases) - An open source kernel extension bringing a platform for arbitrary kext, library, and program patching throughout the system for macOS.

[LucyRTL8125Ethernet](https://github.com/Mieze/LucyRTL8125Ethernet) - A macOS driver for Realtek RTL8125 2.5GBit Ethernet Controllers.

[NVMeFix](https://github.com/acidanthera/NVMeFix) - NVMeFix is a set of patches for the Apple NVMe storage driver, IONVMeFamily. Its goal is to improve compatibility with non-Apple SSDs. It may be used both on Apple and non-Apple computers.

[SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor) - XNU kernel extension for power management and monitoring of AMD processors. Also comes with a plugin for [VirtualSMC](https://github.com/acidanthera/VirtualSMC) to export readings to other applications.

[USBPort](https://github.com/headkaze/Hackintool) - created with Hackintool (see section below "Mainboardlayout") - The Swiss army knife of vanilla Hackintoshing

[VirtualSMC](https://github.com/acidanthera/VirtualSMC) - Advanced Apple SMC emulator in the kernel. Requires [Lilu](https://github.com/vit9696/Lilu) for full functioning.

[VoodooTSCSyncAMD](https://www.hackintosh-forum.de/attachment/109964-voodootscsync-kext-zip/) - Kernel extension that synchronizes the processes between the AMD processors.

[WhateverGreen](https://github.com/acidanthera/WhateverGreen) - [Lilu](https://github.com/acidanthera/Lilu) plugin providing patches to select GPUs on macOS. Requires Lilu 1.4.0 or newer.

Optional:

[**IntelBluetoothFirmware](https://github.com/zxystd/IntelBluetoothFirmware/releases) - IntelBluetoothFirmware is a Kernel Extension that uploads Intel Wireless Bluetooth Firmware to provide native Bluetooth in macOS. On my side i replaced the M2 BT/WIFI Card.

[**RadeonBoost](https://www.hackintosh-forum.de/forum/thread/47791-radeonboost-kext-benchmark-scores-wie-am-echten-mac-unter-windows/?pageNo=1) - GPU Performance Boost - not working with 10.15.5 yet.

[**MacProMemoryNotificationDisabler](https://github.com/IOIIIO/MacProMemoryNotificationDisabler) - [Lilu](https://github.com/acidanthera/Lilu) plugin for disabling the "more than maximum amount of memory" popup on MacPro7,1. I use SMBIOS iMacPro1,1 where it is not needed.



## <u>Mainboardlayout</u>:

###### USB Ports:

Before we begin: the renaming of the controllers have been done with an aml file (SSDT-XHC-customized.aml). That should be possible to be used on any X570 based Mainboard:

\_SB.PCI0.BXBR.BYUP.BYD8.XHC0 -> XHCI

\_SB.PCI0.BXBR.BYUP.BYD8.XHC1 -> XHC

\_SB.PCI0.GP13.XHC0 -> XHC2

![](/docs/img/Mainboard/HackintoolUSBcontrollers.png)

This is the aml file i have used:

![](/docs/img/Mainboard/ACPI-SSDT-XHC-Fullaml.png)

Front:

View from the front to my Tower with the USB ports:

![](/docs/img/Mainboard/USBviewfront.png)

Back:

![](/docs/img/Mainboard/RearIOPanel.png)


<p style='color:red'>This is some red text.</p>
```diff
@@ XHCI PRT1 USB 3.0 (Rear I/O Panel  7 @@

XHCI PRT2 USB 3.0 (Rear I/O Panel @@ 8 @@

XHCI PRT4 USB internal (IOHostAdapter (PCIE x1 Broadcom Karte)

XHCI PRT5 USB 2.0 (Rear I/O Panel @@ 1 @@

XHCI PRT6 USB 2.0 (Rear I/O Panel @@ 2 @@

XHCI PRT7 USB 3.0 (Rear I/O Panel - 7

XHCI PRT8 USB 3.0 (Rear I/O Panel - 7



XHC2 PRT1 USB 3.0 (Rear I/O Panel<div class="text-purple mb-2"> 3</div>

XHC2 PRT2 USB 3.0 (Rear I/O Panel<div class="text-purple mb-2"> 4</div>

XHC2 PRT3 USB 3.0 (Rear I/O Panel <div class="text-purple mb-2">6</div>

XHC2 PRT5 USB 3.0 (Rear I/O Panel <div class="text-red mb-2">3</div>

XHC2 PRT6 USB 3.0 (Rear I/O Panel <div class="text-red mb-2">4</div>

XHC2 PRT7 USB 3.0 (Rear I/O Panel <div class="text-red mb-2">6</div>

<div class="text-purple mb-2">purple = USB 2.0</div>

<div class="text-red mb-2">red = USB 3.0</div>

```

Without changing anything but the names of the XHC controllers, the list of available slots look like this on my side:

![](/docs/img/Mainboard/FullActivatedPorts.png)

All USB 3 and USB 2 Slots marked green are usable. (Just the USB 3.2 Gen 2 Type-C is not marked green, cause i have no device that i can attach to it. So Hackintool cannot check if the port is used. But you can decide yourself if you want to disable a port or not.)

With disabled ports Hackintools USB sectio looks like this. (Again: This varies if you dont disable all the ports i did. It is not really needed as far as i know):
![](/docs/img/Mainboard/ReducedActivatedPorts.png)



## What is working so far:

##### Audio:

Audioplayback with SPDIF tested.

Audioinput not testet.

config.plist
![](/docs/img/Audio/configplist.png)

kext + config.plist

<img src="/docs/img/Audio/kextANDconfigplist.png" title="" alt="" width="508">



##### Graphics acceleration:

I am using Whatevergreeen and the boot-args: 

agdpmod=pikera

config.plist

![](/docs/img/moreGPUpower/configplist.png)

kext + config.plist

![](/docs/img/moreGPUpower/kextANDconfigplist.png)



##### LAN:

With the kext from Mieze the LAN adapter with 2.5 GBit it is working stable when its configured first time properly. 

You have to set the speed in Hardwaresettings manually like the following. First you have to set the speed to 100baseT and accept everything. You will see the "Ethernet" on the left becomes green. Afterwards you can switch the speed to 1000baseT.

![](/docs/img/LAN/Settings.png)

kext and config.plist

![](/docs/img/LAN/kextANDconfigplist.png)

##### Bluetooth:

Worked OOB on my side when i was using the AX200 WIFI/BT card. But to be sure you should use the [IntelBluetoothFirmware]([Releases · zxystd/IntelBluetoothFirmware · GitHub](https://github.com/zxystd/IntelBluetoothFirmware/releases) and add it to the config.plist and kext folder. This isn't done from me in this repo!

![](/docs/img/BluetoothWifi/BluetoothAX200.png)

##### Powermanagement:

###### I took the SSDT-Plug.aml predefined from [Aluveitie](https://github.com/aluveitie). If you want to create it from sratch, you can do so if you follow [this link](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/pm.html).

When you use the SSDT-PLUG.aml you see in ioregistryexplorer, that the powermanagement is working.

![](/docs/img/PowerManagement/withSSDT-Plug.png)

##### **internal drives are shown as external drives

Without adding the following setting, my internal nvme SSD was shown as external device. It has been solved in this repo.

With this change, the master boot device (nvme slot) is told: you are internal.

![](/docs/img/internalDrives/internalDrivesConfig.png)

![](/docs/img/internalDrives/finalView.png)

<div class="text-yellow mb-2">yellow = internal boot-device</div>

<div class="text-purple mb-2">purple = other internal devices</div>



##### Shutdown

##### USB Power





## What is not working:

- ##### WIFI (Intel AX200, maybe [this](https://github.com/zxystd/itlwm) will solve the problem). I have changed the M2 Wifi Card to a compatible device.

- ##### Sleep - only when no device is attached (that is no solution for me).





Credits:
All developer and maintainer.

especially @Aluveitie
