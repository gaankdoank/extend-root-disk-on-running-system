# extend-root-disk-on-running-system
Extend Root partition LVM space on running system


1. Create new partition (ex: /dev/sda3) from unallocated space. I am  use “cfdisk” and type LVM / 8E <br>
2. Check partition applied or not > “cat /proc/partitions”, if /dev/sda3 not shown, apply first > “partprobe /dev/sda” then check it again <br>
3. Create psychal volume > “pvcreate /dev/sda3” <br>
4. Extend volume group > “vgextend centos /dev/sda3” <br>
5. Extend root partition > “lvextend -l +100%FREE /dev/mapper/centos-root” <br>
6. Apply via resize2fs > “resize2fs /dev/mapper/centos-root” <br>
7. Apply via xfs > “xfs_growfs /dev/mapper/centos-root” <br>
