# Lab 01: Role Based Access Control (RBAC) 
## Overview:
This lab focuses on implementing **Role-Based Access Control (RBAC)** in Azure to manage access to resources and groups based on assigned roles. The goal is to enforce the **principle of least privilege**, ensuring users only have permissions necessary to the specific job or task they may have at hand. 
---
## Step 1: Create a New User
From the Azure Portal, I user the search bar to access **Microsoft Entra ID**, I then selected the *Users* bladeand selected *Add -> Create new user*. From Here, I created a new user named **Joseph Price**
![Creating new user](../2025-10-17%20(20).png)
---
## Step 2: Create a Security Group 
Next, I created a **Security Group** named *Senior Admins* to simplify access management by assigning roles to groups instead of idividual users. This is best practise for simplifying RBAC in large scale tenants. 
![Creating new security group](../2025-10-17%20(21).png)
---
## Step 3: Assigning a User as Admin of the Security Group
I then assigned the user *Joseph Price* the admin role for the *Senior Admins* security group. 
![Assigning user as admin of group](../2025-10-17%20(22).png)
---
## Step 4: Add User via PowerShell
Using PowerShell, I then added a user called *Isabel Garcia* and created a group called *Junior Admins*, adding the user to the group.
![User and group creation through powershell](../2025-10-17%20(23).png) ![Continued user and group creation through powershell](../2025-10-17%20(24).png)
---
## Step 5: Add User via Bash 
I then switched to a **Bash** window to add a user called *Dylan Williams* and create a group called *Service Desk*, adding the user to the group.
![User and group creation through bash](../2025-10-17%20(25).png) ![Continued user and group creation through bash](../2025-10-17%20(26).png) ![Final user and group creation through bash](../2025-10-17%20(27).png)
---
## Step 6: Creating a Resource Group 
After this, I navigated back to the **Azure Portal** to create a Resource Group *AZ500-Lab01*.
![Creating the AZ500-Lab01 resource group](../2025-10-17%20(28).png)
---
## Step 7: Assigning a Role at the Resource Group Level
From here, I used the **Access Control Management (IAM)** blade in the AZ500-Lab01 resoure group to assign a role. I searched for the **Virtual Machine Contributor** and added the **Service Desk** group as a member. This gives the permission to any user or resource who is a member of the group to manage virtual machines but not delete the resource group itself, following the **principle of least privilege**
![Using the IAM blade to assign a role to the Service Desk group](../2025-10-17%20(29).png)
---
## Step 8: Verification 
Finally, I verified the users and groups were given the correct roles to verify my actions had taken place. 
![Verification of Users and Roles](../2025-10-17%20(30).png)
---
## Key Takeaways 
- RBAC allows for fine-grained control over Azure users and resources.
- Assigning roles to groups allows for a larger scope in order to simplify management and improve the security of a tenant.
- Following the **principle of least privilege** allows for proper user control and reduces the risk of accidental or malicious actions
---
## Summary 
This lab demonstrates how RBAC helps organisations control access efficiently across Azure. By assigning permissions to groups and verifying access levels, administators can ensure a secure and scalable access model across their tenant or other area of administration. 
*End of Lab 01 - Role-Based Access Control*
