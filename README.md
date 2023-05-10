Домашнее задание: работа с mdadm

Задание:

• добавить в Vagrantfile еще дисков

• собрать R0/R5/R10 на выбор

• прописать собранный рейд в конф, чтобы рейд собирался при загрузке

• сломать/починить raid 

• создать GPT раздел и 5 партиций и смонтировать их на диск.


1. Сначала качаем готовый vagrantfile по ссылке из методички
2. Далее его редактируем, в моем случае я буду делать 10 рейд массив из 6 дисков по 250 мб

 :sata1 => {
                        :dfile => './sata1.vdi',
                        :size => 250,
                        :port => 1
                },
                :sata2 => {
                        :dfile => './sata2.vdi',
                        :size => 250, # Megabytes
                        :port => 2
                },
                :sata3 => {
                        :dfile => './sata3.vdi',
                        :size => 250,
                        :port => 3
                },
                :sata4 => {
                        :dfile => './sata4.vdi',
                        :size => 250, # Megabytes
                        :port => 4
                },
                :sata5 => {
                        :dfile => './sata5.vdi',
                        :size => 250,
                        :port => 5
                },
                :sata6 => {
                        :dfile => './sata6.vdi',
                        :size => 250, # Megabytes
                        :port => 6
                }


3. Запускаем наш vagrantfile

----------------------------------------------------------------------------------------------------------
user@ubuntu-vm:~/DZ-OTUS/DZ-2$ nano vagrantfile
user@ubuntu-vm:~/DZ-OTUS/DZ-2$ vagrant up
Bringing machine 'otuslinux' up with 'virtualbox' provider...
==> otuslinux: Importing base box 'centos/7'...
==> otuslinux: Matching MAC address for NAT networking...
==> otuslinux: Checking if box 'centos/7' version '2004.01' is up to date...
==> otuslinux: Setting the name of the VM: DZ-2_otuslinux_1683750256746_74131
==> otuslinux: Fixed port collision for 22 => 2222. Now on port 2200.
==> otuslinux: Clearing any previously set network interfaces...
==> otuslinux: Preparing network interfaces based on configuration...
    otuslinux: Adapter 1: nat
    otuslinux: Adapter 2: hostonly
==> otuslinux: Forwarding ports...
    otuslinux: 22 (guest) => 2200 (host) (adapter 1)
==> otuslinux: Running 'pre-boot' VM customizations...
==> otuslinux: Booting VM...
==> otuslinux: Waiting for machine to boot. This may take a few minutes...
    otuslinux: SSH address: 127.0.0.1:2200
    otuslinux: SSH username: vagrant
    otuslinux: SSH auth method: private key
    otuslinux:
    otuslinux: Vagrant insecure key detected. Vagrant will automatically replace
    otuslinux: this with a newly generated keypair for better security.
    otuslinux:
    otuslinux: Inserting generated public key within guest...
    otuslinux: Removing insecure key from the guest if it's present...
    otuslinux: Key inserted! Disconnecting and reconnecting using new SSH key...
==> otuslinux: Machine booted and ready!
==> otuslinux: Checking for guest additions in VM...
    otuslinux: No guest additions were detected on the base box for this VM! Guest
    otuslinux: additions are required for forwarded ports, shared folders, host only
    otuslinux: networking, and more. If SSH fails on this machine, please install
    otuslinux: the guest additions and repackage the box to continue.
    otuslinux:
    otuslinux: This is not an error message; everything may continue to work properly,
    otuslinux: in which case you may ignore this message.
