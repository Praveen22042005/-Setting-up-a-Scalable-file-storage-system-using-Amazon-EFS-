# SETTING UP A SCALABLE FILE STORAGE SYSTEM USING AMAZON ELASTIC FILE SYSTEM

### REGISTER NUMBER: 212222100036
### NAME : PRAVEEN B V

 
## AIM :
To set up a scalable file storage system using Amazon Elastic File System (EFS) for two EC2 instances in different availability zones, enabling shared access to data.

## PROBLEM STATEMENT :
This experiment demonstrates how to configure Amazon EFS to provide a shared storage solution for two Linux EC2 instances across different availability zones, enabling easy data sharing. The aim is to ensure both instances can mount and access the EFS file system and validate data consistency across instances.

## ALGORITHM :

#### Step 1: Launch Two EC2 Instances in Different Availability Zones
Go to the EC2 service in the AWS Management Console.</BR>
Launch two Linux-based EC2 instances (e.g., Amazon Linux 2) and place them in different availability zones within the same VPC.</BR>
Assign each instance a security group that allows NFS access on port 2049.</BR>

### Step 2: Set Up Security Group for EFS
Create or configure a security group that allows inbound NFS traffic on port 2049 from the security group of both EC2 instances.</BR>
Attach this security group to the EFS file system to permit access from both instances.</BR>

#### Step 3: Create an EFS File System
In the AWS Console, navigate to the EFS service and select Create file system.</BR>
Select the same VPC as your EC2 instances and configure mount targets in the availability zones where your instances are located.</BR>
Complete the setup and take note of the file system ID (e.g., fs-064645ac116a12816).</BR>

#### Step 4: Configure EC2 Instances to Access EFS

##### Instance 1</BR>
SSH into the first EC2 instance.</BR>
Switch to superuser</BR>
Install the HTTP server and EFS utilities</BR>
Mount the EFS file system to the web server's root directory</BR>
Navigate to the mounted directory and create a sample file:

##### Instance 2
SSH into the second EC2 instance.</BR>
Switch to superuser</BR>
Install the HTTP server and EFS utilities</BR>
Mount the EFS file system to the web server's root directory</BR>
Navigate to the mounted directory, list files, and view the content of the file created on Instance 1</BR>

## COMMANDS :

### EC2 Instance 1
```
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
vi file  # Create a file and add some text
```

### EC2 Instance 2
```
sudo su
yum install httpd -y
yum install -y amazon-efs-utils
mount -t efs -o tls fs-064645ac116a12816:/ /var/www/html
cd /var/www/html
ls
cat file  # Verify shared access by reading content created in Instance 1
```

## OUTPUT :

### Both EC2 instances showing EFS mounting. 

![image](https://github.com/user-attachments/assets/9dc312b2-d310-4d5f-afa6-6c572e23208b)
![image](https://github.com/user-attachments/assets/95cb7de7-0ae9-4a7c-9e63-8d30bf6e4af5)

### The creation of a file on Instance 1.
![image](https://github.com/user-attachments/assets/f219dd0d-08e4-45f8-a339-80661b7170a2)


### The display of that file’s contents on Instance 2 to verify shared access
![image](https://github.com/user-attachments/assets/e7cfc612-ac9a-4f41-ad02-532830f3d96b)


## RESULT :
Successfully set up a scalable file storage system using Amazon EFS shared between two Linux EC2 instances in different availability zones, enabling consistent data sharing.
 
  


