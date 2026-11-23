LSS Staff Portal (Android + iOS)

A professional staff portal mobile app built with Expo (React Native) + Expo Router.

Run locally

npm install
npm run start

Then:





Android emulator / device: npm run android



iOS simulator requires macOS: npm run ios

Configure Supabase (recommended)

This app supports Supabase Auth + Authenticator App (TOTP) MFA.





Create a Supabase project



Enable Email/Password sign-in in Supabase Auth



(Optional but recommended) In Supabase Auth settings, require MFA for the users you want (or enforce in your policy)



Copy .env.example → .env and set:

EXPO_PUBLIC_SUPABASE_URL=https://ilifudfkecqfqegzupid.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=YOUR_ANON_KEY

To find the anon key: Supabase Dashboard → Project Settings → API → anon public key.

For EAS production builds, set the anon key in EAS environment variables (don’t commit it):

# one-time setup (requires eas login)
eas env:create production --scope project --name EXPO_PUBLIC_SUPABASE_ANON_KEY --value YOUR_ANON_KEY --type string --visibility sensitive

Then run the app and go to Profile → Security → Authenticator app to enroll.

Database schema + RLS policies are in supabase/README.md.

Note: Expo public env vars are baked into builds. After changing .env, restart expo start and rebuild production AABs via EAS.

Build for Play Store / App Store (recommended)

This project is configured for EAS Build.

npm install -g eas-cli

eas login



EAS: required env vars

The app requires these to be present at build time:





EXPO_PUBLIC_SUPABASE_URL (set in eas.json)



EXPO_PUBLIC_SUPABASE_ANON_KEY (set in EAS env vars; see command above)

If you build without these, the production app will show “This app is not configured yet” on the sign-in screen.

Android (Google Play Console)





Package name is set to com.lss.staffportal.app in app.json (expo.android.package).



Build an AAB:

npm run build:android:production

Upload the generated .aab to Google Play Console.

iOS (App Store)





Bundle id is set to com.lss.staffportal.app in app.json (expo.ios.bundleIdentifier).



Build:

npm run build:ios:production



Notes





With Supabase configured, sign-in uses Supabase Auth and MFA.



Without Supabase configured, the app allows a local placeholder sign-in only in dev (__DEV__).



Privacy policy (Google Play)

Google Play requires a public Privacy Policy URL.





Drafts are in docs/privacy-policy.md and docs/privacy-policy.html.

Quick hosting option: GitHub Pages




Push the repo to GitHub.



In GitHub: Settings → Pages



Source: Deploy from a branch



Branch: main / Folder: /docs



Your URL will look like:

https://jamesiecod2.github.io/Staff-Portal/privacy-policy.html`

Then paste that URL into Google Play Console: App content → Privacy policy.
