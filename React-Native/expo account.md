
email: dajav47386@hazhab.com
username: joker1223
password: joker$1234

## Steps to Build APK with Expo

### 1. **Go to your project directory:**

```bash
cd your-project-directory
```

### 2. **Build the APK:**

As of Expo SDK 48 and later, the recommended way is using **EAS Build** (Expo Application Services):

```bash
npx expo install eas-cli npx eas build:configure
```


Then run:
```bash
npx eas build -p android --profile preview
```

> `--profile preview` will generate an APK. Use `--profile production` for AAB (Android App Bundle).

By default, Expo now builds AABs for Play Store. To get a downloadable APK for testing:

### 3. **Wait for the build to finish**, then download the APK:

After running the build command, you'll get a URL to monitor the build progress. When it's done, you'll get a link to download the APK file.

---

## 📦 Accessing APK Download

Once the build is complete, Expo CLI will give you a link like:

arduino
```bash
https://expo.dev/accounts/yourusername/projects/yourproject/builds/abc123
```

Visit the link and download the APK directly.