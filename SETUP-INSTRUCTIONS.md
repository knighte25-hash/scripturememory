# Scripture Memory App — Setup

This folder contains a complete web app: `index.html`, `manifest.json`, `OneSignalSDKWorker.js`, and two icons. It needs to be hosted at a real HTTPS URL (not opened as a local file) for two reasons: iOS home-screen install and push notifications both require HTTPS.

## 1. Get a free ESV API key

1. Go to [esv.org](https://www.esv.org/) and create a free account.
2. Go to [api.esv.org/account](https://api.esv.org/account/) and click **Create an API Application**. Some applications need brief staff approval.
3. Copy the API key once approved.
4. You'll paste this into the app itself later (Settings tab) — it's stored only on your device, never in the code.

Free tier limit: 5,000 requests/day, plenty for personal daily use.

## 2. Host the files (pick one, both are free)

**Netlify (easiest):**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop).
2. Drag the whole `scripture-memory-app` folder onto the page.
3. Netlify gives you a URL like `https://random-name-123.netlify.app`. That's your Site URL — write it down.

**GitHub Pages (if you already use GitHub):**
1. Create a new repo, upload these files to the root.
2. Repo Settings → Pages → set source to the main branch root.
3. Your URL will be `https://yourusername.github.io/repo-name/`.

## 3. Set up OneSignal for push notifications

1. Sign up free at [onesignal.com](https://onesignal.com).
2. Create a new app → choose **Web Push** → choose **Typical Site** (no coding needed for the permission prompt).
3. Enter your Site Name and the exact Site URL from step 2 (must match exactly, no trailing slash mismatch).
4. On the next screen, download the app-specific `OneSignalSDKWorker.js` file and use it to **replace** the placeholder file of the same name in this folder.
5. Copy your **App ID** (Settings → Keys & IDs).
6. Open `index.html` in a text editor, find `YOUR_ONESIGNAL_APP_ID` near the top, and replace it with your real App ID.
7. Re-upload/re-deploy the updated files to your host (drag the folder into Netlify Drop again, or push to GitHub).

### Create your daily reminder

OneSignal sends messages on a schedule you configure once in their dashboard — no code needed:
1. In OneSignal, go to **Messages → New Push → Automated** (or **Journeys**, depending on your dashboard version).
2. Set it to send once daily at your preferred time (e.g. 7:00 AM) to **All Subscribed Users**.
3. Write the message, e.g. "Time for your scripture memory 📖".
4. Set the click destination URL to your app's URL so tapping the notification opens straight to it.
5. Save and activate.

## 4. Add it to your iPhone home screen

1. Open your site URL in **Safari** on your iPhone (must be Safari, not Chrome, for the install prompt to appear).
2. Tap the **Share** icon → **Add to Home Screen** → **Add**.
3. Open the app from the new home screen icon (not from Safari) — this matters for notifications to work.
4. The app will ask for notification permission the first time; tap **Allow**.
5. Requires iOS 16.4 or later.

## 5. Using the app

- **Today**: shows your verse of the day (fetched live from ESV), with a shuffle and save option.
- **Practice**: progressively hides more words each time you tap "Hide more words," plus a type-it-from-memory checker that scores your accuracy.
- **My Verses**: add your own references to the rotation, and view/manage saved favorites.
- **Settings**: your ESV API key, reminder time note, and streak/progress stats.

Your streak, favorites, and custom verses are all stored locally in the browser on your phone — they stay put across days as long as you don't clear Safari's website data for this app.

## Troubleshooting

- **Verse text won't load**: check your ESV key is saved correctly in Settings → "Test" button.
- **No notifications arrive**: confirm the app was added via Safari's Add to Home Screen (not just bookmarked), and that you opened it from the home screen icon at least once to trigger the permission prompt.
- **iOS version too old**: web push on iOS requires 16.4+; on older versions the app still works, just without push notifications.
