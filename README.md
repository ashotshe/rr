<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network Files and Permission </h1>

This tutorial demonstrates how to share resources over the network while managing access based on user roles. It covers how to configure permissions for users to Read, Write, or Deny access, depending on their group membership. Additionally, we will use Active Directory to create and manage Security Groups to control access efficiently.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Active Directory Users and Computers(ADUC)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

  <h2>Files and Permissions </h2>

### **Step 1: Log into DC-1 and Client-1**

1. **Log into DC-1**: Use your admin account to log into **DC-1** (the Domain Controller).
2. **Log into Client-1**: Log into **Client-1** as a domain user from the previous lab session. If you're unsure about these steps, please review the following tutorials:
   - [Active Directory Setup](https://github.com/ashotshe/configure-ad)
   - [Users, Group Policy, and Account Management](https://github.com/ashotshe/Users-Group-Policy-Account-Management/tree/main)

---
### **Step 2: Create Folders on DC-1's C:\ Drive**

1. Open the **C:\** drive on **DC-1**.
2. Create the following four folders:
   - **Read-access**
   - **Write-access**
   - **No-access**
   - **Accounting**
---
     
![a1](https://github.com/user-attachments/assets/522267eb-cfc5-4ba9-b494-d4b34322dcd8)

---

### **Step 3: Set Folder Sharing Permissions**

1. **Set Permissions for "Read-access" Folder**:
   - Right-click the **Read-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, then type `domain users` into the "Enter names" field.
   - Click **Add**, and assign **Read** permissions.

---

![ade1](https://github.com/user-attachments/assets/0576cb81-0b7a-4715-8ceb-e7874ed3792c)
![ade2](https://github.com/user-attachments/assets/4dbe8370-c727-454b-9095-085e016f6341)
![ade3](https://github.com/user-attachments/assets/c37aa94b-e7ef-46b8-a77c-df6fcef3842b)
![ade4](https://github.com/user-attachments/assets/105e6fbb-f5b8-4476-b4c4-8ff4956fe943)
![a5](https://github.com/user-attachments/assets/5b3920a4-76ea-492d-a687-67118075ec6d)

---

2. **Set Permissions for "Write-access" Folder**:
   - Right-click the **Write-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, then type `domain users` again.
   - Click **Add**, and assign **Read/Write** permissions.
     
---
![ade6](https://github.com/user-attachments/assets/231d4b13-7a72-4141-9d13-2b46b6c2e714)

---

3. **Set Permissions for "No-access" Folder**:
   - Right-click the **No-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, and add `domain admins`.
   - Assign **Read/Write** permissions to **domain admins**.

4. **Leave the "Accounting" Folder**:
   - No changes are needed for the **Accounting** folder at this time.

---

### **Step 4: Verify Folder Access from Client-1**

1. Log into **Client-1** using one of your domain user accounts.
2. Open **File Explorer** and enter `\\dc-1` in the address bar to view the shared folders on **DC-1**.
3. Check the following:
   - **No-access** folder: You should not be able to access this folder.
   - **Read-access** folder: You should only be able to **read** files (modifying files is not allowed).
   - **Write-access** folder: You should be able to **read and write** files (adding or editing documents is allowed).
     
---  
   
![ade8](https://github.com/user-attachments/assets/2eac2493-9c21-4f38-bbdf-113a0c06df28)
![a8](https://github.com/user-attachments/assets/1190bb2a-19b2-46a8-913c-3a290bb4cf0e)
![a9](https://github.com/user-attachments/assets/cae27bf0-1ce0-40cf-8d88-caf988fe1415)


---

### **Conclusion**
- You've successfully set up and tested folder permissions within a domain environment.
- The different access levels (Read, Write, No Access) should now function as expected when accessed from **Client-1**.


  <h2>Security Groups</h2>



### **Step 1: Create an Organizational Unit (OU) in Active Directory**

1. **Log into DC-1**: Open **Active Directory Users and Computers (ADUC)** on **DC-1**.
2. **Create a New Organizational Unit (OU)**:
   - Right-click on your domain name, select **New**, and then choose **Organizational Unit**.
   - Name the new OU `_TEAMS`.

---

![a10](https://github.com/user-attachments/assets/e87532c9-3d51-440e-89e4-deb55229fe69)

---



### **Step 2: Create a New Group for Accountants**

1. **Create a Group**:
   - Right-click on the newly created **_TEAMS** OU, then select **New** and choose **Group**.
   - Name the group **ACCOUNTANTS**.
     
---
![a10](https://github.com/user-attachments/assets/b85bbcde-01e6-4c48-90fd-53ddf8da0462)

![adey](https://github.com/user-attachments/assets/09ee57a7-f78f-404c-b378-8a26efec52ef)

![a12](https://github.com/user-attachments/assets/3ca83716-8a3f-46d5-b74d-50b79d4c2724)

---

### **Step 3: Set Permissions for the Accountants Folder**

1. **Go to the "Accountants" Folder**: Navigate back to the folder you created earlier for **ACCOUNTANTS** (the one you set permissions for).
2. **Set Permissions**:
   - Right-click the **ACCOUNTANTS** folder and select **Properties**.
   - Go to the **Security** tab.
   - Click **Edit** and add the **ACCOUNTANTS** group.
   - Assign **Read/Write** permissions for the group.
---

![ade12](https://github.com/user-attachments/assets/b549ce79-c838-494a-a442-eaefe014c9e5)

---

### **Step 4: Test Access from Client-1**

1. **Log into Client-1** as a domain user who is not yet part of the **ACCOUNTANTS** group.
2. Open **File Explorer** and navigate to the **ACCOUNTANTS** folder by typing `\\dc-1` in the address bar.
3. **Verify Access**:
   - You should not be able to access the **ACCOUNTANTS** folder, as the user isn’t part of the group yet.
---

![a14](https://github.com/user-attachments/assets/ea33f469-4a06-49e1-855e-a7c4e1287c9a)


---

### **Step 5: Add the User to the ACCOUNTANTS Group**

1. **Go Back to DC-1**: Log back into **DC-1**.
2. **Add the User to the ACCOUNTANTS Group**:
   - In **Active Directory Users and Computers (ADUC)**, find the **Security Group** for the user you want to add.
   - Right-click on the user and select **Properties**.
   - Go to the **Member Of** tab, click **Add**, and type **ACCOUNTANTS** to add the user to the group.
   - Click **OK** to save the changes.
---

![adelast](https://github.com/user-attachments/assets/9dea22c5-0a6f-48d6-b4b3-5586600d5836)


---

### **Step 6: Test Access Again from Client-1**

1. **Log Back into Client-1**: Sign out and log back into **Client-1** with the same user account.
2. Open **File Explorer** and type `\\dc-1` again to access the **ACCOUNTANTS** folder.
3. **Verify Access**:
   - This time, you should be able to access the **ACCOUNTANTS** folder, as the user is now part of the **ACCOUNTANTS** group with **Read/Write** permissions.
---

![Capture](https://github.com/user-attachments/assets/d5e8289e-99c2-46ec-b67a-0b0e0d179a15)


---

### **Conclusion**
- You've successfully used Active Directory to manage folder permissions by creating a group and adding users to it.
- The permissions should now work correctly, allowing group members to access the **ACCOUNTANTS** folder as intended.

---

  
