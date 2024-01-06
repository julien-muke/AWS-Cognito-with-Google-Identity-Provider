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


12. Select `Public client`
13. Add client name, mine is going to be `googleClient`
14. Select `Generate a client secret`
15. For the callback URLs, which is the URL for the app receiving the authorization code issued by Cognito, we will use `https://jwt.io`



![Create-user-pool-User-pools-Amazon-Cognito-us-east-1 (3)-3](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/8dc8d9f7-5724-40ba-af19-936bf8964c53)



16. For the OAuth 2.0 grant types, let's remove "Authorization code grant" and add `Implicit grant` that specifies that the client should get the access token.
17. For the OpenID Connect scopes, select `OpenID`, `Email`, `Profile` (remove "Phone" that was selected by default)


![Create-user-pool-User-pools-Amazon-Cognito-us-east-1 (3)-4-2](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/8fa0e85f-5718-4b27-bacd-7b3d82fa8440)



18. Review your selections, and click "Create user pool"


The user pool is successfully created


![Screenshot 2024-01-04 at 14 49 07](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/f063e12e-ef04-4069-888f-1adfa6381757)



## ➡️ Step 2 - Configure a client using Google Developer Console


Navigate to the Google Developer Console:

1. Create a new project, i will name it `CognitoGoogleIntegration` and then click "Create"


![Screenshot 2024-01-04 at 14 36 39](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/a44d9673-c676-4c08-b896-bd54ce23abc8)



2. Configure the OAuth consent screen with information about your application, to do that, navigate to the google console, select "APIs & Services" then "Credentials"


![Screenshot 2024-01-04 at 14 39 41](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/01ea692c-a4b4-4e01-865c-3f33418cce80)



3. Click "Configure Content Screen" 


![Screenshot 2024-01-04 at 14 40 30](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/2c9d5834-c0db-41a8-bf98-f671ed9d7028)



4. Select `External` as a User Type, this will be available to any test user with a Google Account


![Screenshot 2024-01-04 at 14 41 37](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/6870e3c1-5a0c-4e30-8e1d-b7156ac72e8e)



5. Enter the App name `CognitoApp`, and then Add the support and developer email, you can put your email `YOUREMAIL@gmail.com`, then Save changes.


![Edit-app-registration-–-APIs-Services-–-CognitoGoogleIntegr…-–-Google-Cloud-console-2](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/c267d430-d9fa-4fd7-866d-372c824f13d8)



![Edit-app-registration-–-APIs-Services-–-CognitoGoogleIntegr…-–-Google-Cloud-console-3](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/3bb059ca-a4a9-4b04-8fbf-1b9967598c86)


6. For "Scopes" and "Test users" leave it as default, then click "Save and Continue"
7. Go back to the Dashboard, Select "Credentials" then click "Create Credentials" then click `OAuth client ID`


![Screenshot 2024-01-04 at 14 46 04](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/23a5f7aa-d3eb-4540-87cc-b48c1c1418a1)



8. Select Application type `Web application` and Enter App name `CognitoWebApp`

We need to add the redirect URIs let's get back to that later as of now let create the application.


![Screenshot 2024-01-04 at 14 47 40](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/c97cd9ca-18db-4179-80d3-6106fb0bbf95)



9. the application client app is created successfully, now have a `Client ID` and `Client Secret`, copy and save it we will use it in Cognito



![Screenshot 2024-01-04 at 14 48 32](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/4c374888-25ed-454c-8e35-ec8d40da3835)




10. Now let's to back to Cognito and go to the "Sign-in Experience" and add "Identity Provider" 


![Sign-in-experience-cognitoPool-User-pools-Amazon-Cognito-us-east-1](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/ecc3470d-3a80-4433-870b-fe528756987c)



11. select `Google` for the identity provider
12. Copy and paste the `Client ID` and `Client secret` we created from Google
13. Add the Authorized scopes `openid`, `provile`, `email`
14. Map attributes between Google and your Cognito user pool, add Google attributes `name`, `given_name`, `family_name`, `email` then click "Add Identity Provider"



![Add-identity-provider-cognitoPool-User-pools-Amazon-Cognito-us-east-1](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/cd55a09a-46e4-4209-9419-fc3840822f6a)



15. Let's add the Authorized redirect URIs:

    * For Authorized redirect URIs, enter `https://yourDomainPrefix.auth.region.amazoncognito.com/oauth2/idpresponse`


![Screenshot 2024-01-04 at 15 00 33](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/816a2c1e-6f89-44b9-b371-3ddfebec5ba9)


Note: Replace `yourDomainPrefix` and `region` with the values for your user pool. Find these values in the Amazon Cognito console on the Domain name page for your user pool, under Add Integration.


![Screenshot 2024-01-04 at 14 59 23](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/08b9fc23-6302-4808-b4f8-0d6b7229aecd)



![Screenshot 2024-01-04 at 14 59 35](https://github.com/julien-muke/AWS-Cognito-with-Google-Identity-Provider/assets/110755734/272b6b22-dda6-40d0-9e0f-f5832f67cae2)







































## 💰 Cost

All services used are eligible for the AWS Free Tier. However, charges will incur at some point so it's recommended that you shut down resources after completing this tutorial.

## 🧹 Clean Up

🗑️  Delete the Web Hosting App - Amplify Console

🗑️  Delete the REST API - API Gateway Console

🗑️  Delete the Lambda Function - Lambda Console

🗑️  Delete the Database - DynamoDB Console