==> otuslinux: Setting hostname...
==> otuslinux: Configuring and enabling network interfaces...
==> otuslinux: Rsyncing folder: /home/user/DZ-OTUS/DZ-2/ => /vagrant
==> otuslinux: Running provisioner: shell...
    otuslinux: Running: inline script
    otuslinux: Loaded plugins: fastestmirror
    otuslinux: Determining fastest mirrors
    otuslinux:  * base: de.mirrors.clouvider.net
    otuslinux:  * extras: mirror.23m.com
    otuslinux:  * updates: mirror.eu.oneandone.net
    otuslinux: Resolving Dependencies
    otuslinux: --> Running transaction check
    otuslinux: ---> Package gdisk.x86_64 0:0.8.10-3.el7 will be installed
    otuslinux: ---> Package hdparm.x86_64 0:9.43-5.el7 will be installed
    otuslinux: ---> Package mdadm.x86_64 0:4.1-9.el7_9 will be installed
    otuslinux: --> Processing Dependency: libreport-filesystem for package: mdadm-4.1-9.el7_9.x86_64
    otuslinux: ---> Package smartmontools.x86_64 1:7.0-2.el7 will be installed
    otuslinux: --> Processing Dependency: mailx for package: 1:smartmontools-7.0-2.el7.x86_64
    otuslinux: --> Running transaction check
    otuslinux: ---> Package libreport-filesystem.x86_64 0:2.1.11-53.el7.centos will be installed
    otuslinux: ---> Package mailx.x86_64 0:12.5-19.el7 will be installed
    otuslinux: --> Finished Dependency Resolution
    otuslinux:
    otuslinux: Dependencies Resolved
    otuslinux:
    otuslinux: ================================================================================
    otuslinux:  Package                  Arch       Version                  Repository   Size
    otuslinux: ================================================================================
    otuslinux: Installing:
    otuslinux:  gdisk                    x86_64     0.8.10-3.el7             base        190 k
    otuslinux:  hdparm                   x86_64     9.43-5.el7               base         83 k
    otuslinux:  mdadm                    x86_64     4.1-9.el7_9              updates     439 k
    otuslinux:  smartmontools            x86_64     1:7.0-2.el7              base        546 k
    otuslinux: Installing for dependencies:
    otuslinux:  libreport-filesystem     x86_64     2.1.11-53.el7.centos     base         41 k
    otuslinux:  mailx                    x86_64     12.5-19.el7              base        245 k
    otuslinux:
    otuslinux: Transaction Summary
    otuslinux: ================================================================================
    otuslinux: Install  4 Packages (+2 Dependent packages)
    otuslinux:
    otuslinux: Total download size: 1.5 M
    otuslinux: Installed size: 4.3 M
    otuslinux: Downloading packages:
    otuslinux: Public key for hdparm-9.43-5.el7.x86_64.rpm is not installed
    otuslinux: warning: /var/cache/yum/x86_64/7/base/packages/hdparm-9.43-5.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
    otuslinux: Public key for mdadm-4.1-9.el7_9.x86_64.rpm is not installed
    otuslinux: --------------------------------------------------------------------------------
    otuslinux: Total                                              1.7 MB/s | 1.5 MB  00:00
    otuslinux: Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    otuslinux: Importing GPG key 0xF4A80EB5:
    otuslinux:  Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
    otuslinux:  Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
    otuslinux:  Package    : centos-release-7-8.2003.0.el7.centos.x86_64 (@anaconda)
    otuslinux:  From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
    otuslinux: Running transaction check
    otuslinux: Running transaction test
    otuslinux: Transaction test succeeded
    otuslinux: Running transaction
    otuslinux:   Installing : libreport-filesystem-2.1.11-53.el7.centos.x86_64             1/6
    otuslinux:   Installing : mailx-12.5-19.el7.x86_64                                     2/6
    otuslinux:   Installing : 1:smartmontools-7.0-2.el7.x86_64                             3/6
    otuslinux:   Installing : mdadm-4.1-9.el7_9.x86_64                                     4/6
    otuslinux:   Installing : hdparm-9.43-5.el7.x86_64                                     5/6
    otuslinux:   Installing : gdisk-0.8.10-3.el7.x86_64                                    6/6
    otuslinux:   Verifying  : mdadm-4.1-9.el7_9.x86_64                                     1/6
    otuslinux:   Verifying  : 1:smartmontools-7.0-2.el7.x86_64                             2/6
    otuslinux:   Verifying  : gdisk-0.8.10-3.el7.x86_64                                    3/6
    otuslinux:   Verifying  : mailx-12.5-19.el7.x86_64                                     4/6
    otuslinux:   Verifying  : hdparm-9.43-5.el7.x86_64                                     5/6
    otuslinux:   Verifying  : libreport-filesystem-2.1.11-53.el7.centos.x86_64             6/6
    otuslinux:
    otuslinux: Installed:
    otuslinux:   gdisk.x86_64 0:0.8.10-3.el7          hdparm.x86_64 0:9.43-5.el7
    otuslinux:   mdadm.x86_64 0:4.1-9.el7_9           smartmontools.x86_64 1:7.0-2.el7
    otuslinux:
    otuslinux: Dependency Installed:
    otuslinux:   libreport-filesystem.x86_64 0:2.1.11-53.el7.centos mailx.x86_64 0:12.5-19.el7
    otuslinux:
    otuslinux: Complete!
