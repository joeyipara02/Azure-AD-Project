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
* Step 2: Azure Portal Introduction
* Step 3: Create a Resource Group
* Step 3: Create a Virtual Machine (Windows 11)
* Step 4: Create another virtual machine but this time the windows server (Windows server 2019)

## Step 1: Create an Azure account
Before we can do anything in Azure we are going to have to create an account. When you create this free account you will have a $2oo subscription for a month. 

To create your Azure account [Click Here](https://azure.microsoft.com/en-us/free/) Click "Start Free". You will have to follow the instructions to sign up for the account. It's pretty straight forward and you can sign up with your email. It will ask for a credit card but it will not charge you until the $200 credit is used up or your 30 days expire. After you create your account you are now ready to start using Azure! In the Azure world you are now a Tenant!  

![Alt text](https://i.imgur.com/nj5Ln3I.png)

# Step 2: Azure Portal Introduction 

## What is Azure portal? 

Azure portal is the web based managment interface used on Microsoft Azure. It provides users with a centralized platform to deploy, manage, and monitor various cloud resources such as virtual machines, databases, and storage. Whenever you want to create a VM, NSG, Resource Group among other services Azure has to offer you wil be doing this in the Azure Portal.

To get to your Azure Portal you can [Click Here](https://portal.azure.com/#home)



# Step 3: Create a Resource Group in Azure portal. 

## What is a Resource Group?

A resource group is a way to organize everything that you are going to build in your Azure environment. If you want to create a network with a few vm workstations and some servers you will need a centrailzed place to store all your network devices that you want on the same network. This is what the resource gorup does. Think of it as a container and you want to store all resources to your environment in one container.  

In order to create a resource group we are going to click on Resource Group. 


In the top left I have an arrow pointing to where it says "Create" Click create to create our Resource group. 

![Alt Text](https://i.imgur.com/p6Vy68y.png)



