Great! Here's how to set up the **Google Apps Script** to collect data from your web form and store it into **Google Sheets**.

---

## ✅ Step-by-Step: Set Up Google Apps Script

### 🔧 1. **Create Your Google Sheet**

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new sheet and name it something like `Ultra H2 Leads`
3. In row 1, set the column headers exactly as:

   ```
   Timestamp | Name | Email | Phone | State
   ```

---

### 💡 2. **Open Apps Script**

1. In the same sheet, click:
   `Extensions → Apps Script`
2. Delete the default code and paste the following:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(JSON.stringify(e.parameter));

  sheet.appendRow([
    new Date(),
    data.name,
    data.email,
    data.phone,
    data.state
  ]);

  return ContentService
         .createTextOutput("Success")
         .setMimeType(ContentService.MimeType.TEXT);
}
```

---

### 🔓 3. **Deploy the Script as a Web App**

1. Click the **Deploy** button → **Manage Deployments**
2. Click **+ New deployment**
3. Under **Select type**, choose **Web App**
4. Set:

   * **Description:** `Ultra H2 Form Receiver`
   * **Execute as:** `Me`
   * **Who has access:** `Anyone`
5. Click **Deploy**
6. Copy the **Web App URL** (you’ll use this in your HTML)

---

### ✅ 4. **Insert Script URL in Your HTML**

Replace this line in the HTML:

```javascript
const scriptURL = 'https://script.google.com/macros/s/your-script-id/exec';
```

with your actual deployment link.

---

### 🔐 Optional: Enable CORS (If Needed)

If you later encounter CORS issues (on some browsers), modify your script like this:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = e.parameter;

  sheet.appendRow([
    new Date(),
    data.name,
    data.email,
    data.phone,
    data.state
  ]);

  return ContentService
    .createTextOutput("Success")
    .setMimeType(ContentService.MimeType.TEXT)
    .setContent("Success");
}
```

---

Once this is done, your form data will start saving into the sheet instantly, and the PDF will download after form submission.


