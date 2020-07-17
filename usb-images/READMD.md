Currently there are 2 GoDistrOS USB BASE Images.

!!!! "x" in sdx is your USB Drive device number. 

WARNING !!! You must have correct number for "x" that matches your USB Stick or hard drive goes bye, bye)
   
   Open Terminal,  sudo fdisk -l  
     -> displays /dev/sdx device names for both drives and usb sticks 
   
==================

GoDistrOS-USB-11GBext4-4GBswap-1MBimageV1.0.2.img  Image file 
  - is complete ready for partition copy to ext4 partition once written to your USB Stick.

  Delete and Create Partition Table on USB Stick (!!!!! Erases all Data on USB Stick)
  
    sudo Gparted /dev/sdx --> Device --> Create Partiton Table --> Exit
  
  Write GoDistrOS image with Swap Partiton to your USB Stick:
  
      sudo dd if=./GoDistrOS-USB-11GBext4-4GBswap-1MBimageV1.0.2.img of=/dev/sdx1 bs=4MB status=progress && sync
    
   
  Use dd to copy img file or Hard Drive partition to your USB Stick root partiton (ext4) 
    
  (Below example copies sda2 to USB Stick root partition /dev/sdb1)
  
  - Shrink partiton /dev/sda2 as much as possible +100 MB (It can be up to 10.5GB)
    
  (Copy Hard Drive Partiton to USB Stick)
  
      sudo dd if=/dev/sda2 of=/dev/sdb1 bs=4MB status=progress && sync
    
  (Copy dd img file to USB Stick)
    
      sudo dd if=./my-image-file.img of=/dev/sdb1 bs=4MB status=progress && sync
    
  Your Not Done Yet !! See Tutorial as uuids need to be updated in fstab resume and grub.cfg files.
  
  (Tutorial for GoDistro Files)
  https://github.com/godistro/debian-usb-boot-grub-ext4-swap/blob/master/Docs/GoDistro-base-usb-tutorial.pdf
  
===================
  
GoDistrOS-USB-11GBext4-NoSwap-1MBimageV1.0.2.img  This image file does NOT have a Swap file but, has unallocated spave for one.

Follow above procedure and after GoDistrOS-USB-11GBext4-NoSwap-1MBimageV1.0.2.img file is written to your 16GB+ USB ceate a Swap File:

(CREATE SWAP PARTITON)

      sudo gparted /dev/sdx  --> Click Partition --> New --> Partition --> Apply --> Green Checkmark --> Close --> Exit Gparted.
  
  


 
