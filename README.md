# Dino Run

A calm 2D runner for kids and grown-ups. A friendly dino runs through a meadow, hops striped hurdles and catches golden stars, while the sky slowly turns from day to sunset to night and back.

**▶ Play it in your browser:** https://pallanagendra.github.io/Dino-run/ (updates automatically when `main` changes).

The whole game is one HTML5 canvas file (`www/index.html`) with no external assets: graphics are drawn in code and every sound is synthesized. [Capacitor](https://capacitorjs.com) wraps it as a native iOS app and a native Android app.

## How to play

| Action | Touch | Keyboard |
| --- | --- | --- |
| Jump (hold for a higher jump) | Tap / hold anywhere | Space, Up or W |
| Double jump | Tap again in the air | Press again in the air |
| Pause | Pause button (or switch apps) | P or Esc |
| Sound on/off | Speaker button | M |
| Music on/off | Note button | |

- **Pick your dino.** Six colours on the start screen: Mint, Sky, Sunny, Berry, Grape and Coral. The choice is saved.
- **Obstacles arrive gradually**, so the start stays easy:

  | From | Obstacle | How to pass |
  | --- | --- | --- |
  | Start | Striped hurdle (low / mid / tall), rock, traffic cone | Jump |
  | 12 s | Hay bale, fallen log (wide: jump a little earlier), flower pot | Jump |
  | 25 s | Double hurdles | One long jump |
  | 25 s | Buzzy bee (flies at head height) | **Stay on the ground** and run under; a row of stars waits under it |
  | 35 s | Stacked hay bales (tall) | Hold the jump, or double jump |

- **3 hearts.** Bumping an obstacle costs a heart and gives a short "blink" safety window. Hurdles, cones and pots tip over, bales and logs wobble, and the bee buzzes away. A pink heart sometimes floats in to refill one.
- **Score** = distance + 10 per star. Catching stars in a row plays a rising chime.
- Speed rises gently and caps at a calm maximum. Best score, sound and music settings are saved on the device.

## Project layout

```
www/index.html          the game (edit this one file)
capacitor.config.json   app id, name and background colour
android/                native Android Studio project
ios/                    native Xcode project (Swift Package Manager, no CocoaPods)
assets/                 icon + splash source PNGs (assets/source has the SVGs)
```

## Build it

You'll need **Node.js 22+**.

```bash
npm install
```

Before you publish, change `appId` in `capacitor.config.json` from `com.dinorun.app` to your own reverse-domain id (for example `com.yourstudio.dinorun`). It has to be unique in the stores. If you change it after the native folders exist, also update the bundle identifier in Xcode and `namespace` / `applicationId` in `android/app/build.gradle` (or delete `android/` and `ios/` and run `npx cap add android` and `npx cap add ios` again).

### Android

Requires [Android Studio](https://developer.android.com/studio) (it bundles JDK 21).

```bash
npm run android        # copies www into the project and opens Android Studio
```

In Android Studio, press **Run** to install the app on a phone or emulator. To get a Play Store bundle, use **Build → Generate Signed App Bundle / APK** and choose **Android App Bundle (.aab)**.

### iOS

Requires a Mac with the latest **Xcode**. The app supports iOS 15 and later.

```bash
npm run ios            # copies www into the project and opens Xcode
```

In Xcode, select the **App** target → **Signing & Capabilities**, choose your Team, then pick a device and press **Run**. For the App Store, use **Product → Archive** and upload from the Organizer.

### After editing the game

```bash
npx cap sync           # copies www/index.html into both native apps
```

### Web version (GitHub Pages)

Every push to `main` that changes `www/` redeploys the browser version through `.github/workflows/pages.yml`. You can also run it by hand from the repo's **Actions** tab → *Deploy game to GitHub Pages* → **Run workflow**. One-time setup: repo **Settings → Pages → Source: GitHub Actions**.

### Icons and splash screens

Replace the PNGs in `assets/` (icon 1024×1024, splash 2732×2732), then:

```bash
npm run assets
```

## Native touches already set up

- Full-screen game mode: Android hides the status and navigation bars (swipe from the edge to show them), and iOS hides the status bar.
- Works in portrait and landscape. The game automatically shows more sky in portrait.
- The game pauses and the audio goes quiet when the app goes to the background.
- iOS: Web Audio follows the ring/silent switch, so the game is silent when the phone is on silent.

## Store checklist

- App name, a 1–2 line description, and screenshots (pause the game on a nice moment).
- Age rating: no ads, no in-app purchases, no data collection, so it fits **Everyone / 4+**. If you list it in a Kids category, keep it free of ads and analytics.
- A privacy policy URL (both stores ask for one; this game collects nothing).
