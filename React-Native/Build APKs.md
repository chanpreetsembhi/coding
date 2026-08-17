## Table of Contents

1. [[#1. Initialize Project|Initialize Project]]
2. [[#2. Create a Development Build|Create a Development Build]]
3. [[#3. Dependency & Health Checks|Dependency & Health Checks]]
4. [[#4. Android Build (Production/Preview)|Android Build]]

---

## 1. Initialize Project

Upload/Update project in expo dashboard
```bash
eas init
```

For login

```bash
eas login
```

For login details

```bash
eas whoami
```

---
## 2. Create a Development Build

Dev builds let you use native modules that Expo Go doesn't support.

```bash
npm install -g eas-cli
eas login
eas build:configure
```

Build a dev client:

```bash
eas build --profile development --platform android
# or for local build (no EAS cloud, needs Android Studio SDK)
npx expo run:android
```

Install the resulting `.apk` on your device/emulator, then run:

```bash
npx expo start --dev-client
```

---
## 3. Dependency & Health Checks

Check for outdated/incompatible packages:

```bash
npx expo install --check
npx expo install --fix
```

Run Expo Doctor (validates config, native deps, versions):

```bash
npx expo-doctor
```

Check for outdated `npm` packages generally:

```bash
npm outdated
npm audit
```

Check Expo SDK/CLI versions:

```bash
npx expo --version
npx expo-cli --version
```

---
## 4. Android Build (Production/Preview)

```bash
# Preview APK (for internal testing)
eas build --profile preview --platform android

# Production build (AAB for Play Store)
eas build --profile production --platform android
```

`eas.json` example profiles:

```json
{
  "build": {
    "development": { "developmentClient": true, "distribution": "internal" },
    "preview": { "distribution": "internal", "android": { "buildType": "apk" } },
    "production": {}
  }
}
```

Submit to Play Store:

```bash
eas submit --platform android
```

