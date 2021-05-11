# Linux filesystem

## hierarchy

1. disk
2. physical volume
3. volume group
4. logical volume
5. filesystem / mount point

## mount a logical vol

1. create logical volume on volume group
2. check where it is created under /dev/
3. formate the logical volume
4. mount volume (can be anyhere is not restricted to root / level of filesystem)
5. (optional) add mount to fstab file so it will recreated at startup

```
# 1. 
sudo lvcreate -L 100G -n <new logical volume> <volume group> 

# 2. 
sudo lvscan

# 3. path can be found via step 2
sudo mkfs.ext4 /dev/<volume group>/<logical volume> 

#4  
sudo mount /dev/<volume group>/<logical volume> /<directory_which_exists>

```

## extend a logical volume

1. check how much space is left on volume group 
2. check where the loigcal volume is located under /dev/ (not /dev/mapping but the real path)
3. extend logical volume 
4. check if successful


```shell
# 1.
vgs

# 2. 
lvscan

# 3. path can be found via step 2
# -L50G is target size 50 GB
lvextend -L50G /dev/<volume group>/<logical volume> 


# 4.
lvscan
```

## fstab

/etc/fstab is responsible for mounting volumes on startup.

- always create a backup : ` sudo cp /etc/fstab /etc/fstab.backup`
- before restarting check if fstab is ok. If there are no returned messages everything is okay: `sudo mount -a`

## mount

- a mount point is just a or folder/directory (e.g. mkdir -p /data )
- you do not need to use the /mnt directory. It is just a convention to use it if you do not have a specific directory to mount  
- you can mount formatted devices under /dev to any mountpoint 
- to make a mount persistant after restart you need to add it to /etc/fstab 

## List stuff

```shell
df -h

du -g

# list physical volumes
pvs

# list volume groups
vgs

# list logical volume
lvs

```

## symbolic links vs. hard links

symbolic links (/soft links/symlinks) and hard links


```shell
# soft link (symlink)
ln -s source.file link.file


# hard link
ln source.file link.file
```