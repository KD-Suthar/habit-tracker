# Habit Tracker Dashboard

A personal habit and daily-routine tracker. Define your routine, check off habits every day, and see your consistency broken down by day, month, and year — synced across all your devices for free.

## What it does

- Tracks a fully customizable set of daily habits (times, categories, and per-habit goals — all editable)
- Shows daily, monthly, and yearly consistency at a glance
- Syncs your data live across phone, laptop, and any other device
- Protected by a login, so it's only ever your data

## Features

- **Daily consistency grid** — tap to check off each habit, day by day
- **Monthly stats** — completion %, current & best streaks, check-ins, and "days wasted" (days under 30% completion)
- **Weekly trend + month score** — a line chart and a progress ring for the month you're viewing
- **Category radar** — see which part of your day (Morning / Learning / Work / Evening / Night) is strongest or weakest
- **Month-over-month comparison** — pick any two months and see what improved or slipped, habit by habit
- **Year overview** — a GitHub-style contribution heatmap across 2026–2037, click any month to jump into it
- **All-Time summary** — lifetime stats across every year tracked
- **Editable routine** — add, rename, retime, recategorize, or set a goal % for any habit; edit its time and it re-sorts itself into the right place in the day automatically
- **Deactivate, don't delete** — stop tracking a habit without losing its history; restore it anytime
- **Login-protected** — only your account can see or edit your data, even though the site itself is public

## Make your own copy

1. **Download `index.html`** from this project.
2. **Create a free Firebase project** at [console.firebase.google.com](https://console.firebase.google.com).
3. **Enable Firestore Database** (Build → Firestore Database → Create database).
4. **Enable Email/Password sign-in** (Build → Authentication → Sign-in method), then add one user under the Users tab — that's your login.
5. **Copy your Firebase config** (Project Settings → General → Your apps) into the `firebaseConfig` object near the top of `index.html`.
6. **Lock down your data** — go to Firestore → Rules, and paste in:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /habitApp/{doc} {
         allow read, write: if request.auth != null && request.auth.uid == "YOUR_UID_HERE";
       }
     }
   }
   ```
   (Get your UID from Authentication → Users, after creating your login.)
7. **Host it for free** — create a public GitHub repo, upload `index.html`, then turn on GitHub Pages (Settings → Pages → Deploy from branch → `main` / root). You'll get a live URL in about a minute.
8. Open that URL, sign in, and it's yours.

## Bug fixes already applied

- **Date bug** — "today" used to be stuck on a hardcoded date and never moved. Fixed to always use the real current date on whatever device it's opened on.
- **Security** — the app originally had no login and open Firestore access, meaning anyone with the URL could read or edit the data. Fixed with a real login screen plus a Firestore rule that locks all access to one specific account.

## Want more?

This is easy to extend — more habit categories, reminders, data export, a different chart, a "recovery streak" after a bad day, whatever's useful to you. If there's a feature you want, just ask and it can be added.
