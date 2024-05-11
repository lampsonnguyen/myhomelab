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

Install KVM Packages
* sudo apt install cockpit -y

* sudo apt install cockpit-machines
* sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
* sudo apt install virt-manager
* sudo systemctl start libvirtd
* sudo systemctl start Cockpit

Authorize Users 

* sudo adduser ‘username’ libvirt
* sudo adduser ‘[username]’ kvm

Verify the Installation
* virsh list --all

* sudo systemctl status libvirtd


set up auto start expressvpn 
sudo nano /usr/sbin/smartexpressvpn.sh

smartexpressvpn.sh
#!/bin/bash
expressvpn disconnect
expressvpn refresh
expressvpn list | tail -n+3 | column -ts $'t' | sed 's/   */:/g' > data.tmp
cat data.tmp | while read LINE
do
        if [ `echo $LINE | tail -c 2` == 'Y' ]; then
                TEMP=`echo $LINE | grep : | awk -F: '{print $1}'`
                echo "$TEMP" >> array.tmp
        fi
done
ARRAY_SIZE=`wc -l array.tmp | awk {'print $1'}`
RND_VPN=`shuf -i 1-$ARRAY_SIZE -n 1`
VPN=`sed "${RND_VPN}q;d" array.tmp`
rm -f data.tmp
rm -f array.tmp
expressvpn connect $VPN
---


sudo chmod +x /usr/sbin/smartexpressvpn.sh

then add this to crontab
sudo crontab -e
@reboot /usr/sbin/smartexpressvpn.sh