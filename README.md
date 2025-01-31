## Shared Network Files And Permissions in Azure
![image](https://github.com/user-attachments/assets/05e77b24-b87e-40b8-b02b-916c4e15b7b4)

### Overview
In this lab, we will set up shared network files on DC-1 and configure file access permissions for different user groups. The goal is to control access so that only designated users can view or modify specific folders. The Lab used for Active dirctory setup will be use for this project.

### Prepare The Environment
-  Turn on the Virtual Machines (VMs)
  -  Log into the Azure Portal → Go to Virtual Machines.
  -  Start both DC-1 and Client-1 if they are off.
  -  Use Remote Desktop (RDP) to log into both machines.
 
### Create Shared Folders on DC-1
-  Create Folders in C:\ Drive
-  On DC-1, open File Explorer.
-  Navigate to *C:* and create the following folders:
  -  read-access
  -  write-access
  -  no-access
  -  accounting
![](https://i.imgur.com/fg3F3zW.png)

###  Configure File Sharing And Permissions
-  Set Permissions for Each Folder
-  Right-click a folder → Properties → Sharing tab.
  -  Click Share →add tab: type "Domin Users".
    -  Click and check Permissions level, then share and done:
    -  read-access	Domain Users	Read
    -  write-access	Domain Users	Read & Write
    -  no-access	Domain Admins	Read & Write
    -  accounting	Accountants Group	Read & Write
-  Click OK and Apply on each folder.
![](https://i.imgur.com/GxOiUPx.png)

###  Test Access from Client-1
Attempt to Access the Shared Folders
-  Log into Client-1 as a normal user.
-  Press Win + R, type \\DC-1, and press Enter.
-  Try opening the shared folders:
-  ✅ read-access: Can view files but not edit.
-  ✅ write-access: Can view and modify files.
-  ❌ no-access: Should be denied access.
![image](https://github.com/user-attachments/assets/72d84dd2-313b-4bba-878a-3b375a87d181)
![image](https://github.com/user-attachments/assets/79ed87db-116e-4124-9814-1cbac79faeff)
![image](https://github.com/user-attachments/assets/b37a9ec9-95de-48e6-9847-49bc0fe72dc3)

### Create A Security Group In Active Directory
Create "Accountants" Group
-  On DC-1, open Active Directory Users and Computers (ADUC) (dsa.msc).
-  Create OU _GROUP, open _GROUP, rght click and creat "Accountants"
- Click OK.
![](https://i.imgur.com/O3bDSIo.png)
![](https://i.imgur.com/Jnstbgb.png)

### Assign "Accountants" Group to the Accounting Folder
Go to Accounts Folders in C:\ Drive
-  On DC-1, open File Explorer.
-  Navigate to *C:* 
-  Configure the "accounting" Folder
  -  Right-click a folder → Properties → Sharing tab.
  -  Click Share →add tab: type "ACCOUNTANTS".
    -  Click and check Permissions level, Select Read & Write
     -  then share and done:
-  Click OK and Apply.
-  https://i.imgur.com/O3bDSIo.png

###  Step 7: Test Security Group Permissions
Try to Access "accounting" as a Normal User
-  Log into Client-1 as (normal user). mydomain.com\law.fic
-  Open File Explorer → Type \\DC-1 in the address bar.
-  Try to open the accounting folder → It should be denied.
![image](https://github.com/user-attachments/assets/c36b3585-c3cc-4083-ba1e-9481203b038e)

### Add a User to the Accountants Group
Grant Access to "accounting" Folder
-  On DC-1, open Active Directory Users and Computers (ADUC) (dsa.msc)
-  doble-click _GROUP → right click account security → Properties
-  Go to the Member Of tab → Click Add.
-  Type law.fik → Check name, Click OK and Apply.
![](https://i.imgur.com/C9N4lyi.png)

### Verify Access AS An Accountant
Reattempt Access to "accounting"
-  Log out and log back into Client-1 as <law.fik>.
-  Open \\DC-1 and try to access the accounting folder.
It should now open successfully!
![image](https://github.com/user-attachments/assets/c0dc96bd-ac83-4923-bff2-e6d10891a204)

### Conclusion
In this lab, we successfully: ✅ Created shared folders on DC-1
✅ Configured file permissions
✅ Tested access from Client-1
✅ Created a security group in Active Directory
✅ Assigned users to the group and verified permissions