----------------------------------------------------------------------------------------------------------


4. Подключаемся к запущенной вирт машине vagrant ssh

5. Командой sudo lshw -short | grep disk смотрим какие блочные устройства у нас есть исходя из их кол-ва

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo lshw -short | grep disk
/0/100/1.1/0.0.0    /dev/sdg   disk        42GB VBOX HARDDISK
/0/100/d/0          /dev/sda   disk        262MB VBOX HARDDISK
/0/100/d/1          /dev/sdb   disk        262MB VBOX HARDDISK
/0/100/d/2          /dev/sdc   disk        262MB VBOX HARDDISK
/0/100/d/3          /dev/sdd   disk        262MB VBOX HARDDISK
/0/100/d/4          /dev/sde   disk        262MB VBOX HARDDISK
/0/100/d/5          /dev/sdf   disk        262MB VBOX HARDDISK
----------------------------------------------------------------------------------------------------------

6. Смотрим более детальную информацию по дискам

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo fdisk -l

Disk /dev/sda: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdd: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sde: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdg: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x0009ef1a

   Device Boot      Start         End      Blocks   Id  System
/dev/sdg1   *        2048    83886079    41942016   83  Linux

Disk /dev/sdb: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdc: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdf: 262 MB, 262144000 bytes, 512000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
----------------------------------------------------------------------------------------------------------

7. Далее зачем то обнуляем суперблоки

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo mdadm --zero-superblock --force /dev/sd{a,b,c,d,e,f}
mdadm: Unrecognised md component device - /dev/sda
mdadm: Unrecognised md component device - /dev/sdb
mdadm: Unrecognised md component device - /dev/sdc
mdadm: Unrecognised md component device - /dev/sdd
mdadm: Unrecognised md component device - /dev/sde
mdadm: Unrecognised md component device - /dev/sdf
[vagrant@otuslinux ~]$

----------------------------------------------------------------------------------------------------------

8. Создаем 10 RAID

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo mdadm --create --verbose /dev/md0 -l 10 -n 6 /dev/sd{a,b,c,d,e,f}
mdadm: layout defaults to n2
mdadm: layout defaults to n2
mdadm: chunk size defaults to 512K
mdadm: size set to 253952K
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
[vagrant@otuslinux ~]$
----------------------------------------------------------------------------------------------------------

9. Проверяем, что RAID собрался нормально

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ cat /proc/mdstat
Personalities : [raid10]
md0 : active raid10 sdf[5] sde[4] sdd[3] sdc[2] sdb[1] sda[0]
      761856 blocks super 1.2 512K chunks 2 near-copies [6/6] [UUUUUU]

unused devices: <none>
[vagrant@otuslinux ~]$ sudo mdadm --create --verbose /dev/md0 -l 10 -n 6 /dev/sd{a,b,c,d,e,f}
mdadm: layout defaults to n2
mdadm: layout defaults to n2
mdadm: chunk size defaults to 512K
mdadm: size set to 253952K
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
[vagrant@otuslinux ~]$ cat /proc/mdstat
Personalities : [raid10]
md0 : active raid10 sdf[5] sde[4] sdd[3] sdc[2] sdb[1] sda[0]
      761856 blocks super 1.2 512K chunks 2 near-copies [6/6] [UUUUUU]

unused devices: <none>
[vagrant@otuslinux ~]$ mdadm -D /dev/md0
mdadm: must be super-user to perform this action
[vagrant@otuslinux ~]$ sudo mdadm -D /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Wed May 10 20:45:36 2023
        Raid Level : raid10
        Array Size : 761856 (744.00 MiB 780.14 MB)
     Used Dev Size : 253952 (248.00 MiB 260.05 MB)
      Raid Devices : 6
     Total Devices : 6
       Persistence : Superblock is persistent

       Update Time : Wed May 10 20:45:40 2023
             State : clean
    Active Devices : 6
   Working Devices : 6
    Failed Devices : 0
     Spare Devices : 0

            Layout : near=2
        Chunk Size : 512K

