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
