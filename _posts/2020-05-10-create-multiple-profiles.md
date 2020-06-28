---
title: "How To: Create Multiple Profiles in Chrome"
last_modified_at: 2020-05-10
categories:
  - howto
tags:
  - howto
  - productivity
  - browser
  - chrome
excerpt: |
  How to solve authentication woes by using multiple profiles in Chrome
---

I frequently find myself logging into the same SaaS applications for different clients simultaneously. Examples of such applications include: Azure Portal, Azure DevOps, Microsoft Teams, Microsoft SharePoint, etc. I also have multiple Google accounts for my personal e-mail and Google Play Store. While each of these services support multiple logins, switching accounts is a pain and often doesn’t support you using more than one account at a time across browser windows or tabs. In the past you may have overcome this by installing multiple browsers (ex: Chrome for personal, Edge for company, Firefox for projects) or making heavy use of incognito mode, but browsers like Chrome and Edge (and probably others) now make it easy to run account-specific sandboxes. It’s a far more convenient solution and solves problems like:

* How do I use two instances of Microsoft Teams at the same time?
* How can I pull documents from different SharePoint sites without always having to log in?
* How do I keep my company browsing history separate from my personal browsing history?

I also find it best to create separate Chrome accounts for each tenant to support syncing. Let’s get started!

### Step 1: Add Person
1. Click on your user icon in the top right (just left of the ellipsis menu) and choose “+ Add”
  ![Step 1a](/assets/images/2020-05-10/1a.png)

2. Enter a name that uniquely identifies this account (such as the name of your company), pick any photo, and click “Add” (the photo is easy to change later)
  ![Step 1b](/assets/images/2020-05-10/1b.png)

### Step 2: Create Chrome Profile
A Chrome profile will allow you to save passwords and sync settings and browsing history across multiple devices that might use this account

1. Select “Already a Chrome User? Sign in”
  ![Step 2a](/assets/images/2020-05-10/2a.png)

2. Assuming you don’t already have a Google account for your company’s e-mail address, select “Create Account”. Please note, this is just a “Google” account 
![Step 2b](/assets/images/2020-05-10/2b.png)

3. Choose “Use my current email address instead” and use your company account, this way you don’t need to create a separate email account
![Step 2c](/assets/images/2020-05-10/2c.png)

4. Enter your information, click “Next”
![Step 2d](/assets/images/2020-05-10/2d.png)

5. Choose “Yes, I’m in” to sync your settings
![Step 2e](/assets/images/2020-05-10/2e.png)

### Step 3: Fix Your User Icon
For whatever reason, Chrome replaces the icon selected in Step 1 with a generic icon for your new Google account. You’ll want a unique picture for each Chrome person so you can easily distinguish them.
1. Click the Ellipsis menu in the top right and choose “Settings”
  ![Step 3a](/assets/images/2020-05-10/3a.png)

2. Click “Chrome name and picture”
  ![Step 3b](/assets/images/2020-05-10/3b.png)

3. Select the picture you want (it will now show up right of the Address/Search bar, and in your task bar icon
  ![Step 3c](/assets/images/2020-05-10/3c.png)

### Step 4: Pin Your Chrome Profile to the Taskbar
For easy access and being able to run multiple sessions in parallel, you will want to pin another Chrome icon to the taskbar. All Chrome windows that you open will stack behind the taskbar icon so it will be easy to see what Chrome Person you’re windows are linked to, and to navigate all the windows for a specific Chrome person.

* Right-click on the taskbar icon for your Chrome person
* Click “Pin to taskbar”

![Step 4a](/assets/images/2020-05-10/4a.png)

You can use the same technique in Steps 3 and 4 to associate a user image to your original Chrome taskbar icon. Please note the “Show desktop icon” toggle and ensure it is turned on.

## Using Your “New Browser”
Here are some tips on how to make your new Chrome person work for you:
* Use the “Add shortcut” button to add links to sites you frequently visit with your alternate account. This might include webmail, Microsoft Teams, an Intranet, CRM, or other applications you frequently log in to.
* When opening links that require authentication (like links in an email/PDF/etc. to documents on the company SharePoint or Teams site) they will open in the most recently used Chrome profile.
  * Click the Chrome profile from the task bar you want to open the document in (this means any links that open will open in that profile/program)
  * Click the link in your e-mail
* Try to never log into accounts from one profile while using another profile.
  * I delete any cached company credentials from my personal Chrome and vice versa. This can be done on the authentication page for many web applications by choosing “Forget \[account\]”
  * When I accidentally open a “company” link in my “personal” browser (and get an authentication failure), I close the tab, click on my “company” Chrome person icon to make it the most recently used profile, and click link again.

Now that I’ve started using different profiles in Chrome, there’s no going back. The struggles and frustrations of having to log in and out of the same website are gone and I can go from site to site confident that I’m accessing them using the correct credentials. I hope this technique works just as well for you!
