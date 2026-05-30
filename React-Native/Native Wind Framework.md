Website: https://www.nativewind.dev/

1. Install Native wind in react-native-expo.

```bash
npm install nativewind tailwindcss@^3.4.17 react-native-reanimated@3.16.2 react-native-safe-area-context
```

2. Setup Tailwind CSS 
   - Run `npx tailwindcss init` to create a `tailwind.config.js` file

```bash
npx tailwindcss init
```

-  Add the paths to all of your component files in your `tailwind.config.js` file.

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  // NOTE: Update this to include the paths to all of your component files.
  content: ["./app/**/*.{js,jsx,ts,tsx}", "./components/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

   - Create a CSS file and add the Tailwind directives.

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

- Add a Babel present file `babel.config.js` in root directory.

```js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: [
      ["babel-preset-expo", { jsxImportSource: "nativewind" }],
      "nativewind/babel",
    ],
  };
};
```

- Create `metro.config.js` file with command

```bash
npx expo customize metro.config.js
```

- Replace This Code and input CSS file according to your directory.

```js
const { getDefaultConfig } = require("expo/metro-config");
const { withNativeWind } = require('nativewind/metro');
 
const config = getDefaultConfig(__dirname)
 
module.exports = withNativeWind(config, { input: './app/global.css' })
```

- Import your CSS file as per your directory in `_layout.tsx`.

```ts
import { Stack } from "expo-router";
import "./global.css"
  
export default function RootLayout() {
  return <Stack />;
}
```

- At the root of the project, create a file named `nativewind-env.d.ts` & paste the following code inside it:

```js
/// <reference types="expo/types" />
```
This will enable TypeScript to recognize Tailwind classes, preventing constant error messages.

- Clear cache

```bash
npx expo start --clear
```

- Restart the app press `r`.