# TrackPL (Android Application)

> **TrackPL** is an Android application for financial calendar and daily profit/loss (P&L) tracking, powered by Capacitor Native Bridge, Google Identity Services, and Firebase.

For detailed architecture diagrams, system design specifications, and native integration details, see the [Project Setup & System Design Guide](ProjectGuide.md).

---

## What is TrackPL?

TrackPL is designed to help traders and individuals track, visualize, and analyze their daily financial profit and loss (P&L) in an intuitive calendar format. 

### Core Features
- **P&L Calendar Visualization**: Color-coded daily trading logs and profit/loss summaries at a glance.
- **Offline First**: Instant offline data access and persistence with local caching.
- **Google Sign-In & Cloud Sync**: Secure authentication with Google Play Services and cloud synchronization with Firebase and Google Drive.
- **Native Android Experience**: Smooth hardware-accelerated WebView UI powered by Capacitor Bridge.

### Key Specifications
- **Application ID**: `com.srikanthneela.calendarapp`
- **Application Name**: `TrackPL`
- **Minimum SDK**: Android API 24 (Android 7.0+)
- **Compile / Target SDK**: Android API 36
- **JDK Requirement**: Java 21

---

## Prerequisites & Environment Setup

Before building, verify that you have:
1. **JDK 21** installed (`java -version`).
2. **Android SDK Platform 36** and **Build-Tools 36.x** installed.
3. `local.properties` file in this directory pointing to your Android SDK:
   ```properties
   sdk.dir=C\:\\Users\\<username>\\AppData\\Local\\Android\\Sdk
   ```
4. A connected Android device (USB debugging enabled) or an Android Virtual Device (AVD).

### Local Firebase Configuration
> [!IMPORTANT]
> To prevent leaking production credentials, all Firebase configs and keystores are kept **strictly local** and are ignored by Git.

- **Android Config (`app/google-services.json`)**:
  - The real file is kept locally on disk and never committed.
  - On a fresh clone, copy [`app/google-services.json.example`](app/google-services.json.example) to `app/google-services.json` and insert your Firebase project keys.
- **Web Config (`www/js/firebase-config.js`)**:
  - For frontend development, copy `www/js/firebase-config.example.js` to `www/js/firebase-config.js` or set values via `.env.local` based on [`.env.example`](../.env.example).

---

## How to Build the Application

Use the included Gradle wrapper to build the project.

### 1. Build Debug APK (For Testing)

- **Windows (PowerShell / Command Prompt)**:
  ```powershell
  .\gradlew.bat :app:assembleDebug
  ```
- **macOS / Linux**:
  ```bash
  ./gradlew :app:assembleDebug
  ```

📍 **APK Output Location**:
```
app/build/outputs/apk/debug/app-debug.apk
```

---

### 2. Build Signed Release APK (For Physical Devices)

The project includes pre-configured release signing credentials (`app/release.keystore`).

- **Windows (PowerShell / Command Prompt)**:
  ```powershell
  .\gradlew.bat :app:assembleRelease
  ```
- **macOS / Linux**:
  ```bash
  ./gradlew :app:assembleRelease
  ```

📍 **APK Output Location**:
```
app/build/outputs/apk/release/app-release.apk
```

---

### 3. Build Android App Bundle (AAB for Google Play)

- **Windows**:
  ```powershell
  .\gradlew.bat :app:bundleRelease
  ```
- **macOS / Linux**:
  ```bash
  ./gradlew :app:bundleRelease
  ```

📍 **AAB Output Location**:
```
app/build/outputs/bundle/release/app-release.aab
```

---

## How to Start / Run the Application

### Option A: Using Command Line (Terminal / PowerShell)

1. **Verify your device or emulator is connected**:
   ```powershell
   adb devices
   ```

2. **Install the Debug APK**:
   ```powershell
   .\gradlew.bat :app:installDebug
   ```

3. **Launch TrackPL on your device**:
   ```powershell
   adb shell am start -n com.srikanthneela.calendarapp/.MainActivity
   ```

---

### Option B: Using Android Studio (GUI)

1. Open **Android Studio**.
2. Select **File > Open...** and choose this `TrackPL` directory.
3. Wait for the Gradle project sync to complete.
4. Select the **`app`** configuration in the top toolbar.
5. Choose your target emulator or physical device from the device dropdown.
6. Click the green **Run** button ▶️ (or press `Shift + F10`).

---

## In-Depth Documentation

For the complete technical guide, refer to:
- [**ProjectGuide.md**](ProjectGuide.md) — System design, component architecture, sequence flows, OAuth configurations, and troubleshooting.
