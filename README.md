# debian-usb-boot-grub-ext4-swap READMD.md

The usb-debian-grub-ext4-swap.img file will create a bootable USB 16GB stick.  
1. Download usb-debian-grub-ext4-swap.zip file

2. Unzip it, in Linux Terminal: 
    cd (to directory where usb-debian-grub-ext4-swap.zip file is located)
    sudo unzip ./usb-debian-grub-ext4-swap.zip 
    (File will be unzipped to a directory called: (update with real name)
    cd (Update with real action)
    
3. Write debian-usb-boot-grub-ext4-swap.img file to USB Stick - 16GB (or larger)
    sudo if=./usb-debian-grub-ext4-swap.img of=/dev/sdb

4. Use Gparted to Shrink your custom distro partition all the way except for 25MB or use dd to truncate hard drive partition as it is written to the usb stick u
   (NEED TO ADD MORE HERE)
   
5. Use dd to write your custom distro to /dev/sdb1 (Using /dev/sda2 as an exmple partiton where you built your custom distro)
    sudo if=/dev/sda2 of=/dev/sdb1 bs=4MB count=[number x 4MB total used block sectors on your custom data partition]
    (NEED TO ADD MORE EXPLAIN HERE)

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
      
     
     ]]\\\


