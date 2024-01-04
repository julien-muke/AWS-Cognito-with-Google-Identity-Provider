# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263)     AWS-Cognito-with-Google-Identity-Provider


## 📄 Introduction

AWS Cognito is one of the most widely used Identity Provider. There are scenarios where a customer who uses AWS Cognito wants to support social login with Google, Facebook, Twitter or other Identity providers. In this way, a user doesn’t have to create a new profile to access that particular service or app. For ex: As an organization, I can build a product which is integrated with AWS Cognito using OIDC. If I want my users to easily access my app using their gmail credentials, I can setup a federation between Cognito and Google using OIDC.


## 📐 Architecture Design



![Blank diagram-8](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/6a4b5986-58e6-4b7b-96b6-29b326d7b9c6)




## ➡️ Step 1 - Create DynamoDB table






## 💰 Cost

All services used are eligible for the AWS Free Tier. However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.

## 🧹 Clean Up

🗑️  Delete the Web Hosting App - Amplify Console

🗑️  Delete the REST API - API Gateway Console

🗑️  Delete the Lambda Function - Lambda Console

🗑️  Delete the Database - DynamoDB Console
