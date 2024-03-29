# Azure-AD-Project

# Objective

In this easy-to-follow, step-by-step guide for beginners, I'll walk you through the process of utilizing Microsoft Azure, a cloud-based platform that provides various tools and services. This guide will take you through creating an Azure account, setting up a Windows 11 Virtual Machine, and configuring Active Directory on a Windows Server 2019. The server will then be promoted to a domain controller (DC). Afterward, we'll join the Windows 11 VM to the domain we just created. Following that, we'll create users, organizational units (OUs), groups, and demonstrate how to add a user to a security group and OU. 

## What is Active Directory and a Domain Controller?

* Active Directory is like the phone book for a computer network. It contains a list of users, computers, and groups, ensuring everyone can find and access the right information. It's the organizational backbone of your network. 

* The Domain Controller is a vital server that manages security and access in a network. It holds Active Directory, which keeps track of users, computers, and permissions. The Domain Controller authenticates users, allowing or denying access to network resources based on predefined rules. It acts as the control center, ensuring a secure and organized network environment.

## Environments and Technologies Used

* Microsoft Azure
* Microsoft Remote Desktop to remote into the Vm's.

## Configuration Steps

* Step 1: Create an Azure Account
* Step 2: Azure Portal Introduction
* Step 3: Create a Resource Group
* Step 3: Create a Virtual Machine (Windows 11)
* Step 4: Connect to Virtual Machine Using Remote Desktop
* Step 5: Create a Windows server VM (Windows Server 2019)
* Step 6: Establish a connection between our Windows Server 2019 and Windows 11 VM
* Step 7: Install Active Directory and promote to Domain Controller.
* Step 8: Join Windows 11 VM to the Domain.
* Step 9: Create a User, OUs, and a Security Group in Active Directory  
* Step 10: Log in to the Windows VM with the AD user credentials
* Bounus Step: Create a GPO and link it to an OU 

# Step 1: Create an Azure account

* **Before we can do anything in Azure we are going to have to create an account. When you create this free account you will have a $200 subscription for a month.**

