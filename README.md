# Virtual Private Cloud (VPC) aws-cli
>Creates a VPC with the specified IPv4 CIDR block using aws-cli. 

>Creates public and private subnets and launch EC2 instances under the subnets. 

##Installing aws-cli
The easiest way to install aws-cli is to use pip.   
- $ pip install awscli    

Before using aws-cli, you need to tell it about your AWS credentials.The quickest way to get started is to run the aws configure command:

 - $ aws configure 
 
   AWS Access Key ID: foo  
AWS Secret Access Key: bar  
Default region name [us-west-2]: us-west-2  
Default output format [None]: json  

#Create VPC    
- *To check default VPC cidr range *

####**_$ aws ec2 describe-vpcs_**
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


aws ec2 describe-route-tables  
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

1) create RT

aws ec2 create-route-table --vpc-id vpc-0b733167ec6943ed2
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


2) ADD NAT gateway to RT
===============================

>aws ec2 create-route --route-table-id  rtb-0bc29931df7571f07 --destination-cidr-block 0.0.0.0/0 --nat-gateway-id nat-09ba591c47662ec88
{
    "Return": true
}


Change subnet association
======================


C:\Users\JUZZ>aws ec2 associate-route-table  --subnet-id subnet-0697e7cc1755027a9 --route-table-id rtb-0bc29931df7571f07
{
    "AssociationId": "rtbassoc-06ab5cd69894e9a47"
}


Enable auto assign Pub IP for Public subnets
=================================================


C:\Users\JUZZ>aws ec2 modify-subnet-attribute --subnet-id subnet-0f556b41b890d16f0 --map-public-ip-on-launch

C:\Users\JUZZ>
C:\Users\JUZZ>aws ec2 modify-subnet-attribute --subnet-id subnet-0fbf9d382ec3a7d0c --map-public-ip-on-launch
