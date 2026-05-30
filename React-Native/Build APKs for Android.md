[Official Link](https://docs.expo.dev/build-reference/apk)
**(Not Compulsory)** Create `eas.json` file. When you run build its automatically add in your project.

```json
{
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    },
    "preview2": {
      "android": {
        "gradleCommand": ":app:assembleRelease"
      }
    },
    "preview3": {
      "developmentClient": true
    },
    "preview4": {
      "distribution": "internal"
    },
    "production": {}
  }
}
```

To Solve Issues Use this command.
```bash
npx expo install --check
```

Update project in expo dashboard
```bash
eas init
```

For login details
```bash
eas whoami
```

To solve warning run this command
```bash
npx -y expo-doctor
```

Build APK command
- for abb file used in (android emulator)
```bash
eas build --platform android
```

for APK file
```bash
eas build --platform android --profile preview 
```

```bash
npx --yes eas-cli build --platform android --profile preview
```

Download APK file from expo dashboard

#### To Reduce the APK size

Run this command
```bash
npx expo prebuild -p android
```

Then open `grade.properties` file, go to the very last property, `expo.useLegacyPackaging`, and change it from false to true, then run the command to generate your APK.

Run this command to check the issues.
```bash
npx expo-doctor@latest
```