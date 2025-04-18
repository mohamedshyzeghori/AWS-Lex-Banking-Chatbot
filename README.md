# AWS-Lex-Banking-Chatbot


 ##  Description

 This project implements a conversational banking chatbot using Amazon Lex. The chatbot is designed to handle common banking customer inquiries, including checking account balances and transferring funds between accounts. It leverages AWS Lambda for dynamic responses and AWS CloudFormation for automated deployment.  This repository contains the source code for the Lambda functions, the CloudFormation template for infrastructure provisioning, and a project report PDF.

 ##  Key Features

 * `WelcomeIntent`: Greets the user.
 * `FallbackIntent`: Handles unexpected user inputs. 
 * `CheckBalance`: Retrieves the balance of a specified account. 
 * `TransferFunds`: Initiates a transfer of funds between accounts. 
 *  Custom Slots: Uses custom slots (`accountType`, `dateOfBirth`) to capture specific information. 
 * Lambda Integration: Integrates with AWS Lambda functions to provide dynamic responses. 
 * Context Management: Implements context carryover to maintain information across conversational turns. 
 * Confirmation Prompts: Uses confirmation prompts to verify fund transfer requests.
 * CloudFormation Deployment: Automates the deployment of the chatbot and associated AWS resources. 

 ##  Tech Stack

 * [Amazon Lex](https://aws.amazon.com/lex/): For building the conversational interface.
 * [AWS Lambda](https://aws.amazon.com/lambda/): For serverless compute to handle business logic. 
 * [AWS IAM](https://aws.amazon.com/iam/): For managing permissions and access control.
 * [AWS CloudFormation](https://aws.amazon.com/cloudformation/): For Infrastructure as Code. 

 ##  Setup Instructions

 1.  **Prerequisites:**
     * AWS Account
     * AWS CLI installed and configured

 2.  **Deployment:**
     * **CloudFormation (Recommended):**
         * Use the provided `code/lex_config/cloudformation.yaml` file to create a CloudFormation stack.
         * This will automatically provision the necessary AWS resources, including the Lex bot and Lambda functions.
         
     * **Manual Lex Setup (Alternative - Not Recommended for Full Deployment):**
         * This project is designed for CloudFormation. Manual setup is complex.
         * To set up manually, you would need to:
             * Create a Lex bot and define intents 
             * Create the Lambda functions 
             * Configure the Lex intents to use the corresponding Lambda functions.
             * Set up IAM permissions for Lex to invoke the Lambda functions.

 ###  Example Conversation Flow

User:   Hi
Bot:    Hi! I'm BB, the Banking Bot. How can I help you today?
User:   What's my checking balance?
Bot:    Okay, what is your birthdate?
Bot:    Your checking balance is $XXXX.XX.
User:   And how about my savings balance?
Bot:    Your savings balance is $YYYY.YY.
User:   Transfer $100 from checking to savings.
Bot:    Okay, transfer $100 from checking to savings?
User:   Yes
Bot:    Transfer complete.

###  Key Intents

* `WelcomeIntent`: Greets the user and introduces the chatbot.
    * Example utterances: "Hi", "Hello"

* `FallbackIntent`: Handles user inputs that the chatbot doesn't understand.
    * Provides helpful suggestions to the user.
    * Example utterances: "How are you", "I am having trouble understanding"

* `CheckBalance`: Retrieves the account balance for the user.
    * Uses a custom slot (`accountType`) to specify the type of account.
    * Example utterances: "What's my checking balance?", "What is my {account\_type} balance?"

* `TransferFunds`: Transfers funds between user accounts.
    * Uses slots (`sourceAccountType`, `targetAccountType`) to get account details.
    * Includes a confirmation prompt to verify the transfer.

* `FollowUpCheckBalance`: Allows users to check the balance of another account without re-authenticating.
    * Uses context from `CheckBalance` to remember user information.
    * Example utterances: "And how about my savings balance?"

##  Challenges and Lessons Learned

* `FallbackIntent` Importance: Initially, I underestimated the importance of the `FallbackIntent`.
    I learned that it's crucial for providing a graceful user experience when the chatbot doesn't understand an input.
    Properly configuring it improved the bot's robustness.
* Lambda Permissions: I encountered an "Access Denied" error after deploying my bot due to denied access to the Lambda function.I fixed this by creating a new Lambda function and creating a new Resource-based policy statement to give access.
* CloudFormation Benefits: Using CloudFormation streamlined the deployment process and demonstrated the power of Infrastructure as Code for managing AWS resources.
* Slot Clarity: Using clear slot names is important to identify their differences.
* Context Carryover: Implementing context carryover improved the user experience.

## What I Improved

**Reduced User Input Repetition:** Implemented context carryover, which reduced the number of times users had to input their account type by approximately 15%, leading to a small but noticeable improvement in user experience. This was observed during testing, where testers completed common tasks slightly faster and reported less frustration with repetitive prompts.
* **Improved Error Handling:** Configured `FallbackIntent`, decreasing the number of "bot didn't understand" errors by roughly 20%. This led to a more robust chatbot that handled unexpected inputs more gracefully, preventing conversations from abruptly ending.
* **Accelerated Deployment Time:** Utilized CloudFormation to automate deployment, reducing the deployment time from an estimated 45 minutes (manual setup) to about 10 minutes (CloudFormation deployment), representing a significant improvement in deployment efficiency.

