# PD Warriors Philippines — Get Together 2027 Registration System

This package is a Google Apps Script web app that connects directly to a Google Sheet.

## Included

- Mobile-first registration form
- Parkinson's-friendly large controls and reduced-motion support
- Auto-generated Registration IDs such as `PDW-2027-0001`
- Duplicate detection
- Google Sheets storage
- Confirmation email to attendee
- Organizer notification email
- QR registration pass
- Staff PIN login
- Camera QR scanning
- Manual name / ID / mobile search
- One-tap check-in
- Live check-in counters
- Check-In Log sheet
- Registration open/close setting
- Optional registration capacity

## Event defaults

- Event: Parkinson's Disease Warriors Philippines – Get Together 2027
- Theme: New Hope: Moving Forward Beyond Parkinson’s
- Date: January 16, 2027
- Time: 9:00 AM–1:00 PM
- Venue: St. Luke’s Medical Center – Quezon City

All of these can be changed in the **Event Config** sheet after setup.

---

## SETUP — easiest method

### 1. Create the Google Sheet

Create a blank Google Sheet, for example:

`PDW Get Together 2027 Registration`

### 2. Open Apps Script

In the Google Sheet:

**Extensions → Apps Script**

### 3. Add the project files

In Apps Script:

- Replace the default `Code.gs` with the included `Code.gs`.
- Add a new HTML file named **Index** and paste `Index.html`.
- Add another HTML file named **CheckIn** and paste `CheckIn.html`.

You do not type `.html` when Apps Script asks for the HTML file name. Enter `Index` and `CheckIn`.

### 4. Run setupSystem()

At the top of Apps Script, select:

`setupSystem`

Then press **Run**.

Google will ask for authorization because the app needs to:

- write registrations to your Sheet
- send confirmation emails
- send organizer notification emails

Complete the authorization.

After setup, your spreadsheet will have:

1. `Registrations`
2. `Event Config`
3. `Check-In Log`

### 5. Edit Event Config

In your Google Sheet, open **Event Config**.

Important settings:

- `ORGANIZER_EMAIL` — put the email that should receive every new registration
- `ADMIN_PIN` — change `2027` to your private staff PIN
- `REGISTRATION_OPEN` — use `YES` or `NO`
- `MAX_REGISTRATIONS` — use `0` for unlimited, or enter a number such as `150`

### 6. Deploy as a web app

In Apps Script:

**Deploy → New deployment → Web app**

Use:

- Execute as: **Me**
- Who has access: **Anyone**

Then click **Deploy**.

Copy the Web App URL.

### 7. Your two links

Public registration:

`YOUR_WEB_APP_URL`

Staff check-in:

`YOUR_WEB_APP_URL?page=checkin`

Do not publicly post the staff check-in link or staff PIN.

---

## REGISTRATION FLOW

Attendee completes:

- Full Name
- Mobile Number
- Email
- City / Province
- Participant Type
- Number of Companions
- Accessibility / Assistance Request — optional
- Dietary Concern — optional
- Emergency Contact — optional
- Privacy consent

After submission:

1. Google Sheet receives the record.
2. A Registration ID is generated.
3. Attendee sees a QR pass.
4. Attendee receives a confirmation email.
5. Organizer receives a notification email.

---

## CHECK-IN FLOW

Staff opens:

`YOUR_WEB_APP_URL?page=checkin`

Staff enters:

- Staff / volunteer name
- Staff PIN

Then they can:

### QR check-in

Tap **START CAMERA** and scan the attendee QR.

### Search check-in

Search by:

- Name
- Registration ID
- Mobile number

Then tap **CHECK IN**.

The system changes:

`REGISTERED → ATTENDED`

and records:

- check-in time
- staff member
- check-in method

---

## PRIVACY / DATA HANDLING

This registration system may contain personal and accessibility-related information.

Recommended:

- Keep the Google Sheet restricted to authorized organizers.
- Do not publicly share the spreadsheet.
- Collect only information needed for the event.
- Do not ask participants to enter diagnoses, medications, or unnecessary medical history.
- Delete or archive personal data according to your event organization's privacy practice after it is no longer needed.

---

## EMAIL LIMITS

The confirmation feature uses Google Apps Script `MailApp`.

Google accounts have daily email quotas. If you expect a large number of registrations, check the current Apps Script email quota for the Google account that owns the script.

Even if the email quota is reached, successful registrations remain saved in the Google Sheet.

---

## CAMERA NOTE

The staff QR scanner uses the browser camera and the open-source `html5-qrcode` browser library loaded from a CDN.

If camera access is unavailable, staff can use:

- QR text paste
- Name / ID / mobile search

---

## QR NOTE

The visual QR image is generated using the QuickChart QR endpoint.

The QR stores only:

`PDW2027 | Registration ID | random validation token`

It does not put the attendee's name, mobile number, email, or accessibility information inside the QR code.


## Staff Offline Mode + Reports

The GitHub version now includes an upgraded Staff Check-In page with:

- Offline roster download to the event device
- Offline attendee search
- Offline QR/manual check-in queue
- Sync Now when internet returns
- Unsynced action counter and last-sync time
- Clear Offline Data for privacy after the event
- Live attendance report
- Attendance rate, pending/no-show count, companions, assistance requests
- Participant breakdown and staff activity
- CSV export

Important: the offline mode works after the Staff Check-In page has already been opened and the roster has been downloaded at least once while online. Keep the page open if venue internet becomes unstable.

These files are the GitHub source version. The separate Floot production site is not automatically updated by GitHub commits.
