# AWS_Final
#pic#

This application provides user management capabilities through an API built with AWS Lambda, API Gateway, and DynamoDB. It supports operations such as creating, retrieving, updating, and deleting users, as well as handling user profile pictures and likes.

## Technologies

- **Frontend**: HTML, CSS, JavaScript
- **Backend**: AWS Lambda functions
- **Database**: AWS DynamoDB
- **API Management**: AWS API Gateway
- **File Storage**: AWS S3
- **Notifications Queue**: AWS SQS

# Getting Started:

to run the code, you need to have:
1. AWS Account
2. Workspace - you can use GitHub workspace (this is our recommendation).

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

it should look like this:

 ✅  SocialNetworkStack

✨  Deployment time: 294.49s

Outputs:
SocialNetworkStack.UserApiEndpoint22DD5314 = https://pmigg2t2y6.execute-api.us-east-1.amazonaws.com/prod/
Stack ARN:
arn:aws:cloudformation:us-east-1:447578051232:stack/SocialNetworkStack/da28f3c0-65ce-11ef-bccd-0e0aabdc6377

✨  Total time: 300.33s


great! you have deployed the code successfuly!


# Our Solution:
we have build a user management system

<img width="767" alt="image" src="https://github.com/user-attachments/assets/47a67bed-62e3-42e7-bb94-c9234a595f0e">

It supports operations such as creating, retrieving, updating, and deleting users, as well as handling user profile pictures and likes.

After deployment, find the API URL in the CloudFormation outputs or AWS API Gateway console. 
<img width="596" alt="image" src="https://github.com/user-attachments/assets/455cbcfd-1722-4272-9abc-5c7212e133c7">

Update the `API_BASE_URL` in `index.html` (full path is \lambda\serveStaticContent\public\index.html) with the provided URL.

### Usage

1. **View User**

   - **Endpoint**: `GET /{userId}`
   - **Description**: Retrieve user details.
   - **Example**: `GET /12345` will retrieve details for user with ID `12345`.

2. **Upload Profile Picture**

   - **Endpoint**: `PUT /{userId}/updateProfilePicture`
   - **Description**: Upload a profile picture for a user.
   - **Parameters**: `userId` (path parameter), `image file` (in the request body).

3. **View All Users**

   - **Endpoint**: `GET /users`
   - **Description**: List all user IDs stored in DynamoDB.

4. **Create User**

   - **Endpoint**: `POST /`
   - **Description**: Add a new user.
   - **Request Body**: JSON object containing user details (e.g., name, email, age, address).

5. **Delete User**

   - **Endpoint**: `DELETE /{userId}`
   - **Description**: Remove a user based on `userId`.
   - **Example**: `DELETE /12345` will delete the user with ID `12345`.

6. **Like Profile Picture**

   - **Endpoint**: `POST /like`
   - **Description**: Like a user's profile picture.
   - **Request Body**: JSON object containing `profilePictureUserId` and `likerUserId`.

7. **View Likes for Profile Picture**

   - **Endpoint**: `GET /{userId}/likes`
   - **Description**: Retrieve likes for a specific user's profile picture.

8. **Check Messages**

   - **Endpoint**: `GET /{userId}/messages`
   - **Description**: Get notifications of like and unlike of profile pictures.
<img width="392" alt="image" src="https://github.com/user-attachments/assets/f08423b5-d102-4852-a02d-bca303900110">

## Lambda Functions

- **Create User**: Handles `POST` requests to create a new user.
- **Get User**: Handles `GET` requests to retrieve user details.
- **Update User Profile Picture**: Handles `PUT` requests to upload a profile picture.
- **Delete User**: Handles `DELETE` requests to remove a user.
- **Get All Users**: Handles `GET` requests to list all user IDs.
- **Like Profile Picture**: Handles `POST` requests to like a profile picture.
- **Get Likes for Profile Picture**: Handles `GET` requests to retrieve likes for a profile picture.
- **Check Messages**: Handles `GET` requests to check messages from the SQS queue.
- **Serve Static Content**: Serves static content from the root.

## API Gateway Configuration

The API Gateway is configured with the following endpoints:

- `POST /`: Create a new user.
- `GET /{userId}`: Retrieve user details.
- `DELETE /{userId}`: Delete a user.
- `PUT /{userId}/updateProfilePicture`: Update the profile picture for a user.
- `GET /users`: List all user IDs.
- `POST /like`: Like a profile picture.
- `GET /{userId}/likes`: Retrieve likes for a profile picture.
- `GET /{userId}/messages`: Check messages related to likes.
- `GET /`: Serve static content (e.g., `index.html`).

### DynamoDB Tables

- **Users Table**:
  - **Table Name**: `stav-shlomit-users-table`
  - **Primary Key**: `userId` (string)

- **Likes Table**:
  - **Table Name**: `stav-shlomit-likes-table`
  - **Primary Key**: `profilePictureUserId` (string)
  - **Sort Key**: `likerUserId` (string)

### S3 Bucket

- **Bucket Name**: `stav-shlomit-profile-pictures`
- **Purpose**: Stores user profile pictures.

### SQS Queue

- **Queue Name**: `stav-shlomit-likes-queue`
- **Purpose**: Handles notifications of likes and unlikes of profile pictures.

## Notes

- Ensure that your Lambda functions have the necessary permissions to access DynamoDB and S3.
- You may need to adjust IAM roles and policies based on your application's requirements.
- The `index.html` file is your frontend interface, where you interact with the API through the provided tabs.

# Testing:
we have build a test that covers the following:

| **Lambda Function**                  | **Edge Cases Checked**                                                                                   |
|--------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **`createUser`**                     | - Checks if the user is created successfully with valid input.                                             |
|                                      | - Checks for an error response when the input is invalid (e.g., missing username or email).               |
|                                      |                                                                                                           |
| **`deleteUser`**                     | - Checks if an existing user is deleted successfully.                                                     |
|                                      | - Checks for an error response when attempting to delete a non-existent user.                             |
|                                      |                                                                                                           |
| **`getUser`**                        | - Checks if the details of an existing user are returned successfully.                                     |
|                                      | - Checks for an error response when attempting to retrieve a non-existent user.                           |
|                                      |                                                                                                           |
| **`updateUserProfilePicture`**       | - Checks if a pre-signed URL for uploading a profile picture is returned for a valid user.                |
|                                      | - Checks if the system handles profile picture updates correctly for existing users.                      |
|                                      |                                                                                                           |
| **`getLikesForProfilePicture`**      | - Checks if the list of likes for an existing user’s profile picture is returned successfully.            |
|                                      | - Checks for an empty list when there are no likes for the profile picture.                               |
|                                      |                                                                                                           |
| **`getAllUsers`**                    | - Checks if a list of all users is returned successfully.                                                 |
|                                      | - (Note: This function doesn't have specific edge cases in the provided script, but typically handles large datasets gracefully).|


#### Running the tests
in order to run the test, make sure you are on 'social-media-cdk' folder
you can run the test with the command `npm test`
<img width="439" alt="image" src="https://github.com/user-attachments/assets/db1ecbc2-3ca6-4516-bff1-11924c5da1b3">

