---
toc: false
comments: true
layout: post
title: Accounts
description: This class will require you to make a Portfolio 2026 Web Site, a GitHub Account, a Slack Account, and as part of final exam will require you update your LinkedIn account.
dcategories: [DevOps]
permalink: /devops/tools/accounts
menu: nav/tools_setup.html
toc: true
comments: true
---

## What Is PII?

**PII (Personal Identifiable Information)** is any detail that can identify you—like your name, address, or account info.

In this course, you may share or work with PII. Let’s make sure it’s handled wisely.

---

<div style="display: flex; align-items: flex-start; gap: 24px; margin-top: 20px;">

  <img src="{{site.baseurl}}/images/accounts.png" alt="PII graphic" style="width:50%; max-width:400px; border-radius: 12px;"/>


<div id="pii-container"></div>

<script>
  const piiData = {
    Public: [
      "Name, Email, Photo",
      "Schools, City, Property",
      "Credit Reports, Router Info"
    ],
    Sensitive: [
      "Birthdate, Address, Phone",
      "Place of Birth, Maiden Names",
      "Driver’s License"
    ],
    Private: [
      "Social Security Number",
      "Login Credentials",
      "Two-Factor Sources"
    ]
  };

  const container = document.getElementById("pii-container");
  const heading = document.createElement("h3");
  heading.textContent = "Know Your PII";
  container.appendChild(heading);

  Object.entries(piiData).forEach(([category, items]) => {
    const button = document.createElement("button");
    button.textContent = `▶ ${category}`;
    button.style.margin = "10px 0";
    button.style.padding = "8px 14px";
    button.style.border = "none";
    button.style.borderRadius = "8px";
    button.style.backgroundColor = "#2c2a5d";  // dark blue/purple
    button.style.color = "white";
    button.style.fontSize = "16px";
    button.style.cursor = "pointer";
    button.style.transition = "background-color 0.3s";

    button.onmouseover = () => button.style.backgroundColor = "#3a3770";
    button.onmouseout = () => button.style.backgroundColor = "#2c2a5d";

    const list = document.createElement("ul");
    list.style.display = "none";
    list.style.margin = "8px 0 16px 20px";

    items.forEach(item => {
      const li = document.createElement("li");
      li.textContent = item;
      li.style.padding = "4px 0";
      list.appendChild(li);
    });

    button.addEventListener("click", () => {
      list.style.display = list.style.display === "none" ? "block" : "none";
    });

    container.appendChild(button);
    container.appendChild(list);
  });
</script>



</div>

<div style="display: flex; align-items: flex-start; gap: 24px; margin-top: 12px;">

  <img src="{{site.baseurl}}/images/mfa.jpg" alt="Multi-Factor-Authentication" style="width:50%; min-width:120px; border-radius: 12px;" title='This is an Multi-Factor-Authentication'/>

  <div>
    <strong>Protect Your Information</strong>
    <ul>
      <li>Use <strong>Multi-Factor Authentication (MFA)</strong></li>
      <li>Create <strong>strong, unique passwords</strong></li>
      <li>Keep your <strong>software updated</strong></li>
      <li><strong>Encrypt</strong> data and backups</li>
      <li>Secure your <strong>Wi-Fi and router</strong></li>
      <li>Use <strong>biometrics</strong> where possible</li>
    </ul>
  </div>

</div>

---

### Online Risks

- **Phishing & malware** try to steal your data
- **Social engineering** tricks you into revealing info
- **Respond quickly** if compromised: update passwords and review your security

---

# Nighthawk Coders Accounts

In this lesson, you'll create several accounts and provide a public-facing name and email for some of them.

<div style="display: flex; align-items: flex-start; gap: 32px; margin-top: 16px;">

  <div>
    <h3><u style="color:white">Email Accounts</u></h3>
    Used for communication with your teacher and classmates.<br>
     Tip: Use different emails for junk, school, and important info.

    <h3><u style="color:white">Github Account</u></h3>
    Create a public-facing account for coding.<br>
     Use a junk/common email, not your school email.

    <h3><u style="color:white">GitHub Pages</u></h3>
    Build a public portfolio site.<br>
     It will be Google-indexed and viewable by anyone.

    <h3><u style="color:white">Slack Account</u></h3>
    Class-only communication tool.<br>
     Use a junk/common email. PII is limited to classmates and teacher.

    <h3><u style="color:white">Portfolio 2026 Account</u></h3>
    Tied to your GitHub ID.<br>
     Used for course tools, services, and analytics.
  </div>

  <img src="{{site.baseurl}}/images/12we.png" alt="Account Types" style="width:600px; border-radius: 12px;"/>
</div>

## PII Strategy on Account Creation

It is in the your interest that you establish and continually refine your PII (Personal Identifiable Information) strategy. It is likely that you are already active in sharing common PII, considering for yourself what is OK to share. As you progress in the digital world, you will likely need to adapt.

### Key Points to Consider:

1. **Categorize Information**: 
   - **Public Information**: Information you are comfortable sharing publicly, such as your name and general interests.
     <img src="{{site.baseurl}}/images/information.jpg" alt="Multi-Factor-Authentication" style="width:25%; min-width:120px; border-radius: 12px;"/>

   - **Sensitive Information**: Information that should be shared cautiously, such as your full birth date and phone number.
        <img src="{{site.baseurl}}/images/something.png" alt="Multi-Factor-Authentication" style="width:50%; min-width:120px; border-radius: 24px;"/>

   - **Highly Confidential Information**: Information that should be kept strictly private, like social security number and internet access credentials.
        <img src="{{site.baseurl}}/images/confidential.jpeg" alt="Multi-Factor-Authentication" style="width:40%; min-width:120px; border-radius: 12px;"/>


2. **Use Different Email Accounts**: 
   - Maintain different email accounts for different purposes (e.g., junk email, common email, work/school email, important email). This helps manage the type and volume of information you receive and sets expectations for the importance of the information.

3. **Be Prepared for Security Incidents**: 
   - Anticipate that you may be hacked and will need to secure any vulnerabilities. Regularly update your passwords and use multi-factor authentication where possible.

4. **Adapt and Evolve**: 
   - As you gain more experience and your digital footprint grows, continually reassess and adapt your PII strategy to ensure it remains effective.

### Parting Advice:

Be cautious with the information you share online. Protect your personal data by using separate email accounts, staying aware of security risks, and adapting your practices as the digital world evolves. Taking steps now helps safeguard your digital identity in the future.

<details style="border: 2px solid #006600; border-radius: 12px; padding: 10px; margin-bottom: 16px; box-shadow: 2px 2px 10px rgba(0,0,0,0.1); font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; font-size: 1.1rem;">
  <summary style="font-weight: bold; cursor: pointer;"> 🧠 Test Your Knowledge</summary>
  <div style="margin-top: 10px;">
    <p>Ready to check your understanding?</p>
    <a href="{{site.baseurl}}/piiquiz/" style="background-color: #006600; color: white; padding: 10px 15px; border-radius: 8px; text-decoration: none; font-weight: bold;">
      Take the Quiz
    </a>
  </div>
</details>