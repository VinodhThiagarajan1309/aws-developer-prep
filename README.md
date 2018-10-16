# [IAM-EC2](IAM-EC2)
* * *
### IAM
* Nothing New 
* Always create a user with Admin Access and never use the root user

### EC2
Consists of 4 components,
* Virtual Machines - EC2
* Storing Data - EBS
* Load Balancing - ELB
* Scalability - ASG
* Bootstraping can be done using the *Advance Config Option* where we can provide additional commands for installing tools and downloading files. Example script.
```
#!/bin/bash

########################################################
##### USE THIS FILE IF YOU LAUNCHED AMAZON LINUX 2 #####
########################################################

# get admin privileges
sudo su

# install httpd (Linux 2 version)
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```

### Security Group

* By default there is no inbound rules we need to add it
* By default it can talk to anyone outside
* They act as the firewall
* Available only to a VPC-Region combination

### Public IP:
* If you stop and start the machine the PUBLIC IP will change

### Private IP
* Wont change

### Elastic IP

* By default we can have upto 5 IPs
* Its not free
* Say that your EC2 insance is failing which has this IP assigned. Then spin up a new instance and associate this IP to the new instance.
* But using this IP is bad architecture solution
* Right way is to use DNS or ELB

* * *
# [ELB + ASG + EBS](ELB+ASG+EBS)

### ELB - Elastic Load Balancer
* They help spread the load across multiple instances
* They do healthchecks
* They enable SSL
* They run across zones and can be either Internal or External LB
* Three types,
  * Class Load Balancer
  * Application Load Balancer
  * Network Load Balancer
#### Application Load Balancer Features

*   They support HTTP/HTTPS
*   The EC2 machines beyond the ALB will not see the actual client IP but can access it from Header X-Forwarded-For , X-Forwarded-Port or X-Forwarded-Proto
*   ALB generates stickiness, means same request get routed to the same instance.
*   ALB sees the private IP of the load balancer
