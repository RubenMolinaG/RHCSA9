
1. You will have two VMs with CLI as **red.example.com** & **blue.example.com**

2. One of the VM’s password need to reset that is **blue.example.com**

3. You need to break **"root" password** and set password as “**ablerate**” on **red.example.com**

4. You need to set "hostname" according to Examiner.

---
**Note**: you will get 3 disks
1. /dev/vda -> OS Installed
2. /dev/vdb -> To create partition (Pre-created partitions lvm is available)
3. /dev/vdc -> for vdo, Stratis pool,filesystem and snapshots
---

### Perform Task on Red Machine
**Question 1**: Configure TCP/IP and "hostname" as follwing:
- **IP ADDRESS** = 172.25.250.10
- **NETMASK** = 255.255.255.0
- **GATEWAY** = 172.25.250.254
- **DNS** = 172.25.250.254
- **Hostname** = serverX.example.com
```bash
[root@red.example.com]#nmtui (use this command to network configuration)
[root@red.example.com]#hostnamectl set-hostname serverX.example.com
```

**Question 2**: Configure Your red VM repository installed the packages distribution is available via YUM:
- **baseos url** = http://content.example.com/rhel8.2/x86_64/dvd/BaseOS
- **appstream url** = http://content.example.com/rhel8.2/x86_64/dvd/AppStream
```bash
[root@red.example.com]#cd /etc/yum.repos.d
[root@red.example.com]#vim server.repo
[AppStream]
name=yum
baseurl= http://content.example.com/rhel8.2/x86_64/dvd/BaseOS
gpgcheck=0
enabled=1
[BaseOS]
name=base yum
baseurl= http://content.example.com/rhel8.2/x86_64/dvd/AppStream
gpgcheck=0
enabled=1
[root@red.example.com]#yum clean all
[root@red.example.com]#yum repolist
[root@red.example.com]#yum install vim
```
**Question 3**: SELINUX PORT
- Your system httpd service is having some issues. Service is not running on port 82.
- In your system httpd service have some files in /var/www/html (do not change or alter files)
- Solve the port issue.

```bash
[root@red.example.com]#firewall-cmd --permanent --add-service=http
[root@red.example.com]#firewall-cmd --permanent --add-port=82/tcp
[root@red.example.com]#firewall-cmd --reload
[root@red.example.com]#semanage port -l | grep http
[root@red.example.com]#semanage port -a -t http_port_t 82 -p tcp
[root@red.example.com]#semanage port -l | grep http
[root@red.example.com]#firewall-cmd --list-all
```

**Question 4**: Create the following users, groups, and group membership:
- A **group** named **sysadm**.
- A **user** "**harry**" who **belongs to sysadm as a secondary group**.
- A user "**natasha**" who **belongs to sysadm as a secondary group**.
- A user "**sarah**" who does NOT have access to an interactive shell & who is NOT a member of sysadm
- "harry", "natasha", and "sarah" should all have the password of "password".

```bash
[root@red.example.com]#groupadd sysadm
[root@red.example.com]#useradd -G sysadm harry
[root@red.example.com]#useradd -G sysadm natasha
[root@red.example.com]#useradd -s /sbin/nologin sarah
[root@red.example.com]#passwd (set password for all users as given)
```

**Question 5**: Create a collaborative directory "**/shared/sysadm**" with the following characteristics:
- Group ownership of /shared/sysadm is sysadm.
- The directory should be readable, writable, and accessible to member of sysadm, but not to any other user. (It is understood that root has access to all files and directories on the system.)
- Files created in /shared/sysadm automatically have group ownership set to the sysadm group.

```bash
[root@red.example.com]#mkdir -p /shared/sysadm
[root@red.example.com]#chgrp sysadm /shared/sysadm
[root@red.example.com]#chmod 2770 /shared/sysadm
```

**Question 6**: Set The Cron Job for the user "Natasha" that should runs daily every 1 minutes local time and executes "Ex200 Testing" with logger.

```bash
[root@red.example.com]#crontab -e -u natasha
*/2 * * * * echo "EX200 Testing"
[root@red.example.com]#systemctl restart crond.service
[root@red.example.com]#systemctl enable crond.service
[root@red.example.com]#crontab -l -u natasha
```

**Question 7**: Configure autofs to automount the home directories of netuserX user. Note the following:
- netuserX home directory is exported via NFS, which is available on classroom.example.com (172.25.254.254) and your NFS-exports directory is /netdir/netuserX for netuserX,
- netuserX's home directory should be automounted using autofs service.
- home directories must be writable by their users.

