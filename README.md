# Dualbooting Windows10 with Linux

This is a guide for dualbooting your laptop with a linux based os. I made this repo for my own future reference. 

Relevant details about the laptop:  
1. Dell Inspiron 5000 series
2. Preinstalled windows 10
3. NVIDIA Geforce MX250 GPU
4. 512 GB SSD

Important details that need to be checked before starting the dualboot procedure:  
1. SATA mode should be AHCI and nor RAID/IDE(E.g. Intel Rapid Storage Technology)
2. UEFI booting
3. Secure Boot should be disabled

Steps:  
1. Download the iso image of the OS you want to dualboot your system with from the corresponding website.
2. Install Rufus for making the boot device.
3. Run Rufus, settings as GPT and UEFI(non CMS).
4. Allocate some space for your OS in the disk management. 
5. Restart the system.
6. Tap f12.
7. Boot using the USB.
8. Try liveboot first to check if preinstalled nvidia drivers are working.
9. If liveboot does not work try again after appending nomodeset=0 at the end of the linux line in the GRUB.
10. Play around in the liveboot and once sure that everything works fine continue with the installation.

Steps to remove OS from dualboot:
1. Open BIOS settings by tapping on f2 after restarting.
2. Open Boot Options.
3. Remove the boot option that has the Linux OS name.
4. Make Sure Windows boot Manager is at the top of the boot list.
5. Exit from BIOS settings.
6. In windows, open Disk Management and delete the volumes of the partitions that held your OS.
7. Extend your current drives to take in the unallocated space.
8. Restart to check once more.
