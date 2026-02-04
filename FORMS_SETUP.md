# Google Forms Setup – Get Entry IDs So Your Site Forms Send Data Correctly

Your site forms (Newsletter, Contact, Donation, Get Involved) submit **directly to Google Forms in the background** (no redirect). For Google to receive what users type or select, each field must use the **correct entry ID** from your Google Form.

---

## Newsletter – get Email entry ID in 30 seconds (easiest)

1. Open your **Newsletter** Google Form in **edit mode** (forms.google.com → open the form).
2. Click the **three dots (⋮)** in the top right.
3. Click **"Get pre-filled link"**.
4. In the **Email** question, type anything (e.g. `test`).
5. Click **"Get link"**.
6. Copy the full URL. It will look like:  
   `https://docs.google.com/forms/d/e/1FAIpQLSf.../viewform?usp=pp_url&entry.XXXXXXXXXX=test`  
   The part **`entry.XXXXXXXXXX`** (with numbers) is your Email field's entry ID.
7. **Paste that full URL or just the `entry.XXXXXXXXXX` value** into the chat so we can update `index.html` with it. Once that's in the code, the Newsletter form will send the email to Google correctly.

---

## How to get entry IDs (for any form)

1. **Open your Google Form** in a browser (the normal “view” or “preview” link, e.g. `.../viewform`).
2. **Right‑click the first question** (e.g. “Name” or “Email”).
3. Click **Inspect** (or Inspect Element).
4. In the HTML, find the **`<input>` or `<textarea>`** for that question.
5. Copy its **`name`** attribute. It looks like **`entry.1234567890`** (numbers will differ). That is the entry ID for that field.
6. Repeat for **every question** in the form (Name, Email, Phone, etc.).

## How to get the formResponse URL

- Your form URL looks like:  
  `https://docs.google.com/forms/d/e/XXXXXXXXXX/viewform?...`
- The **formResponse** URL (used for submitting) is:  
  `https://docs.google.com/forms/d/e/XXXXXXXXXX/formResponse`  
  (same ID, but **`formResponse`** instead of **`viewform`**).

---

## 1. Newsletter (footer on home page)

- **File:** `index.html`  
- **Form response URL:** already set  
- **What to replace:** In the script, find `var emailEntryId = 'entry.1234567890';`  
  Replace **`entry.1234567890`** with the **entry ID of the “Email” field** from your Newsletter Google Form (see “How to get entry IDs” above).

---

## 2. Contact (contact page)

- **File:** `contact.html`  
- **What to replace:**
  1. **Form URL:** Find  
     `var formAction = 'https://docs.google.com/forms/d/e/REPLACE_WITH_YOUR_CONTACT_FORM_ID/formResponse';`  
     Replace **`REPLACE_WITH_YOUR_CONTACT_FORM_ID`** with the ID from your Contact form URL (the part between `/d/e/` and `/viewform`).
  2. **Entry IDs:** Find the line  
     `var entryIds = { name: 'entry.1000000001', email: 'entry.1000000002', ... };`  
     Replace each `entry.1000000001`, etc., with the **real entry IDs** from your Contact form for: **Name, Email, Phone, Subject, Message** (in that order in the form).

---

## 3. Donation (donate page)

- **File:** `donate.html`  
- **Form response URL:** already set  
- **What to replace:** In the script, find  
  `var entryIds = { name: 'entry.3000000001', phone: 'entry.3000000002', cause: 'entry.3000000003', amount: 'entry.3000000004' };`  
  Replace each value with the **real entry IDs** from your Donation form for: **Name, Phone Number, Choose a Cause, Amount**.

---

## 4. Get Involved (volunteer form)

- **File:** `get-involved.html`  
- **Form response URL:** already set  
- **What to replace:** In the script, find  
  `var entryIds = { name: 'entry.2000000001', email: 'entry.2000000002', ... };`  
  Replace each value with the **real entry IDs** from your Get Involved form for: **Name, Email, Phone, Location, Area of Interest, Availability, Short Message**.

---

## After you replace the IDs

1. Save the file.
2. Submit a test from your site (Newsletter, Contact, Donate, or Get Involved).
3. Check the **Google Form responses** (or linked Google Sheet). You should see the typed/selected values in the right columns.

If responses still appear empty, double‑check that each entry ID in the code **exactly** matches the `name` of the corresponding input in the form’s HTML (from Inspect).
