# TV Browser — Android TV / TCL / Google TV Browser App

A full web browser built for Android TV (TCL TVs, Sony, Hisense, Nvidia Shield, any
Android TV / Google TV device). It has an address bar, back/forward, reload, and
bookmarks, and everything is reachable with a standard TV remote D-pad.

## What's included
- Address bar (type a URL or a search term)
- Back / Forward / Reload buttons
- Bookmark a page (★+) and open a saved list (☰) with delete support
- Registered as a **Leanback launcher app**, so it appears as a normal app tile
  on the TCL/Android TV home screen (not hidden in a "sideloaded apps" folder)
- Loads pages with JavaScript, DOM storage, and mixed content enabled so most
  modern sites work

## Why I couldn't hand you a finished .apk directly
Building an .apk requires the Android SDK build tools, which aren't available in
this chat environment. What you have instead is the **complete, ready-to-build
Android Studio project**. Turning it into an APK takes about a minute once it's
open in Android Studio — no coding needed on your end unless you want to
customize something.

## How to build the APK
1. Install [Android Studio](https://developer.android.com/studio) (free) if you
   don't have it.
2. Unzip the project you downloaded, then in Android Studio choose
   **File → Open** and select the `TVBrowser` folder.
3. Let Android Studio finish "Gradle Sync" (it will auto-generate the Gradle
   wrapper and download dependencies the first time — needs internet).
4. Go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
5. When it finishes, click the "locate" link in the notification, or find the
   file at:
   `app/build/outputs/apk/debug/app-debug.apk`

## How to sideload it onto your TCL / Android TV
**Option A — ADB over network (easiest, no cables):**
1. On the TV: Settings → Device Preferences → About → click "Build" 7 times to
   enable Developer Options, then Settings → Device Preferences → Developer
   Options → turn on "USB debugging" / "Network debugging" (naming varies by TV).
2. Find the TV's IP address (Settings → Network).
3. On your computer, with `adb` installed (comes with Android Studio, in
   `platform-tools`):
   ```
   adb connect <TV_IP_ADDRESS>:5555
   adb install app-debug.apk
   ```
4. The app icon "TV Browser" will appear on the TV's home screen / app list.

**Option B — USB drive:**
1. Copy `app-debug.apk` onto a USB flash drive.
2. Install a file manager app on the TV that supports APK installs (e.g.
   "Send Files to TV", "X-plore", or TCL's built-in file manager if present).
3. Plug in the USB drive, browse to the APK, and select Install.
   You may need to enable "Install unknown apps" for that file manager in
   Settings → Apps → Special app access.

## Customizing
- **Home page**: change `homeUrl` in `MainActivity.kt`.
- **App icon / TV banner**: the project ships with simple placeholder shapes
  (`res/drawable/ic_launcher_foreground.xml`, `res/drawable/tv_banner.xml`).
  Replace these with your own artwork any time — the TV banner should ideally
  be a 320×180 image for a polished look.
- **Package name**: currently `com.tvbrowser.app` — rename via Android
  Studio's refactor tool if you want your own.

## Known limitation to be aware of
Some websites are designed for mouse/touch and don't respond well to D-pad-only
navigation once you're inside the page content (the browser chrome — address
bar, back/forward, bookmarks — is always fully D-pad friendly). If you have a
specific site in mind that needs to work smoothly, let me know and I can tune
the WebView settings (e.g., injecting a virtual cursor) for that case.