```bash
[root@red.example.com]#rpm -qa autofs
[root@red.example.com]#yum install autofs
[root@red.example.com]#systemctl restart autofs.service
[root@red.example.com]#systemctl enable autofs.service
[root@red.example.com]#vim /etc/auto.master
/netdir /etc/auto.misc
[root@red.example.com]#vim /etc/auto.misc
netuserX -fstype=nfs,rw classroom.example.com:/home/guests/netuserX
[root@red.example.com]#su - netuserX
```

**Question 8**: Create a tar archive of "/etc/" Directory with .bzip2 extension. Tar archive named "myetcbackup.tar.bz2" should be place in "/root/" Directory.
```bash
[root@red.example.com]#tar -cvjf /root/myetcbackup.tar.bz2 /etc
```

**Question 9**: Copy the file /etc/fstab to /var/tmp. Configure the permissions of /var/tmp/fstab so that:
- the file /var/tmp/fstab is owned by the root user
- the file /var/tmp/fstab belong to the group root
- the file /var/tmp/fstab should not be execubable by anyone
- the user "natasha" is able to read and write /var/tmp/fstab
- the user "harry" can neither write nor read /var/tmp/fstab
- all other users (current or future) have the ability to read /var/tmp/fstab

```bash
[root@red.example.com]#cp /etc/fstab /var/tmp/
[root@red.example.com]#cd /var/tmp/
[root@red.example.com]#getfacl fstab
[root@red.example.com]#setfacl -m u:natasha:rw- fstab
[root@red.example.com]#setfacl -m u:harry:--- fstab
[root@red.example.com]#getfacl fstab
```

**Question 10**: Configure your system to syncronize the time from form "classroom.example.com".

```bash
[root@red.example.com]#rpm -qa chrony
[root@red.example.com]#vim /etc/chrony.conf
pool classroom.example.com iburst
[root@red.example.com]#systemctl restart chronyd.service
[root@red.example.com]#chronyc sources -v
```

**Question 11**: Find all files and directories which is created by a user "natasha" in to this system and copy it into a "/root/natashafiles" directory.

```bash
[root@red.example.com]#mkdir natashafile
[root@red.example.com]#find / -user natasha -exec cp -rvp {} /root/natashafile/ \; 2> /dev/null
```

**Question 12**: Find all strings "ich" from "/usr/share/dict/words" file and copy that strings in a /root/lines file.

```bash
[root@red.example.com]#grep -o ich /usr/share/dict/words > /root/list
```

**Question 13**: Create a user "unilao" with UID "2334" with password as "ablerate".

```bash
[root@red.example.com]#useradd -u 2334 unalio
[root@red.example.com]#passwd unalio
```

**Question 14**: run container as a regular user "charlie" , autostart container and run container as a service. Details as follows:
- **Image Name** -> rsyslog
- **Container Name** -> logserver
- **Registry** -> registry.lab.example.com
- **Registry Login Details**: **Username**: admin | **Password**: redhat321

```bash
[root@red.example.com]#ssh charlie@localhost
[charlie@red.example.com]$podman login registry.lab.example.com
Username: admin
Password: redhat321
[charlie@red.example.com]$podman search rsyslog
[charlie@red.example.com]$podman run -d --name logserver rsyslog
[charlie@red.example.com]$podman images
[charlie@red.example.com]$podman container list
[charlie@red.example.com]$mkdir -p ~/.config/systemd/user
[charlie@red.example.com]$cd ~/.config/systemd/user
[charlie@red.example.com]$podman generate systemd --name logserver --files
[charlie@red.example.com]$systemctl --user daemon-reload
[charlie@red.example.com]$podman stop logserver
[charlie@red.example.com]$systemctl --user start container-logserver
[charlie@red.example.com]$systemctl --user enable container-logserver
[charlie@red.example.com]$podman ps
[charlie@red.example.com]$loginctl enable-linger
[charlie@red.example.com]$loginctl show-user username
```

**Question 15**: Configure **journalctl** logs persistance storage

```bash
[root@red.example.com]#vim /etc/systemd/journald.conf
[journal]
Storage = persistent
[root@red.example.com]#systemctl restart system-journald.service
[root@red.example.com]#**journalctl --flush**
```
**Question 16**: Create a directory /home/charlie/container_journal and mount it on the running container logserver. Copy the logs of /var/log/journal to the /home/charlie/container_journal

```bash
[charlie@red.example.com]$mkdir /home/username/container_journal
[charlie@red.example.com]$podman run –d –v /home/charlie/container_journal:/var/log/journal:Z --name logserver rsyslog
[root@red.example.com]#cp -rv /var/log/journal/* /home/username/container_journal
```

**Question 17**: Scripting question
Create a script with name myscript.sh in /mnt directory Which will find all the files in /usr directory whose size is more than 30 kb and less than 50 kb in and store it in /root/myfile.

