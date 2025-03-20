# People Affected Management (PAM)

## Introduction

**People Affected Management (PAM)** is a data management solution based on EspoCRM for humanitarian organizations to manage the data of the people they serve.

#### Why PAM?
Management of people's personal information is a critical aspect of humanitarian work. It is essential to have a system that is **secure**, **easy to use**, **fast to set up**, and **customizable** to the needs of your organization. PAM is designed to meet these requirements.

#### Why EspoCRM?
[EspoCRM](https://www.espocrm.com/) is an open-source data management system. It is highly customizable, directly from the user interface. It is free to use, lightweight, and has a large, supportive user community. For more information, visit the [EspoCRM Documentation](https://docs.espocrm.com/) and [510's EspoCRM knowledge base](https://github.com/rodekruis/EspoCRM-knowledge-base/wiki).


## Description

PAM consists of _Entities_ and _Roles_. 
* Entities are data structures that hold information (about people, programs, etc.).
* Roles are sets of permissions that define what each user can do in the system.

#### Entities and their relationships:
* **Person Affected (PA)**: a person affected by a disaster, e.g. a beneficiary of a program. Linked to HHs, programs, and tasks.
* **Household (HH)**: a group of people living together, e.g. a family. Linked to one or more PAs.
* **Program**: a project or activity, e.g. a cash distribution. Linked to one or more PAs.
* **Task**: an action to be taken, e.g. a follow-up phone call, that can be assigned to a user, e.g. a volunteer. Linked to one or more PAs.

#### Roles:
* **Volunteer**: registers PAs and HHs. Sees PAs and HHs of their team (e.g. a branch). Can be assigned tasks.
* **Volunteer Manager**: registers PAs and HHs. Sees and edit all PAs and HHs of their team (e.g. a branch). Can create and assign tasks to volunteers in their team.
* **Program Officer**: registers, sees, and edits all PAs and HHs. Can create and assign tasks.
* **Program Manager**: registers, sees, and edits all PAs and HHs. Can create and assign tasks. Can create and edit programs.
* **Movement Partner or Higher Management**: Sees all data except personally identifiable information (PII).

## Installation

> [!IMPORTANT]  
> Make sure to back up your EspoCRM instance before installing this extension.

1. If not done already, [install EspoCRM](https://docs.espocrm.com/administration/installation/).
2. Download the .zip file with the extension: [extension.zip](https://github.com/rodekruis/espocrm-template-pam/raw/refs/heads/main/extension.zip).
2. Install the extension
    * Log in EspoCRM as an administrator.
    * Go to `Administration` > `Extensions`.
    * Select the .zip file with the extension.
    * Click `Install`.

> [!WARNING]  
> If you already have entities with the same names, the installation will overwrite them.
 
3. Make the entities visible in the `Navbar`:
    * Go to `Administration` > `User Interface`.
    * Under `Navbar` > `Tab List`, add the entities `Persons Affected`, `Households`, `Programs`, and `Tasks`.
4. For every file in the [import](/import) folder, import it in EspoCRM:
    * Go to `Administration` > `Import`.
    * Under `What to Import?` > `Entity Type`, select the entity corresponding to the file name; e.g. if the file name is `Roles.csv`, select `Roles`.
    * Click `Next`.
    * Click `Run Import`.

> [!WARNING]  
> If you already have records with the same names, the import will overwrite them.

## Terms of Use
* This extension is developed by [the Netherlands Red Cross' 510](https://www.510.global/) and is not officially supported by EspoCRM.
* It is free to use and modify, as specified in the [GNU AGPLv3 License](/LICENSE.md).
* It is provided as-is, without any warranty. Please ensure it works as intended before using it in a real humanitarian program.
* It is meant to be used as a starting point for organizations to build their own data management system. It is recommended to customize it to the specific needs of your organization.
* If you have any questions, please [contact us](https://www.510.global/contact/). We cannot guarantee support, but we will do our best to help you.


