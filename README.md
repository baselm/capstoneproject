## Capstone Project


 <a href="https://youtu.be/AwH6drwfuAU">Youtube video</a>
 
 [![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/AwH6drwfuAU/0.jpg)](https://www.youtube.com/watch?v=AwH6drwfuAU)


### Summary of the tasks:
- Step 0:  Inspect the archtecture 00:02:23
- Step 1: Create a Cloud9 IDE 00:05:49
- Step 2: Get the Project Assets 00:07:51
- Step 3: Install a LAMP web server on CLoud9 IDE 00:08:49
- Step 4: Create a MySQL RDS database instance 00:13:15
- Step 5: Create an Application Load Balancer 00:20:53
- Step 6: Importing the data into the RDS database 00:25:18
- Step 7: Configure the system parameters in Parameter Store Systems Manager 00:38:20

# Step 0:  Inspect the archtecture 
- Inspect the example VPC. 
- Inspect the subnets. 
- Inspect the Security Groups.
- Inspect the AMI.  


# Step 1: Create a Cloud9 IDE
1. Search `Cloud9` in AWS Management Console
2. Click on `Create Environment`
3. Name is `Project IDE` (You can give any appropriate name need not be same)
4. VPC : Example VPC
5. Subnet : Public Subnet 2
6. Next and launch Cloud9



# Step 2: Get the Project Assets 
In Cloud9 Terminal  
1. Clone the repository:
```sh
   git clone https://github.com/baselm/capstoneproject.git
   or 
   wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/capstone-project/Example.zip
   ```
2. Extract the files to the Apache www folder:
```sh
   chown ec2-user Example.zip
   unzip Example.zip -d /var/www/html/
   ```
   
# Step 3: Install a LAMP web server on Amazon Linux 2

### LAMP (Linux, Apache HTTP server, MySQL database, and PHP) stack
Original tutorial for LAMP Stack <a href='https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html'> Tutorial: Install a LAMP web server on Amazon Linux 2 </a>

```sh
sudo yum -y update
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2

sudo yum install -y httpd mariadb-server
sudo systemctl start httpd

sudo systemctl enable httpd
sudo systemctl is-enabled httpd
```




- Open port 80 from the security group of the Cloud9 EC2 instance
- Get the cloud9 EC2 public instance IP address and test that you can access the website 

# Step 4: Create a MySQL RDS database instance 
with the following specifications.
- [ ] Create a db subnet group 
- [ ] Database type: MySQL
- [ ] Template: Dev/Test
 - [ ] DB instance identifier(Database ID): Example
 - [ ] DB instance size: db.t3.micro
 - [ ] Storage type: General Purpose (SSD)
 - [ ] Allocated storage: 20GiB
 - [ ] Storage autoscaling: Enabled
 - [ ] Standby instance: Enabled
- [ ]  Virtual private cloud: ExampleVPC
- [ ]  Database authentication method: Password authentication 
- [ ]  Initial database name: exampledb
- [ ]  Enhanced monitoring: Disabled

# Step 5: Create an Application Load Balancer
- Create target group 
- Create an auto scaling group 
- Lunch Web Instances in the private subnet
# Step 6: Importing the data into the RDS database
 _Importing the data into the RDS database instance from CLoud9 or by accessing the web instance via bastion host
 1. get the SQLDump file:
 

 2. connect to the RDS database, run this command:
```sh
mysql -u admin -p --host <rds-endpoint>
 ```
 3. Test that you can access the RDS DB 
 ```sh
use exampledb;	
show tables; 

 ```
 
  
4. Import the data into the RDS database.
```sh
mysql -u admin -p exampledb --host <rds-endpoint>  < Countrydatadump.sql       
```
# Test the ALB 
- Test data was imported 
```sh
use exampledb;	
show tables; 
select * from countrydata_final; 
 ```

# Step 7: Configure the system parameters in Parameter Store Systems Manager

Add the following parameters to the Parameter Store and set the correct values:
1. /example/endpoint 
2. /example/username   
3. /example/password  
4. /example/database
