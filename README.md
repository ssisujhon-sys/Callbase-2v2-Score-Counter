# Callbase 2v2 Score Counter

Offline score counter for the 2 vs 2 Callbase card game (English / বাংলা).
Everything (app code, fonts, icons) is bundled, so the installed Android app
works with no internet.

## Get the APK (no Android Studio needed)

1. Create a free GitHub repository and upload this whole folder to it.
2. Open the repo's **Actions** tab, choose **Build Android APK**, click **Run workflow**.
3. After ~5-8 minutes, open the finished run and download **Callbase-2v2-apk** (contains `Callbase-2v2.apk`).

To get a permanent public download link anyone can use, push a tag instead:
`git tag v1.0.0 && git push origin v1.0.0`. The APK is then attached to the
repo's **Releases** page. Share that link.

## Installing on a phone

1. Send `Callbase-2v2.apk` to the phone (WhatsApp, Telegram, Drive, USB, link).
2. Tap it. If Android asks, allow "Install unknown apps" for that app (Chrome, Files, etc.).
3. Tap **Install**. The app then works fully offline.

## Keep the same signing key for updates (recommended)

Without this, every build gets a new random key, and a new APK can't update an
older install (users would have to uninstall first, losing saved history).
Create a key once:

    keytool -genkeypair -keystore release.jks -alias callbase -keyalg RSA -keysize 2048 -validity 10000

Then in GitHub: Settings > Secrets and variables > Actions, add
`KEYSTORE_BASE64` (output of `base64 -w0 release.jks`) and `KEYSTORE_PASSWORD`
(use the same password for store and key). Keep `release.jks` backed up and private.

## Build locally instead

Needs Node 22, JDK 21, Android Studio/SDK.

    npm install
    npm run build
    npx cap add android
    npm run android:assets
    npx cap sync android
    npx cap open android      # Build > Build APK(s)

## Develop

    npm install
    npm run dev
