# Email Invoice to Google Sheets - Setup Guide

## Workflow Overview

```
Gmail Trigger → Has Attachments? → Extract PDF Text → OpenAI Extract Data → Parse Response → Google Sheets
```

**What it does**: Monitors Gmail for new emails with PDF invoices, extracts key data using GPT-4o, and appends it to a Google Sheet.

**Extracted fields**: Invoice Number, Date, Total Amount, Tax Amount, Currency, Vendor Name, Email Subject, Sender, Processed Timestamp.

---

## Import Instructions

1. Open your n8n instance: https://erikberger123.app.n8n.cloud
2. Click **Add workflow** (+ button)
3. Click the **⋯** menu (top right) → **Import from File**
4. Select `workflows/invoice-extraction.json`

---

## Credentials to Configure

After importing, you need to set up 3 credentials:

### 1. Gmail OAuth2
- Click the **Gmail Trigger** node
- Under Credentials, click **Create New Credential**
- Follow the OAuth2 flow to connect your Gmail account
- The trigger polls every minute for unread emails

### 2. OpenAI API
- Click the **OpenAI - Extract Invoice Data** node
- Under Credentials, click **Create New Credential**
- Enter your OpenAI API key (needs GPT-4o access)

### 3. Google Sheets OAuth2
- Click the **Google Sheets - Append Row** node
- Under Credentials, click **Create New Credential**
- Follow OAuth2 flow to connect your Google account
- Then select your **Document** (spreadsheet) and **Sheet** name

---

## Google Sheet Setup

Create a Google Sheet with these column headers in row 1:

| invoice_number | invoice_date | total_amount | tax_amount | currency | vendor_name | email_subject | email_from | processed_at |
|---|---|---|---|---|---|---|---|---|

---

## Testing

1. After configuring all credentials, click **Test workflow**
2. Send yourself a test email with a PDF invoice attached
3. The workflow should extract the data and append a row to your sheet

## Activation

Once tested, toggle the workflow **Active** to run it automatically.

---

Conceived by Romuald Członkowski - [www.aiadvisors.pl/en](https://www.aiadvisors.pl/en)
