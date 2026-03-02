# 🔥 Firebase Setup — Do This ONCE (5 Minutes)

After this, every admin change goes live INSTANTLY. No uploads. No redeploy. Ever.

---

## STEP 1 — Create Firebase Project (2 min)

1. Go to https://console.firebase.google.com
2. Click **"Add Project"**
3. Name it: `next-gen-creative`
4. Disable Google Analytics (not needed) → **Create Project**

---

## STEP 2 — Create Realtime Database (1 min)

1. In your project sidebar, click **Build → Realtime Database**
2. Click **"Create Database"**
3. Choose any region (e.g. United States)
4. Select **"Start in test mode"** → Enable
   *(This allows reads/writes without login — fine for this setup)*

---

## STEP 3 — Get Your Database URL (30 sec)

After creating the database, you'll see a URL like:
```
https://next-gen-creative-abc12-default-rtdb.firebaseio.com/
```
**Copy this URL.**

---

## STEP 4 — Paste Into firebase-config.js (30 sec)

Open `firebase-config.js` and replace the placeholder:

```javascript
// BEFORE:
const FIREBASE_URL = "https://YOUR-PROJECT-default-rtdb.firebaseio.com";

// AFTER (your actual URL):
const FIREBASE_URL = "https://next-gen-creative-abc12-default-rtdb.firebaseio.com";
```
*(Remove the trailing slash if present)*

---

## STEP 5 — Deploy to Vercel (1 min)

1. Go to https://vercel.com/new
2. Drag and drop this entire project folder
3. Click **Deploy**
4. Done — your site is live!

---

## STEP 6 — Seed Initial Data

1. Go to your live site: `yourproject.vercel.app/admin`
2. Login: `admin / nextgen2025`
3. Click **"🟢 Live Status"** in the sidebar
4. Click **"🌱 Seed Database with Default Data"**
5. All default content is now in Firebase

---

## HOW IT WORKS AFTER SETUP

```
You change price in admin → Saves to Firebase → Customer sees new price on refresh
You upload new design    → Saves to Firebase → Design appears on live site immediately
You edit testimonial     → Saves to Firebase → Live site shows new testimonial
```

**No export. No upload. No redeploy. Ever.**

---

## OPTIONAL: Vercel Auto-Deploy Hook

Only needed if you update the HTML/CSS code (not for content changes).

1. Vercel Dashboard → Your Project → Settings → Git → Deploy Hooks
2. Click **"Create Hook"** → Name it "Admin Trigger" → Copy the URL
3. In Admin Panel → Live Status → paste the URL → Click "Trigger Vercel Redeploy"

---

## Firebase Security (After Launch)

Once live, secure your database:
Go to Firebase → Realtime Database → Rules → replace with:

```json
{
  "rules": {
    "site-config": { ".read": true, ".write": false },
    "designs": { ".read": true, ".write": false },
    "orders": { ".read": false, ".write": true }
  }
}
```

This allows the public website to read, but only your backend to write.
For admin writes, you'll add Firebase Auth — contact your developer.
