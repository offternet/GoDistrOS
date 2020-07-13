#debian-usb-boot-grub-ext4-swap READMD.md

The usb-debian-grub-ext4-swap.img is only 1MB in size but, is the BASE (See BASE comment) to create Master Boot Record, Grub, 11GB ext4 and 3GB swap partitons on a USB Stick. All you do is add the filesystem via dd command to /dev/sdbX (X represents the drive device name for your USB Stick); modify a few files after file system is installed on USB Stick, reboot, update initramfs and grub2 ( all explained below) and you can distribute your own Custom Distro on a USB Stick. 

(FUTURE TO DO: Automated YAD GUI - Bash Script to handle all terminal commands.)


BASE Comment: BASE as being defined as, "missing an OS filesystem from ext4 partition /dev/sdX that contians a Debian Linux OS.

This image does NOT include a filesystem in its ext4 (root) partition, you must add your own complete customized Debian System
If your file system is different than ext4 type, use Gparted to reformat the ext4 partition to your file system.

1. Download debian-usb-boot-grub-ext4-swap-master.zip:
	Click "Code" ---> Click "Download ZIP"

2. Unzip it, in Linux Terminal: 
    cd ~/Dowloads (or where the file was downloaded on your system)
    sudo unzip ./debian-usb-boot-grub-ext4-swap-master.zip 
    (File will be unzipped to a directory (folder) with the name of: debian-usb-boot-grub-ext4-swap-master
    cd debian-usb-boot-grub-ext4-swap-master
    
3. Write the debian-usb-boot-grub-ext4-swap.img file to USB Stick - 16GB (or larger)
    sudo if=./debian-usb-boot-grub-ext4-swap.img of=/dev/sdb

4. Use Gparted to Shrink your custom distro partition all the way except for 25MB or 
	(Preferred way) use dd to truncate hard drive partition as it is written to the usb stick u
  	(ADD MORE ABOUT dd count= and bs= here to get only used block sectors to USB /dev/sdb1)
	
5. Use dd to write your custom distro to /dev/sdb1 (Using /dev/sda2 as an exmple partiton where you built your custom distro)
    sudo if=/dev/sda2 of=/dev/sdb1 bs=4MB count=[number x 4MB total used block sectors on your custom data partition]
    (NEED TO ADD MORE EXPLAIN HERE)
    Or if you shrunk your custom distro partition use this command:
    sudo if=/dev/sda2 of=/dev/sdb1 bs=4M status=progress && sync

6. Open Gparted and create new uudi number for ext4 and swap partitions on USB Stick after distro is written to /dev/sdb1
    sudo gparter /dev/sdb
    Select ext4 partition
	    Ckick Partition --> Click Check	--> Click Green Checkmark
  	  Click Close
	  Select Swap partition
	    Click Partition --> Click New UUID --> Click Green Checkmark
	    CLick Close 
	  Exit Gparted
  
7. 5. Insert Correct uuid numbers in 2 critical files of partition /dev/sdb1

	A. sudo blkid 
		Find uuid for ext4 Partition sdb1 (Root) (goes in /etc/initramfs-tools/conf.d/resume and /etc/fsab files
		Find uuid for swap partition sdb2 (swap) (goes in /etc/fstab file)

	B. sudo nano /etc/initramfs-tools/conf.d/resume) (Use arrow keys, then backspace to delete, then use mouse to paste correct uuid number)
	   	(Will be this format: RESUME=UUID=number-here-uuid-for-root-sdb1)
		Save & Exit: CTRL+o / CTRL+x

	C. sudo nano /etc/fstab

	   (----Will be this format: 

		# /etc/fstab: static file system information.
		#
		# <file system> <mount point>   <type>  <options>       <dump>  <pass>
		
		# root /dev/sda1
		UUID=here-uuid-root-sdb1	/	ext4	errors=remount-ro,defaults	0	1
		# swap /dev/sda6
		UUID=here-uuid-swap-sdb2	none	swap	sw	0	0
		# cdrom
		/dev/cdrom	/media/cdrom0	udf,iso9660	user,noauto,exec,utf8	0	0
	   ----)

	Save: CTRL+o / then exit Nano: CTRL+x

	D. Write Down uuid for (root) sdb1. We will put in several locations in /boot/grub/grub.cfg

	E. sudo /boot/grub/grub.cfg 
		(Replace existing uuid numbrer above the "menuentry" and in the 1st "menuentry" section but, not in submenuentry)

		Save: CTRL+o / then exit Nano: CTRL+x

	F. Disable 30_os-prober in Grub2 (this will prevent hard drive partitions listed on USB Stick)

		sudo chmod -x /etc/grud.d/30_os-prober

	G. Reboot Computer

8. Boot from USB Stick

  Login as you normally do on your custom distro.
  
	Open terminal and update initramfs and grub:

		sudo update-initramfs -u

		sudo update grub (Since 

9. Distribute your Custom Distro USB to friends and family. or use gzip to make small img of whole USB Stick
	(Note: Do not distribute custom logos or images and include License files for all non-free programs. See terms of these licenses as well.)

10. [FUTURE: Process to write null characters to unused space and swap partition so Gzip will create smaller compressed image of completed Distributable Custom Distribution]
     
     ]]\\\


