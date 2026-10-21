1.
sudo groupadd students
sudo useradd -u 1234 -m -s /bin/bash user1
sudo passwd user1
sudo passwd -n 1 user1
sudo passwd -x 90 user1
sudo groupadd -aG students user1
2.
.1 ps -eo pid,ruid,euid,user,comm | awk '$3 == 0 && $2 != 0'
.2 sudo find / -type f -perm /4000 2>/dev/null
3.
 cp /usr/bin/cat .
   sudo chown root:root ~/cat
   sudo chown u+s ~/cat
4.
cp /usr/bin/chown ~/chown
sudo setcap cap_chown+ep ./chown 
5.
echo "user1 ALL=(ALL:ALL) NOPASSWD: /usr/bin/timedatectl" >> /etc/sudoers

