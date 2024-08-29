# AWS_Final
#pic#

on our final project we chose to develop a ###.

# Getting Started:
to run the code, you can use GitHub workspace (this is our recommendation).

#### Install AWS CLI
```bash
# Download the AWS CLI 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
# Unzip the package
unzip awscliv2.zip 
# Install the AWS CLI
sudo ./aws/install 
# Clean up the installation files 
rm -rf awscliv2.zip aws
``` 
#### Set your Credentials

Inside `Launch AWS Academy Learner Lab` section go to `AWS Details`
and then click on `show` close to the `AWS CLI`.

<img width="198" alt="image" src="https://github.com/user-attachments/assets/91a98af2-a172-4889-b4b6-c1b5c93879a4">

copy the credentials.

go back to the terminal, and write `aws configre` - put the right value according to the fields.
than, write `nano ~/.aws/credentials`
double check your credentials, and add the file if needed.
for verification, just write`aws s3 ls` 
and make sure that you see some s3 bucket from you account. 
<img width="476" alt="image" src="https://github.com/user-attachments/assets/0d67bd76-5c48-4ea5-97a7-59318242ff06">


#### Install AWS CDK 
```bash
# Install Typescript
npm -g install typescript

# Install CDK
npm install -g aws-cdk

# Verify that CDK Is installed
cdk --version
```
### Bootstrap your account for CDK

> Note that: If you already bootstrap your account, no need to execute that action
```bash
# Go to CDK Directory
cd social-network-cdk

# Install NPM models
npm install

# Run bootsrap
cdk bootstrap --template bootstrap-template.yaml
```

### Deploy the Base Stack
Make sure that you are at folder `social-network-cdk`, Change the Account ID and the VPC ID for your own details, you can find all the places easily when searching `#TODO` on lib and bin folders. 

#output#



great you have deployed the code successfuly!


# Our Solution:
we have build a #social network# BLA BLA.

#### Part A
in this part we have created ###

#### Part B
in this part we:
1. sqs
2. wd


# Testing:
we have build a test that covers the following:
1. create
2. delete

#### Running the tests
in order to run the test, you will need to run `npm test`

