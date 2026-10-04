# n8n Resume Mailer using Gemini

An n8n-based automation workflow for streamlining resume-based job applications by extracting company email addresses, generating personalized cover emails using Gemini AI, and sending applications automatically with a resume attachment.

## 📌 Project Overview

This project was developed as part of a **Semester 5 PEP / RPA learning project** using **n8n** and **Gemini AI**.

The workflow automates several steps involved in applying to multiple companies:

- Reads company and job information from an Excel file.
- Fetches company websites.
- Extracts available email addresses.
- Determines whether a valid email address was found.
- Generates a personalized cover email using Gemini AI.
- Downloads the resume from Google Drive.
- Sends the job application through Gmail with the resume attached.
- Collects companies where an email address could not be found and generates a failure summary.

This project was initially provided as a classroom workflow reference and was then **configured, adapted, tested, and debugged in my own n8n environment**.

---
## ⚙️ Workflow Architecture

The automation follows two main paths depending on whether an email address is successfully found.

### 1. Email Found — TRUE Branch

**Start**  
↓  
**Run Config**  
↓  
**Download Excel**  
↓  
**Parse Excel**  
↓  
**Fetch Website**  
↓  
**Extract Email**  
↓  
**Email Found?**  
↓  
**TRUE**  
↓  
**Generate Cover Email (Gemini)**  
↓  
**Download Resume (Google Drive)**  
↓  
**Send Application (Gmail)**

### 2. Email Not Found — FALSE Branch

**Start**  
↓  
**Run Config**  
↓  
**Download Excel**  
↓  
**Parse Excel**  
↓  
**Fetch Website**  
↓  
**Extract Email**  
↓  
**Email Found?**  
↓  
**FALSE**  
↓  
**Aggregate Failures**  
↓  
**Build Summary**  
↓  
**Send Failures Summary**

---

## 🤖 How Gemini AI Is Used

Gemini AI is used to generate a personalized and professional cover email for each application.

The workflow provides Gemini with relevant information such as:

- Applicant background
- Company name
- Job role
- Company information
- Extracted email address

Gemini then generates an HTML-formatted email that can be sent directly through Gmail.

The prompt is designed to avoid inventing qualifications or experience that are not provided.

---

## 📂 Input Data

The workflow uses an Excel dataset containing company and job-related information.

The Excel file is downloaded from Google Drive and then parsed by n8n for processing.

The workflow processes each company individually and attempts to identify a suitable contact email address from the company's website.

---

## 📧 Email Extraction

The workflow fetches the company website and searches the returned HTML content for email addresses.

The extraction logic also filters out unwanted or irrelevant email patterns.

If an email cannot be obtained, the workflow records the failure reason, such as:

- Could not fetch website
- No email found on site

---

## 🔀 Conditional Branching

The **Email Found?** node determines which path the workflow follows.

### TRUE

If an email address is found:

1. Gemini generates a personalized cover email.
2. The resume PDF is downloaded from Google Drive.
3. Gmail sends the application with the resume attached.

### FALSE

If no email address is found:

1. The company is collected as a failure.
2. The failure information is aggregated.
3. A summary is generated.
4. The summary is sent through Gmail.

---

## 📎 Resume Attachment

The resume is stored in Google Drive.

For the successful TRUE-branch workflow, the resume is downloaded using the **Google Drive** node as an actual PDF file.

The downloaded binary data is then passed to the Gmail node as an attachment.

---

## 🧪 Testing

Both workflow branches were tested separately.

### Email Not Found Workflow

The complete workflow was executed using the company dataset, successfully demonstrating the **FALSE branch** and generating a summary of companies for which no email address was found.

### Email Found Workflow

The TRUE branch was tested separately using a controlled single-company test.

The test verified that:

- Gemini successfully generated the cover email.
- The resume was successfully downloaded from Google Drive.
- The PDF was correctly attached.
- Gmail successfully delivered the application email.

---

## 🛠️ Technologies Used

- **n8n** — Workflow automation
- **Gemini AI** — Cover email generation
- **Google Drive** — Excel input and resume storage
- **Gmail** — Application email delivery
- **JavaScript** — Email extraction and workflow logic
- **Excel / XLSX** — Company and job dataset

---

## 🔐 Credentials & Security

The GitHub versions of the workflow have been sanitized before publication.

Personal:

- Email addresses
- Google Drive URLs
- Google Sheets/Excel URLs
- Credential configurations
- n8n instance information

have been removed or replaced with placeholders.

To run the workflows in your own environment, you will need to configure your own:

- Google Drive OAuth2 credentials
- Gmail OAuth2 credentials
- Gemini/Gateway credentials

**Never upload API keys, passwords, OAuth tokens, or other private credentials to a public repository.**

---
## 📁 Repository Structure

The repository is organized as follows:

**n8n-resume-mailer-using-gemini/**

&nbsp;&nbsp;├── **README.md**

&nbsp;&nbsp;└── **workflows/**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── **.gitkeep**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;├── **N8N Resume Mailer - Gemini - Email Not Found - GitHub.json**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;└── **N8N Resume Mailer - Gemini - Email Found - GitHub.json**

---
## 🎯 Learning Outcomes

Through this project, I gained practical experience with:

- Building workflows in n8n
- Working with workflow nodes and connections
- Using conditional TRUE/FALSE branches
- Working with expressions in n8n
- Processing Excel data
- Fetching and parsing website content
- Extracting information using JavaScript
- Integrating Gemini AI into an automation workflow
- Working with Google Drive files
- Handling binary PDF data
- Sending emails and attachments through Gmail
- Debugging workflow and credential issues
- Testing different workflow execution paths
- Preparing workflow files for GitHub

---

## 📌 Project Status

**Completed as a Semester 5 PEP / RPA learning project.**

The workflows were configured, tested, debugged, and prepared as sanitized GitHub versions for learning and demonstration purposes.
