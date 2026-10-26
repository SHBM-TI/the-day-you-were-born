# The Day You Arrived – hosted version with owner-only stats

Files: index.html (public site), admin.html (only you), firebase-config.js, firestore.rules.

## Setup (about 15 minutes)
1. Firebase console > Add project > Add a Web app. Copy its config into firebase-config.js and set ADMIN_EMAIL to your Google email.
2. Build > Firestore Database > Create database (production mode; region asia-south1 Mumbai is close to India).
3. Build > Authentication > Sign-in method > enable Google. Under Settings > Authorized domains, add the domain you will host on.
4. In Firestore, create collection `stats` with document id `counters` and four number fields set to 0: visits, uniqueVisitors, uses, uniqueUsers.
5. Firestore > Rules: paste firestore.rules, replace YOUR_EMAIL@gmail.com with your email, Publish.
6. Host the folder (it must be served over https, not opened as a file): Firebase Hosting (`firebase init hosting`, then `firebase deploy`), Netlify (drag the folder in), or GitHub Pages. To test locally: `npx serve`.
7. Open /admin.html on your site and sign in with the admin Google account.

## What gets stored
- stats/counters: visits (once per browser session), uniqueVisitors (first visit per browser), uses (each "Reveal my day"), uniqueUsers (first reveal per browser).
- entries: first name (optional), date of birth, birth place, timestamp. Birth time is not saved. The sample-day buttons are not counted or saved.
- Only you (admin account) can read or delete entries; the rules block everyone else.

## Know the limits
- Counters and entries are written from visitors' browsers, so a technically skilled person could inflate counts or spam entries. The rules limit each write to +1 and a valid shape. For stronger protection turn on Firebase App Check.
- Unique means per browser, not per person.
- You are collecting personal data. Keep the consent checkbox, only use the data for counting/analysis, and delete an entry (Delete button) when someone asks.
