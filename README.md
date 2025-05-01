# Feedback Management 

## Introduction

**Feedback Management** is a data management solution based on EspoCRM for humanitarian organizations to manage feedback data of community members.

#### Why Feedback Management Template?
Management of feedback is a critical aspect of humanitarian work. It is essential to have a system that is **secure**, **easy to use**, **fast to set up**, and **customizable** to the needs of your organization. This Feedback Management Template is designed to meet these requirements by offering:
* A generic data model defining basic data tables and their relationships​
* A simple layout for ease of use​
* Standard user roles to control access down to individual records and fields​
* Workflows that automate operational processes​
* Can be connected with KoboToolbox Feedback Forms for offline data collection capabilities
* Possibility to link with PowerBI dashboards
* Integrations with other tools via REST API
* Can work with other Templates for humanitarian use cases, such as the [People Affected Management (PAM) Template](https://github.com/rodekruis/espocrm-template-pam).

#### Why EspoCRM?
[EspoCRM](https://www.espocrm.com/) is an open-source data management system. It is highly customizable, directly from the user interface. It is free to use, lightweight, and has a large, supportive user community. For more information, visit the [EspoCRM Documentation](https://docs.espocrm.com/) and [510's EspoCRM knowledge base](https://github.com/rodekruis/EspoCRM-knowledge-base/wiki).


## Description

The Feedback Management Template consists of _Entities_, _Roles_ and _Teams_. 
* Entities are data structures that hold information (about feedback, people, programs, etc.).
* Roles are sets of permissions that define what each user can do in the system.
* Teams are groups of users 

#### Entities and their relationships:
* **Feedback Form**: can  
* **Report**: 
* **Dashboard**: 
* **Flowchart**: 

#### Roles:
* **CEA Focal Point/Officer**: can create, read, edit and delete all Feedback Forms; can create, read, edit, delete Reports
* **Branch Manager**: can create, read and edit all Feedback Forms related to the specific Branch; can read Reports related to the specific Branch
* **Director/Manager/Officer of Programs/Services**: ???
* **PMER**: can create, read, edit and delete Reports; can create, read, edit and delete Dashboards (collection of Reports)
* **Admin/IT/IM**: can create, read, edit and delete (almost) everything in the system
* **KoboConnect API**: automatic system role to be able to send Feedback Forms from KoboToolbox to EspoCRM; this will not be assigned to a user 

#### Teams (Default):
* **Sensitive Feedback**: are the only one that can see Feedback Forms that have been marked as sensitive. They can manage sensitive Feedback Forms and mark them as non-sensitive so that others can see these too. 
* **Branch XXX**: can see only the forms related to that branch location.

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

## Updating the Kobo form for the Kobo-EspoCRM connection
> [!WARNING]  
> Since this method is using a large-language model (LLM) to update automatically, there might be errors.

### When to update the Kobo-EspoCRM connection?

Assumptions:
1. You **already** have updated the EspoCRM Feedback Form entity and you **want to also** have the Feedback Form in Kobo updated. 
2. The updates that you did are in the EspoCRM Feedback Form entity named CFeedbackForm (can be seen in the Entity Manager or URL)
3. The updates to fields/questions have followed the correct naming convention: 
   1. EspoCRM field name is in lowerCamelCase format (first word starting without capital letter, following words start with capital letter, no whitespaces, no symbols or special characters)
   2. EspoCRM field answer options are in snake_case format (all words without any capital letters, all whitespaces are replaced by underscores (_), no symbols or special characters) 

### Instructions

#### Download the latest configurations from EspoCRM in a zip file
1. As Admin in EspoCRM, go to `Administration` > `Entity Manager` -> Three horizontal dots next to `+ Create Entity` (the settings button) -> `Export`
2. You will now have to input values under `Name`, `Module`, `Version`, `Author` and `Description`. For the purpose of updating the Kobo-EspoCRM connection, it does not really matter what you will input here, as long as there is input.
3. Click `Export` and save the zip file somewhere locally on your computer

#### Download the XLSform from KoboToolbox
1. As user with (at least) edit rights, go to the relevant KoboToolbox Form `landing`/`FORM` page. (the url should be similar to: https://kobo.ifrc.org/#/forms/[your Kobo Form ID]/landing)
2. Click on the three horizontal dots (settings button) on the top-right of the screen. Click `Download XLS` and save the it somewhere locally on your computer.

#### Use ChatGPT to get the updated XLSform and JSON for KoboConnect Headers 
1. Start a chat in ChatGPT 4o (other LLMs/models are not tested)
2. Upload the ZIP file and the XLSform with the following prompt:


```

# Prompt to Process EspoCRM ZIP Export and Generate XLSForm and Field Mapping for CFeedbackForm

You will receive a ZIP file exported from EspoCRM, which contains:
- The entity definition:  
  files/custom/Espo/Modules/Entity/Resources/metadata/entityDefs/CFeedbackForm.json
- The field and option labels:  
  files/custom/Espo/Modules/Entity/Resources/i18n/en_US/CFeedbackForm.json

---

## Step 1: Extract and prepare field data

- Load field definitions and option labels from the two JSON files.
- Only include fields with a valid label that is **not** empty or marked as [DONT USE] or [not in use].

---

## Step 2: Manually include Kobo metadata in the XLSForm

Add the following rows manually at the top of the survey sheet:

| type            | name                                 | label |
|-----------------|--------------------------------------|--------|
| start           | datetimeFeedbackCollectionStartedRaw |        |
| end             | datetimeFeedbackCollectionEndedRaw   |        |
| start-geopoint  | gpsCoordinates                        |        |
| today           | today                                 |        |
| username        | username                              |        |
| deviceid        | deviceid                              |        |
| phonenumber     | phonenumber                           |

---

## Step 3: Exclude these fields from the XLSForm

Do not include these fields:

- createdAt  
- feedbackFormID  
- gpsCoordinates  
- datetimeReceived  
- datetimeClosed  
- datetimeFeedbackCollectionStarted  
- datetimeFeedbackCollectionEnded  
- koboToolboxUUID  
- koboToolboxFormID  
- koboToolboxFormVersion  
- datetimeReceivedByKoboToolboxServer  
- datetimeFeedbackCollectionStartedRaw  
- datetimeFeedbackCollectionEndedRaw  
- datetimeReceivedByKoboToolboxServerRaw  
- datetimeReceivedRaw  
- gpsLatitude, gpsLongitude, gpsAltitude, gpsAccuracy  
- deviceIDKoboToolbox, usernameKoboToolbox, phonenumberKoboToolbox

---

## Step 4: Rename datetime fields

For any field whose name contains datetime (case-insensitive), rename it by adding Raw at the end.  
For example:
- datetimeClosed → datetimeClosedRaw
- datetimeReceivedByKoboToolboxServer → datetimeReceivedByKoboToolboxServerRaw

---

## Step 5: Generate the XLSForm

- The survey sheet should include: type, name, label, and appearance (if applicable)
- The choices sheet should include: list_name, name, label
- Use the following type mappings:

| EspoCRM Type     | XLSForm Type                   |
|------------------|--------------------------------|
| varchar, text| text                         |
| enum           | select_one [field_name]      |
| multiEnum      | select_multiple [field_name] |
| datetime       | datetime                     |
| number         | decimal                      |

- Apply appearance: multiline to:

  - feedbackDescription
  - additionalComments
  - processImprovementSuggestion
  - actionTaken
  - responseGiven
  - noteEnumerator

- Exclude any choice option where name or label is empty

---

## Step 6: Generate JSON field mapping and show it in the chat

- Each key = XLSForm name (use multi. prefix for select_multiple)
- Each value = "CFeedbackForm.[EspoFieldName]"

- Manually include system field mappings with correct names:

json
{
  "gpsCoordinates": "CFeedbackForm.gpsCoordinates",
  "_uuid": "CFeedbackForm.koboToolboxUUID",
  "_id": "CFeedbackForm.koboToolboxFormID",
  "__version__": "CFeedbackForm.koboToolboxFormVersion",
  "_submission_time": "CFeedbackForm.datetimeReceivedByKoboToolboxServerRaw",
  "datetimeFeedbackCollectionStartedRaw": "CFeedbackForm.datetimeFeedbackCollectionStartedRaw",
  "datetimeFeedbackCollectionEndedRaw": "CFeedbackForm.datetimeFeedbackCollectionEndedRaw",
  "deviceid": "CFeedbackForm.deviceIDKoboToolbox",
  "username": "CFeedbackForm.usernameKoboToolbox",
  "phonenumber": "CFeedbackForm.phonenumberKoboToolbox"
}

Do not save this mapping to a file. Show it directly in the chat.

---

## Step 7: Output naming
Save the XLSForm using this format:
YYYYMMDD_HHMM_CFeedbackForm_XLSForm.xlsx
Example: 20250501_0705_CFeedbackForm_XLSForm.xlsx

```

3. Go through the steps in[ KoboConnect to Create a Headers Endpoint](https://github.com/rodekruis/kobo-connect?tab=readme-ov-file#create-headers-endpoint)
4. Test the connection 

## Terms of Use
* This extension is developed by [the Netherlands Red Cross' 510](https://www.510.global/) and is not officially supported by EspoCRM.
* It is free to use and modify, as specified in the [GNU AGPLv3 License](/LICENSE.md).
* It is provided as-is, without any warranty. Please ensure it works as intended before using it in a real humanitarian program.
* It is meant to be used as a starting point for organizations to build their own data management system. It is recommended to customize it to the specific needs of your organization.
* If you have any questions, please [contact us](https://www.510.global/contact/). We cannot guarantee support, but we will do our best to help you.


