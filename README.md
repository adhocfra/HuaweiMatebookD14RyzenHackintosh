<div align="center">


Huawei Matebook D14 2020 Ryzen 5 3500U Hackintosh
==========================================

  <img src="https://github.com/adhocfra/HuaweiMatebookD14RyzenHackintosh/blob/main/images/huaweiMAC.png" width="650"/>

![Static Badge](https://img.shields.io/badge/macOS-Monterey-violet)
![Static Badge](https://img.shields.io/badge/OpenCore-0.9.4-green)

</div>




HARDWARE
--------



| Component    |                       |
|---------------|-----------------------------------|
| CPU           | AMD Ryzen 5 3500u (4 cores 8 threads) |
| iGPU          | AMD Vega 8                    |
| RAM           | 8GB 3200mhz DDR4                 |
| SSD           | Hynix Nvme BC511             |
| USB           |  XHC0 XHC1   |
| AUDIO         | Realtek ALC 256                  |
| WIFI + BT     | Intel 7265                   |
| DISPLAY       | 60HZ IPS                  |
| CAMERA        | 720p                        |
| KEYBOARD       | USB                      |
| TRACKPAD      | I2C HID                           |
| BATTERY      | 56Wh                              |


* * *

## Table of Contents

- [**WHAT WORKS AND WHAT DOESN'T?**](#what-works-and-what-doesnt)

  - [General](#general)
  - [Multimedia](#multimedia)
  - [Functions](#functions)

- [**USED SSDTs**](#used-ssdts)

- [**USED KEXTS**](#used-kexts)

- [**USED SMBIOS**](#used-smbios)
  
- [**BIOS OPTIONS**](#bios-options)

- [**HELP**](#help)

- [**CREDITS**](#credits)


***
***

WHAT WORKS AND WHAT DOESN'T?
---------------------------


### GENERAL


| Component                | Compatibility |
|--------------------------|---------------|
| CPU                      | ✅             |
| iGPU                     | ✅             |
| RAM                      | ✅             |
| WIFI + BT                 | ✅ ( sometimes i have issues with BT)           |
| USB                      | ✅             |
| DISPLAY                  | ✅ |
| BATTERY                  | ✅             |
| KEYBOARD and FN keys     | ✅             |
| TRACKPAD                 | ✅             |

### MULTIMEDIA


| Component               | Compatibility                   |
|-------------------------|----------------------------------|
| HDMI      | ✅ |
| AUDIO                   | ✅                              |
| MICROPHONE              |  ✅ (with a special variant of AppleALC |
| CAMERA                  | ✅                              |

### FUNCTIONS


| Function                 | Compatibility                              |
|--------------------------|---------------------------------------------|
| SHUTDOWN/RESTART         | ✅                                           |
| SLEEP                    |  ✅                    |
| DISPLAY: BRIGHTNESS CONTROL | ✅            |
| AIRDROP                  | ✅, ANDROID TO MAC ONLY ([WARPSHARE](https://github.com/moseoridev/WarpShare)) |
| iServices (AppStore,Facetime...) | ✅|

If you want me to test more functions, open an ISSUE asking about the function, and I will test it.

* * *

USED SSDTs
-----------


| SSDT                                  | Description                                                                                                                                      |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)           | Creates a fake Embedded Controller device for macOS to work correctly but does not disable the original EC, as laptops need it for battery status, FN keys, etc. |
| [SSDT-PLUG-ALT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)       | Sets the plugin-type property to 1 on the first CPU core, enabling X86PlatformPlugin, which allows (Intel) CPU Power Management and AGPM (Apple GPU Power Management). It also redefines processors with Processor objects instead of Device objects if necessary since macOS does not support the new standard. |
| [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)        | Creates a fake PNLF device with a user-selectable _UID (basically the profile it uses) to allow native brightness control on laptops. |
| [SSDT-ALS0](https://chefkissinc.github.io/Extras/SSDTs/SSDT-ALS0.aml)                          | Simulates the presence of the ambient light sensor, necessary for brightness operation on laptops. |
| [SSDT-SMBUS-MCHC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html)     | Used for communication with the power source for ON/OFF instructions and more. Exact functionality and hardware interfaces vary by providers. |
| [SSDT-XOSI](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)         | Makes macOS believe we are using Windows, allowing any peripherals locked behind non-macOS to be active in macOS. |
| [SSDT-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)        | Creates a USBX device containing the necessary USB power properties to work correctly. This also requires a valid EC device. |
|[SSDT-GPRW](https://dortania.github.io/OpenCore-Post-Install/usb/misc/instant-wake.html)        |       macOS will instant wake if either USB or power states change while sleeping. To fix this we need to reroute the GPRW  |
|[SSDT-HPET](https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html)        |      to omit conflicting legacy IRQs  |
|[SSDT-SLPB](https://github.com/5T33Z0/OC-Little-Translated/tree/main/01_Adding_missing_Devices_and_enabling_Features/Power_and_Sleep_Button_(SSDT-PWRB%3ASSDT-SLPB))        |      Enabling Sleep Button  |
|[SSDT-RMNE](https://github.com/RehabMan/OS-X-Null-Ethernet)| In order to cause the kext to be loaded, you need to apply the DSDT patch provided in patch.txt. It adds a fake device ‘RMNE’ which the driver will attach to.|


* * *

### USED KEXTS 
(Warning: Some of these Kexts are only for macOS Monterey, for other macOS versions, you will need different Kexts and configurations)
---------------------------------------------------------------------------------------------------------------------------------------------------------



| KEXT                                       | Description                                                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------|
| [NootedRed](https://github.com/NootInc/NootedRed) | Provides graphics acceleration for AMD Vega iGPU.                                                  |
| [AirportItlwm](https://github.com/OpenIntelWireless/itlwm) | Supports most Intel Wi-Fi cards. AirportItlwm uses the macOS Wi-Fi stack.               |
| [AMDTscSync](https://github.com/naveenkrdy/AmdTscSync)   | Synchronizes the Timestamp Counter (TSC), generally only useful for AMD APU, which would be extremely slow without it. |
| [AppleALC](https://github.com/acidanthera/AppleALC)     | Patches the Apple audio stack (AppleHDA/AppleGFXHDA) to allow unsupported audio codecs and HDMI audio.   |
| [BrightnessKeys](https://github.com/acidanthera/BrightnessKeys) | Provides support for ACPI brightness change notifications (usually coming from keyboard function (FN) keys). |
| [ECEnabler](https://github.com/1Revenger1/ECEnabler)    | Allows macOS to read EC fields over 8 bits, eliminating the need to split them manually. |
| [GenericUSBXHCI](https://github.com/RattletraPM/GUX-RyzenXHCIFix) | Fixes USB3 issue found in some Ryzen-based hackintoshes. |
| [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Supports most Intel Wi-Fi cards. On macOS 11 and earlier, you need to use all 3 included Kexts. On macOS 12+, you need to use IntelBluetoothFirmware, IntelBTPatcher, and BlueToolFixup. |
| [IntelBTPatcher](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Found inside IntelBluetoothFirmware. |
| [Lilu](https://github.com/acidanthera/Lilu)          | Performs arbitrary kext, library, and program patching within macOS. |
| [NVMeFix](https://github.com/acidanthera/NVMeFix)      | Patches the NVMe stack (IONVMeFamily) to support Autonomous Power State Transition (APST) and fix kernel panic issues in some NVMe drivers. |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents) | Corrects CPU name in About This Mac and memory and PCI warnings in MacPro7,1 SMBIOS. Also allows forcing VMM to correct OTA updates on T2 SMBIOS on macOS Sonoma+, among other features. |
| [SMCBatteryManager](https://github.com/acidanthera/VirtualSMC) | Monitors laptop battery status. |
| [SMCLightSensor](https://github.com/acidanthera/VirtualSMC) | Adds ACPI ambient light sensor support. |
| [USBMap](https://github.com/USBToolBox/tool)          | (In my case, UsbToolBox doesn't work, use the built-in USBMap option to avoid using the USBToolBox Kext). |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC)  | Emulates Apple SMC. |
| [VoodooI2C (AMD)](https://chefkissinc.github.io/Extras/Kexts/VoodooI2C.zip) | Driver for I2C input devices. The linked one is a preliminary version with additional support for AMD I2C controllers. |
| VoodooI2CHID | Found within VoodooI2C. |
| [AppleIntelMCEReporter (Monterey +)](https://chefkissinc.github.io/Extras/Kexts/AppleMCEReporterDisabler.zip) | Disables AppleIntelMCEReporter panics on AMD systems and even some Intel systems. |
|[NullEthernet](https://github.com/RehabMan/OS-X-Null-Ethernet)|  The purpose of this driver is to enable Mac App Store access even if you don’t have a built-in Ethernet port with supporting drivers    |
|[HoRNDIS](https://github.com/jwise/HoRNDIS)|  HoRNDIS (pronounce: "horrendous") is a driver for Mac OS X that allows you to use your Android phone's native USB tethering mode to get Internet access    |
|[VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2)|   Driver for PS/2 peripherals. Used for laptop keyboards or PS/2 mice/keyboards on desktops. (YOU NEED TO DELETE VOODOOINPUT INSIDE THE KEXT, BECAUSE VOODOOI2C HAVE AN VOODOOINPUT)   |
|[SMCProcessorAMD](https://github.com/Lorys89/SMCProcessorAMD)|  Monitors CPU temperatures on AMD |

* * *

### USED SMBIOS


    MacBookPro16,3

* * *

 BIOS OPTIONS
 ----


    Secure Boot : Disabled
    VRAM igpu: 2GB (if not Bios Option, use UMAF tool)


* * *



HELP
----


<div align="center">

**Join ChefKissInc**, a community where we make it possible for all AMD laptops to use macOS (click the image below):

[<img src="https://i0.wp.com/img.talkandroid.com/uploads/2015/05/telegram_app_icon.png" alt="Telegram" width="90" height="90">](https://t.me/+Bx3MO9Hq8whhNzk9)

</div>

* * *

CREDITS
-------

[@ChefKissInc](https://github.com/ChefKissInc) Many thanks for your help and making all this possible; with you, a new era for AMD begins.

[@Acidanthera](https://github.com/acidanthera) Thanks for multiple Kexts and thanks for Opencore.

[@OpenIntelWireless](https://github.com/OpenIntelWireless) Thanks for supporting Intel Wi-Fi cards.

[@WarpShare](https://github.com/moseoridev/WarpShare) Many thanks for making Airdrop possible between Android and Mac.

[@Rxxbertx](https://github.com/Rxxbertx) Thanks for help me friend.


</details>

***

<img src="https://github.com/adhocfra/HuaweiMatebookD14RyzenHackintosh/blob/main/images/mac.png" width="650"/>


