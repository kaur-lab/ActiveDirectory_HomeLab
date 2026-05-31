<h1 id="top"> Active Directory: Basic Tasks </h1>

We’ll perform some beginner-friendly but essential Active Directory tasks inside the lab environment that we had created in our Lab-Setup file. 
If you haven't completed that, I recommend starting there first. [Lab Setup Guide](../Lab-setup.md)

We’ll be working inside our Windows Server 2019 virtual machine and our Windows 10 client machine, both of which should already be part of the same domain.

---

## 📜 Table of Contents

- [📁 Step 1. Create Organizational Units (OUs)](#-create-organizational-units)
- [👤 Step 2. Create User Accounts](#-create-user-accounts)
- [👥 Step 3. Create Security Groups](#-step-3-create-security-groups)
- [🔗 Step 4. Add Users to Groups](#-step-4-add-users-to-groups)
- [🧠 Step 5. Move CLIENT01 into the Appropriate OU](#step-5)
- [🖥️ Step 6. Create and Link a GPO](#-step-6-create-link-and-push-a-gpo)
- [🧪 Step 7. Test the GPO](#-step-7-test-the-gpo)
- [📦 Wrapping Up](#-wrapping-up)
- [💬 Questions or Feedback?](#questions-or-feedback)

---
## 📁 Step 1. Create Organizational Units (OUs)

OUs (Organizational Units) help organize users, groups, and computers into logical containers. You’ll start by creating two OUs: one for IT Support and one for HR.

1. Open **Server Manager** → **Tools** → **Active Directory Users and Computers**.

![Users and Computers](images/ad-tasks/03-create-ou.png)

2. In the left panel, expand your domain (`corp.local`).
3. Right-click `corp.local` → **New** → **Organizational Unit**.

![New OU](images/ad-tasks/04-create-ou.png)

4. Name it: `Departments`, and click OK.
   - 🔒 **Best practice**: Leave **"Protect container from accidental deletion"** checked. For *lab* purposes, however, its your choice.

![Departments OU](images/ad-tasks/05-create-ou.png)

5. Right-click `Departments` → **New** → **Organizational Unit** again.
   - 💡 **Tip**: You can also left click `Departments` and right-click in the detail window to bring up the menu. I'll show you in the screenshot.

![New OU, again](images/ad-tasks/05-create-ou.png)

6. Use this process to create two sub-OUs:
   - `HR`
   - `ITSupport` 

<p float="left">
  <img src="images/ad-tasks/07-create-ou.png" alt="HR Sub-OU" width="400" />
  <img src="images/ad-tasks/08-create-ou.png" alt="ITSupport Sub-OU" width="400" />   
</p>

🎉 You now have a clean structure for organizing your user accounts and departments.

[🔝 Back to Top](#top)

---

## 👤 Step 2. Create User Accounts

Let’s create one user for each department.

1. In **Active Directory Users and Computers**, right-click `HR` → **New** → **User**.
   - 💡 **Tip**: Remember, you can also left click `HR` and right-click in the detail window to bring up the menu. 

![New HR User](images/ad-tasks/09-create-user.png)

2. Use these details:
   - **First name**: `John`
   - **Last name**: `Smith`
   - **User logon name**: `jsmith`
3. Click `Next`.

![John Smith](images/ad-tasks/10-create-user.png)

4. Set a password.
   - Don't forget this one. Maybe write it down this time...
   - 🔒 **Best practice**: Leave “User must change password at next logon” checked. This is a security habit used in real-world environments.
     
5. Click `Next`, then click `Finish`.

![Set Password](images/ad-tasks/11-create-user.png)

6. Repeat for the `ITSupport` OU:

![New HR User](images/ad-tasks/12-create-user.png)

7. Use these details:
   - **First name**: `Jane`
   - **Last name**: `Doe`
   - **User logon name**: `jdoe`
8. Click `Next`.

![Jane Doe](images/ad-tasks/13-create-user.png)

![Set Password](images/ad-tasks/14-create-user.png)

🎉 This is all for create users one by one.

[🔝 Back to Top](#top)

---
