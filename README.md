# Capstone Project

Step 0:  Inspect the archtecture 



Step 1: Create a Cloud9 IDE
Set SG and Assign the App role to it
cd ~/environment


Step 2: Get the Project Assets 

wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/capstone-project/Example.zip

unzip Example.zip -d /var/www/html/

Step 3: Install a LAMP web server on Amazon Linux 2

LAMP (Linux, Apache HTTP server, MySQL database, and PHP) stack


sudo yum -y update
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

sudo yum install -y httpd mariadb-server
sudo systemctl start httpd

sudo systemctl enable httpd
sudo systemctl is-enabled httpd


chown apache:root /var/www/html/rds.conf.php


Open port 80 in Cloud9
Get the cloud9 EC2 public instance IP and test that you can access the website 

Step 4: Create a MySQL RDS database instance 
with the following specifications.
Create a db subnet group 
Databasetype: MySQL
 Template: Dev/Test
 DBinstanceidentifier: Example
 DB instance size: db.t3.micro
 Storage type: General Purpose (SSD)
 Allocatedstorage: 20GiB
 Storageautoscaling: Enabled
 Standbyinstance: Enabled
 Virtualprivatecloud: ExampleVPC
 Databaseauthenticationmethod: Passwordauthentication 
 Initialdatabasename: exampledb
 Enhancedmonitoring: Disabled
Step 5: Create an ALB

 Step 6: Importing the data into the RDS database instance from CLoud9 or by accessing the web instance via bastion host
 get the SQLDump file:
 wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/capstone-project/Countrydatadump.sql
 Add Cloud9 to SG of the RDS 
 connect to the RDS database, run this command:
 mysql -u admin -p --host <rds-endpoint> 
 mysql -u admin -p --host example.chtaacebezpy.us-east-1.rds.amazonaws.com

 mysql -u admin -p --host <rds-endpoint> < Countrydatadump.sql     

mysql -u admin -p exampledb --host example.chtaacebezpy.us-east-1.rds.amazonaws.com  < Countrydatadump.sql       

Test data was imported 
use exampledb;	
show tables; 
select * from countrydata_final; 
Step 7: configure the php  app to use the RDS 
look to get-parameters.php 
/example/endpoint example.chtaacebezpy.us-east-1.rds.amazonaws.com

/example/username admin 
/example/password lab-password 
/example/database exampledb


