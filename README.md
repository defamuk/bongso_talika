# বংশাবলী · Bongso Talika

**Interactive Family Tree PWA with Firebase Realtime Database Sync**

A progressive web app for documenting and exploring your family tree across generations. Pre-loaded with the Dey family data spanning 6 generations. Syncs in real-time across all family members' devices via Firebase.

## Features

- **6-Generation Tree View** — Visual generational layout with color-coded gender indicators
- **Full Person Profiles** — Name, nickname, photo, DOB, birth location, life details
- **Family Connections** — Parents, spouses, children, auto-detected siblings
- **Reciprocal Linking** — Add a parent-child link and the reverse is created automatically
- **Firebase Realtime Sync** — All family members see updates instantly
- **Offline Support** — Works without internet via service worker caching
- **Import/Export** — JSON backup and restore
- **Installable PWA** — Add to home screen on any device
- **Search & Filter** — Find anyone by name, location, or generation

## Deploy to GitHub Pages

### Option 1: Quick Deploy

1. Create a new GitHub repository (e.g. `Bongso Talika`)
2. Upload all files from this folder to the repository:
   ```
   index.html
   manifest.json
   sw.js
   icon.svg
   icon-192.png
   icon-512.png
   ```
3. Go to **Settings → Pages**
4. Under "Source", select **Deploy from a branch**
5. Select **main** branch and **/ (root)** folder
6. Click **Save**
7. Your site will be live at `https://yourusername.github.io/Bongso Talika/`

### Option 2: Command Line

```bash
# Create repo on GitHub first, then:
git init
git add .
git commit -m "Initial deploy"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/Bongso Talika.git
git push -u origin main

# Enable GitHub Pages in repo Settings → Pages → main branch
```

## Firebase Setup (for cross-device sync)

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Click **Create a project** (or use existing)
3. Navigate to **Build → Realtime Database**
4. Click **Create Database** → Start in **test mode**
5. Go to **Project Settings** (gear icon) → **General** → scroll to **Your apps**
6. Click **Add app** → **Web** (</> icon)
7. Register the app and copy the config values
8. In Bongso Talika, go to **Settings** and paste all config values
9. Make sure to include the **databaseURL** (e.g. `https://your-project-default-rtdb.firebaseio.com`)
10. Click **Save & Connect**
11. Click **Push All** to upload your tree to Firebase
12. Share the same Firebase config with family — they'll all sync in real time

### Security Rules (for family-only access)

After initial setup, update your Realtime Database rules:

```json
{
  "rules": {
    "familyTree": {
      ".read": true,
      ".write": true
    }
  }
}
```

For tighter security, consider adding Firebase Authentication and restricting by user.

## Pre-loaded Data

The app comes pre-loaded with the Dey family tree transcribed from a handwritten chart, including:

- **Gen 1**: Narshai Dey (earliest ancestor)
- **Gen 2**: Motilal, Chunilal, Mahakal, Maniklal
- **Gen 3**: Satish Chandra, Kedar, Shombol, Jogdeb, and others
- **Gen 4**: Pantha Deb, Ramesh Chandra, Bhupendra Nath, Gobindo, and others
- **Gen 5**: Gopal, Swapan, Govindo, Shyam, Ram, Jamuna, Murari, Laxmi, and many more
- **Gen 6**: Current generation — Bablu, Ranjan, Tamal, Rittik, Indranil, Pampa, Atanu, and many more

All parent-child and spouse connections are wired up. You can edit, add, or correct any entries.

## File Structure

```
Bongso Talika/
├── index.html       # Complete app (HTML + CSS + JS, single file)
├── manifest.json    # PWA manifest
├── sw.js           # Service worker for offline support
├── icon.svg        # Vector app icon
├── icon-192.png    # 192x192 app icon
├── icon-512.png    # 512x512 app icon
└── README.md       # This file
```

## Tech Stack

- **Vanilla JS** — No build step, no dependencies, just deploy
- **Firebase Realtime Database** — Real-time sync via CDN-loaded SDK
- **Service Worker** — Offline-first caching strategy
- **Web App Manifest** — Installable as native-like app
- **localStorage** — Persistent offline storage

## Data Format

Each person is stored as JSON:

```json
{
  "id": "p_abc123xyz",
  "firstName": "Ramesh Chandra",
  "lastName": "Dey",
  "nickname": "",
  "gender": "Male",
  "dob": "1940-01-15",
  "birthLocation": "Kolkata",
  "dod": "",
  "generation": "4",
  "lifeDetails": "Teacher, lived in Kolkata...",
  "photo": "",
  "parentIds": ["p_parent1"],
  "spouseIds": ["p_spouse1"],
  "childIds": ["p_child1", "p_child2"]
}
```

Export your tree as JSON at any time from Settings for backup.
