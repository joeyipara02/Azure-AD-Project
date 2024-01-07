# Azure-AD-Project
                                                                                                  

Microsoft Azure is a cloud-based platform that provides various tools and services. This guide will take you through creating an account, setting up a Windows 11 virtual machine (VM), and configuring Active Directory (AD) on a Windows Server 2019. The server will then be promoted to a domain controller (DC). Afterward, we'll join the Windows 11 VM to the domain we just created. Following that, we'll create users, organizational units (OUs), groups, and demonstrate how to add a user to a security group and OU.

## What is Active Directory and a Domain Controller?

Active Directory is like the phone book for a computer network. It contains a list of users, computers, and groups, ensuring everyone can find and access the right information. It's the organizational backbone of your network. 

The Domain Controller is a vital server that manages security and access in a network. It holds Active Directory, which keeps track of users, computers, and permissions. The Domain Controller authenticates users, allowing or denying access to network resources based on predefined rules. It acts as the control center, ensuring a secure and organized network environment.

## Environments and Technologies Used

* Microsoft Azure
* Microsoft Remote Desktop to remote into the Vm's.

##Configuration Steps

* Step 1: Create an Azure Account
* Step 2: Create a Resource Group
* Step 3: Create a Virtual Machine (Windows 11)
* Step 4: Create another virtual machine but this time the windows server (Windows server 2019)

## Step 1: Create an Azure account
Before we can do anything in Azure we are going to have to create an account. When you create this free account you will have a $2oo subscription for a month. 

To create your Azure account [Click Here](https://azure.microsoft.com/en-us/free/)

Click "Start Free". You will have to follow the instructions to sign up for the account. It's pretty straight forward and you can sign up with your email. It will ask for a credit card but it will not charge you until the $200 credit is used up or your 30 days expire. After you create your account you are now ready to start using Azure! In the Azure world you are now a Tenant!  

![Alt text](https://i.imgur.com/nj5Ln3I.png)



