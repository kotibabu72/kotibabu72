AWS CLI installation in centos/ amazon:

yum install python3
curl -O https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py --user
ls -a ~
export PATH=~/.local/bin:$PATH
source ~/.bash_profile
pip3 --version
pip3 install awscli --upgrade --user

Installation in ubuntu

sudo apt update 
sudo apt install awscli -y

9:$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json


Launch one AWS instance with aws command tools

create keypair

aws ec2 create-key-pair --key-name vijay --output text > vijay.pem


1. display your \keypairs

aws ec2 describe-key-pairs


2. deleting your key pair

aws ec2 delete-key-pair --key-name vijay

3. how to see what are the VPC id's are available

Virtual Private Cloud

aws ec2 describe-vpcs


4. create security group attached to default VPC network

aws ec2 create-security-group --group-name vijay-ext --description "vijay-ext" --vpc-id vpc-0c593d3051801d1f3


5.list security groups

aws ec2 describe-security-groups


6. Delete security group

aws ec2 delete-security-group --group-id sg-0bc338d6663c85ef8


7. how to allow ssh traffic to all ip 

aws ec2 authorize-security-group-ingress --group-id sg-be76b5c8 --protocol tcp --port 22 --cidr 0.0.0.0/0

aws ec2 authorize-security-group-ingress --group-id sg-be76b5c8 --protocol tcp --port 22 --cidr 192.168.10.0/24


8.delete the port opened rule only

aws ec2 revoke-security-group-ingress --group-id sg-be76b5c8 --protocol tcp --port 22 --cidr 0.0.0.0/0

9. to list all ami images

aws ec2 describe-images --owners self amazon --filters "Name=root-device-type,Values=ebs"


10. launch the instance

aws ec2 run-instances --image-id ami-04505e74c0741db8d --count 1 --instance-type t2.micro --key-name terraform --security-group-ids sg-0f3b68f97f91509d1 --subnet-id subnet-0ac4be71aa723b6f6

11:terminate the instalnce 

aws ec2 start-instances --instance-ids i-0d9d077670263bf6a
aws ec2 stop-instances --instance-ids i-0d9d077670263bf6a
aws ec2 terminate-instances --instance-ids i-0d9d077670263bf6a

aws ec2 describe-instances --query 'Reservations[*].Instances[*].{Instance:InstanceId,PublicIP:PublicIpAddress}' --output table

12:how to find out instance id

 aws ec2 describe-instances --instance-ids i-0aeda77a7aa41091f

13:creat a bucket 

aws s3 mb s3://vijaycnl1234

14:delete a bicket

aws s3 rb s3://bucket-name

15:to remove a nonempty bucket 

aws s3 rb s3://bucket-name --force

16:to list out buckets

 aws s3 ls

17:to list out specfic buckets

 aws s3 ls s3://bucket-name

18:to delete specfic file in bucket

aws s3 ls s3://bucket-name/path/

19:create a user

aws iam create-user --user-name MyUser

20:add a user yo group

aws iam add-user-to-group --user-name MyUser --group-name MyIamGroup

21:to list out the users in group

 aws iam get-group --group-name MyIamGroup

22:to set a intial password for a user

aws iam create-login-profile --user-name MyUser --password My!User1Login8P@ssword

23:create a acces key for a user

aws iam create-access-key --user-name MyUser

24:to delete a access key for a user

aws iam delete-access-key --user-name MyUser --access-key-id AKIAI44QH8DHBEXAMPLE
