# StockPulse India — free-source Android app

Personal NSE/BSE watchlist and price-change notifier. It has no trading, order, broker, paid API, WhatsApp, or SMS features.

## What the free build does

- Searches Yahoo Finance's public search endpoint for NSE (`.NS`) and BSE (`.BO`) equity tickers.
- Fetches the latest available Yahoo Finance chart quote for each watchlist stock.
- Checks prices every 60 seconds while the app is active, and sends a local Android notification only after a fetched price differs from the previous fetched price. The first quote establishes a baseline and does not alert.
- Reads the public NSE corporate-announcements RSS feed every 5 minutes while the app is active, filters announcements against the watchlist's symbols/company names, and avoids repeating announcements already seen on the device.
- Stores the watchlist and seen announcement IDs locally on the phone.
- Includes a manual refresh button and pause/resume control.

## Important limitations

1. Yahoo Finance is an unofficial, best-effort source for this use. It is not an exchange-authorized real-time feed, may be delayed, rate-limited, incomplete, or unavailable, and may change without notice. Do not rely on it for trading or financial decisions.
2. The NSE RSS feed is official, but RSS delivery may be delayed and it covers NSE announcements only. It is not a guaranteed all-exchange alert service; BSE announcements are not integrated in this free build.
3. Android may suspend the app when it is in the background, the phone is in battery-saver mode, or the process is killed. Therefore this free, phone-only build cannot promise 60-second checks or 24/7 alerts while the app is closed. Keep the app open and exempt it from battery optimization for best-effort foreground monitoring.
4. A 60-second polling interval does not mean the market publishes a new price every minute. During closed sessions or when no new quote is available, the app should not invent a price change.
5. This app is for personal monitoring only, not a redistribution service.

## Build an installable APK from an Android phone (free)

This project uses GitHub Actions as a cloud build machine. The source ZIP is not itself an APK. You need a free GitHub account and must perform the following one-time steps on your phone:

1. Download and extract this ZIP with your phone's file manager.
2. Open https://github.com/ and create a **private** repository named `stockpulse-india`.
3. Upload the extracted project contents, including the hidden `.github` folder. If the GitHub mobile upload screen hides dot-folders, use Chrome's **Desktop site** view.
4. In the repository, open **Actions** and enable workflows if prompted.
5. Select **Build StockPulse India APK** and tap **Run workflow**.
6. When the run completes successfully, open it and download the `stockpulse-india-apk` artifact. Extract that artifact ZIP; it contains `app-release.apk`.
7. Tap the APK to install. Android may ask you to allow installs from the browser or file manager you used.

No paid GitHub plan, Firebase project, backend host, TrueData account, WhatsApp account, SMS service, or API key is needed for this free build.

## Data sources

- Yahoo Finance chart/search endpoints, via ordinary HTTPS requests. Yahoo does not offer this as a supported public developer API; use is best-effort.
- NSE corporate-announcements RSS: `https://archives.nseindia.com/content/RSS/Online_announcements.xml`.

## Development

Flutter stable, Android SDK, and Java 17 are used by the GitHub Actions workflow. Dependencies are declared in `android_app/pubspec.yaml`.
