# Terraform-Driven Game-Day Notifications System for Real-Time Alerts

"NBA Game Day Notification"

# Technical Architecture

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/c2a302281b7d6de8936b89d3397833d9db20c4ca/img/Screenshot%202025-02-10%20200330.png)

## Project Overview

This project is an alert system that sends real-time NBA game day score notifications to subscribed users via SMS/Email. It leverages Amazon SNS, AWS Lambda and Python, Amazon EvenBridge and NBA APIs to provide sports fans with up-to-date game information. The project demonstrates how we can use Infrastructure as Code by leveraging Terraform to automate the deployement and destruction of this solution in seconds.

## Features

1.Fetches live NBA game scores using an external API.

2.Sends formatted score updates to subscribers via SMS/Email using Amazon SNS.

3.Scheduled automation for regular updates using Amazon EventBridge.

4.Designed with security in mind, following the principle of least privilege for IAM roles.

## Prerequisites

1.Free account with subscription and API Key at sportsdata.io

2.Personal AWS account with basic understanding of AWS and Python

3.AWS CLI installed and configured to your personal account

4.Terraform CLI version 1.10.5 installed on your local environment

## Technologies

1.Cloud Provider: AWS

2.Infrastructure as Code tool: Terraform

3.Core Services: SNS, Lambda, EventBridge

4.External API: NBA Game API (SportsData.io)

5.Programming Language: Python 3.x

6.IAM Security:
Least privilege policies for Lambda, SNS, EventBridge and Systems Manager

## Project Structure

```python
game-day-notifications_terraform/
├── nba_notifications.py         # Main Lambda function code
├── nba_notifications.zip        # Main Lambda function zipped file
├── game_day_notifications.tf    # Game Day notification Terraform config file
├── LICENSE                     
├── .gitignore
└── README.md                    # Project documentation
Setup Instructions

```

## Step 1: Clone the Repository

1.1.Clone this repository to your local machine

```language
git clone https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-.git
cd game-day-notifications

```

## Step 2: Store API Key as secret in Parameter store

2.1.Lets run this aws cli command with your api key to store it in Paremeter store 

```language
aws ssm put-parameter --name "nba-api-key" --value "<API_KEY>" --type "SecureString"
```

## Step 3: Run Terraform workflow to initialize, validate, plan then apply

3.1.In your local terraform visual code environment terminal, to initialize the necessary providers, execute the following command in your environment terminal —

```language
Terraform init 
```

Upon completion of the initialization process, a successful prompt will be displayed, as shown below.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/00336aa0891efb4d14c497b2158c9e50a39de78c/img/Screenshot%202025-02-10%20203245.png)


3.2.Next, let’s ensure that our code does not contain any syntax errors by running the following command —

```language
Terraform validate
```

The command should generate a success message, confirming that it is valid, as demonstrated below.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/88a1ac1c416cf3afdb4090ce9b99b59560789ba7/img/Screenshot%202025-02-10%20203351.png)


3.3.Let’s now execute the following command to generate a list of all the modifications that Terraform will apply. —

```language
Terraform plan
```

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/47b48e996e045f95699f605363dadab26857d9a3/img/Screenshot%202025-02-10%20203604.png)

The list of changes that Terraform is anticipated to apply to the infrastructure resources should be displayed. The “+” sign indicates what will be added, while the “-” sign indicates what will be removed.


3.4.Now, let’s deploy this infrastructure! Execute the following command to apply the changes and deploy the resources.

Note — Make sure to type “yes” to agree to the changes after running this command

```language
Terraform apply
```

Terraform will initiate the process of applying all the changes to the infrastructure. Kindly wait for a few seconds for the deployment process to complete.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/3c4a8d4d7b0f06988221071a9d103bbeec7b9379/img/Screenshot%202025-02-10%20203909.png)


## Success!

The process should now conclude with a message indicating “Apply complete”, stating the total number of added, modified, and destroyed resources, accompanied by several resources.


![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/56d8b265027df0e10b9e9044240453e1ddf4aab2/img/Screenshot%202025-02-10%20203940.png)


## Step 4: Verify creation of AWS Lambda, AWS EventBridge and Amazon SNS 

4.1.In the AWS Management Console, head to the Amazon SNS dashboard and verify that the topic was successfully created.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/cdbb166fa08d4771be72f1a5cbc11d5759b2e03e/img/Screenshot%202025-02-10%20205028.png)

4.2.Navigate to the Subscriptions tab and click Create subscription.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/a28be8ae15fac13d1be0aa620d89d9e205fcf39b/img/Screenshot%202025-02-10%20205042.png)

4.3.Select a Protocol:
For Email:
Choose Email.
Enter a valid email address.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/dfb3fa3407c7a4909393cf006556def90ea227a9/img/Screenshot%202025-02-10%20205056.png)

4.4.Click Create Subscription.
If you added an Email subscription:
Check the inbox of the provided email address.


4.5.Confirm the subscription by clicking the confirmation link in the email.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/1dbaadfbed3b17a860174f5dd6dea31c0e15c996/img/Screenshot%202025-02-10%20205154.png)

## Step 5: Lets Test Our System if it is working

5.1.In the AWS Management Console, head to the AWS Lambda dashboard and verify if the lambda function was successfully created.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/be395bf59a521d00d61af5a04b5d88702b3cd29d/img/Screenshot%202025-02-10%20210411.png)

5.2.Lets Create a Test to simulate execution to check if our system is working

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/bc017e033ee88be8cbeb8d5dd23215d5c7ca7a0f/img/Screenshot%202025-02-10%20210745.png)

5.3.Run the function and check CloudWatch Logs for errors.


![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/ef2331f544cde634524b0501a956beedb1028bac/img/Screenshot%202025-02-10%20210955.png)


5.4.Verify that SMS notifications are sent to the subscribed users.

![image_alt](https://github.com/Tatenda-Prince/Terraform-Gama-Day-Notifications-/blob/e5b44af349bd9b3166bc46ccf3b5276f52ba73b0/img/Screenshot%202025-02-10%20211603.png)

## Congratulations 

In this project, We have successfully learned how to design a cloud-based notification system using AWS SNS and Lambda, ensuring secure access with least privilege IAM policies. We automated workflows with Amazon EventBridge and integrated an external NBA Open API (SportsDataIO) into our architecture. Additionally, we leveraged Terraform to automate the entire infrastructure as code, making deployment and management more efficient.