Consistency Policy : resync

              Name : otuslinux:0  (local to host otuslinux)
              UUID : c6a391ac:c7bf1567:a6c59128:b6a4e454
            Events : 17

    Number   Major   Minor   RaidDevice State
       0       8        0        0      active sync set-A   /dev/sda
       1       8       16        1      active sync set-B   /dev/sdb
       2       8       32        2      active sync set-A   /dev/sdc
       3       8       48        3      active sync set-B   /dev/sdd
       4       8       64        4      active sync set-A   /dev/sde
       5       8       80        5      active sync set-B   /dev/sdf

----------------------------------------------------------------------------------------------------------

10. Проверяем компоненты RAID массива

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo mdadm --detail --scan --verbose
ARRAY /dev/md0 level=raid10 num-devices=6 metadata=1.2 name=otuslinux:0 UUID=c6a391ac:c7bf1567:a6c59128:b6a4e454
   devices=/dev/sda,/dev/sdb,/dev/sdc,/dev/sdd,/dev/sde,/dev/sdf
----------------------------------------------------------------------------------------------------------


11. Создаем конфигурационный файл mdadm.conf (но переде этим создадим каталог mdadm, потом сам файл mdadm.conf и дадим
    права на запись пользователю в этот файл

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux ~]$ sudo mkdir /etc/mdadm
[vagrant@otuslinux /]$ cd /etc/mdadm/
[vagrant@otuslinux mdadm]$ sudo touch mdadm.conf
[vagrant@otuslinux mdadm]$ ls
mdadm.conf
[vagrant@otuslinux mdadm]$ sudo chmod 777 mdadm.conf
[vagrant@otuslinux mdadm]$ echo "DEVICE partitions" > /etc/mdadm/mdadm.conf
[vagrant@otuslinux mdadm]$ sudo echo "DEVICE partitions" > /etc/mdadm/mdadm.conf
[vagrant@otuslinux mdadm]$ vi mdadm.conf
----------------------------------------------------------------------------------------------------------

12. Ломаем RAID, помечаем диск fail

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo mdadm /dev/md0 --fail /dev/sda
mdadm: set /dev/sda faulty in /dev/md0
----------------------------------------------------------------------------------------------------------

13. Смотрим на состояние RAID

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ cat /proc/mdstat
Personalities : [raid10]
md0 : active raid10 sdf[5] sde[4] sdd[3] sdc[2] sdb[1] sda[0](F)
      761856 blocks super 1.2 512K chunks 2 near-copies [6/5] [_UUUUU]

[vagrant@otuslinux /]$ sudo mdadm -D /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Wed May 10 20:45:36 2023
        Raid Level : raid10
        Array Size : 761856 (744.00 MiB 780.14 MB)
     Used Dev Size : 253952 (248.00 MiB 260.05 MB)
      Raid Devices : 6
     Total Devices : 6
       Persistence : Superblock is persistent

       Update Time : Wed May 10 21:35:56 2023
             State : clean, degraded
    Active Devices : 5
   Working Devices : 5
    Failed Devices : 1
     Spare Devices : 0

            Layout : near=2
        Chunk Size : 512K

Consistency Policy : resync

              Name : otuslinux:0  (local to host otuslinux)
              UUID : c6a391ac:c7bf1567:a6c59128:b6a4e454
            Events : 19

    Number   Major   Minor   RaidDevice State
       -       0        0        0      removed
       1       8       16        1      active sync set-B   /dev/sdb
       2       8       32        2      active sync set-A   /dev/sdc
       3       8       48        3      active sync set-B   /dev/sdd
       4       8       64        4      active sync set-A   /dev/sde
       5       8       80        5      active sync set-B   /dev/sdf

       0       8        0        -      faulty   /dev/sda

----------------------------------------------------------------------------------------------------------

14. Удаляем неисправный диск из RAID массива

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo mdadm /dev/md0 --remove /dev/sda
mdadm: hot removed /dev/sda from /dev/md0
----------------------------------------------------------------------------------------------------------

15. Добавляем новый диск в RAID массив

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo mdadm /dev/md0 --add /dev/sda
mdadm: added /dev/sda
----------------------------------------------------------------------------------------------------------

16. Проверяем, что RAID собрался и отребилдился, в мойем случае это сделалось мгновенно, т.к. маленькие диски

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ cat /proc/mdstat
Personalities : [raid10]
md0 : active raid10 sda[6] sdf[5] sde[4] sdd[3] sdc[2] sdb[1]
      761856 blocks super 1.2 512K chunks 2 near-copies [6/6] [UUUUUU]

