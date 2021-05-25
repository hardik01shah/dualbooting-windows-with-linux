# Dualbooting Windows10 with Linux

This is a guide for dualbooting your laptop with a linux based os. I made this repo for my own future reference. 

## Relevant details about the laptop:  
1. Dell Inspiron 5000 series
2. Preinstalled windows 10
3. NVIDIA Geforce MX250 GPU
4. 512 GB SSD

## Important details that need to be checked before starting the dualboot procedure:  
1. _SATA mode should be AHCI and nor RAID/IDE(E.g. Intel Rapid Storage Technology)_  
    >To check the SATA mode use Device Manager and check your storage drivers.</br>
    >If the SATA mode is RAID, follow the belo link for conversion to AHCI: (do not use the ALT commands)</br>
    >https://support.thinkcritical.com/kb/articles/switch-windows-10-from-raid-ide-to-ahci
2. _UEFI booting_
3. _Secure Boot should be disabled_
    >Open the boot menu using F2 key(maybe different for different laptops).</br>
    >In the boot options disable secure boot by unchecking it.

## Steps:  
1. Download the iso image of the OS you want to dualboot your system with from the corresponding website.
2. Install Rufus/Ventoy/USBImager/balenoEtcher for preparing the boot media.
3. Run Rufus, settings as GPT and UEFI(non CMS).
4. Allocate some space for your OS in the disk management. 
    >Shrink the drive that has free space.
5. Restart the system.
6. Tap f12.
7. Boot using the USB.
8. Try liveboot first to check if preinstalled nvidia drivers are working.
    >This is not needed for Pop!\_OS. It already has Nvidia drivers installed.</br>
    >Just check if all essential devices work with the OS in the live boot.</br> 
    >Check wifi, bluetooth, speakers, headphones, graphics etc.
9. If liveboot does not work try again after appending nomodeset=0 at the end of the linux line in the GRUB.
    >For more info check this: </br>
    >https://askubuntu.com/questions/747314/is-nomodeset-still-required#:~:text=Highlight%20the%20Ubuntu%20entry%20in,line%20%2D%20press%20F10%20to%20boot.&text=Generally%20it%20is%20recommended%20to,from%20the%20official%20Ubuntu%20repositories.
10. Play around in the liveboot and once sure that everything works fine continue with the installation.
11. In the installation, if you get an option for automatic partitioning i.e. the OS will handle allocation of memory to different partitions, you can go for it.
12. However, in systems like Pop!\_OS, you have to go for a custom install i.e. make the partitions yourself:
    >Make the partitions as follows:</br>
    >1. boot - 512 MiB (EFI)
    >2. swap - 4096 MiB (linux-swap)
    >3. root - whatever space remains (ext4)</br>
    >A further /home partition can be added but it is optional. That too will be ext4.  
13. Systems like Pop!\_OS won't have GRUB as the bootloader, instead they have systemd. 
    >To install GRUB on a Pop!\OS installation follow this link:</br>
    >https://jacci.net/linux/pop-os/how-to-install-grub-on-pop-os-20-04/ 

## Steps to remove OS from dualboot:
1. Open BIOS settings by tapping on f2 after restarting.
2. Open Boot Options.
3. Remove the boot option that has the Linux OS name.
4. Make Sure Windows boot Manager is at the top of the boot list.
5. Exit from BIOS settings.
6. In windows, open Disk Management and delete the volumes of the partitions that held your OS.
7. You will have to delete the /boot partition using cmd.
8. Extend your current drives to take in the unallocated space.
9. Restart to check once more.  
</br>

## References:  
- For Pop!\_OS:
    - Complete tutorial:</br>
         https://www.youtube.com/watch?v=hbzCSjlbInY
         https://forum.bpgc-cte.org/d/111-dualboot-guide-faq-with-pop-os
    - Add windows in the default bootloader of POp!\_OS:</br>
         https://pop-planet.info/forums/threads/copy-the-microsoft-bootloader-into-pops-efi-beginners-guide.357/ 
- For computers with Intel(RST): 
    - https://discourse.ubuntu.com/t/ubuntu-installation-on-computers-with-intel-r-rst-enabled/15347
- For general dualbooting:</br>
    - https://itsfoss.com/install-ubuntu-dual-boot-mode-windows/
    - https://itsfoss.com/install-ubuntu-1404-dual-boot-mode-windows-8-81-uefi/
    - https://www.forbes.com/sites/jasonevangelho/2018/08/29/beginners-guide-how-to-install-ubuntu-linux/?sh=1b28ba6f951c
- For NVIDIA Laptops:
    - https://www.pugetsystems.com/labs/hpc/The-Best-Way-To-Install-Ubuntu-18-04-with-NVIDIA-Drivers-and-any-Desktop-Flavor-1178/
    - https://www.reddit.com/r/Ubuntu/comments/b5tcf7/dualbooting_ubuntu_with_the_latest_nvidia/
    - https://gist.github.com/bitsurgeon/b0f4440984c9e60dcd8fe8bbc346c029
    - https://www.forbes.com/sites/jasonevangelho/2018/08/30/ubuntu-guide-how-to-install-nvidia-drivers-and-play-windows-games-on-linux/?sh=4ab8a17b3a2d

_Note:_</br>
I was getting the below error for ubuntu-based Linux installations(except Pop!\_OS): </br>
```console
Failed to parse WDG method when booting
```
This error arises because the laptop hardware is too new for the old kernels used by Ubuntu. Hopefully this should be fixed in newer releases.</br>
**To prevent this error try installing rolling release distros like arch, openSUSE, fedora, or POP!\_OS(if you want ubuntu based)**
