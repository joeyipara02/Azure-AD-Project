# Azure-AD-Project
                                                                                                  

Microsoft Azure is a cloud-based platform that provides various tools and services. This guide will take you through creating an account, setting up a Windows 11 virtual machine (VM), and configuring Active Directory (AD) on a Windows Server 2019. The server will then be promoted to a domain controller (DC). Afterward, we'll join the Windows 11 VM to the domain we just created. Following that, we'll create users, organizational units (OUs), groups, and demonstrate how to add a user to a security group and OU.

## What is Active Directory and a Domain Controller?

* Active Directory is like the phone book for a computer network. It contains a list of users, computers, and groups, ensuring everyone can find and access the right information. It's the organizational backbone of your network. 

* The Domain Controller is a vital server that manages security and access in a network. It holds Active Directory, which keeps track of users, computers, and permissions. The Domain Controller authenticates users, allowing or denying access to network resources based on predefined rules. It acts as the control center, ensuring a secure and organized network environment.

## Environments and Technologies Used

* Microsoft Azure
* Microsoft Remote Desktop to remote into the Vm's.

##Configuration Steps

* Step 1: Create an Azure Account
* Step 2: Azure Portal Introduction
* Step 3: Create a Resource Group
* Step 3: Create a Virtual Machine (Windows 11)
* Step 4: Connect to Virtual Machine Using Remote Desktop
* Step 5: Create another virtual machine (Windows server 2019)

## Step 1: Create an Azure account

* **Before we can do anything in Azure we are going to have to create an account. When you create this free account you will have a $200 subscription for a month.**

