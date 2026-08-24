# ETOG Portal — Account System Setup (one time, ~5 minutes)

The portal's account system runs on Firebase (free). Until you finish these
steps, the portal shows "SYSTEM OFFLINE" on the sign-in screen.

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com and sign in with your Google account.
2. Click **Create a project** (or "Add project"), name it `etog-portal`.
3. You can turn OFF Google Analytics when it asks. Finish creating.

## 2. Turn on username/password login
1. In the left menu: **Build → Authentication → Get started**.
2. Pick **Email/Password** and switch **Enable** on. Save.
   (The portal turns Roblox usernames into fake emails behind the scenes —
   nobody needs a real email.)

## 3. Create the database
1. Left menu: **Build → Firestore Database → Create database**.
2. Choose **Start in production mode**, pick any location, Done.

## 4. Paste the security rules  (IMPORTANT — this is what stops cheaters)
1. In Firestore, open the **Rules** tab.
2. Delete everything there and paste in the whole contents of the
   `firestore.rules` file in this repo. Click **Publish**.

## 5. Connect the website
1. Click the gear ⚙ (top left) → **Project settings**.
2. Scroll to **Your apps** → click the web icon **</>** → nickname `etog` →
   Register app (no hosting needed).
3. It shows a code block with `const firebaseConfig = { ... }`.
   Copy just the `{ ... }` part.
4. In `portal.html`, find the line near the bottom that says
   `var firebaseConfig = null;` and replace `null` with what you copied.
   (Or paste the config to Claude and it'll wire it in and push.)
5. Commit + push. Done — the portal is live.

## 6. Make yourself the boss
1. On the live portal, enter the access code, then **Create Account** with
   your Roblox username and a NEW password (not your Roblox one!).
2. Back in Firebase: **Firestore Database → Data → users** → click the one
   document in there (that's you).
3. Change `admin` from `false` to `true`, and `verified` to `true`.
   You can also change `rank` to `Head of ETOG`.
4. Refresh the portal — you'll see the amber **Command Panel** with pending
   accounts and the full roster.

## Notes
- The `apiKey` in firebaseConfig is safe to be public — it just identifies
  the project. The security rules are what protect the data.
- You verify people in the Command Panel (Verify button). Deny bans them.
- Firebase's free plan easily covers a Roblox group's traffic.
