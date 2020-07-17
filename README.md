#debian-usb-boot-grub-ext4-swap READMD.md

WARNING !!! **The Improper Use of the Linux dd command and/or Gparted can destroy your data and even hard drives** 
		Aways launch gparted with "sudo gparted /dev/sdxX (x for usb device name is usually /dev/sdb, /dev/sdc, etc. Could also be /dev/hdb, etc.
		X refers to drive device partition number: (for example) root partition /dev/sdb1 | swap partition /dev/sdb2 (as built in my BASE USB Image)
		Double check dd commands that you are using the correct sdxX - Same in Gparted, top right: /dev/sdx is shown.
		
The usb-debian-grub-ext4-swap.img is only 1MB in size but, is the BASE (See BASE comment) to create Master Boot Record, Grub, 11GB ext4 and 3GB swap partitons on a USB Stick. All you do is add the filesystem via dd command to /dev/sdxX; modify a few files after your file system is written to USB BASE Stick, reboot, update initramfs and grub2 (all explained below) and you can distribute your own Custom Distro on a USB Stick. 

(FUTURE TO DO: Automated YAD GUI - Bash Script to handle all terminal commands. Automate reducing image size of the Finished Custom Distro USB Stick)


**BASE Comment: BASE as being defined as, "missing the required Linux OS filesystem from ext4 partition on /dev/sdx1.

The BASE image does NOT include a filesystem in its ext4 (root) partition, you must add your own complete customized Debian System
If your file system is different than type ext4, use Gparted to reformat the current ext4 partition to your file system type.

See pdf Tutorial for more information: https://github.com/godistro/debian-usb-boot-grub-ext4-swap/blob/master/Docs/GoDistro-base-usb-tutorial.pdf
     
     
Note: Do not distribute custom logos or images of your base LinuxOS and include the required License files for all non-free programs. Do not distribute Google-Chrome --> Use Chromium. See terms of "ALL" required licenses as well. If you choose to a Respin of Sparkylinux, you are required to include this statement where is obvious:

"This is an UnOfficial Respin of Sparky Linux and it is NOT SUPPORTED BY the Author and his Development Team or Sparkylinux Community."

==============

**Disclaimer: YOU MUST ACCEPT AND AGREE TO TERMS OF THIS DISCLAIMER: 

Your use and/or continued use of any GoDistro and/or GoPortal information, et-al, is proof of your complete and absolute acceptance and agreement to our Disclaimer terms and conditions.

This is an experimental process for installing a modified Debian based LinuxOS build on to a USB Stick. As such, you must not use this process unless you accept 100% responsiblity for your actions and any and all possible consequences that could result known and unknown now or in the future. You must agree to release author, Robert J. Cooper, Nevada, USA from any and all responsibilty for your use of any part of this process. This Disclaimer and document is subject to change without any prior notice of anykind to the extent allowed by applicable laws.  Any possible claims to be arbitrated under the laws of Nevada, USA. You must read and accept terms of GPL 3.0 License.

License Granted:  GPL 3.0 --> https://www.gnu.org/licenses/gpl-3.0.en.html

================

     ]]\\\


