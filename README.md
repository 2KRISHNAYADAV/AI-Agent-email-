# AI-Agent-email-
<img width="629" height="304" alt="Screenshot 2025-11-30 111849" src="https://github.com/user-attachments/assets/c1af3df7-2eb0-47a0-a39a-ab33f174aadb" />


# 🚀 AI-Agent Email Automation (n8n + Google Sheets)

A fully automated **cold email outreach AI-agent** built using **n8n**, **Google Sheets**, and **Gmail/SMTP**.

This project helps you send **personalized bulk emails**, pick **random templates**, avoid **spam triggers**, and **log results back into Google Sheets** — all automatically.

---

<img width="1583" height="415" alt="Screenshot 2025-12-01 155401" src="https://github.com/user-attachments/assets/744feee9-ac13-4656-af6c-cb1b64572d4a" />



## 📌 Features

* 🔄 Fully automated email-sending workflow
* 🧠 Random template selection using JavaScript
* 🎯 Personalization using dynamic variables (e.g., `[name]`)
* 📡 Works with both **Gmail** and **Custom SMTP**
* 🛡 Anti-spam delay using `Wait` node
* 📊 Live status logging in Google Sheets (SENT / UNREAD / FAILED)
* 🕒 Auto timestamp logging with Indian time zone (IST)
* 📁 Includes complete workflow JSON files

---

## 🧰 Prerequisites

Before you begin, make sure you have:

* ✔️ n8n instance (Cloud / Desktop / Self-hosted)
* ✔️ Google account with access to Sheets API
* ✔️ Gmail or Custom SMTP (Brevo / Zoho / Outlook / Mailgun)
* ✔️ Google Sheet containing your leads & templates

Your Google Sheet must have:

### **Sheet 1 – Leads**

| Name | Email |
| ---- | ----- |

### **Sheet 2 – Templates**

| Subject | Body |

---

## 📂 Download Resources

| File                  | Description                        | Link         |
| --------------------- | ---------------------------------- | ------------ |
| Workflow JSON (Gmail) | Complete workflow using Gmail node | **Download** |
| Workflow JSON (SMTP)  | Complete workflow using SMTP node  | **Download** |
| Leads Sheet           | Sample Google Sheet with leads     | **Download** |

> After downloading, import the JSON inside n8n using **Import Workflow**.

---

## 🔧 JavaScript Snippets Used

### **1️⃣ Pick Random Template (JavaScript Node)**

```js
// Get templates from previous node
const templates = items.map(item => item.json);

// Check if templates exist
if (!templates || templates.length === 0) {
  throw new Error('No templates found');
}

// Pick a random template
const index = Math.floor(Math.random() * templates.length);
const template = templates[index];

// Convert body to HTML
const bodyHtml = template.Body.replace(/\n/g, '<br>');

return [
  {
    json: {
      subject: template.Subject,
      body: bodyHtml
    }
  }
];
```

---

### **2️⃣ Personalize Email Body**

(Set Node in n8n)

```js
{{ $json.body.replace("[name]", $json["Name"] && $json["Name"].trim() !== '' ? $json["Name"].trim() : "there") }}
```

---

### **3️⃣ Gmail Send Status**

```js
{{ $json.labelIds[0] }}
```

### **4️⃣ SMTP Send Status**

```js
{{ $json.response.includes("250 2.0.0 Ok") ? "SENT" : "Failed" }}
```

---

### **5️⃣ Timestamp (IST)**

```js
{{ new Date().toLocaleTimeString("en-GB", { timeZone: "Asia/Kolkata", hour12: false }) }}
```

---

## 🧠 Workflow Overview

This automation does the following:

1. 📥 **Reads leads** from Google Sheets (Sheet 1)
2. 📄 **Reads email templates** from Google Sheets (Sheet 2)
3. 🎲 **Selects a random template** for each lead
4. ✍️ **Replaces personalization variables** (`[name]` → actual name)
5. 📧 **Sends email** using Gmail or SMTP
6. 🏷 **Records send status** (SENT / FAILED / UNREAD)
7. 🕒 **Logs timestamp** in Sheet 1
8. ⏳ **Adds delay** to avoid Gmail/SMTP spam detection
9. 🔁 **Repeats for all leads**

---

## 📸 Workflow Screenshot

(Add your screenshots here)

---

## ⚙️ How to Use This Project

1. Clone this repository
2. Open n8n → Import Workflow JSON
3. Configure Google Sheets credentials
4. Add Gmail/SMTP credentials
5. Add your Google Sheet ID
6. Turn workflow ON
7. Click **Execute** and watch the AI-Agent send personalized emails automatically!

---

## ❤️ Support & Contributions

Feel free to contribute, add improvements, and submit pull requests.

If you like this project — ⭐ **Star this repo!**

---

## 📞 Contact

Created by **Krishna**

For help or collaboration, message anytime!