* **To create your Azure account [Click Here](https://azure.microsoft.com/en-us/free/)**

![Alt text](https://i.imgur.com/nj5Ln3I.png)

* **Click "Start Free". You will have to follow the instructions to sign up for the account. It's pretty straight forward and you sign up with your email. It'll ask for a credit card but it will not charge you until the $200 credit is used up or your 30 days expire. After you create your account you are now ready to start using Azure! In the Azure world you are now a Tenant!** 


# Step 2: Azure Portal Introduction 

## What is Azure portal? 


* Azure portal is the web based managment interface used on Microsoft Azure. It provides users with a centralized platform to deploy, manage, and monitor various cloud resources such as virtual machines, databases, and storage. Whenever you want to create a VM, NSG, Resource Group among other services Azure has to offer you wil be doing this in the Azure Portal.


* **To get to your Azure Portal you can [Click Here](https://portal.azure.com/#home)**


# Step 3: Create a Resource Group in Azure portal. 

## What is a Resource Group?

* A resource group is a way to organize everything that you are going to build in your Azure environment. If you want to create a network with a few vm workstations and some servers you will need a centrailzed place to store all your network devices that you want on the same network. This is what the resource group does. 

* **In order to create a resource group, we're going to click on "Resource Group".**



![Alt Text](https://i.imgur.com/p6Vy68y.png)



* **In the top left, I have a red circle showing where it says "Create." Click "Create" to create our Resource Group**



![Alt Text](https://i.imgur.com/alKRJST.png)


* **Next, we're going to name our Resource Group. It doesn't matter what you name it, just make sure to select this Resource Group when creating your VMs. For this demonstration, I'm going to name it "ADProject**


![Alt Text](https://i.imgur.com/e6S70iR.png)


* **Select from the drop down bar of what region you want to use. Select the region that you are closest to. This will help to reduce latency and improve performance. You will need to put all the machines that you want on the same network in the same region. I'm from the best coast the west coast so I'm going to select the Region "(Us) West US 3".**

* **Click "Review and Create".**
 
![Alt Text](https://i.imgur.com/W3YnU6n.png)

* **On the next page click "Create" on the bottom left. You have now created your resource group!**

![Alt Text](https://i.imgur.com/amMSExQ.png)

# Step 3: Create a Windows Virtual Machine (Windows 11)

* **The next step is to create a virtual machine. Lets's go back to the Azure home portal. Once you're back at the home portal click on virutal machine.**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)



* **Click "Create" and select on Azure Virtual Machine.**



![Alt Text](https://i.imgur.com/vnJPr37.png)


* **The first thing we're going to do is click on the drop-down bar on "Resource Group" and select the Resource Group you just created. The name of my Resource Group is ADProject, so I'm going to select ADProject.**

![Alt Text](https://i.imgur.com/YDrpxtB.png)

* **Name your Virtual Machine, for this demonstration, I'm just going to name it "WindowsVm". Make sure your Region matches the same region you set for your Resource Group. After that, choose the image of the virtual machine you want to create. Since we are creating a Windows 11 VM, I'm going to scroll down and select Windows 11.**

![Alt Text](https://i.imgur.com/RpSsZbQ.png)

* **The next thing you're going to do is select the size of your VM. This will allocate your CPU and Ram for your VM. I had some issues running my VM with the Standard size. If you don't want to wait and see if your VM is slow I'll show how to change to size of your VM. Click on "See all sizes"**

![Alt Text](https://i.imgur.com/fmFNKEr.png)

* **Select B2ms for the size of the VM. This VM will have 2 virtual CPUs and 8 GB of virtual RAM. Once you've done that, click on "Select" at the bottom left corner. Also, don't let the cost of the size scare you. You will not be charged for this, it just shows the cost if you were paying for the feature. The cost will be deducted from your subscription, so you are not being charged separately. Additionally, you are limited on resources, so by doing this on your workstation VM and your Windows Server, it'll max out your vCPU usage. Once you delete your VMs everything will be removed and you can create new VMs without being maxed out on vCPUs**

![Alt Text](https://i.imgur.com/IBYoYcJ.png)

* **Next, we're going to set the administrative username and password for the workstation. This will be the login to remote into your VM, so don't forget this username and password. Make sure you create a strong password for this VM. Don't forget to check the box on the bottom left, I have it circled. It's easy to miss when creating a VM**

![Alt Text](https://i.imgur.com/HuML7RE.png)

* **Select on the networking tab**

![Alt Text](https://i.imgur.com/34JCsIn.png)

* **Check the box that says "Delete public IP and NIC when VM is deleted". You're only given a certain amout of public IP addresses so I recommend selecting this when creating VM's. It's also good practice for the real world. In the real world this will help prevent potential costs, enhances security and it assures the removal of any associated networking components. After you check that box you can select "Review and Create".**

![Alt Text](https://i.imgur.com/LAnYqcf.png)

* **Your VM is now creating and once it's been validated it will say "Validation Passed". Just select "Create" and that will deploy your VM**

![Alt Text](https://i.imgur.com/v7nUCI7.png)

* **Once the deployment is complete the VM is ready to use. Congrats on creating your first VM in Azure!!**


![Alt Text](https://i.imgur.com/ZICzVAv.png)


# Step:4 Connect to Virtual Machine Using Remote Desktop


* **Now that we've created our VM, let's check it out and see how we connect to it. Go to the Azure portal and click on "Virtual Machine."**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)

* **Once you're there click on your Virtual Machine. For me it's "WindowsVM" so I'm going to click on that.**

![Alt Text](https://i.imgur.com/Ze0bJrX.png) 

* **In the overview of the Virtual Machine, it shows the "essentials" of our machine on the right. Look for your public IP address for your Virtual Machine. There's a "copy to clipboard" option right next to the public IP address. Copy the public IP address, and once you've done that, click on "Connect" and select the first option, "Connect." This will be if you're using remote desktop to connect to the VMs**

![Alt Text](https://i.imgur.com/OdN0OnO.png)

* **If you're using a Windows PC, you already have RDP. If you're a Mac user, you can download RDP for Mac** [Click Here](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12)

* **Download the RDP file and open it once it's done. It'll ask you for the IP address of the PC that you're connecting to, and that's where you want to paste your public IP address. Type in the administrative username and password that you created when you set up the VM**

![Alt Text](https://i.imgur.com/W8EemPm.png)

* **CONGRATULATIONS!!!! You've just successfully set up a Vm and remoted into it!**

![Alt Text](https://i.imgur.com/dYOiR9J.png)


# Step 5: Create a Windows Server VM (Windows Server 2019)

* **The next step is to create a virtual machine with windows server 2019. Go back to the Azure home portal and click on virutal machine and "create".**

![Alt Text](https://i.imgur.com/5Rn5Fxx.png)


* **Make sure to use the the same Resource Group and Region that we initially created. I have mine under ADProject and (US) West US 3, so I'm going to select those options. Then, name this VM "Domain Controller.**

![Alt Text](https://i.imgur.com/kYyJwg7.png)


* **After that, you want to choose the image of the virtual machine you want to create. We are creating a Windows 2019 Server so I'm going to scroll down and select "Windows Server 2019 Datacenter"** 

![Alt Text](https://i.imgur.com/RmuwdXC.png)

* **I'm going to choose the same size for the VM as I did for my workstation. I had issues installing AD on this server with only 1GB, so I recommend upgrading the size for this. I selected the B2ms**

 ![Alt Text](https://i.imgur.com/M2zNy95.png)


 * **Create the username and password for the Windows 2019 Server. This will be the username and password you use to remote Windows Server. Again, make sure to use a strong password**


![Alt Text](https://i.imgur.com/dlYuXfH.png)


* **Go to the Networking tab and ensure you check the box to delete your public IP address and NIC after the VM is deleted. After that, click on "Review and Create." Once your VM passes validation, it'll be ready to deploy and remote into!!**

![Alt Text](https://i.imgur.com/iSoTK2k.png)

* **But before we remote into our Windows 2019 Server, we have to assign a static IP address to our server. This will be our Domain Controller, so we don't want this IP address to change. If the DC obtained a new IP address from DHCP, all devices on the network would lose connection to the Domain Controller, and no devices will be on the network. Click on your Windows 2019 Server VM and then click on "Network Settings."**

 ![Alt Text](https://i.imgur.com/NQNZObS.png)

 * **Click on the Network Interface/IP Configuration**

 ![Alt Text](https://i.imgur.com/RKyPrlG.png)

 * **Click on "ipconfig1" and under "Private IP Address Settings" change the Allocation to "Static" and then hit the save button**

![ALt Text](https://i.imgur.com/KcylFlZ.png)

* **Now that we've set our Windows Server to a static IP, we can remote into our server. When you remote into your Windows 2019 Server with your administrator username and password, your VM will load up, and the Server Manager dashboard will appear. This is where we will install Active Directory later on. Congratulations on successfully creating and remoting into your Windows Server!**


![Alt Text](https://i.imgur.com/dbEd28C.jpg)

# Step 6: Establish a connection between our Windows Server 2019 and Windows 11 VM

* **Now that both machines are installed, ensure they can communicate using the "ping" command. Login to your Windows 2019 Server and in the windows search bar type in "cmd" and hit enter. This will bring up your command prompt and you can now use the ping command to ping your windows 11 VM.**

![Alt Text](https://i.imgur.com/GMSgu2W.png)

* **Now lets try and ping our Windows VM from the command prompt in our Windows 2019 Server. My private IP Address for my Windows 11 VM is 10.0.0.4 so I will type in "ping 10.0.0.4". As you can see, we are not getting any successful pings. That's because they are getting blocked by our Windows Defender Firewall. To fix this, we will need to add a few rules in our firewall**

![Alt Text](https://i.imgur.com/GP2UpFk.png)

 
 * **To enable this, we will have to enable two firewall rules on our Windows 11 VM. Remote into your windows 11 VM with your administrator username and password. Open "Windows Defender Firewall with Advanced Security" by typing it into the Windows search bar and click on "open" or just press enter.**

![Alt Text](https://i.imgur.com/jsmzlmn.png)

* **Click on "Inbound Rules." Look for the rule that says "Core Networking Diagnostics-ICMP Echo Request (ICMPv4-in)." Enable both the private and domain firewall rules for echo requests. This will allow this machine to receive ping requests from other machines on a private or domain network**

![Alt Text](https://i.imgur.com/fwOitmK.png)

* **Double-click on the rule, check the box to "enable," and then click "Apply" and "OK." Repeat this process for both rules that I showed you.**

![Alt Text](https://i.imgur.com/adwdL97.png)

* **Once you've enabled those rules log back into your Windows 2019 Server and try and ping your Windows 11 VM. Now you should be getting successful pings which means your Windows 2019 Server can talk to the Windows Vm.**

![Alt Text](https://i.imgur.com/miZQubq.png)

* **Now we need to check if our Windows 11 VM can ping the Windows 2019 Server. However, we already know there are firewall rules in place to block ping requests, so you'll have to follow the same steps on the Windows 2019 Server. Just follow the same steps we did on the Windows VM**

![Alt Text](https://i.imgur.com/fwOitmK.png)

**$${\color{red}NOTE!!}$$ If your Windows 2019 Server doesn't show the firewall rule, you can run a command in the cmd prompt that will create this firewall rule and will allow you to make this change. For some reason, my Windows 2019 Server didn't show the firewall rules that I needed. So, if this happens to you, just open up your cmd prompt on your Windows 2019 Server and run this command. When it says "OK," it was successful: netsh advfirewall firewall add rule name="ICMP Allow Incoming V4 Echo Request" protocol=icmpv4:8,any dir=in action=allow**

![Alt Text](https://i.imgur.com/Tq4T5Wq.png)

* **If you didn't have to create a firewall rule with the command proceed to ping your Windows Server. If you had to create the firewall rule manually, you'll want to go into the firewall settings and uncheck the box labeled 'public.' This rule is specifically for private and domain networks, and we don't want the public to be able to ping our machines. Double-click on the rule "ICMP Allows Incoming V4 Echo Request"**

![Alt Text](https://i.imgur.com/bXfVRoA.png)

* **Uncheck the box for public and then hit "Apply" and "Ok"**

![Alt Text](https://i.imgur.com/GLVEYOW.png)

* **After you make the firewall changes to your Windows 2019 Server, log back into your Windows 11 VM and ping your Windows 2019 Server. You should now be getting successful pings from your Windows 11 VM to your Windows 2019 Server. Now we know both machines can talk to each other!**

![Alt Txt](https://i.imgur.com/NOIdH1g.png)


# Step 7: Install Active Directory and promote to Domain Controller

* **Log back into your Windows 2019 Server Machine and click on your Windows icon and open "Server Manager". This is where we are going to install Active Directory**

![Alt Text](https://i.imgur.com/822f6RH.png)

* **Click on the "Add roles and features" in Server Manager**

![Alt Text](https://i.imgur.com/K0Aetmo.png)

* **Click on "Next" until you get to the "Server Roles" page.**

![Alt Text](https://i.imgur.com/BtGqdmd.png) 

* **When you get to the "Server Roles" page you want to select on "Active Directory Domain Services"**

![Alt Text](https://i.imgur.com/2ozgLVu.png)

* **Click on "Add Features" and click "Next" until you see "Install"**

![Alt Text](https://i.imgur.com/WyXtzpj.png)

![Alt Text](https://i.imgur.com/h1wstvF.png)

* **Once the installation of Active Directory is complete you will see see a yellow hazard symbol next to the notifications flag. Click on the the yellow hazard then click "Promote this server to a domain controller".**

![Alt Text](https://i.imgur.com/cimPbA2.png)

* **Check the box to "Add a new forest" and type in the name you want your domain to be. I'm just going to use "Domain.com" to keep it simple. After you name it click "Next"**

![Alt Text](https://i.imgur.com/xIJFftv.png)

* **Type in the password you created for Windows 2019 Server and click "Next"**

![Alt Text](https://i.imgur.com/ZCN9UfV.png)

* **Dont worry about this message just go ahead and click "Next".**

![Alt Text](https://i.imgur.com/FvF47lq.png)

* **Finish the installation by clicking "Install." You will encounter warning signs, but don't mind them; it's normal. This process will take a little while and will restart when it's done.**

![Alt Text](https://i.imgur.com/3OBKDiM.png)

* **Login to the Domain Controller we just promoted. Click on the Windows start button and type "About this PC" and hit enter.**

![Alt Text](https://i.imgur.com/N9t7MeP.png)

* **You can see that we successfully promoted Active Directory to a Domain Controller with the PC name showing "DomainControlle"🤣(missing the "r" I think it was too long of a name). You can also see that we're on the domain "Domain.com" which is the name of the domain I just created.**

![Alt Text](https://i.imgur.com/PcvHAdc.png)

# Step 8: Join Windows 11 VM to the Domain

* **Go back to your Azure portal and and click on your Windows 11 VM**

![Alt Text](https://i.imgur.com/KKlL3kF.png)

* **Click on "Networking" under the "Settings" section**

![Alt Text](https://i.imgur.com/bW383LX.png)

* **Click on the Network Interface of the VM**

![Alt Text](https://i.imgur.com/usiexg8.png)

* **Click on "DNS Servers"**

![Alt Text](https://i.imgur.com/6WcBr01.png)

* **Check the "Custom" box and then type in the private IP Address of your Domain Controller. Mine is 10.0.0.5 so I will type that in and the click on the "Save" disk.**

![Alt Text](https://i.imgur.com/2NNHy8W.png)

* **Login to your Windows 11 VM and in the Windows search bar type "About this PC" and hit enter**

![Alt Text](https://i.imgur.com/StbRVJw.png)

* **Click on the "Domain or Workgroup"**

![Alt Text](https://i.imgur.com/tXpkFxJ.png)


* **Click on "Change"**

![Alt Text](https://i.imgur.com/O1mnbiX.png)

* **Check the box "Domain" and type in the name of the domain you created. I will type in domain.com since that's the domain name I created for my domain. Click on "Ok"**

 ![Alt Text](https://i.imgur.com/ksfkfgj.png)

 * **It will then ask you for the Administrative username and password for the Windows VM. Click "Ok" and it will say "Welcome to @<YOURDOMAIN> domain" and it will have you restart your VM**

  ![Alt Text](https://i.imgur.com/aWujWon.png)

* **Log back into your Windows VM when it restarts and type in "CMD" in the windows search bar and hit enter.**

![Alt Text](https://i.imgur.com/Y8uKRIQ.png)

* **In the CMD type in "ipconfig /all" and hit enter. Here you will see the Windows 11 VM Primary DNS Suffix is"domain.com". That's telling us that this VM belongs to the domain of "domain.com". The DNS server for this VM is 10.0.0.5 which is the IP of our Domain Controller! Congrats!!! You have now joined your windows 11 vm to the domain !!!**

![Alt Text](https://i.imgur.com/sqWicBf.png)

# Step 9: Create a User, OUs, and a Security Group in Active Directory

* **Login to your Domain Contoller. The "Server Manager" will automatically open up. On the right hand side click on "Tools" and select "Active Directory Users and Computers"**

![Alt Text](https://i.imgur.com/s9ADIzg.png)

* **Click on the expand button next to your domain name.**

![Alt Text](https://i.imgur.com/nZYi0S3.png)

* **Right click on your domain name and select "New" and "Organizational Unit"**

![Alt Text](https://i.imgur.com/TS30cb3.png)

* **To keep it simple I'm just going to name this Organizational Unit "IT" and click on "Ok".**

![Alt Text](https://i.imgur.com/qkwYEok.png)

* **I'll create a sub-OU inside 'IT' by right-clicking on it, selecting 'New,' and then choosing 'Organizational Unit"**
![Alt Text](https://i.imgur.com/1e7mHyd.png) 


* **I'm going to name this sub-OU "Users" and click "OK"**

![Alt Text](https://i.imgur.com/kbw6ogX.png)

* **Now, we're going to create a user in Active Directory and place that user in the 'Users' Sub-OU within the 'IT' OU. Click on the "IT" OU and right click the sub-ou "Users". Select "New" and then select "User"**

![Alt Text](https://i.imgur.com/hpjlNLG.png)

* **Fill out the information for your user. I'm going to name this user Mike Jones and create a username of "mjones281@domain.com". and click "Next"**

![Alt Text](https://i.imgur.com/4XaqTLh.png)

* **Create a password for your user. I'm going to uncheck "User must change password at next login". In the real world you will keep this box checked. Help Desk will assign a password like "example123" to create the profile. When the user logins for the first time with this password they will then be asked to change their password to the length and security requirements of the organization password requirements.**

![Alt Text](https://i.imgur.com/6DlCMjV.png)

* **Click on finish and now the user has been created! Click on the "IT" OU and click on the sub-Ou of "Users" and you will see the user you just created!!**

![Alt Text](https://i.imgur.com/Ky5jdUk.png)

![Alt Text](https://i.imgur.com/tJZnRrZ.png) 

* **Now we will create a Security Group and add this user to that security group. But before we do this lets go over what a security group is.  A security group allows us to easily manage rights and permissions for a user based on the group they belong to. So, if you're added to the Information Technology group, you will have rights and permissions for systems and networks as other IT members. Someone in payroll won't have these rights, instead, they will have their own rights and permissions by being added to the 'Payroll' group. Click on your domain and select "New" and then "Group".**

![Alt Text](https://i.imgur.com/yYjBrMf.png)

* **Type in the name of your group and click "OK". I'm going to name this group "Information Technology." Members of this security group will have the permissions and rights associated with it.**

![Alt Text](https://i.imgur.com/p7ztfsD.png)

* **Right Click on your user and select "Add to a group".**

![Alt Text](https://i.imgur.com/CXW0TK5.png)

* **Type in "Information Technology" and click "Check Names" and press "OK". You've now added your user to a security group**

![Alt Text](https://i.imgur.com/wMtQoZc.png)

![Alt Text](https://i.imgur.com/kKSroVe.png)

* **Now to verify if the user has been added to our security group you can right click on the user and select "Properties". Click on the tab that says "Members of". As you can see our user has successfully been added to the "Information Technology" group.**
![Alt Text](https://i.imgur.com/5Lp3K2q.png)

# Step 10: Log in to the Windows VM with the AD user credentials

* **Login to your Domain Controller**

* **The first thing we are going to do is add our user to the security group "Remote Desktop Users". While we previously learned how to create a security group, this time we'll join a group that already exists. Adding a user to the "Remote Desktop Users" group grants them the rights to use Remote Desktop. We want to right click on our user and select "Add to a group". Type in "Remote" and then click "Check Names".**

![Alt Text](https://i.imgur.com/CXW0TK5.png)

![Alt Text](https://i.imgur.com/Kwwar1n.png)

* **Check on "Remote Desktop Users" and click "OK". We have now added this user to the "Remote Desktop Users"**

![Alt Text](https://i.imgur.com/XJUBK8Q.png)

* **Now, we are going to log in to our Windows 11 VM with our administrative username and password for our machine. Not the username and password we just created, but the admin username and password we created for this machine. So, I'm going to log in with Admin123 into my Windows 11 VM.**

![Alt Text](https://i.imgur.com/i6dDp5H.png)

* **In your windows search bar type in "System Properties" and hit enter**

![Alt Text](https://i.imgur.com/zvzqo8S.png)

* **Click on "Advanced System Settings"**

![Alt Text](https://i.imgur.com/a8ucorm.png)

* **Click on the "Remote" tab and click on "Select Users**

![Alt Text](https://i.imgur.com/KIgvTY9.png)

* **Click on "Add"**

![Alt Text](https://i.imgur.com/WgX3Gfe.png)

* **Type in the name of the user and click "Check Names". It'll ask for the admin username and password, after that click on "OK"**

![Alt Text](https://i.imgur.com/HlVPKXa.png)


* **Now this user is added to the "Remote" users on this PC and we can now remote into our Windows VM with this user**

![Alt Text](https://i.imgur.com/bJ8drSb.png)


* **Log in to your Windows 11 VM, click on "More choices" and then select "Use a different account"**

 ![Alt Text](https://i.imgur.com/sJbH5T3.png)

* **Enter your username, followed by @domain you created. For example, for me, it will be mjones281@domain.com. Yours will be your created username followed by <@YOURDOMAIN>**

 
 ![Alt Text](https://i.imgur.com/fbep0OU.png)

 * **You have successfully remoted in with the user you just created in Active Directory congrats!!!!!!**

![Alt Text](https://i.imgur.com/ekHMnXU.png)


* **You can open the CMD prompt and type am "whoami" and it will show you are signed in with the user you created!!**

 ![Alt Text](https://i.imgur.com/OPjcH06.png)


# Bonus Section: Create a GPO and link it to an OU.

* **In this bonus step I'm going to show you how to create a GPO and link it to an OU. We are going to deny access to the CMD prompt to users in a certain OU**

* **First, we're going to create another OU. I've already created a few, but for this demo, I'll go ahead and create a few more. I'm going to open Active Directory Users and Computers, navigate to "domain.com," select "New," and then choose "Organizational Unit."**

![Alt Text](https://i.imgur.com/TS30cb3.png)

* **I'm going to name my OU "Payroll" and click "OK." Next, I'll create a sub-OU inside "Payroll" and name it "Users."**

![Alt Text](https://i.imgur.com/nj5EUiY.png)


![Alt Text](https://i.imgur.com/noqmWAm.png)


* **Create a user and place them in the "Users" sub-OU you just created**


![Alt Text](https://i.imgur.com/sQ1fpQR.png)


* **Next, open Group Policy Management. Click on the Windows tab, and under "Windows Administrative Tools," scroll down to "Group Policy Management" and open it..**


![Alt Text](https://i.imgur.com/LO7ohmz.png)


* **Expand on the Forest: domain.com and navigate to your domain. Double-click on your domain.**


![Alt Text](https://i.imgur.com/1bUI4zP.png)

* **Right-click on "Group Policy Object" and select "New."**

* **Name it "Deny CMD Access" and click "Ok."**

![Alt Text](https://i.imgur.com/d4pH7cF.png)


![Alt Text](https://i.imgur.com/MtA1Guz.png)

* **Right click on the GPO and select "Edit"**


![Alt Text](https://i.imgur.com/l5pGRqw.png)

* **Expand "User Configuration," then navigate to "Policies," and further expand "Administrative Templates."**


![Alt Text](https://i.imgur.com/t8Hp8Cg.png)

* **Click on "System," and in the settings to your right, we are going to click on "Prevent access to the command prompt."**

![Alt Text](https://i.imgur.com/9XbDyYV.png)

* **Double click on it. Check the box for "Enabled" and then click "Apply" and "OK"**


![Alt Text](https://i.imgur.com/i5M881e.png)


* **Right click on "Payroll" OU and select "Link an Existing GPO". Select the GPO we just created and click "OK".**

![Alt Text](https://i.imgur.com/ZQKYRyr.png)


![Alt Text](https://i.imgur.com/9F3xE9B.png)

* **Next open your command prompt and type in gpupdate /force**

 ![Alt Text](https://i.imgur.com/VIL2boP.png)


* **Make sure the user you just created is added to the "Remote Desktop Users" group. Additionally, log in to your Windows VM with your admin rights to add the new user to the remote users on the Windows VM**


* **Once you've done that, remote into the machine with the new user who has been denied access to CMD**


![Alt Text](https://i.imgur.com/UAWFfAA.png)

* **In the windows search bar type in cmd and press enter. You can see that user is denied access to the CMD prompt!. Congrats you have just set your first GPO!!!!**

![Alt Text](https://i.imgur.com/25uchWl.png)



## Thank You

* **Thank you so much for following along with me during this step-by-step guide. I hope you were able to learn about Active Directory and the importance it holds in organizations. I also hope you gained insight into the domain controller and its pivotal role in organizational functioning. Whether you're brand new to IT or have been in the field for years, interaction with Active Directory and domain controllers is inevitable. I hope you learned how to set up and configure a server, as well as how to set up a Windows VM. Thank you for sticking with me through this long and detailed tutorial. I hope you can walk away with confidence and a passion to learn more**



## **PLEASE DON'T FORGET TO DELETE YOUR RESOURCES WHEN YOU ARE DONE WITH YOUR VMs!!!**
