unused devices: <none>
[vagrant@otuslinux /]$ sudo mdadm -D /dev/md0
/dev/md0:
           Version : 1.2
     Creation Time : Wed May 10 20:45:36 2023
        Raid Level : raid10
        Array Size : 761856 (744.00 MiB 780.14 MB)
     Used Dev Size : 253952 (248.00 MiB 260.05 MB)
      Raid Devices : 6
     Total Devices : 6
       Persistence : Superblock is persistent

       Update Time : Wed May 10 21:43:09 2023
             State : clean
    Active Devices : 6
   Working Devices : 6
    Failed Devices : 0
     Spare Devices : 0

            Layout : near=2
        Chunk Size : 512K

Consistency Policy : resync

              Name : otuslinux:0  (local to host otuslinux)
              UUID : c6a391ac:c7bf1567:a6c59128:b6a4e454
            Events : 39

    Number   Major   Minor   RaidDevice State
       6       8        0        0      active sync set-A   /dev/sda
       1       8       16        1      active sync set-B   /dev/sdb
       2       8       32        2      active sync set-A   /dev/sdc
       3       8       48        3      active sync set-B   /dev/sdd
       4       8       64        4      active sync set-A   /dev/sde
       5       8       80        5      active sync set-B   /dev/sdf

----------------------------------------------------------------------------------------------------------

17. Создаем GPT раздел, шесть партиций и монтируем их на диск

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo parted -s /dev/md0 mklabel gpt

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 0% 15%
Information: You may need to update /etc/fstab.

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 15% 30%
Information: You may need to update /etc/fstab.

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 30% 45%
Information: You may need to update /etc/fstab.

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 45% 60%
Information: You may need to update /etc/fstab.

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 60% 75%
Information: You may need to update /etc/fstab.

[vagrant@otuslinux /]$ sudo parted /dev/md0 mkpart primary ext4 75% 100%
Information: You may need to update /etc/fstab.
----------------------------------------------------------------------------------------------------------

18. Создаем файловую систему на партициях

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ for i in $(seq 1 6); do sudo mkfs.ext4 /dev/md0p$i; done
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
28112 inodes, 112128 blocks
5606 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33685504
14 block groups
8192 blocks per group, 8192 fragments per group
2008 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
28800 inodes, 115200 blocks
5760 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33685504
15 block groups
8192 blocks per group, 8192 fragments per group
1920 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
28448 inodes, 113664 blocks
5683 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33685504
14 block groups
8192 blocks per group, 8192 fragments per group
2032 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
28800 inodes, 115200 blocks
5760 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33685504
15 block groups
8192 blocks per group, 8192 fragments per group
1920 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
28448 inodes, 113664 blocks
5683 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33685504
14 block groups
8192 blocks per group, 8192 fragments per group
2032 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=512 blocks, Stripe width=1536 blocks
47232 inodes, 188928 blocks
9446 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=33816576
24 block groups
8192 blocks per group, 8192 fragments per group
1968 inodes per group
Superblock backups stored on blocks:
        8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
----------------------------------------------------------------------------------------------------------

19. Монтируем партиции по каталогам

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo mkdir -p /raid/part{1,2,3,4,5,6}
[vagrant@otuslinux /]$ for i in $(seq 1 6); do sudo mount /dev/md0p$i /raid/part$i; done
----------------------------------------------------------------------------------------------------------

20. Проверяем результат

----------------------------------------------------------------------------------------------------------
[vagrant@otuslinux /]$ sudo df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        489M     0  489M   0% /dev
tmpfs           496M     0  496M   0% /dev/shm
tmpfs           496M  6.8M  489M   2% /run
tmpfs           496M     0  496M   0% /sys/fs/cgroup
/dev/sdg1        40G  4.7G   36G  12% /
tmpfs           100M     0  100M   0% /run/user/1000
tmpfs           100M     0  100M   0% /run/user/0
/dev/md0p1      103M  1.6M   93M   2% /raid/part1
/dev/md0p2      105M  1.6M   96M   2% /raid/part2
/dev/md0p3      104M  1.6M   95M   2% /raid/part3
/dev/md0p4      105M  1.6M   96M   2% /raid/part4
/dev/md0p5      104M  1.6M   95M   2% /raid/part5
/dev/md0p6      175M  1.6M  161M   1% /raid/part6
----------------------------------------------------------------------------------------------------------















