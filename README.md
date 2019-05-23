# Install macOS Mojave 10.14.5 on Dell Inspiron 7559 (i5-6300HQ/HDD)
>This repo gives tutorial &amp; files to install macOS Mojave 10.14.5 on Dell Inspiron 7559 (i5 6700HQ/HDD).
Credit to [fengwenhua's repo](https://github.com/fengwenhua/dell-7559-hackintosh)  and [RehabMan's tutorial](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/)

## 0.0  Specs & Config
>Dell Inspiron 7559  
&emsp; -i5 6300HQ  
&emsp; -HDD  
&emsp; -For Legacy boot (Strongly Recommended)  
&emsp;&emsp; --BIOS 1.3.0(newest till May,2019),default bios settings  
&emsp; *-For UEFI boot (failed to make it boot unless unplug battery after ANY POSSIBLE DEBUG TRAILS, although some people reported succeed, NOT RECOMMENDED)  
&emsp;&emsp; --BIOS 1.0.1 with some bios features turned off (See details at [this repo](https://github.com/fengwenhua/dell-7559-hackintosh))*

## 1.0  Creat USB install media
>USB 3.0 Disk  
&emsp;-Have a real mac / install VMware Workstation Pro & [Unlocker](https://github.com/DrDonk/unlocker), get a packed sierra/highsierra.**iso** on ~~some torrent site~~, and set up a mac virtual machine on your Windows  
&emsp;-Download Mojave 10.14.5 app on App Store (About 6 GB)  
&emsp;-Format USB to MBR with EFI and HFS+ partitions  (NOTE: Replace /dev/disk1 with your actual USB disk number, refer to [RehabMan's Guide: Clover Legacy+MBR Install](https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093) )  
”diskutil partitionDisk /dev/disk1 2 MBR FAT32 "EFI" 200Mi HFS+J "install_osx" R“  
&emsp;-Create Mojave install media on HFS+ section
&emsp;&emsp;  
&emsp;-Install Clover (v4920 till May,2019) on USB:  
&emsp;&emsp;--Set install location on USB  
&emsp;&emsp;--Choose Customize, select:  
&emsp;&emsp;&emsp;---Install at EFI section  
&emsp;&emsp;&emsp;---Bios0af  
&emsp;&emsp;&emsp;---BiosBlockIO  
&emsp;&emsp;&emsp;---drivers64/ApfsDriverLoader.efi  
&emsp;&emsp;&emsp;---Install RC Scipts to all Bootable partition & Install extra RC Script  
&emsp;-Refer to my Legacy CLOVER files, make your EFI looks like mine  
&emsp;&emsp;--config.plist/drivers64/kexts

BOOM....

(Actually installed UEFI Boot & unplug battery)

## 2.0 Install Mojave on HDD  
-Boot into USB and erase a blank section on HDD into Apfs  
-install macOS on this Apfs section  
-wait for install complete  
-install Clover on HDD like above   
&emsp;&emsp;--(copy and paste Clover files in EFI will boot, but press F4 at Clover bootloader won't generate ACPI files for you to patch later, so you need to INSTALL it)  
-patch DSDT/SSDT like [fengwenhua's repo](https://github.com/fengwenhua/dell-7559-hackintosh)

## 3.0 Results   
>What's not working:  
&emsp;-F1/F2 to adjust backlight (though refered repo says it's working,emm..)  
&emsp;-Intel 3165 wifi  
&emsp;-Subwoofer  
&emsp;-NTFS mount in read & write (that's also a real mac problem)  
&emsp;-FaceTime/Message

>What's confusing:  
&emsp;-CPU fan too lazy to work  
&emsp;-CPU-S report up to 3200 MHz turbo, but Intel Power gadget report no higher than 3000 MHz during CPU-S testing

>What's working:  
-well, all others, pretty good

