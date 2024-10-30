# Wild-rydes-Webapp
Provided by Aws Workshop

This project demonstrates deploying a serverless application using AWS services like Amplify, Cognito, IAM, Lambda, DynamoDB, and API Gateway.

![Screenshot (38)](https://github.com/user-attachments/assets/7a13c3e3-af17-40f9-8d86-5b63ff3bd5fb)

![Screenshot (23)](https://github.com/user-attachments/assets/12cd3418-4279-4849-967e-c714dc9c7536)


## Table of Contents
1. [Project Setup on GitHub](#project-setup-on-github)
2. [Deploy with AWS Amplify](#deploy-with-aws-amplify)
3. [Configure Authentication with Cognito](#configure-authentication-with-cognito)
4. [Set Up DynamoDB for Data Storage](#set-up-dynamodb-for-data-storage)
5. [Configure IAM Role for Lambda Access](#configure-iam-role-for-lambda-access)
6. [Set Up Lambda Function](#set-up-lambda-function)
7. [Set Up API Gateway](#set-up-api-gateway)
8. [Complete Testing of Application](#complete-testing-of-application)
9. [Clean Up Resources](#clean-up-resources)

---

### Step 1: Create a GitHub Repository

1. **Create a New Repository**:
   * Go to your GitHub account and create a new repository (e.g., `wild-rydes-project`).
   * Clone the repository to your local machine if you plan to edit locally, or proceed directly with online files.

2. **Add Project Files**:
   * Add the Wild Rydes project files to the repository. If you’re using the AWS-provided code, upload all the necessary files, including `config.js`.
   * Commit and push the changes to ensure the repository is ready for integration.

---

### Step 2: Deploy with AWS Amplify

1. **Set Up Amplify**:
   * In the **AWS Management Console**, go to **AWS Amplify**.
   * Select **Host Web App** > **Connect with GitHub**. Authorize GitHub access, then select the repository you created.
   * Choose the main branch and click **Deploy** to build, deploy, and host the website.
     
     ![Screenshot (8)](https://github.com/user-attachments/assets/e9ec89f9-3819-4820-a49a-bf506f478fb5)


2. **Verify Deployment**:
   * After deployment, Amplify will provide a URL for the live site. Access this URL to confirm the app is live.
     
     ![Screenshot (9)](https://github.com/user-attachments/assets/d6438d6a-f2dc-46ed-81f9-685ff0e3a37a)


---

### Step 3: Configure Authentication with Cognito

1. **Create a User Pool in Cognito**:
   * Go to **Amazon Cognito** and create a **User Pool**. Customize as needed, enabling username or email as the login.
   * Save the **User Pool ID** and **Client ID** for later.
     
     ![Screenshot (12)](https://github.com/user-attachments/assets/8d3d5dd5-96f2-49c0-8d70-030d12ccb571)


2. **Update `config.js` in GitHub**:
   * In your GitHub repository, open `config.js` and paste the **User Pool ID** and **Client ID** from Cognito.
     
     ![Screenshot (35)](https://github.com/user-attachments/assets/3b861794-003f-4624-a7c9-7bf486afcda6)
     
   * Commit and push changes to GitHub. Amplify will automatically redeploy with these updates.

3. **User Sign-Up and Verification**:
   * Go to the deployed site, sign up with a new account, verify the email, and log in. This ensures Cognito authentication is correctly set up.
     
     ![Screenshot (14)](https://github.com/user-attachments/assets/ded991ce-59ea-4462-bc64-9e1c6bf5ad34)
     
     ![Screenshot (16)](https://github.com/user-attachments/assets/70666eec-a920-40d9-93f3-600216d7cb9f)
     
     ![Screenshot (18)](https://github.com/user-attachments/assets/bd33f775-0a1b-4682-900e-d4232d6649aa)
     
     ![Screenshot (19)](https://github.com/user-attachments/assets/e999906e-76ee-4c19-b475-8d2e54dcbaa4)


---

### Step 4: Set Up DynamoDB for Data Storage

1. **Create a DynamoDB Table**:
   * In **DynamoDB**, create a new table (e.g., `RideRequests`).
   * Add a **Partition Key** (e.g., `RequestID`).
   * Note the **DynamoDB ARN**; you’ll need it when setting up IAM policies for Lambda.
     
    ![Screenshot (24)](https://github.com/user-attachments/assets/db88e6d8-1087-4a1b-82ee-fbbab01132b6)


---

### Step 5: Configure IAM Role for Lambda Access

1. **Create IAM Role for Lambda**:
   * Go to **IAM** and create a new role with **Lambda permissions**.
   * Attach a custom policy or add `AmazonDynamoDBFullAccess` for access to your DynamoDB table.
   * Attach a custom policy that specifies the ARN of your DynamoDB table. This ensures that the Lambda function has access only to that particular table, enhancing security by preventing access to other resources.
     
     ![Screenshot (25)](https://github.com/user-attachments/assets/286c4989-e6c0-4aea-abe1-24fdaa158d99)


---

### Step 6: Set Up Lambda Function

1. **Create a Lambda Function**:
   * In **AWS Lambda**, create a new function. Choose the runtime and configure permissions to include the IAM role you just created.
   * Write code to interact with DynamoDB as needed for handling ride requests.
     
     ![Screenshot (26)](https://github.com/user-attachments/assets/390043ad-086a-4526-8a98-9a0e1221eb19)


2. **Deploy and Test**:
   * Deploy the Lambda function, set up a test event, and run it to confirm functionality.
     
    ![Screenshot (27)](https://github.com/user-attachments/assets/94fbce88-6388-49f9-a93c-3ee4f90e7169)
   
    ![Screenshot (28)](https://github.com/user-attachments/assets/13150668-d695-4916-a119-14901200c2a1)
   
    ![Screenshot (29)](https://github.com/user-attachments/assets/e43dc705-a7fc-4f37-884d-8d9137ecd3d1)

---

### Step 7: Set Up API Gateway

1. **Create a REST API**:
   * In **API Gateway**, create a new **REST API**.
     
     ![Screenshot (30)](https://github.com/user-attachments/assets/7f77a4f5-8fc1-45ec-8066-0b9ec3d0f618)


2. **Create an Authorizer**:
   * Under the **Authorizers** section, add a Cognito authorizer linked to your User Pool.
     
     ![Screenshot (31)](https://github.com/user-attachments/assets/b147c7b4-5c2e-4e15-89dc-85614383db51)
   
    ![Screenshot (32)](https://github.com/user-attachments/assets/ccee4584-649d-47a5-ab14-b82507adc24b)


3. **Create Resources and Methods**:
   * Add a `/requests` resource and configure a **POST method**.
   * Link the method to your Lambda function and attach the Cognito authorizer to secure it.
     
     ![Screenshot (33)](https://github.com/user-attachments/assets/51de9f79-ad5a-46f9-a7cf-57a10f589bb9)


4. **Deploy API**:
   * Deploy the API and get the **Invoke URL**.
     
     ![Screenshot (34)](https://github.com/user-attachments/assets/d3f26136-cbb7-4428-8673-9c5d36b2b285)

   * Update the **config.js** in GitHub with this Invoke URL, commit the changes, and Amplify will redeploy.
     
     ![Screenshot (35)](https://github.com/user-attachments/assets/3b861794-003f-4624-a7c9-7bf486afcda6)
     
    ![Screenshot (36)](https://github.com/user-attachments/assets/f33d3a10-e968-467f-9684-d74c396a4d21)
   
    ![Screenshot (37)](https://github.com/user-attachments/assets/42000bee-b81f-47f1-9187-e3f78f4404a1)


---

### Step 8: Complete Testing of Application

1. **Testing**:
   * Go to the deployed website, sign in, and attempt to make a ride request. Confirm that the API integration and data storage are functioning correctly.
     
     ![Screenshot (39)](https://github.com/user-attachments/assets/8d4ee100-1e60-4d0a-86db-a6eb3177f169)
     
    ![Screenshot (40)](https://github.com/user-attachments/assets/50685ffe-c350-43fd-81bd-f3b22b30b317)
   
    ![Screenshot (41)](https://github.com/user-attachments/assets/20143478-53c8-4efc-adda-ccb41f65a730)
   
    ![Screenshot (42)](https://github.com/user-attachments/assets/2280fb6c-4002-4ccc-8e27-28bb7425d092)


---

### Step 9: Clean Up Resources

1. **Delete Amplify Project**:
   * In **AWS Amplify**, delete the application to remove hosted resources.

2. **Delete Cognito User Pool**:
   * Go to **Amazon Cognito** and delete the User Pool.

3. **Delete DynamoDB Table**:
   * In **DynamoDB**, delete the table you created for ride requests.

4. **Delete Lambda Function**:
   * In **AWS Lambda**, delete the function created for handling requests.

5. **Delete IAM Role**:
   * Go to **IAM** and delete the custom IAM role along with any policies attached.

6. **Delete API Gateway**:
   * In **API Gateway**, delete the REST API you set up.

---

#### For a detailed video watch this : https://tinyurl.com/2bmkc5da
