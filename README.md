# Huawei Matebook D14 2020 Ryzen 5 3500U Hackintosh
---------------------------------------------------------------





![Schermata 2023-09-02 alle 19 14 55](https://github.com/adhocfra/HuaweiMatebookD14RyzenHackintosh/assets/36541427/705dfd25-8ad5-4b67-96d6-fb6ef8c0c7c6)






-------------------------------------

Successfully installed Monterey on Huawei Matebook D14 2020 (Ryzen 3500U + Vega8)

----------------------------------------------------------------------------------------------------
ACPI used:
----------------------------------------------------------------------------------------------------
 -->SSDT-ALS0
 
 -->SSDT-EC
 
 -->SSDT-GPRW
 
 -->SSDT-HPET
 
 -->SSDT-PLUG
 
 -->SSDT-PLNF
 
 -->SSDT-RMNE
 
 -->SSDT-SBUS-MCHC
 
 -->SSDT-SLBP
 
 -->SSDT-USBX
 
 -->SSDT-XOSI
 
 
KEXT used:
----------------------------------------------------------------------------------------------------
 -->AppleALC.kext //This Version enables Audio (jack+speakers) + Microphone
 
 -->AppleMCEReporterDisabler.kext
 
 -->BrightnessKeys.kext
 
 -->ECEnabler.kext
 
 -->GenericUSBXHCI.kext
 
 -->HoRNDIS.kext //Enables Tethering USB in order to install the system without WiFi (which unfortunately is unsopported)
 
 -->Lilu.kext
 
 -->NootedRed.kext //Enables GPU Acceleration on AMD APU's
 
 -->NullEthernet.kext
 
 -->NVMeFix.kext
 
 -->RestrictEvents.kext
 
 -->SMCBatteryManager.kext
 
 -->SMCProcessorAMD.kext
 
 -->USBPorts.kext
 
 -->VirtualSMC.kext
 
 -->VoodooI2C.kext
 
 -->VoodooI2CHID.kext
 
 -->VoodooPS2Controller.kext
 

WHAT'S WORKING:
----------------------------------------------------------------------------------------------------
-GPU Acceleration

-Audio+Microphone

-iCloud, iMessages, Apple Music (Dolby Atmos included) and Apple Services in general

-Sleep/Wake: After installation, from terminal, execute this commands: 

sudo pmset autopoweroff 0

sudo pmset powernap 0

sudo pmset standby 0

sudo pmset proximitywake 0

sudo pmset tcpkeepalive 0

-Keyboard (Backlight included) and Trackpad

-HDMI (not audio but is totally solvable)

WHAT'S NOT WORKING:
----------------------------------------------------------------------------------------------------
-Wifi and Bluetooth (you can buy an Intel Wifi+Bluetooth card in order to get it working, but it requires additional kexts)

-DRM services (Streaming platforms doesn't work in Safari but only in Chrome or Firefox)

 ATTENTION: If you download Chrome, be aware that after installation YOU CANNOT open it by clicking on it, but from terminal you have to digit "/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --disable-gpu" (without " ") and in the search bar digit chrome://flags. You will find a series of options, find "GPU Rasterization" and disable it. Now you can open chrome by clicking on it.

Remember to generate your own SMBIOS and add it into the config.plist, follow Dortania's Guide if you don't know how to do that.

Credits:
----------------------------------------------------------------------------------------------------
Dortania's Guide (https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html)

ChefKissInc for NootedRed (https://chefkissinc.github.io)

[@Rxxbertx](https://github.com/Rxxbertx/Rxxbertx)

Corpnewt for Tools (https://github.com/corpnewt)

Acidanthera for Opencore (https://github.com/acidanthera/OpenCorePkg)


