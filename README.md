# Shithead for Android

The whole game is one file, `www/index.html`. There are three ways to get it on an Android phone.

## 1. Install it from Chrome (easiest, no tools needed)

The `www` folder is an installable web app. Put it on any free HTTPS host, then open it in Chrome on the phone and choose **Add to Home screen** (or **Install app**). It opens full screen in portrait and works offline after the first visit.

Free hosts that take a folder as-is:
- **Netlify Drop**: go to app.netlify.com/drop and drag the `www` folder onto the page.
- **GitHub Pages**: push this folder to a repository and turn on Pages for the `www` folder.

## 2. Get a real APK from GitHub (no Android Studio)

1. Create a new GitHub repository and push this whole folder to its `main` branch.
2. The workflow in `.github/workflows/build-apk.yml` runs automatically.
3. Open the repository's **Actions** tab, pick the latest "Build Android APK" run, and download `shithead-apk`.
4. Copy `app-debug.apk` to the phone and open it. Android will ask you to allow installs from that app (Files or your browser) the first time.

## 3. Build the APK yourself

Needs Node.js 22, Java 21 and Android Studio (which brings the Android SDK).

```
npm install
npm run apk          # builds android/app/build/outputs/apk/debug/app-debug.apk
npm run android:open # or open the project in Android Studio and press Run
```

After changing `www/index.html`, run `npx cap sync android` before building again.

The app id is `com.example.shithead`. Change `appId` in `capacitor.config.json` (and `applicationId` in `android/app/build.gradle`) before publishing to the Play Store; a store release also needs a signed release build rather than the debug APK.
