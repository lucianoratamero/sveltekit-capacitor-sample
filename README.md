# sveltekit-capacitor-test

This repo has a sample sveltekit + capacitor app, with geolocation and filesystem examples.

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

If you want to emulate the app on android, be sure to have Android Studio with an AVD installed, then run `npx cap open android`.

## Building

To build the app, just run:

```bash
npm run build
```

To have an apk ready for production, you'll need to remove the `server` key on `capacitor.config.json`, run `npx cap sync`, and finally `npx cap open android`. From there, you can generate apks.
