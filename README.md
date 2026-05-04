# MugangaConnect+ Doctor Portal

MugangaConnect+ is a static web doctor portal for viewing patients and managing appointment requests. It uses Firebase Authentication for login and Cloud Firestore for storing doctors, patients, and appointments.

## Features

- Doctor login with Firebase Authentication
- Doctor-only access check using the `doctors` Firestore collection
- Dashboard with appointment summary cards
- Recent appointments table
- Appointment filtering by status
- Confirm, reject, and complete appointment actions
- Patient list with search
- Patient profile modal with appointment history
- Custom 404 page

## Project Structure

```text
WebApp/
├── index.html          # Doctor login page
├── dashboard.html      # Dashboard and appointment statistics
├── appointments.html   # Appointment management page
├── patients.html       # Patient list and patient profile modal
├── 404.html            # Page not found screen
├── styles.css          # Shared app styles
└── firebase-config.js  # Firebase app configuration
```

## Technologies Used

- HTML
- CSS
- JavaScript
- Bootstrap 5
- Bootstrap Icons
- Firebase Authentication
- Cloud Firestore

## Firestore Collections

The app expects these collections:

### `doctors`

Each doctor document ID should match the Firebase Authentication user UID.

Example document:

```json
{
  "name": "Doctor Name",
  "email": "doctor@hospital.com"
}
```

### `patients`

Example document:

```json
{
  "name": "Patient Name",
  "email": "patient@example.com",
  "phone": "+250700000000",
  "biometricEnabled": true
}
```

### `appointments`

Example document:

```json
{
  "patientId": "PATIENT_DOCUMENT_ID",
  "patientName": "Patient Name",
  "date": "2026-05-04",
  "time": "10:30",
  "status": "pending"
}
```

Supported appointment statuses:

- `pending`
- `confirmed`
- `completed`
- `cancelled`
- `missed`

## Running Locally

Because this is a static website, you can open `index.html` directly in a browser.

For a local server, run one of these commands from the project folder:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## Usage

1. Add a doctor user in Firebase Authentication.
2. Create a matching document in the `doctors` collection using that user's UID.
3. Fill in `firebase-config.js`.
4. Open `index.html`.
5. Log in with the doctor email and password.

After login, the doctor can view the dashboard, manage appointments, and inspect patient profiles.

## Notes

- Bootstrap and Firebase scripts are loaded from CDNs, so an internet connection is required.
- The app currently uses Firebase compat SDK version `9.23.0`.
- Firestore security rules should restrict access so only authenticated doctors can read and update the required data.
