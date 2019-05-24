# Install macOS Mojave 10.14.5 on Dell Inspiron 7559 (i5-6300HQ/HDD)

>This repo gives tutorial &amp; files to install macOS Mojave 10.14.5 on Dell Inspiron 7559 (i5 6700HQ/HDD).
Credit to [fengwenhua's repo](https://github.com/fengwenhua/dell-7559-hackintosh)  and [RehabMan's tutorial](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)


## 0.0  Specs & Config

### Dell Inspiron 7559  
&emsp; -i5 6300HQ  
&emsp; -HDD  
&emsp; -SSD is for Windows install, mount-able on macOS (Not experimented installing macOS on SSD)  

1. For Legacy boot  
&emsp;&emsp;(Strongly Recommended)  
&emsp;&emsp; --BIOS 1.3.0(newest till May,2019),default bios settings  
&emsp;&emsp; --You can update it to whatever latest version  
2. For UEFI boot   
&emsp;&emsp;(after ANY POSSIBLE DEBUG TRAILS, unplug battery is a must to make it boot, or clover will stuck at Start InitDevicetree, NOT RECOMMENDED)  
&emsp;&emsp; --BIOS 1.0.1 with some bios features turned off (See details at [this repo](https://github.com/fengwenhua/dell-7559-hackintosh))


## 1.0  Creat USB install media

### USB 3.0 Disk  
1. Have a real mac, or   
install VMware Workstation Pro & [Unlocker](https://github.com/DrDonk/unlocker), get a packed sierra/highsierra.**iso** on ~~some torrent site like piratebay~~, and set up a mac virtual machine on your Windows  
2. Download Mojave 10.14.5 app on App Store (About 6 GB)  
3. Format USB to MBR with EFI and HFS+ partitions  
&emsp;&emsp;**(NOTE: Replace ```/dev/disk1``` with your actual USB disk number, refer to [RehabMan's Guide: Clover Legacy+MBR Install](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093) )**  
&emsp; ```diskutil partitionDisk /dev/disk1 2 MBR FAT32 "EFI" 200Mi HFS+J "Mojave" R```   
4. Create Mojave install media on HFS+ section  
&emsp; ```sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/Mojave /Applications/Install\ macOS\ Mojave.app --nointeraction```  
5. Install Clover (v4920 till May,2019) on USB:  
&emsp;&emsp;--Set install location on USB  
&emsp;&emsp;--Click Customize, select:  
&emsp;&emsp;&emsp;&emsp;Install at EFI section  
&emsp;&emsp;&emsp;&emsp;Bios0af  
&emsp;&emsp;&emsp;&emsp;BiosBlockIO  
&emsp;&emsp;&emsp;&emsp;drivers64/ApfsDriverLoader.efi  
&emsp;&emsp;&emsp;&emsp;Install RC Scipts to all Bootable partition & Install extra RC Script  

6. Refer to my Legacy CLOVER files, make your EFI looks like mine  
&emsp;&emsp;(config.plist/drivers64/kexts...)

BOOM....

(Actually I installed it by Bios 1.0.1 & UEFI Boot & unplug battery, ~~damn~~)

## 2.0 Install Mojave on HDD  
1. Boot into USB and erase a blank section on HDD into Apfs  
2. Install macOS on this Apfs section  
3. ait for install complete  
4. install Clover on HDD like USB    
&emsp;(copy and paste Clover files in EFI will boot, but press F4 at Clover bootloader won't generate ACPI files for you to patch later, so you really need to INSTALL it)  
5. patch DSDT/SSDT like [fengwenhua's repo](https://github.com/fengwenhua/dell-7559-hackintosh)

## 3.0 Results   
1. What's not working:  
&emsp;-F1/F2 to adjust backlight (though refered repo says it's working,emm..)  
&emsp;-Intel 3165 wifi  
&emsp;-Subwoofer  
&emsp;-NTFS mount in read & write (that's also a real mac problem)  
&emsp;-FaceTime/Message

2. What's confusing:  
&emsp;-CPU fan too lazy to work  
&emsp;-CPU-S report up to 3200 MHz turbo, but Intel Power gadget report no higher than 3000 MHz during CPU-S testing. Cinebench R20 multicore runs at 2.80GHz, single core hits up to 2.97Ghz (Peak) and 2.87Ghz (steady)  
&emsp;&emsp;```Cinebench R20 Multi-core:1126 Single-core:323    ```  
&emsp;-Ocassionally, battery icon still shows as charging though AC adapter is unpluged  
&emsp;-Boot with headphone jack plugged-in causes no audio output, you have to unplug (speaker working) then plug (headphone working now)

3. What's working:  
&emsp;-Well, all others, pretty good

