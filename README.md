# Dual-Boot-Win11-CachyOS
How to Dual Boot Windows 11 25H2 and CachyOS (2025)

When trying to install CachyOS alongside a Windows 11 install, the installation of CachyOS will fail due to the size of the 'System EFI Partiton' being too small.

These are the steps required to make sure CachyOS will install alongside a FRESH Windows 11 installation.

Prerequisites:
- 1x Bootable USB stick with a Windows 11 installation from ISO file (I used Windows 11 25H2 from UUP Dump)
- 1x Bootable USB sick with CachyOS installation from ISO file (I used cachyos-desktop-linux-251129.iso)

(Use rufus to make bootable USB sticks from ISO) // (You can put both ISO's on the 1 USB stick using Ventoy if you prefer, it works fine aswell!)

Steps:
1) Make sure the hard drive is formatted first and is completely blank. You can boot from the CachyOS ISO and do this inside the live environment. I did mine in the BIOS.
2) Boot from the Windows 11 USB Installation USB Stick.
3) When the Windows 11 Installation GUI appears, press SHIFT+10 to open a Command Prompt window.
4) Type these specific commands to create a 2GB 'System EFI Partition':

  **diskpart**<br/>
  **list disk**<br/>
  **select disk x** (where x is the number of the harddrive, eg: 'select disk 0')<br/>
  **convert gpt**<br/>
  **create partition efi size=2048**<br/>
  **format quick fs=fat32**<br/>
  **exit**<br/>

6) Close the Command Prompt window and proceed with the installation.
7) When you get to the section on what HDD to select, you will have two partitions, select the one that says 'unallocated space'

  disk 0 - 2.0gb System EFI Partition

  disk 0 - unallocated space (xxxGB free space) <-------- Install to this partition.

9) Complete the Windows installation, when you get to the desktop feel free to complete initial setup steps, installing drivers and software if required.

Once you have finished the Windows 11 installation (and customised the system if you wish), proceed to boot from the CachyOS installation USB stick, and during the installation, choose 'Install alongside Windows' and drag the slider to the required partition size.<br/>
(I used the system-d boot loader FYI. The others should work, but I know this works perfectly...)

This will fix the error from appearing due to Windows only creating a 128mb/256mb System EFI Parition.

The End :)
