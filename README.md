# 🏡 Open House Sign-In Page

A clean, mobile-friendly sign-in page for real estate open houses. Guests fill out a short form on a tablet or laptop, and their information is automatically sent to **Follow Up Boss** (via Zapier) and saved locally as a **CSV spreadsheet** backup.

Each listing gets its own copy of the file with its own photo, address, and guest list.

---

## Features

- Guest sign-in form — name, email, phone, agent status, pre-approval status
- Auto-tags each contact in Follow Up Boss with the listing address (e.g. `Open House - 12861 Foothill Ln, Saratoga, CA 95070`)
- Sends data to Follow Up Boss via a Zapier webhook
- Saves every sign-in to the browser locally as a backup — survives page refreshes and tablet sleep
- **Download Sign-In Sheet** button exports all guests to a `.csv` file at any time
- Background photo support — set a different photo per listing
- One config block at the top of the file — the only thing you ever need to edit
- Works as a plain HTML file — no server, no hosting required

---

## Files

```
open-house-signin.html   ← The sign-in page (duplicate this for each listing)
foothill-front.jpg       ← Example background photo (replace with your own)
README.md                ← This file
```

---

## How to Set Up a New Listing

### Step 1 — Duplicate the file

Right-click `open-house-signin.html` → Duplicate. Rename the copy to something like `456-oak-ave.html`.

### Step 2 — Open and edit the config block

Open the file in **TextEdit** (Mac) or **Notepad** (Windows). Use **⌘F / Ctrl+F** to search for `LISTING`. You'll find this block near the top:

```js
const LISTING = {
  address:         "12861 Foothill Ln",
  cityStateZip:    "Saratoga, CA 95070",
  price:           "$3,888,000",
  openHouseDate:   "Sunday, March 29, 2026",

  backgroundImage: "foothill-front.jpg",
  overlayDarkness: 0.45,

  agentName:       "Paul Pham",
  agentPhone:      "(408) 824-0674",

  zapierWebhook:   "https://hooks.zapier.com/hooks/catch/...",
  fubSource:       "Open House",
};
```

Edit **only the values inside the quote marks**. Never remove the commas at the end of each line.

### Step 3 — Add a background photo (optional)

1. Copy a photo of the listing into the **same folder** as the HTML file
2. Give it a simple filename with no spaces, e.g. `456-oak-exterior.jpg`
3. Type that filename into the `backgroundImage` field

Leave `backgroundImage: ""` for a plain gray background.

**Tip:** Adjust `overlayDarkness` to control how much the photo is dimmed:
- `0.3` = light dimming (bright photos)
- `0.45` = default (works for most photos)
- `0.6` = heavy dimming (very bright/light photos)

### Step 4 — Save and open

Save the file, then double-click it to open in your browser. It's ready to use.

---

## Connecting to Follow Up Boss via Zapier

The page sends guest data to Follow Up Boss through a Zapier webhook. Each sign-in includes:

| Field | Example |
|---|---|
| First Name | Jane |
| Last Name | Smith |
| Email | jane@email.com |
| Phone | (555) 000-0000 |
| Tag | `Open House - 12861 Foothill Ln, Saratoga, CA 95070` |
| Source | Open House |
| Notes | Working with agent: No · Pre-approved: Yes |

### Zapier Setup (one-time)

1. Go to [zapier.com](https://zapier.com) and create a free account
2. Click **Create Zap**
3. **Trigger:** Webhooks by Zapier → Catch Hook → copy the webhook URL
4. Paste the URL into `zapierWebhook` in your HTML file
5. Submit a test sign-in from the page
6. Back in Zapier, click **Test Trigger** — it will detect the test submission
7. **Action:** Follow Up Boss → Create or Update Contact
8. Map the fields: `firstName`, `lastName`, `email`, `phone`, `tag`, `source`, `notes`
9. Turn the Zap on

> **Note:** Even if Zapier is not connected, every sign-in is saved locally in the browser and can be downloaded as a CSV at any time.

---

## Downloading the Guest List

At the bottom of the page, a small bar shows how many guests have signed in and a **⬇ Download Sign-In Sheet** button. Clicking it downloads a `.csv` file named:

```
Open House Sign-Ins - 12861 Foothill Ln - 2026-03-29.csv
```

This file can be opened in Excel, Google Sheets, or Numbers.

Each listing stores its guest list separately — duplicating the file for a new address will not mix up the data.

---

## Tips

- **Tablet use:** Open the file in Chrome or Safari on an iPad or laptop. The layout is mobile-friendly and works well in landscape mode.
- **Between guests:** After each sign-in, the page shows a confirmation screen with a **Next Guest →** button that clears the form for the next person.
- **End of open house:** Hit Download Sign-In Sheet to save the CSV, then optionally click "Clear list" to reset for next time.
- **Multiple listings:** Keep each listing's HTML file and photo in the same folder. They are fully independent of each other.

---

## Built With

- Plain HTML, CSS, and JavaScript — no frameworks, no dependencies
- [Zapier Webhooks](https://zapier.com/apps/webhook/integrations) for Follow Up Boss integration
- [Follow Up Boss](https://followupboss.com) as the CRM destination
