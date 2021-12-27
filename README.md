# extend-root-disk-on-running-system
Extend Root partition LVM space on running system

Type _lsblk_ and see where your partition attached on same disk or not. If you have at least 1 partition not used on same disk go following to number 1 step.
And if you adding physichal disk, run this :
_fdisk /dev/sdb_
See the screenshot for the options you should pick
_n_ (new partition)
_p_ (primary)
(Press ENTER) (Use default partition number)
(Press ENTER) (Use default first sector)
(Press ENTER) (Use default last sector)
_t_ (change the partition type)
_8e_ (Linux LVM)
_w_ (write) 
Continue to number 1 step.

1. Create new partition (ex: /dev/sda3) from unallocated space. I am  use “cfdisk” and type LVM / 8E <br>
2. Check partition applied or not > “cat /proc/partitions”, if /dev/sda3 not shown, apply first > “partprobe /dev/sda” then check it again <br>
3. Create psychal volume > “pvcreate /dev/sda3” <br>
4. Extend volume group > “vgextend centos /dev/sda3” <br>
5. Extend root partition > “lvextend -l +100%FREE /dev/mapper/centos-root” <br>
6. Apply via resize2fs > “resize2fs /dev/mapper/centos-root” <br>
7. Apply via xfs > “xfs_growfs /dev/mapper/centos-root” <br>
