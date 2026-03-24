# Bass Lake Camping Trip - Interactive Planning Website

## Project Overview
An interactive, real-time camping trip planning website for a group trip to Bass Lake Provincial Park (May 16-17, 2026). Built as a single-page app with Firebase Firestore for real-time data sync across all group members.

## Architecture
- **Hosting:** GitHub Pages (static site, free)
- **Database:** Firebase Firestore (free Spark plan)
- **Frontend:** Single HTML file with embedded CSS and JS (no build tools, no framework)
- **Firebase SDK:** v9+ compat mode via CDN

## Tech Stack
- Vanilla HTML/CSS/JavaScript
- Firebase Firestore (compat SDK v9.23.0)
- No npm, no bundler, no framework — intentionally simple for easy maintenance

## Firebase Setup
1. Go to https://console.firebase.google.com
2. Create a new project (e.g., "bass-lake-camping")
3. Enable Firestore Database (start in test mode for now)
4. Go to Project Settings > General > Your Apps > Add Web App
5. Copy the `firebaseConfig` object
6. Replace the placeholder config at the top of `index.html`:
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### Firestore Security Rules
For a small trusted group, test mode works. For better security, use:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
Since there's no authentication, the site relies on trust (everyone picks their own name). This is fine for a small friend group.

### Firestore Collections
- **`roles`** — One document per role. Fields: `claimedBy` (string), `timestamp` (timestamp)
- **`checklist`** — One document per gear item. Fields: `checked` (boolean), `checkedBy` (string), `timestamp` (timestamp)
- **`comments`** — One document per message. Fields: `name` (string), `message` (string), `timestamp` (timestamp)

## GitHub Pages Deployment
1. Create a GitHub repo (e.g., `bass-lake-camping`)
2. Push `index.html` to the `main` branch
3. Go to repo Settings > Pages > Source: Deploy from branch > Branch: `main`, folder: `/ (root)`
4. Site will be live at `https://<username>.github.io/bass-lake-camping/`

## Site Structure (Single Page)
All sections are in `index.html` with smooth-scroll navigation:

1. **Hero** — Title, date, tagline
2. **Trip Overview** — Park info, dates, drive time, group breakdown (2 campsites)
3. **Important Reminders** — 8 cards with key rules (quiet hours, food storage, weather, etc.)
4. **Trip Timeline** — Visual schedule for Friday and Saturday with time blocks
5. **Meal Plan** — 5 meal cards (Fri dinner, Fri night snacks, Sat breakfast, Sat lunch, Sat afternoon) + grocery tips
6. **Role Assignments** — Interactive cards with Firebase sync. Claim/unclaim roles. Pre-assigned: Trip Coordinator (Danial), Cleanup Crew (Everyone)
7. **Gear Checklist** — 7 categories, ~50 items. Checkboxes sync in real-time with name + timestamp
8. **First-Timer's Guide** — 4 collapsible accordion sections (tent setup, staying warm, campfire, comfort stations)
9. **Group Chat** — Real-time comment section for coordination
10. **Emergency Footer** — Hospital, 911, Ontario Parks phone, park store info

## Group Members
Names in the name picker dropdown:
- Danial, Saif, Sania, Mohid, Nida, Eshal, Iman, Alina

### Campsite Assignments
- Campsite 1: Danial's family + Saif & Sania
- Campsite 2: Mohid & Nida + Eshal, Iman & Alina

## Design
- **Theme:** Outdoorsy & warm
- **Colors:** Earthy greens (#2D5016, #4A7C28), browns (#5C4033, #8B6914), campfire oranges (#E8820C, #D46B08), cream backgrounds (#FDF6E3, #FAF0DC)
- **Responsive:** Mobile-friendly, works on all screen sizes
- **Font:** System fonts (Segoe UI stack)

## Known Issues / Notes
- Some details in the original planning doc may need correction (user noted inaccuracies)
- No authentication — anyone with the link can interact. Suitable for a trusted friend group.
- Firebase falls back gracefully to offline mode if config is invalid (3-second timeout)
- localStorage stores the selected username as a fallback

## File Structure
```
bass-lake-camping/
  index.html    — The entire site (HTML + CSS + JS, ~1650 lines)
  Claude.md     — This file (project context)
```
