<h1 id="top"> Active Directory: Basic Tasks </h1>

We’ll perform some beginner-friendly but essential Active Directory tasks inside the lab environment that we had created in our Lab-Setup file. 
If you haven't completed that, I recommend starting there first. [Lab Setup Guide](../Lab-setup.md)

We’ll be working inside our Windows Server 2019 virtual machine and our Windows 10 client machine, both of which should already be part of the same domain.

---

## 📜 Table of Contents

- [📁 Step 1. Create Organizational Units (OUs)](#-create-organizational-units)
- [👤 Step 2. Create User Accounts](#-create-user-accounts)
- [👥 Step 3. Create Security Groups](#step-1)
- [🔗 Step 4. Add Users to Groups](#step-2)
- [🧠 Step 5. Move CLIENT01 into the Appropriate OU](#step-3)
- [🖥️ Step 6. Create and Link a GPO](#step-4)
- [🧪 Step 7. Test the GPO](#step-5)

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

## 👥 Step 3. Create Security Groups

Groups are used to manage permissions or apply policies to multiple users at once. Let's create some groups!

1. In **Active Directory Users and Computers**, right-click `HR` → **New** → **Group**.

![New HR Group](images/ad-tasks/16-create-sg.png)

2. Use these details:
   - Group name: `Managers`
   - Group scope: `Global`
   - Group type: `Security`
4. Click `OK`.

![Managers Group](images/ad-tasks/17-create-sg.png)

🧑‍💻 Repeat for `ITSupport`:

![New HR Group](images/ad-tasks/18-create-sg.png)

- Use these details:
   - Group name: `HelpDesk`
   - Group scope: `Global`
   - Group type: `Security`
- Click `OK`.

![Managers Group](images/ad-tasks/19-create-sg.png)


[🔝 Back to Top](#top)

---

## <h2 id="step-2"> 🔗 Step 4. Add Users to Groups </h2>

Let’s assign our users to their department groups.

1. Still in **Active Directory Users and Computers**, double-click `jsmith` in the `HR` OU.

![Double Clicky](images/ad-tasks/20-create-gu.png)

2. Go to the **Member Of** tab, then click `Add...`

![Member Of Tab](images/ad-tasks/21-create-gu.png)

3. Type `Managers`, click `Check Names`, then click `OK`.

![Check Name: Managers](images/ad-tasks/22-create-gu.png)

![Name Checked: Managers](images/ad-tasks/23-create-gu.png)

4. Click `OK` to close **John Smith Properties** window.

![Close Properties](images/ad-tasks/24-create-gu.png)

🧑‍💻 Do the same for `jdoe` in `ITSupport`:

![Double Clicky](images/ad-tasks/25-create-gu.png)

![Member Of Tab](images/ad-tasks/26-create-gu.png)

- Add `jdoe` to `HelpDesk`.

![Check Name: Managers](images/ad-tasks/27-create-gu.png)

![Name Checked: Managers](images/ad-tasks/28-create-gu.png)

[🔝 Back to Top](#top)

---

## <h2 id="step-3"> 🖥️ Step 5. Move CLIENT01 into the Appropriate OU </h2>

To make sure GPOs apply correctly, you need to move your client machine (`CLIENT01`) into the OU you're working with.
Follow these steps:

1. In **Active Directory Users and Computers**, expand your domain (`corp.local`) and click on **Computers**.

![AD Users and Computers](/images/ad-tasks/29-create-gpo.png)

2. In the right panel, right-click `CLIENT01`, the click `Move...`.

![Move CLIENT01](/images/ad-tasks/30-create-gpo.png)

3. Choose the `HR` OU
4. Click `OK`.

![Select HR](/images/ad-tasks/31-create-gpo.png)

✅ **Why this matters:** GPOs targeting computers will only work if the computers are in the right OU. 

[🔝 Back to Top](#top)

---

## <h2 id="step-4">  🧠 Step 6. Create, Link, and Push a GPO </h2>

We’ll now create a **Group Policy Object (GPO)** that displays a message when users log in. This will help confirm the GPO is working.

1. Open **Server Manager** → **Tools** → **Group Policy Management**.

![Server Manager - Tools](/images/ad-tasks/32-create-gpo.png)

2. Expand `corp.local` → `Departments`.
3. Right-click `HR` → **Create a GPO in this domain, and Link it here...**

![Create a GPO](/images/ad-tasks/33-create-gpo.png)

4. Name it: `HR Login Message`, then click OK.

![Name GPO](/images/ad-tasks/34-create-gpo.png)

5. Right-click the new GPO under `HR` and click `Edit`.

![Edit HR GPO](/images/ad-tasks/35-create-gpo.png)

6. In the **Group Policy Management Editor**, navigate to:
   - **Computer Configuration** → **Policies** → **Windows Settings** → **Security Settings** → **Local Policies** → **Security Options**
7. Find and double-click **Interactive logon: Message title for users attempting to log on**.

![Interactive Logon:](/images/ad-tasks/36-create-gpo.png)

8. Set the title to 'HR Notice' and click `OK`.

![Interactive Logon:](/images/ad-tasks/37-create-gpo.png)

9. Find and double-click **Interactive logon: Message text for users attempting to log on**.

![Interactive Logon:](/images/ad-tasks/38-create-gpo.png)

10. Set the message to 'This system is for HR use only.' and click `OK`.

![Set Title](/images/ad-tasks/39-create-gpo.png)

11. In the left panel, right-click `HR` and click **Group Policy Update...**
   - 💡 This pushes the GPO update remotely to all computers in that OU — including `CLIENT01`.

![Push GPO](/images/ad-tasks/39-create-gpo.png)

✔️ This message will now show every time a user logs into CLIENT01.

🎉 Now we're ready to test!

[🔝 Back to Top](#top)

---

##<h2 id="step-5"> 🧪 Step 7. Test the GPO </h2>

Now let's test that the login message works.

1. Power on `CLIENT01`, or restart if it's already running.

2. You should see the login message!

![Login Message](/images/ad-tasks/40-create-gpo.png)

🎉 That’s it! The GPO is working.

[🔝 Back to Top](#top)

---
