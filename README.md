# ![aws](https://github.com/julien-muke/Search-Engine-Website-using-AWS/assets/110755734/01cd6124-8014-4baa-a5fe-bd227844d263)     AWS-Cognito-with-Google-Identity-Provider


## 📄 Introduction

AWS Cognito is one of the most widely used Identity Provider. There are scenarios where a customer who uses AWS Cognito wants to support social login with Google, Facebook, Twitter or other Identity providers. In this way, a user doesn’t have to create a new profile to access that particular service or app. For ex: As an organization, I can build a product which is integrated with AWS Cognito using OIDC. If I want my users to easily access my app using their gmail credentials, I can setup a federation between Cognito and Google using OIDC.


## 📐 Architecture Design



![Blank diagram-8](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/6a4b5986-58e6-4b7b-96b6-29b326d7b9c6)




## ➡️ Step 1 - Create a basic user pool


An Amazon Cognito user pool is a user directory for web and mobile app authentication and authorization. From the perspective of your app, an Amazon Cognito user pool is an OpenID Connect (OIDC) identity provider (IdP). A user pool adds layers of additional features for security, identity federation, app integration, and customization of the user experience.

To create a basic user pool:

1. Navigate to the conlose, search for Amazon Cognito, click "Create user pool"



![Screenshot 2024-01-04 at 14 15 11](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/d661e9b1-1374-4c8c-8f97-575cfc487480)



2. Click `User name` as a sign-in option
3. Click "Next"



![Create-user-pool-User-pools-Amazon-Cognito-us-east-1](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/5fe286c9-27d9-4304-a2b7-2d96c1e7e610)



4. Desable MFA and Self-service account recovery, we don't need these optoins for this particular tutorial


![Create-user-pool-User-pools-Amazon-Cognito-us-east-1 (1)](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/c0d925b4-04a3-4ab7-8e4f-91ce63c32b7d)



5. Desable "Self-registration" and "Cognito-assisted verification and confirmation, we don't need these optoins for this particular tutorial.

6. For required attributes select `email`, `family_name`, `given_name`, `name`



![Create-user-pool-User-pools-Amazon-Cognito-us-east-1 (2)](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/07ffc7bc-1de2-4d51-90ce-751d55787e74)



7. Select `Send email with Cognito`
8. Click "Next"


![Screenshot 2024-01-04 at 14 22 09](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/3e86c3e4-3d00-4abf-ba65-5464ef1ca9da)



9. Enter `cognitoPool` as User pool name (you can taype any name you want)
10. Select `Use the Cognito Hosted UI`
11. For the Domain, select `Use a Cognito domain` and enter a ramdon doamin name my is going to be `testcong`



![Create-user-pool-User-pools-Amazon-Cognito-us-east-1 (3)-2](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/e0754971-bef6-4d7b-8b15-97eee694acd8)





## 💰 Cost

All services used are eligible for the AWS Free Tier. However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.

## 🧹 Clean Up

🗑️  Delete the Web Hosting App - Amplify Console

🗑️  Delete the REST API - API Gateway Console

🗑️  Delete the Lambda Function - Lambda Console

🗑️  Delete the Database - DynamoDB Console
