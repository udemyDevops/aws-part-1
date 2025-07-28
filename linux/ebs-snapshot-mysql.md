* First create a volume in aws ---> attach it to the ec2 ---> create partition for the new volume
* When the mysql/mariadb is installed it creates a directory '/var/lib/mysql' and stores the data in this path.
* Here we create the directory and mount it to the volume before installing the mysql/mariadb service
```
mkdir /var/lib/mysql
```
* mount it to the new partition
* now install the mariadb service
```
dnf install mariadb105-server -y
```

- now if 'ls /var/lib/mysql' ---> empty folder

* start the mariadb service
```
systemctl start mariadb
```
- now 'ls /var/lib/mysql' ---> should see the data

- mariadb data is in a separate volume, so if the volume is corrupted can be restored from a snapshot
