## Capstone Project


 <a href="https://youtu.be/AwH6drwfuAU">Youtube video</a>
### Summary of the tasks:
- Step 0:  Inspect the archtecture 00:02:23
- Step 1: Create a Cloud9 IDE 00:05:49
- Step 2: Get the Project Assets 00:07:51
- Step 3: Install a LAMP web server on CLoud9 IDE 00:08:49
- Step 4: Create a MySQL RDS database instance 00:13:15
- Step 5: Create an Application Load Balancer 00:20:53
- Step 6: Importing the data into the RDS database 00:25:18

# Step 0:  Inspect the archtecture 
- check the example VPC 
- check the subnets 
- Check the AMI  


# Step 1: Create a Cloud9 IDE




# Step 2: Get the Project Assets 
'''sh
unzip Example.zip -d /var/www/html/
'''



# Step 3: Install a LAMP web server on Amazon Linux 2

### LAMP (Linux, Apache HTTP server, MySQL database, and PHP) stack

'''sh
sudo yum -y update
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

sudo yum install -y httpd mariadb-server
sudo systemctl start httpd

sudo systemctl enable httpd
sudo systemctl is-enabled httpd
'''




- Open port 80 in Cloud9
- Get the cloud9 EC2 public instance IP and test that you can access the website 

# Step 4: Create a MySQL RDS database instance 
with the following specifications.
- [ ] Create a db subnet group 
- [ ] Databasetype: MySQL
- [ ] Template: Dev/Test
 - [ ] DBinstanceidentifier: Example
 - [ ] DB instance size: db.t3.micro
 - [ ] Storage type: General Purpose (SSD)
 - [ ] Allocatedstorage: 20GiB
 - [ ] Storageautoscaling: Enabled
 - [ ] Standbyinstance: Enabled
- [ ]  Virtualprivatecloud: ExampleVPC
- [ ]  Databaseauthenticationmethod: Passwordauthentication 
- [ ]  Initialdatabasename: exampledb
- [ ]  Enhancedmonitoring: Disabled

# Step 5: Create an Application Load Balancer
- Create target group 
- Create an auto scaling group 
- Lunch Web Instances in the private subnet
# Step 6: Importing the data into the RDS database
 _Importing the data into the RDS database instance from CLoud9 or by accessing the web instance via bastion host
 - get the SQLDump file:
 

 - connect to the RDS database, run this command:
'''sh
mysql -u admin -p --host <rds-endpoint>
 '''
 
 '''sh
 use exampledb;	
show tables; 
select * from countrydata_final; 
 '''
 
  

'''sh
mysql -u admin -p exampledb --host <rds-endpoint>  < Countrydatadump.sql       
'''
# Test the ALB 
- Test data was imported 

# Step 7: configure the php  app to use the RDS 
look to get-parameters.php 
/example/endpoint example.chtaacebezpy.us-east-1.rds.amazonaws.com

/example/username admin 
/example/password lab-password 
/example/database exampledb


