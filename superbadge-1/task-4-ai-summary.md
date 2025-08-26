# Task 4: Build an AI-Generated Summary of Related Records

## 🎯 Objective
Create a custom rich text field on the Contact record (`Interest_Summary__c`) to display an AI-generated summary of all related Fitness records, powered by a Field Generation prompt template.

---

## 🛠️ Steps I Followed

### 1. Enable Org Settings
- Setup → **Einstein Generative AI Settings** → Enabled.
- Setup → **Prompt Builder Settings** → Enabled.

### 2. Create Custom Field
- Object Manager → **Contact → Fields & Relationships → New**.
- Type: **Rich Text Area**  
- Label: `Interest Summary`  
- API: `Interest_Summary__c`  
- Added description & help text.  
- Set **System Administrator** visibility.  
- Saved.

### 3. Enable Field for Generative AI
- Setup → **Generative AI Field Enablement**.  
- Object: **Contact**.  
- Enabled `Interest_Summary__c` for Generative AI.  
- Saved.

### 4. Create Prompt Template
- Setup → **Prompt Builder → New**.  
- Type: **Field Generation**.  
- Label: `Summarize Client Goals`.  
- API: `Summarize_Client_Goals`.  
- Description: Generate summaries of client fitness interests.  
- Target: **Contact → Interest Summary (`Interest_Summary__c`)**.  
- Model: Standard.  

### 5. Add Template Inputs
- Added **Contact → FirstName**.  
- Added **Fitness → Related List (all records)**.  

### 6. Prompt Text
```text
You are a wellness coach from a company called Tranquil Trails who wants to see a quick summary of a client's fitness interests. 

Review the content in the list of fitness records related to a contact record: {!Fitness}  
In this list all records relate to the individual contact.  
Fitness records: {!Fitness}  
Contact name: {!Contact.FirstName}  

Instructions: """
Follow these instructions precisely. Don’t add any information not provided.
The "contact" must be referred to as a "client" in the summary.
Use clear, concise, and straightforward language in the active voice and a friendly, informal, informative tone.
The summary must include the following:
- Use the client's first name in the first sentence.
- Interpret any reported stress level based on a scale from 1-10, with values of 7-10 being ideal.
- If any values are missing, do not include any reference to missing information.
- Do not address any content or generate answers that don’t have complete data.
- Do not use filler words or phrases or redundant language.
- Use an introductory summary sentence and closing sentence in addition to several bullet points.
- When you format the list, use a variety of emoji as bullet points to add interest.
- Limit the summary to seven sentences.
"""