* **To create your Azure account [Click Here](https://azure.microsoft.com/en-us/free/)**

![Alt text](https://i.imgur.com/nj5Ln3I.png)

* **Click "Start Free". You will have to follow the instructions to sign up for the account. It's pretty straight forward and you can sign up with your email. It will ask for a credit card but it will not charge you until the $200 credit is used up or your 30 days expire. After you create your account you are now ready to start using Azure! In the Azure world you are now a Tenant!** 


# Step 2: Azure Portal Introduction 

## What is Azure portal? 


* Azure portal is the web based managment interface used on Microsoft Azure. It provides users with a centralized platform to deploy, manage, and monitor various cloud resources such as virtual machines, databases, and storage. Whenever you want to create a VM, NSG, Resource Group among other services Azure has to offer you wil be doing this in the Azure Portal.


* **To get to your Azure Portal you can [Click Here](https://portal.azure.com/#home)**


# Step 3: Create a Resource Group in Azure portal. 

## What is a Resource Group?

* A resource group is a way to organize everything that you are going to build in your Azure environment. If you want to create a network with a few vm workstations and some servers you will need a centrailzed place to store all your network devices that you want on the same network. This is what the resource gorup does. Think of it as a container and you want to store all resources to your environment in one container.  

* **In order to create a resource group, we are going to click on Resource Group.**



![Alt Text](https://i.imgur.com/p6Vy68y.png)



* **In the top left I have a red circle showing where it says "Create". Click "create" to create our Resource group**



![Alt Text](https://i.imgur.com/YCggkD1.png)


* **Name the Resource Group whatever you want but for this illustration I'm going to name it ADProject**


![Alt Text](https://i.imgur.com/e6S70iR.png)


* **Select from the drop down bar of what region you want to use. Select the region that you are closest too. This will help to reduce latency and improve performance. You also need to put all the machines that you want on the same network in the same region. I'm from the best coast the west coast so I'm going to select the Region (Us) West US 3.**

* **Click "Review and Create".**
 
![Alt Text](https://i.imgur.com/W3YnU6n.png)

* **On the next page just Click on "Create" on the bottom left where theres another arrow pointing to where its located. You have now created your resource group!**

![Alt Text](https://i.imgur.com/amMSExQ.png)

# Step 3: Create a Windows Virtual Machine (Windows 11)

* **The next step is to create a virtual machine. Lets's go back to the Azure home portal. Once your back at the home portal click on virutal machine.**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)



* **Just like we did with the resource group, we want to click "Create" and select on Azure Virtual Machine.**



![Alt Text](https://i.imgur.com/jLLpnRZ.png)


* **First thing we are going to do is click on the drop down bar on Resource Group and select the Resource Group you just created. The name of my Resource Group is ADProject so I'm going to select on ADProject.**

![Alt Text](https://i.imgur.com/YDrpxtB.png)

* **Name your Virtual Machine, for this example I'm just going to name it WindowsVm. Make sure your Region matches the same as the region you set your Resource Group to. After that you want to choose the image of the virtual machine you want to create. We are creating a Windows 11 VM so im going to scroll down and select Windows 11.**

![Alt Text](https://i.imgur.com/RpSsZbQ.png)

* **The next thing you're going to do is select the size of your vm. This will allocate your CPU and Ram for your VM. I had some issues running my VM's with the Standard size. If you are having performance issues or don't want to wait and see if your VM is slow I'll show how to change to size of your Vm. Click on "See all sizes"**

![Alt Text](https://i.imgur.com/fmFNKEr.png)

* **Select B2ms for the size of the VM. This VM will have 2 virtual CPU's and 8 gb's of virtual ram. Once you've done that click on "Select" at the bottom left corner. Also don't let the cost of the size scare you. You will not be charged for this. It just shows the cost if you were paying for the feature. It will be taken from your subscription so you are not being charged. Also, you are limited on resources, so by doing this on your workstation VM and your DC will max out your VCPU usage. Once you delete them, you can create VMs again**

![Alt Text](https://i.imgur.com/IBYoYcJ.png)

* **Next we are going to set the Administrative username and password for the workstation. This will be the login to remote into you VM. So don't forget this and make it simple. As you can see I just set mine to Admin123 and made a simple password. Dont forget to check the box on the bottom left. I have it circled, it's easy to miss when making a VM.**

![Alt Text](https://i.imgur.com/HuML7RE.png)

* **Select on the networking tab**

![Alt Text](https://i.imgur.com/34JCsIn.png)

* **Check on the box that says "Delete public IP and NIC when VM is deleted". You're only given a certain amout of public IP addresses so I recommend selecting this when creating VM's. It's also good practice for the real world. In the real world this will help prevent potential costs,enhances security and it assures the removal of any associated networking components. After you check that box you can select "Review and Create".**

![Alt Text](https://i.imgur.com/LAnYqcf.png)

* **Your VM is now creating and once it's been validated it will say "Validation Passed". Just select "Create" and that will deploy your VM**

![Alt Text](https://i.imgur.com/v7nUCI7.png)

* **Once the deployment is complete you have now creating a VM on Azure. Congrats!!**


![Alt Text](https://i.imgur.com/ZICzVAv.png)


# Step:4 Connect to Virtual Machine Using Remote Desktop


* **Now that we created our VM let's go take a look at it and see how we connect to it. Navigate to the Azure portal and click on "Virtual Machine"**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)

* **Once you're there click on your Virtual Machine. For me it's "WindowsVM" so I'm going to click on that.**

![Alt Text](https://i.imgur.com/Ze0bJrX.png) 

* **In the overview of Virtual Machine it shows the "essentials" of our machine on the right. Look for your public IP address for your Virtual Machine. There's a "copy to clipboard" right next to the public IP address. So copy the public IP address and once you've done that click on "Connect" and select the first option of "Connect" This will be if you're using remote desktop to remote into the VM's**

![Alt Text](https://i.imgur.com/OdN0OnO.png)

* **If you are using a windows pc you will already have RDP. If you're a Mac user you can download RDP for Mac here.** [Click Here](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12)

* **Download the RDP file and open it once it's done. It'll ask you for the PC that you are connecting to and that's where you want to paste your public IP Address. Type in the Administrative username and password that you created when you set up the VM.**

![Alt Text](https://i.imgur.com/W8EemPm.png)

* **CONGRADULATIONS!!!! You've just successfully set up a Vm and remoted into it!**

![Alt Text](https://i.imgur.com/dYOiR9J.png)






