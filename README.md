# Walk Tracker

A simple Android walk tracker. Tap **Start walk**, put the phone in your pocket, and it keeps recording with the screen off.

Shows live **distance, time, pace, total climb (cumulative uphill), and current elevation**, draws your route on a map (street or topo), and keeps a history of past walks with an elevation profile. Walks can be exported as GPX.

## How it works
- `www/index.html` is the whole app: plain HTML/JS, no build step. Map by [Leaflet](https://leafletjs.com) with OpenStreetMap / OpenTopoMap tiles.
- [Capacitor](https://capacitorjs.com) wraps it as an Android app. Background GPS uses `@capacitor-community/background-geolocation` (a foreground service with a notification).
- Walks are stored on the phone (browser local storage). Nothing is uploaded anywhere.
- Total climb = sum of all uphill steps. Altitude is smoothed and changes under 3 m are ignored, to cut GPS noise.

## Build and run
You need [Node.js](https://nodejs.org) (22+) and [Android Studio](https://developer.android.com/studio).

```
npm install
npx cap sync android
```

Then in Android Studio: **File → Open** and choose the `android` folder, wait for Gradle sync, plug in a phone with **USB debugging** on (choose File transfer mode), select it in the device dropdown, and press **Run**.

After editing `www/index.html`, run `npx cap sync android` again, then Run.

To make a shareable file: **Build → Build Bundle(s) / APK(s) → Build APK(s)**. The APK is in `android/app/build/outputs/apk/debug/`.

## Notes
- On first start, allow location (and notifications). If recording stops with the screen off, set Settings → Apps → Walk Tracker → Battery to **Unrestricted**.
- Map tiles come from OpenStreetMap and OpenTopoMap. That is fine for personal use; if you distribute the app widely, use your own tile provider and follow their usage policies.
- App ID is `com.mark.walktracker`. Change it in `capacitor.config.json` and `android/app/build.gradle` if you publish your own version.

## License
MIT. Leaflet is BSD-2-Clause; Capacitor and the plugins are MIT.