```bash
[root@red.example.com]#vim myscript.sh
#!/bin/bash
mkdir /root/myfile
find /usr -type f -size +30k -a -size -50k -exec cp "{}" /root/myfile \;
[root@red.example.com]#chmod u+x myscript.sh
[root@red.example.com]#./myscript.sh
```

Write a script with name myscript.sh . Place it in the location /usr/local/bin. When the script runs it should search for all files under /usr With file size less than 10M and special group permission set.

```bash
[root@red.example.com]#vim myscript.sh
#!/bin/bash
mkdir /root/myfile
find /usr -type f -size -10M -a -perm /2000 -exec cp "{}" /root/myfile \;
[root@red.example.com]#chmod u+x myscript.sh
[root@red.example.com]#./myscript.sh
```

---

### Perform Task on Blue Machine

**Question 1**: Break root password and set "root" password to "ablerate"
1. Reboot blue.example.com
2. Use the cursor keys to highlight the default boot-loader entry.
3. Press "**e**" to edit the current entry.
4. Use the cursor keys to navigate to the line that starts with linux.
5. Press End to move the cursor to the end of the line.
6. Append rd.break to the end of the line.
7. **Press Ctrl+x** to boot using the modified configuration
```bash
switch_root:/# mount -o remount,rw /sysroot
switch_root:/# chroot /sysroot
sh-4.4# passwd root
sh-4.4# touch /.autorelabel
sh-4.4#exit
switch_root:/#exit
```

**Question 14**: Configure Your blue VM repository installed the packages distribution is available via YUM:
- baseos url = http://content.example.com/rhel8.2/x86_64/dvd/BaseOs
- appstream url= http://content.example.com/rhel8.2/x86_64/dvd/Appstream
  
**Question 15**: Create an LVM name engineering from storage volume group. Note the following:
- PE size should be 16MB
- LVM size should be 100 extents
- Format with "vfat" file system and mount it permanent under /mnt/lvm.

```bash
[root@red.example.com]#fdisk /dev/vdb -> n -> type -> +2000M -> select type LVM -> w
[root@red.example.com]#cat /proc/partitions
[root@red.example.com]#pvcreate /dev/vdb2
[root@red.example.com]#pvs
[root@red.example.com]#vgcreate -s 16MB storage /dev/vdb2
[root@red.example.com]#vgs
[root@red.example.com]#lvcreate -l 100 -n engineering storage
[root@red.example.com]#lvs
[root@red.example.com]#lvdisplay
[root@red.example.com]#mkfs.vfat /dev/storage/engineering
[root@red.example.com]#mkdir /mnt/lvm
[root@red.example.com]#vim /etc/fstab
/dev/storage/engineering /mnt/lvm vfat defaults 0 0
[root@red.example.com]#mount -a
```

**Question 16**: Create a swap partition of 400M MB and make it available permanent.

```bash
[root@red.example.com]#fdisk /dev/vda -> n -> type -> +400M -> select type swap -> w
[root@red.example.com]#mkswap /dev/vda5
[root@red.example.com]#vim /etc/fstab ( make persistent entry)
/dev/vda5 swap swap defaults 0 0
[root@red.example.com]#swapon -a
[root@red.example.com]#swapon -s
[root@red.example.com]#free -m
```

**Question 17**: Resize your logical volume lv1, it should be approx 300MB (note -> only size accepted from 270mb to 290mb).

```bash
[root@red.example.com]#lvresize -r /dev/vg1/lv1 -L 300M
```

**Question 18**: Configure VDO file system, use device /dev/vdc , format it with xfs file system and make persistent mount under /database

```bash
[root@red.example.com]#rpm -qa | grep vdo
[root@red.example.com]#yum install vdo -y
[root@red.example.com]#vdo create --name=vdo1 --device=/dev/vdc --vdoLogicalSie=50G
[root@red.example.com]#vdo list
[root@red.example.com]#mkfs.xfs /dev/mapper/vdo1
[root@red.example.com]#udevadm settle
[root@red.example.com]#mkdir /database
[root@red.example.com]#vim /etc/fstab
/dev/mapper/vdo1 /database xfs defaults,x-systemd.requires=vdo.service 0 0
[root@red.example.com]#mount -a
[root@red.example.com]#vdostats --human-readable
```

**Question 19**: Configure recommended tuned profile

```bash
[root@red.example.com]#yum install tuned
[root@red.example.com]#systemctl start tuned
[root@red.example.com]#systemctl enable tuned
[root@red.example.com]#tuned-adm active
[root@red.example.com]#tuned-adm recommend
[root@red.example.com]#tuned-adm profile virtual-host
```
