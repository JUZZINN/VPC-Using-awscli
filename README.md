# Virtual Private Cloud (VPC) aws-cli
>Creates a VPC with the specified IPv4 CIDR block using aws-cli. 

>Creates public and private subnets and launch EC2 instances under the subnets. 

## Installing aws-cli
The easiest way to install aws-cli is to use pip.   
- $ pip install awscli    

Before using aws-cli, you need to tell it about your AWS credentials.The quickest way to get started is to run the aws configure command:

 - $ aws configure 
 
   AWS Access Key ID: foo  
AWS Secret Access Key: bar  
Default region name [us-west-2]: us-west-2  
Default output format [None]: json  

# Create VPC    
- *To check default VPC cidr range *

#### **_$ aws ec2 describe-vpcs_**
**_Output_**
>*"Vpcs":*
   
  > *{
            "CidrBlock": "172.31.0.0/16"*  
            
            
                    
- *_Creating a VPC with diffrerent cidr block_*

####**_$ aws ec2 create-vpc --cidr-block 172.16.0.0/16_**

**_Output_**
>*{*  
    *"Vpc": {*  
        *"CidrBlock": "172.16.0.0/16",*
        *"DhcpOptionsId": "dopt-3e728455",*  
        *"State": "pending",*  
        *"VpcId": "vpc-0b733167ec6943ed2",*  
        *"OwnerId": "706532313551",*     
        *"InstanceTenancy": "default",*  
        *"Ipv6CidrBlockAssociationSet": [],*
        *"CidrBlockAssociationSet": [*
            {  
                "AssociationId": "vpc-cidr-assoc-05bc350f0dcae4c2f",  
                "CidrBlock": "172.16.0.0/16",
                "CidrBlockState": {  
                        "State": "associated"  
                  }  
              }  
          ],  
        "IsDefault": false,  
        "Tags": []  
    }  
}  
  
  
            
- *To add Name tag for VPC*   
#####**_$ aws ec2 create-tags --resources vpc id --tags Key=Name,Value=VPC-CLI_**   

    
# Create subnet 
####**_$ aws ec2 describe-availability-zones_**  
- #####*_To get AvailabilityZones details_*

*{*  
    *"AvailabilityZones": [*  
        *{  
            *"State": "available",*  
            *"Messages": [],*  
            *"RegionName": "us-east-2",*  
            *"ZoneName": "us-east-2a",*  
            *"ZoneId": "use2-az1"*  
        *},  
        *{*  
            *"State": "available",*  
            *"Messages": [],*  
            *"RegionName": "us-east-2",*  
            *"ZoneName": "us-east-2b",* 
            *"ZoneId": "use2-az2"*  
        *},*  
        *{*  
            *"State": "available",*  
            *"Messages": [],*  
            *"RegionName": "us-east-2",*  
            *"ZoneName": "us-east-2c",*  
            *"ZoneId": "use2-az3"*
 


####**_$ aws ec2 create-subnet --vpc-id vpc-0b733167ec6943ed2 --availability-zone-id use2-az1 --cidr-block 172.16.0.0/19_**
{  
    "Subnet": {  
        "AvailabilityZone": "us-east-2a",  
        "AvailabilityZoneId": "use2-az1",  
        "AvailableIpAddressCount": 8187,  
        "CidrBlock": "172.16.0.0/19",  
        "DefaultForAz": false,  
        "MapPublicIpOnLaunch": false,  
        "State": "pending",  
        "SubnetId": "subnet-0f556b41b890d16f0",  
        "VpcId": "vpc-0b733167ec6943ed2",  
        "OwnerId": "706532313551",  
        "AssignIpv6AddressOnCreation": false,  
        "Ipv6CidrBlockAssociationSet": [],  
        "SubnetArn": "arn:aws:ec2:us-east-2:706532313551:subnet/subnet-0f556b41b890d16f0"  
    }  


####**_$ aws ec2 create-subnet --vpc-id vpc-0b733167ec6943ed2 --availability-zone-id use2-az2 --cidr-block 172.16.32.0/19_**


{  
    "Subnet": {  
        "AvailabilityZone": "us-east-2b",  
        "AvailabilityZoneId": "use2-az2",  
        "AvailableIpAddressCount": 8187,  
        "CidrBlock": "172.16.32.0/19",  
        "DefaultForAz": false,  
        "MapPublicIpOnLaunch": false,  
        "State": "pending",  
        "SubnetId": "subnet-0fbf9d382ec3a7d0c",  
        "VpcId": "vpc-0b733167ec6943ed2",  
        "OwnerId": "706532313551",  
        "AssignIpv6AddressOnCreation": false,  
        "Ipv6CidrBlockAssociationSet": [],  
        "SubnetArn": "arn:aws:ec2:us-east-2:706532313551:subnet/subnet-0fbf9d382ec3a7d0c"  
    }  
}  

 ####**_$ aws ec2 create-subnet --vpc-id vpc-0b733167ec6943ed2 --availability-zone-id use2-az3 --cidr-block 172.16.64.0/19_**

{  
    "Subnet": {  
        "AvailabilityZone": "us-east-2c",  
        "AvailabilityZoneId": "use2-az3",  
        "AvailableIpAddressCount": 8187,  
        "CidrBlock": "172.16.64.0/19",  
        "DefaultForAz": false,  
        "MapPublicIpOnLaunch": false,  
        "State": "pending",  
        "SubnetId": "subnet-0697e7cc1755027a9",  
        "VpcId": "vpc-0b733167ec6943ed2",  
        "OwnerId": "706532313551",  
        "AssignIpv6AddressOnCreation": false,  
        "Ipv6CidrBlockAssociationSet": [],  
        "SubnetArn": "arn:aws:ec2:us-east-2:706532313551:subnet/subnet-0697e7cc1755027a9"  
    }  
}  

##Create IGW


####**_$ aws ec2 create-internet-gateway_**
{  
    "InternetGateway": {  
        "Attachments": [],  
        "InternetGatewayId": "igw-06e79759556cbb111",  
        "Tags": []  
    }  
}  


###Creating an Elastic IP address


Allocates an Elastic IP address to your AWS account. After you allocate the Elastic IP address you can associate it with an instance or network interface.

 ####**_$ aws ec2 allocate-address_**
 
 
 {  
    "PublicIp": "18.189.123.243",  
    "AllocationId": "eipalloc-0fdeec081aeabba82",  
    "PublicIpv4Pool": "amazon",  
    "Domain": "vpc"  
}  


 ### Creating NAT GW

####**_$ aws ec2 create-nat-gateway  --subnet-id  subnet-0fbf9d382ec3a7d0c --allocation-id eipalloc-0fdeec081aeabba82_**


{  
    "NatGateway": {  
        "CreateTime": "2019-09-27T09:09:33.000Z",  
        "NatGatewayAddresses": [  
            {  
                "AllocationId": "eipalloc-0fdeec081aeabba82"  
            }  
        ],  
        "NatGatewayId": "nat-09ba591c47662ec88",  
        "State": "pending",  
        "SubnetId": "subnet-0fbf9d382ec3a7d0c",  
        "VpcId": "vpc-0b733167ec6943ed2"  
    }  
}  

}  




###Attach the Internet gateway to your VPC

#####**_$ aws ec2 attach-internet-gateway --vpc-id  vpc-0b733167ec6943ed2 --internet-gateway-id igw-06e79759556cbb111_**

####To know default-rtb fetails for our VPC


#####**_$ aws ec2 describe-route-tables_**  
{  
    "RouteTables": [  
        {  
            "Associations": [  
                {  
                    "Main": true,  
                    "RouteTableAssociationId": "rtbassoc-0092e868af9110bd2",  
                    "RouteTableId": "rtb-065c6986a9c8900f8"  
                }  
            ],  
            "PropagatingVgws": [],  
            "RouteTableId": "rtb-065c6986a9c8900f8",  
            "Routes": [  
                {  
                    "DestinationCidrBlock": "172.16.0.0/16",  
                    "GatewayId": "local",  
                    "Origin": "CreateRouteTable",  
                    "State": "active"  
                }  
            ],  
            "Tags": [],  
            "VpcId": "vpc-0b733167ec6943ed2",  
            "OwnerId": "706532313551"  



  

- **_Create a route in the route table_**

#####**_$aws ec2 create-route --route-table-id  rtb-065c6986a9c8900f8 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-06e79759556cbb111_**




##Making private subnet

###1. Create RT

#####**_$ aws ec2 create-route-table --vpc-id vpc-0b733167ec6943ed2_**
{  
    "RouteTable": {  
        "Associations": [],  
        "PropagatingVgws": [],  
        "RouteTableId": "rtb-0bc29931df7571f07",  
        "Routes": [  
            {  
                "DestinationCidrBlock": "172.16.0.0/16",  
                "GatewayId": "local",  
                "Origin": "CreateRouteTable",  
                "State": "active"  
            }  
        ],  
        "Tags": [],  
        "VpcId": "vpc-0b733167ec6943ed2",  
        "OwnerId": "706532313551"  


###2. ADD NAT gateway to RT


#####**_$aws ec2 create-route --route-table-id  rtb-0bc29931df7571f07 --destination-cidr-block 0.0.0.0/0 --nat-gateway-id nat-09ba591c47662ec88_**  
{  
    "Return": true  
} 


###3. Change subnet association



#####**_$aws ec2 associate-route-table  --subnet-id subnet-0697e7cc1755027a9 --route-table-id rtb-0bc29931df7571f07_**
{  
    "AssociationId": "rtbassoc-06ab5cd69894e9a47"  
}  


###Enable auto assign Pub IP for Public subnets



#####**_$aws ec2 modify-subnet-attribute --subnet-id subnet-0f556b41b890d16f0 --map-public-ip-on-launch_**


#####**_$aws ec2 modify-subnet-attribute --subnet-id subnet-0fbf9d382ec3a7d0c --map-public-ip-on-launch_**


###Create a key pair 


>#####**_$aws ec2 create-key-pair --key-name vpcclikey --query 'KeyMaterial' --output text > vpcclikey.pem_**

##Creating security groups 


###1. Security Group for Bastion server


#####**_$aws ec2 create-security-group --group-name blog-bastion --description "allow ssh from my ip" --vpc-id vpc-0b733167ec6943ed2_**
>{  
    "GroupId": "sg-03312ce2960517906"  
}  


#####**_$aws ec2 authorize-security-group-ingress --group-id sg-03312ce2960517906 --protocol tcp --port 22 --cidr 0.0.0.0/0_**


###2. Security Group for webserver 


#####**_$aws ec2 create-security-group --group-name webserverclivpc --description "allow ssh from Bastion server, 80 from all" --vpc-id vpc-0b733167ec6943ed2_**
>{  
    "GroupId": "sg-0539904efff19b31b"  
}  


#####**_$aws ec2 authorize-security-group-ingress --group-id sg-0539904efff19b31b --protocol tcp --port 80 --cidr 0.0.0.0/0_**


#####**_$aws ec2 authorize-security-group-ingress --group-id sg-0539904efff19b31b --protocol tcp --port 22  --source-group sg-03312ce2960517906_**



###2. Security Group for Database



#####**$_aws ec2 create-security-group --group-name dbclivpc --description "allow ssh from bastion  3306 from web" --vpc-id vpc-0b733167ec6943ed2_**

>{  
    "GroupId": ""  
}  


#####**_$aws ec2 authorize-security-group-ingress --group-id sg-05f7a2809f1e8d4ad --protocol tcp --port 22  --source-group sg-03312ce2960517906_**

#####**_$aws ec2 authorize-security-group-ingress --group-id sg-05f7a2809f1e8d4ad --protocol tcp --port 3306  --source-group sg-0539904efff19b31b_**



                


##Creating instances


###1. Bastion server 




#####**_$aws ec2 run-instances --image-id ami-00c03f7f7f2ec15c3 --count 1 --instance-type t2.micro --key-name vpcclikey --security-group-ids sg-03312ce2960517906 --subnet-id subnet-0fbf9d382ec3a7d0c_**
{  
    "Groups": [],  
    "Instances": [  
        {  
            "AmiLaunchIndex": 0,  
            "ImageId": "ami-00c03f7f7f2ec15c3",    
            "InstanceId": "i-035c1639ef7bc4e2f",  
            "InstanceType": "t2.micro",  
            "KeyName": "vpcclikey",  
            "LaunchTime": "2019-09-27T09:54:46.000Z",  
            "Monitoring": {  
                "State": "disabled"  
            },  
            "Placement": {  
                "AvailabilityZone": "us-east-2b",  
                "GroupName": "",  
                "Tenancy": "default"  
            },  
            "PrivateDnsName": "ip-172-16-40-41.us-east-2.compute.internal",  
            "PrivateIpAddress": "172.16.40.41",  
            "ProductCodes": [],  
            "PublicDnsName": "",  
            "State": {  
                "Code": 0,  
                "Name": "pending"  
            },  
            "StateTransitionReason": "",  
            "SubnetId": "subnet-0fbf9d382ec3a7d0c",  
            "VpcId": "vpc-0b733167ec6943ed2",  
            "Architecture": "x86_64",  
            "BlockDeviceMappings": [],  
            "ClientToken": "",  
            "EbsOptimized": false,  
            "Hypervisor": "xen",  
            "NetworkInterfaces": [  
                {  
                    "Attachment": {  
                        "AttachTime": "2019-09-27T09:54:46.000Z",  
                        "AttachmentId": "eni-attach-0740fda2b341005eb",  
                        "DeleteOnTermination": true,  
                        "DeviceIndex": 0,  
                        "Status": "attaching"  
                    },  
                    "Description": "",  
                    "Groups": [  
                        {  
                            "GroupName": "blog-bastio",  
                            "GroupId": "sg-03312ce2960517906"  
                        }  
                    ],  
                    "Ipv6Addresses": [],  
                    "MacAddress": "06:ad:d7:75:2c:1c",  
                    "NetworkInterfaceId": "eni-08504ac8150d5c478",  
                    "OwnerId": "706532313551",  
                    "PrivateIpAddress": "172.16.40.41",   
                    "PrivateIpAddresses": [  
                        {  
                            "Primary": true,  
                            "PrivateIpAddress": "172.16.40.41"  
                        }  
                    ],  
                    "SourceDestCheck": true,  
                    "Status": "in-use",  
                    "SubnetId": "subnet-0fbf9d382ec3a7d0c",  
                    "VpcId": "vpc-0b733167ec6943ed2",  
                    "InterfaceType": "interface"  
                }  
            ],  
            "RootDeviceName": "/dev/xvda",  
            "RootDeviceType": "ebs",  
            "SecurityGroups": [  
                {  
                    "GroupName": "blog-bastion",  
                    "GroupId": "sg-03312ce2960517906"   
                }  
            ],  
            "SourceDestCheck": true,  
            "StateReason": {  
                "Code": "pending",  
                "Message": "pending"  
            },  
            "VirtualizationType": "hvm",  
            "CpuOptions": {  
                "CoreCount": 1,  
                "ThreadsPerCore": 1  
            },  
            "CapacityReservationSpecification": {  
                "CapacityReservationPreference": "open"  
            }  
        }  
    ],
    "OwnerId": "706532313551",  
    "ReservationId": "r-0a36585d369fc90e7"  
}  

- *To add Name tag for Instance*   
#####**_aws ec2 create-tags --resources instance id --tags Key=Name,Value=Bastion-server_**  


###2. Webserver



#####**_aws ec2 run-instances --image-id ami-00c03f7f7f2ec15c3 --count 1 --instance-type t2.micro --key-name vpcclikey --security-group-ids sg-0539904efff19b31b --subnet-id subnet-0f556b41b890d16f0_**
{  
    "Groups": [],  
    "Instances": [  
        {  
            "AmiLaunchIndex": 0,  
            "ImageId": "ami-00c03f7f7f2ec15c3",  
            "InstanceId": "i-09b3bed04cb0a8eeb",  
            "InstanceType": "t2.micro",  
            "KeyName": "vpcclikey",  
            "LaunchTime": "2019-09-27T09:56:43.000Z",  
            "Monitoring": {  
                "State": "disabled"  
            },  
            "Placement": {  
                "AvailabilityZone": "us-east-2a",  
                "GroupName": "",  
                "Tenancy": "default"  
            },  
            "PrivateDnsName": "ip-172-16-1-178.us-east-2.compute.internal",  
            "PrivateIpAddress": "172.16.1.178",  
            "ProductCodes": [],  
            "PublicDnsName": "",  
            "State": {  
                "Code": 0,  
                "Name": "pending"  
            },  
            "StateTransitionReason": "",  
            "SubnetId": "subnet-0f556b41b890d16f0",  
            "VpcId": "vpc-0b733167ec6943ed2",  
            "Architecture": "x86_64",  
            "BlockDeviceMappings": [],  
            "ClientToken": "",  
            "EbsOptimized": false,  
            "Hypervisor": "xen",  
            "NetworkInterfaces": [  
                {  
                    "Attachment": {  
                        "AttachTime": "2019-09-27T09:56:43.000Z",  
                        "AttachmentId": "eni-attach-08f89a2fd783a6704",  
                        "DeleteOnTermination": true,  
                        "DeviceIndex": 0,  
                        "Status": "attaching"  
                    },  
                    "Description": "",  
                    "Groups": [  
                        {  
                            "GroupName": "webserverclivpc",  
                            "GroupId": "sg-0539904efff19b31b"  
                        }  
                    ],  
                    "Ipv6Addresses": [],  
                    "MacAddress": "02:65:13:b1:fe:d2",  
                    "NetworkInterfaceId": "eni-0a40ce63d3ac12121",  
                    "OwnerId": "706532313551",  
                    "PrivateIpAddress": "172.16.1.178",  
                    "PrivateIpAddresses": [  
                        {  
                            "Primary": true,  
                            "PrivateIpAddress": "172.16.1.178"  
                        }  
                    ],  
                    "SourceDestCheck": true,  
                    "Status": "in-use",  
                    "SubnetId": "subnet-0f556b41b890d16f0",  
                    "VpcId": "vpc-0b733167ec6943ed2",  
                    "InterfaceType": "interface"  
                }  
            ],  
            "RootDeviceName": "/dev/xvda",  
            "RootDeviceType": "ebs",  
            "SecurityGroups": [  
                {  
                    "GroupName": "webserverclivpc",  
                    "GroupId": "sg-0539904efff19b31b"  
                }  
            ],  
            "SourceDestCheck": true,  
            "StateReason": {  
                "Code": "pending",  
                "Message": "pending"  
            },  
            "VirtualizationType": "hvm",  
            "CpuOptions": {  
                "CoreCount": 1,  
                "ThreadsPerCore": 1  
            },  
            "CapacityReservationSpecification": {  
                "CapacityReservationPreference": "open"  
            }  
        }  
    ],  
    "OwnerId": "706532313551",  
    "ReservationId": "r-0749cecd87e536aba"  
}  


- *To add Name tag for Instance*   
#####**_aws ec2 create-tags --resources instance id --tags Key=Name,Value=webserver_**   


###3. Database ec2





#####**_aws ec2 run-instances --image-id ami-00c03f7f7f2ec15c3 --count 1 --instance-type t2.micro --key-name vpcclikey --security-group-ids sg-05f7a2809f1e8d4ad --subnet-id subnet-0697e7cc1755027a9_**
{  
    "Groups": [],  
    "Instances": [  
        {  
            "AmiLaunchIndex": 0,  
            "ImageId": "ami-00c03f7f7f2ec15c3",  
            "InstanceId": "i-0e3f310527cdd7b78",  
            "InstanceType": "t2.micro",  
            "KeyName": "vpcclikey",  
            "LaunchTime": "2019-09-27T09:58:22.000Z",  
            "Monitoring": {  
                "State": "disabled"  
            },  
            "Placement": {  
                "AvailabilityZone": "us-east-2c",  
                "GroupName": "",  
                "Tenancy": "default"  
            },  
            "PrivateDnsName": "ip-172-16-89-65.us-east-2.compute.internal",  
            "PrivateIpAddress": "172.16.89.65",  
            "ProductCodes": [],   
            "PublicDnsName": "",  
            "State": {  
                "Code": 0,  
                "Name": "pending"  
            },  
            "StateTransitionReason": "",  
            "SubnetId": "subnet-0697e7cc1755027a9",  
            "VpcId": "vpc-0b733167ec6943ed2",  
            "Architecture": "x86_64",  
            "BlockDeviceMappings": [],  
            "ClientToken": "",  
            "EbsOptimized": false,  
            "Hypervisor": "xen",  
            "NetworkInterfaces": [  
                {  
                    "Attachment": {  
                        "AttachTime": "2019-09-27T09:58:22.000Z",  
                        "AttachmentId": "eni-attach-09e9841187e1049f6",  
                        "DeleteOnTermination": true,  
                        "DeviceIndex": 0,  
                        "Status": "attaching"  
                    },  
                    "Description": "",  
                    "Groups": [  
                        {  
                            "GroupName": "dbclivpc",  
                            "GroupId": "sg-05f7a2809f1e8d4ad"  
                        }  
                    ],  
                    "Ipv6Addresses": [],  
                    "MacAddress": "0a:e9:36:e7:2b:0a",  
                    "NetworkInterfaceId": "eni-07c74516cbeaddf95",  
                    "OwnerId": "706532313551",  
                    "PrivateIpAddress": "172.16.89.65",  
                    "PrivateIpAddresses": [  
                        {  
                            "Primary": true,  
                            "PrivateIpAddress": "172.16.89.65"  
                        }  
                    ],  
                    "SourceDestCheck": true,  
                    "Status": "in-use",   
                    "SubnetId": "subnet-0697e7cc1755027a9",  
                    "VpcId": "vpc-0b733167ec6943ed2",  
                    "InterfaceType": "interface"  
                }  
            ],  
            "RootDeviceName": "/dev/xvda",  
            "RootDeviceType": "ebs",  
            "SecurityGroups": [  
                {  
                    "GroupName": "dbclivpc",  
                    "GroupId": "sg-05f7a2809f1e8d4ad"  
                }  
            ],  
            "SourceDestCheck": true,  
            "StateReason": {  
                "Code": "pending",  
                "Message": "pending"  
            },  
            "VirtualizationType": "hvm",  
            "CpuOptions": {  
                "CoreCount": 1,  
                "ThreadsPerCore": 1  
            },  
            "CapacityReservationSpecification": {  
                "CapacityReservationPreference": "open"  
            }  
        }  
    ],  
    "OwnerId": "706532313551",  
    "ReservationId": "r-081bbaa6690e16a2d"  
}  


- *To add Name tag for Instance*   
#####**_aws ec2 create-tags --resources instance id --tags Key=Name,Value=database_**  


                





