# Vap-Sure Android app

A signed Android **APK** that wraps the [Vap-Sure quoting portal](https://portal.vapsure.co.za)
as a [Trusted Web Activity](https://developer.chrome.com/docs/android/trusted-web-activity/) (TWA) —
it runs the existing PWA full-screen in the Chrome engine.

The app is built **entirely on GitHub Actions** (no local Android SDK needed). On every change to
`twa-manifest.json` (or manually via the **Actions ▸ Build Android APK ▸ Run workflow** button), CI:

1. Sets up JDK 17 + the Android SDK + [Bubblewrap](https://github.com/GoogleChromeLabs/bubblewrap).
2. Restores (or, on the first run, creates and commits) the signing keystore.
3. Generates the TWA project from `twa-manifest.json` and builds a **signed** `vapsure.apk`.
4. Publishes it to the **`latest`** GitHub Release.

**Download:** https://github.com/BoomslangChips/vapsure-app/releases/latest/download/vapsure.apk
(the same link the in-site *Mobile App* page uses).

## Full-screen (no browser bar)
For the app to open without the Chrome address bar, the site must serve a Digital Asset Links file at
`https://portal.vapsure.co.za/.well-known/assetlinks.json` containing the signing key's SHA-256
fingerprint. The first build prints that fingerprint (Actions log ▸ "Show signing SHA-256"); drop it
into the site's `wwwroot/.well-known/assetlinks.json` and redeploy.
