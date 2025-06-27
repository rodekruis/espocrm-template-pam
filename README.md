# EspoCRM Feedback Management Template

The EspoCRM Feedback Management Template is created by the [510 Data & Digital team](https://510.global/) of the Netherlands Red Cross.
It is designed to help humanitarian teams strengthen trust with communities by making it easy to listen and respond to community feedback in a structured way.

---

## Table of Contents

- [About](#about)  
- [Features](#features)  
- [Requirements](#requirements)  
- [Installation](#installation)  
- [How to Use](#how-to-use)  
- [Terms of Use](#terms-of-use)  

---

## About

This template enables you to easily record, track, and manage feedback from staff, volunteers or community members, all within EspoCRM with the possibility to integrate with KoboToolbox. It provides simple forms, clear status tracking, and visual dashboards to help humanitarian teams improve feedback handling.

**Flexibility and simplicity are at the heart of this template:**
- It provides many example questions and feedback types, so organisations can easily adapt it to their own needs and contexts.
- The data model is kept as simple as possible. This makes the system easy to understand, maintain, and use, even as teams make their own custom changes.

This template is designed so anyone, no matter their digital skills, can collect and act on feedback in a clear and organised way.


---

## Features

- 📝 **User-friendly feedback forms** for easy data entry  
- 🔄 **Clear status tracking** (open, in progress, closed)  
- 📊 **Visual dashboards and reports** to see feedback at a glance  
- ❓ **Pre-built examples** of questions and answer options to help you get started 
- 👤 **Role-based permissions:** control who can view, edit, or manage feedback according to their role in EspoCRM
- 📊 **Dashboard and Reports**: See an easy overview of feedback status and counts 
- 📱 **Possible integration with KoboToolbox:** collect feedback offline and sync with EspoCRM when back online  
- 📈 **Possible integration with Power BI:** connect EspoCRM data to PowerBI for advanced visualisations and reports  
- 🛠 **Customization**: Add your own fields, layouts, dashboards and automatic flowcharts without coding  

---

## Requirements

### Hard Requirements
These are needed to install and use the template:
- Installed EspoCRM **v7.2 or higher** ([docs](https://github.com/rodekruis/EspoCRM-knowledge-base/wiki/Installation#install-a-virtual-machine-for-espocrm-in-azure)) 
- **Admin user** access to install the template
- Already procured and installed **[EspoCRM Advanced Pack extension](https://www.espocrm.com/extensions/advanced-pack/)**  

### Recommendations:
These are not required, but will improve your experience:

- **Backup of your EspoCRM data**  
  (Recommended before installation.
- **Email notifications configured**  
  (So your team can receive alerts about new feedback.)
- **Single Sign-On (SSO) configured**  
  (If your organisation uses SSO, this makes it easier and safer for team members to log in.)
- **Up-to-date web browser**  
  (For best performance and security.)

---

## Installation
The following steps will install the template itself and recommends the installation of additions and changes to the UI. See [INSTALL.md](INSTALL.md) for a more detailed guide with screenshots, also for integration of KoboToolbox with template.

1. Download the [latest release ZIP]() from this repository.  
2. Log in as **Admin** in your EspoCRM instance.  
3. Go to **Administration ▸ Extensions ▸ Import**.  
4. Upload the ZIP file and Click `Install`
6. **Import data files:**  
   For every file in the [import folder]() of this repository, import it into EspoCRM:
   1. Go to **Administration ▸ Import**.
   2. Under **What to Import? > Entity Type**, select the entity that matches the file name.  
      (For example: if the file is `Roles.csv`, select `Roles`.)
   3. Click **Next**.
   4. Click **Run Import**.
7. **Make entities visible in the Navbar:**
   1. Go to **Administration ▸ User Interface ▸ General**.
   2. Change **Theme** to `Light` and `Top Navbar` 
   2. Go to **Administration ▸ User Interface ▸ Navbar**.
   4. Under **Tab List**, add the following in this order: `Feedback Forms`, `...` and `Reports`
   5. Save your changes. Now, you have adjusted the layout, you will see these entities in your Navbar and can access them easily at any time.


---

## How to Use
For more in-depth guides for specific roles, see the [Guides]() section.

1. Open the **Feedback** entity in EspoCRM.  
2. Click **Create Feedback** and fill in the form.  
   - Add title, description, source, and choose a status.  
   - Optionally assign to a team member.  
3. Feedback is now added and visible in a list view.  
4. Change feedback status as work progresses.  
5. Use the **Dashboard** to get an overview of all feedback (counts, status).  
6. For more examples and explanations, see [USER_GUIDE.md](USER_GUIDE.md).



---
## Terms of Use
* This extension is developed by [the Netherlands Red Cross' 510](https://www.510.global/) and is not officially supported by EspoCRM.
* It is free to use and modify, as specified in the [GNU AGPLv3 License](/LICENSE.md).
* It is provided as-is, without any warranty. Please ensure it works as intended before using it in a real humanitarian program.
* It is meant to be used as a starting point for organizations to build their own data management system. It is recommended to customize it to the specific needs of your organization.
* Suggestion for improvements? [Open an issue](https://github.com/rodekruis/espocrm-template-feedbackmanagement/issues) in GitHub.
* Need support or have any questions? Please [contact us](https://www.510.global/contact/). We cannot guarantee support, but we will do our best to help you.
