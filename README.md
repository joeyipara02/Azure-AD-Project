# Azure-AD-Project

# Objective

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
* Step 5: Create a Windows server VM (Windows Server 2019)

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

* **CONGRATULATIONS!!!! You've just successfully set up a Vm and remoted into it!**

![Alt Text](https://i.imgur.com/dYOiR9J.png)


# Step 5: Create a Windows Server VM (Windows Server 2019)

* **The next step is to create a virtual machine with windows server 2019. Go back to the Azure home portal and click on virutal machine and "create".**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)


* **Make sure you sync the same Resource Group and Region that we first created. I have mine under ADProject and (US) West US 3 so I'm going to select those options and then name this vm Domain Controller.**

![Alt Text](https://i.imgur.com/kYyJwg7.png)


* **After that you want to choose the image of the virtual machine you want to create. We are creating a Windows 2019 Server so im going to scroll down and select "Windows Server 2019 Datacenter"** 

![Alt Text](https://i.imgur.com/RmuwdXC.png)

* **I'm going to choose the same size of the vm as I did for my workstation. I had issues installing AD on this server with only 1GB. So I recommend upgrading the size on this. I selected the B2ms**

 ![Alt Text](https://i.imgur.com/M2zNy95.png)


 * **Create the username and password for the DC. This will be the username and password you use to remote into your DC. Im going to keep it simple and keep it as Admin123**


![Alt Text](https://i.imgur.com/dlYuXfH.png)


* **Go to the networking tab and make sure you check the box to delete your public IP address and Nic after the vm is deleted. After that click on "Review and Create" Once your vm passes validation it'll be ready to deploy and remote into!!**

![Alt Text](https://i.imgur.com/iSoTK2k.png)


* **When you remote into your DC with your administrator username and password your pc wil load up and this Server Manager dashboard will pop up. This is where we will install Active Directory from and how we will promote it to our Domain Controller. Congrats on sucessfully creating and remoting into your windows server!!**


![Alt Text](https://i.imgur.com/dbEd28C.jpg)

* **Now that both machines are installed, ensure they can communicate using the "ping" command. Login to your Windows 2019 server and in the windows search bar type in "cmd" and hit enter. This will bring up your command prompt and you can now use the ping command to ping your windows 11 VM.**

![Alt Text](https://i.imgur.com/GMSgu2W.png)

* **Now lets try and ping our Windows Vm from the command prompt in our Windows 2019 Server. My private IP Address for my Windows 11 VM is 10.0.0.4 so I will type in "ping 10.0.0.4". As you can see we are not getting any successful pings. That's because it's getting blocked by our Windows Defender Firewall. We will need to enable a few rules in our firewall**

![Alt Text](https://i.imgur.com/GP2UpFk.png)

 
 * **To enable this, we will have to enable two firewall rules on our Windows 11 VM. Remote into your windows 11 VM with your administrator username and password. Open "Windows Defender Firewall with Advanced Security" by typing it into the Windows search bar and click on "open" or just press enter.**

![Alt Text](https://i.imgur.com/jsmzlmn.png)

* **Click on "Inbound Rules". We are looking for the rule that says "Core Networking Diagnostics-ICMP Echo Request (ICMPv4-in)". We want to enable both the private and domain firewall rule for echo requests. This will allow this machine to recieve ping requests from other machines that are on a private or domain network.**

![Alt Text](https://i.imgur.com/fwOitmK.png)

* **Double click on the rule and check the box to "enable" and then hit "apply" and "ok". Do this for both the rules that I showed you.**

![Alt Text](https://i.imgur.com/adwdL97.png)

* **Once you've enabled those rules log back into your windows 2019 server and try and ping your Windows 11 VM. Now you should be getting successful pings which means your devices can successfully talk to each other.**

![Alt Text](https://i.imgur.com/miZQubq.png)

* **Now that we know we can ping our Windows Vm from our Windows 2019 Server. We need to check if our Windows 11 VM can ping the windows server machine. But we already know they have firewall rules in place to block ping request so you're going to have to do the same steps on the windows server. Just follow the same steps we just did in the Windows VM**

![Alt Text](https://i.imgur.com/fwOitmK.png)

* **NOTTEEE!! If your windows 2019 server doesn't show the firewall rule you can run a command in the cmd prompt that will create this firewall rule and will allow you to make this change. For some reason my Windows 2019 Server didn't show the firewall rules that I needed. So if this happens to you just open up your cmd prompt on your Windows 2019 Server and run this command: netsh advfirewall firewall add rule name="ICMP Allow Incoming V4 Echo Request" protocol=icmpv4:8,any dir=in action=allow**

![Alt Text](https://i.imgur.com/U504RSU.png)

* **After you make the firewall changes to your Windows 2019 Server, log back into your Windows 11 VM and ping your Windows 2019 Server. You should now be getting successful pings to your Windows 2019 Server. Now we know both machines can talk to each other!**

![Alt Txt](https://i.imgur.com/NOIdH1g.png)

* **If you had to create the firewall rule manually, you'll want to go into the firewall settings and uncheck the box labeled 'public.' This rule is specifically for private and domain networks, and we don't want the public to be able to ping our machines. Double-click on this rule.**

![Alt Text](https://i.imgur.com/bXfVRoA.png)

* **Uncheck the box for public and then hit "Apply" and "Ok"








