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
        *"VpcId": "vpc-08c6ed2b90d386052",*  
        *"OwnerId": "706532313551",*  
        
