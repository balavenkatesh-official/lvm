# 1. create the lvm partition :


#### List available disks :
```bash
lsblk
```

#### Create a physical volume :
```bash
sudo pvcreate /dev/xvdf
```

#### Create a volume group :
```bash
sudo vgcreate vg1 /dev/xvdf
```

#### Create a logical volume :
```bash
sudo lvcreate -L 10G -n lv1 vg1
```

#### Format the logical volume :
```bash
sudo mkfs.ext4 /dev/vg1/lv1
```

#### Create a mount point directory :
```bash
sudo mkdir -p /opt/application
```

#### Mount the logical volume :
```bash
sudo mount /dev/vg1/lv1 /opt/application
```

#### Edit /etc/fstab to add the following line :
```bash
/dev/vg1/lv1  /opt/application  ext4  defaults  0  2
```

#### Verify the setup :
```bash
df -h /opt/application
```

