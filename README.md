# Install-macOS-Sierra-on-VirtualBox
For test purpose only, I created a batch to create Mac OS Sierra on VirtualBox on Windows 10

Not often but sometimes, I need to do some test on Mac OS. Following below instructure, I found create a MacOS Sierra with VirtualBox is very easy.  
https://techsviewer.com/install-macos-sierra-virtualbox-windows/

To make it even faster, I created a batch script to finish all the jobs with just one-click.

```
set VM="macOS 10.12 Sierra"
set PATH="C:\Program Files\Oracle\VirtualBox\"
VBoxManage createvm --name %VM% --ostype "MacOS1011_64" --register

VBoxManage storagectl %VM% --name "SATA Controller" --add sata --controller IntelAHCI
VBoxManage storageattach %VM% --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium "%~dp0macOS 10.12 Sierra Final by TechReviews.vmdk"

VBoxManage modifyvm %VM% --memory 4096 --vram 128 --cpus 2
VBoxManage modifyvm %VM% --firmware efi --pae on --chipset ich9 --rtcuseutc on 
VBoxManage modifyvm %VM% --accelerate3d on
VBoxManage modifyvm %VM% --boot1 disk --boot2 none --boot3 none --boot4 none

VBoxManage modifyvm %VM% --cpuidset 00000001 000106e5 00100800 0098e3fd bfebfbff
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct" "iMac11,3"
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion" "1.0"
VBoxManage setextradata %VM% "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct" "Iloveapple"
VBoxManage setextradata %VM% "VBoxInternal/Devices/smc/0/Config/DeviceKey" "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"
VBoxManage setextradata %VM% "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC" 1
pause
```
