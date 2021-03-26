# Configuring Loadbalancer Backend-Server Architecture on EC2 Instances

## Description

In this project we set up a loadbalancer on ec2 instance and connect it with backend servers also running on ec2 instances and all of this will be done using ansible. We launch ec2 instances on aws cloud and we use ansible on our workstation to configure different instances with haproxy and httpd server. We use dynamic inventory to retrieve ip's of the instances from aws cloud. We group the retrieved ip's based on the assigned tags to the instances and then apply different roles for different groups. 

When we launch the ec2 instances we create a server tag and assign the values loadbalancer to the instance on which we want to configure haproxy and value backend to instances on which we configure httpd servers. 

## Steps

For ansible to go to cloud and retrieve group-wise instance ip's , boto and boto3 python module should be installed in the workstation.

To install boto and boto3

```bash
pip3 install boto boto3
```

To create a dynamic inventory we use ec2.py and ec2.ini file. These files can be donwloaded from github.

```bash
wget https://raw.githubusercontent.com/ansible/ansible/stable-2.9/contrib/inventory/ec2.py

wget https://raw.githubusercontent.com/ansible/ansible/stable-2.9/contrib/inventory/ec2.ini
```

We pass the aws access key id and aws secret access key to the ec2 ini file. This will help the script to login to our aws account and retrieve the desired contents. 
Both the files need to be placed in a separate folder and this folder is declared as the inventory in ansible config file. 

Now we can use ansile list host command to retrieve the ip's. 

To list hosts with tags server backend and loadbalancer

```bash
ansible tag_server_backend --list-hosts

ansible tag_server_loadbalancer  --list-hosts
```

**output:**
![output-image](images/picture-16.png)

