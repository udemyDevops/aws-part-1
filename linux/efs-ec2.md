* Create a security group for EFS --> add inbound rule to allow NFS port from ec2 security group
* create EFS ---> Edit the sdefault ecurity group configuration for EFS to change it to the one created for it
* Different ways to authenticate EFS ---> IAM user, access points, others
* This will cover using access points
* create access point
* Follow the aws documentation (https://docs.aws.amazon.com/efs/latest/ug/efs-mount-helper.html) to mount EFS to an ec2 instance
  - Install amazon-efs-utils package (if using amazon linux), the driver to acces efs
    for other linux follow the doc for respective linux distributions
    ```
    sudo yum install -y amazon-efs-utils
    ```
  - Mounting efs automatically (doc) -- use the command for access point (https://docs.aws.amazon.com/efs/latest/ug/mounting-access-points.html)
    update the file-system-id, efs-mount-point (directory) and access-point-id, then put it in '/etc/fstab'
    ```
    <file-system-id> <efs-mount-point> efs _netdev,tls,accesspoint=<access-point-id> 0 0
    ```
  - before mounting move the data in the selected directory to another tmp  directory as backup
  - run the below command
    ```
    mount -fav
    ```
  - now copy the data from tmp directory to the mount point
  - take AMI of ec2 configured with EFS to use for spinning up other servers
