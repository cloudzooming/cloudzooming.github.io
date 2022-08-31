## Migrate RAID 1 to Snapraid on Openmediavault

I was using Openmediavault for about 10 years from version 2.x, and was using raid 1 all the time. Now I want to replace raid 1 to snapraid to get 
more storage space and flexible management of disks. 

## About Snapraid
Snapraid requires at least two disks to get started. One for data, one for parity, the parity disk must be the largest one amont all the disks.
I've already have 2 4TB drive for the raid 1 at the moment, so I decied to get another 4TB drive for parity. 

### Backup data
First, I need to back all the data from RAID 1 to the new bought 4TB hard drive. There are many ways to do the copy job, but I prefer to using "rsync"
It took hours to finish. 

### Remove one of the drive from RAID 1
check raid storage by 
```
lsblk
```

check details about the raid 1 by running
```
mdadm --detail /dev/md0 
```

this will show the drives of the raid storage

remove one of the drive from raid 1, here I remove /dev/sda
```
mdadm /dev/md0 --fail /dev/sda
```

remove the drive from raid
```
mdadm  /dev/md0 --remove /dev/sda
```

erase the magic flags on drive head
```
mdadm --zero-superblock /dev/sda
```

repeat the steps to remove both drives from raid 


### build snapraid
add the drive with data as data disk to snapraid, and another one as well


add the last drive as parity disk  


### Sync snapraid 


### create cron job to sync data daily

```

```

