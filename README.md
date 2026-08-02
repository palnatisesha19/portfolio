[README.md](https://github.com/user-attachments/files/30634252/README.md)
# Portfolio Manager

A private, multi-account, real-time-synced portfolio dashboard: buy ledger,
sell ledger, and dividend ledger, with capital-gains holding-period
classification and Excel/PDF/Word/Text export.

## This version uses a real database (Firebase)

Every account's ledgers now live in **Firebase Authentication + Cloud
Firestore**, Google's free-tier backend. That means:

- Data syncs **live** — sign in on your phone and your laptop at the same
  time, add a buy on one, and it appears on the other within a second or
  two, no refresh needed.
- Each friend's account is a real, separately-authenticated account —
  not just a name typed into a browser.
- Data is no longer tied to one device or browser.

This is a one-time setup (about 10 minutes) that only *you* need to do,
before publishing. Friends never see any of this — they just use the
account name + password screen as before.

## One-time setup: create your Firebase project

1. Go to **console.firebase.google.com** and sign in with any Google account.
2. Click **Add project** → give it a name (e.g. `portfolio-manager`) →
   you can skip Google Analytics → **Create project**.
3. In the left sidebar, click **Build → Authentication → Get started**.
   Under "Sign-in method", enable **Email/Password** → **Save**.
4. In the left sidebar, click **Build → Firestore Database → Create
   database**. Choose **Start in production mode** → pick a region close
   to you → **Enable**.
5. Once created, click the **Rules** tab in Firestore and replace the
   contents with:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /portfolios/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
     }
   }
   ```
   Click **Publish**. This is what actually keeps everyone's data private —
   it ensures a signed-in user can only ever read or write their *own*
   document, never anyone else's.
6. Back in the project, click the **gear icon → Project settings**, scroll
   to "Your apps", click the **</> (web)** icon, give the app any nickname,
   and register it. Firebase will show you a `firebaseConfig` object with
   your `apiKey`, `authDomain`, `projectId`, etc.
7. Open `index.html` in this download, find the `firebaseConfig` block
   near the top of the `<script>` section, and paste your real values in
   place of the `YOUR_API_KEY` / `YOUR_PROJECT_ID` placeholders.

These config values are **not secret** — Firebase's security comes from
the Rules you set in step 5, not from hiding this object — so it's normal
and safe for them to sit in a public `index.html`.

## Publish it (same as before)

1. Upload the updated `index.html` to your GitHub repo's root, replacing
   the old one, and commit.
2. Your existing GitHub Pages link stays the same:
   `https://<your-username>.github.io/portfolio-manager/`
3. Give it a minute to rebuild, then open the link — the login screen will
   now say "connected" instead of the setup notice (which only appears if
   the config still has placeholder values).

## Notes

- Firebase's free "Spark" plan comfortably covers a handful of friends
  tracking personal portfolios — no billing needed unless usage grows far
  beyond that.
- If a friend forgets their password, there's currently no "forgot
  password" flow built in — ask if you'd like that added.
- The Wipro/Lloyds/Coffee Day sample data is no longer auto-loaded for new
  accounts on this version; every new sign-up starts empty.
