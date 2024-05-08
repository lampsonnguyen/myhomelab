# myhomelab
Collection of linux commands when I set up my homelab


Use Your Default Free Space

checking your root filesystem free space 

* df -h

To check for existing free space on your Volume Group (where it is left by the installer default settings), run the command 

* vgdisplay

* sudo lvextend -l 100%VG ubuntu-vg/ubuntu-lv

* fdisk -l /dev/mapper/ubuntu--vg-ubuntu--lv


* sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv