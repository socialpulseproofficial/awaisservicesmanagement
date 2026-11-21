# Awais Services Hub: Google login version

This version signs in with real Google accounts and keeps one shared database, so staff can use their own phones and see the same records.

## Setup (about 15 minutes, free plan is enough)

1. Go to https://console.firebase.google.com and create a project.
2. Project settings → Your apps → add a **Web app**. Copy the `apiKey`, `authDomain`, `projectId` and `appId` values into the `FIREBASE_CONFIG` block at the top of `index.html`.
3. Authentication → Sign-in method → turn on **Google**.
4. Firestore Database → Create database (production mode).
5. Firestore → Rules → paste the contents of `firestore.rules`. Replace `owner@gmail.com` with the owner's Gmail (lower case). Also set the same address as `OWNER_EMAIL` in `index.html`. Publish the rules.
6. Host the file: Firebase Hosting (`firebase deploy`) or any HTTPS static host. Opening the file directly from your computer will not work for Google sign-in.
7. Authentication → Settings → Authorized domains → add the domain where you host it.

## First use

1. The owner opens the site and signs in with the owner Gmail. This creates the shared database.
2. Owner → **Staff & access** → **Add staff (Gmail)**. Staff then sign in with their own Google account.
3. Anyone not on the list sees "not on the staff list" and cannot read or write data. The rules enforce this on the server.

## Good to know

- All data is stored as one document, and the last save wins. If two people save at the same moment, one change can be overwritten. This is fine for a small shop but not for many users at once.
- Page restrictions by role (Staff, Viewer, Admin) are applied in the app. The server rules only decide who is allowed in at all.
- Take a backup from Settings regularly.
