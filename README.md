
$\color{red}{\textsf{1. create the lvm partition :}}$

- lsblk -f

- sudo pvcreate /dev/xvdf

- sudo vgcreate vg1 /dev/xvdf

- sudo lvcreate -L 10G -n lv1 vg1

- sudo mkfs.ext4 /dev/vg1/lv1

- sudo mkdir -p /opt/application

- sudo mount /dev/vg1/lv1 /opt/application  

$\color{green}{\textsf{Add this below line on "/etc/fstab" file for pemanent mount:}}$

- /dev/vg1/lv1  /opt/application  ext4  defaults  0  2

- df -h /opt/application


$\color{red}{\textsf{2. Extend the lvm partition :}}$

- lsblk -f

- sudo pvcreate /dev/xvdg

- sudo vgextend vg1 /dev/xvdg

- sudo lvextend -L +10G /dev/vg1/lvm1

- sudo resize2fs /dev/vg1/lvm1

- df -h /opt/application

$\color{red}{\textsf{3. Decrease the lvm partition :}}$

- sudo umount /opt/application

- sudo e2fsck -f /dev/vg1/lvm1

- sudo resize2fs /dev/vg1/lvm1 15G

- sudo lvreduce -L 15G /dev/vg1/lvm1

- sudo mount /dev/vg1/lvm1 /opt/application

- df -h /opt/application
  
- lvdisplay /dev/vg1/lvm1

$\color{red}{\textsf{3. Add additional disk and increase the VG and lvm partition :}}$

Note: (The LV can be extended only by a single VG, so we need to attach all PV's with a single VG)

- sudo vgextend vg1 /dev/xvdb

- lvextend -l +100%FREE /dev/vg1/lv1




