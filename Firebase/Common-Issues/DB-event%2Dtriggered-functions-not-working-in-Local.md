For us to be able to work with and leverage DB-triggered functions, we need to **Emulate** `Firestore` locally so that our `Functions` Emulator can pick up the events and execute them as necessary

---

To do this, you must setup the emulator first by configuring it in the `/functions/firebase.json` file as:

![image.png](/.attachments/image-883d74c6-3f90-49f5-890a-47e9396adf44.png)


Next, you need to update the `/functions/package.json` that contains the command to `serve` your `functions` locally as:

`"serve": "npm run build && firebase emulators:start --import=./emulator-data --export-on-exit --only functions,firestore --project dev-yourproject"`

The command above will start/**emulate** both `functions` and `firestore` locally using the setup ports in `firebase.json`. It will also automatically export and import data so that you can still work on test data in your local. Otherwise, the firestore automatically clears local data every time it is started