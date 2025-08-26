# Task 5: Create a Prompt Template for an Engagement Email

## 🎯 Objective
Build a prompt template that allows wellness coaches at Tranquil Trails to easily draft personalized program recommendation emails. The template should compare a client’s goals with available programs and suggest relevant offerings dynamically.

---

## 🛠️ Steps I Followed

### 1. Enable Org Settings
- Verified **Einstein Generative AI Settings** is enabled.
- Verified **Prompt Builder Settings** is enabled.

### 2. Create the Prompt Template
- Setup → **Prompt Builder → New**.
- Type: **Sales Email**.
- Label: `Program Recommendation Email`.
- API Name: `Program_Recommendation_Email`.
- Description: Generate personalized emails recommending programs based on client goals.
- Recipient Object: **Contact**.
- Related Object: None.

### 3. Add Template Inputs
- Added **Sender’s Full Name** (free text input).
- Added **Recipient’s Full Name** (Contact.FullName).
- Added **Recipient Goals** (related Fitness records).
- Added **Programs** via Apex class `Prompt_Program_Recommendation_Invocable`.

### 4. Prompt Text
```text
You are a wellness specialist from a company called Tranquil Trails and the sender of this email, [sender's full name]. 
You are writing an email to an individual client, [recipient's full name].

Instructions: """
Follow these instructions precisely. Don’t add any information not provided.
Do not use phrases like "I hope this email finds you well" or any variation of it. 
Use clear, concise, and straightforward language in the active voice, strictly avoiding filler words and redundant language.

The email should include the following:
- Generate a subject line that increases open rate using words and content related to the body.
- The salutation must only contain the recipient's first name.
- Refer to the sender in the singular voice ("I" not "we").
- Convey that you are checking in to follow up and encourage the client's progress.
- Evoke enthusiasm with intensifiers but limit exclamation points.
- Maintain a casual tone with contractions and direct references to the client, but do not use discourse markers.

Below are two sets of reference information:
1. A list of the recipient's interests tagged as :Goals.
2. A list of current active programs in a JSON object tagged as :Programs.

Craft a sales email identifying a maximum of two programs that would be of key interest to the recipient based on their :Goals and the available :Programs.

### Goals
[Insert the related list of all Fitness records for this contact.]

### Programs
[Call the Apex class Prompt_Program_Recommendation_Invocable.]
"""
