# Motor Sound

A buildless iPhone Home Screen web app that uses GPS speed to drive synthesized engine audio or a bundled BMW exhaust loop. Connect the iPhone to car speakers over Bluetooth, then start audio from a tap.

## Files

| Path | Purpose | Needed on the hosted site? |
| --- | --- | --- |
| `index.html` | The app, including all CSS and JavaScript | Yes |
| `manifest.json` | Home Screen app metadata | Yes |
| `icon.png` | Home Screen icon | Yes |
| `audio/bmw_exhaust.mp3` | Original BMW MP3 copy; audio is also embedded in `index.html` | Keep it in Git |
| `.nojekyll` | Serves the folder as a plain static site on GitHub Pages | Include it |
| `README.md` | Setup and testing instructions | No, but keep in Git |
| `backups/motor-sound-v1.html` | Original version before the loop library | No, but keep in Git for rollback |
| `backups/motor-sound-before-local-fix.html` | Version before local BMW playback was fixed | No, but keep in Git for rollback |

Keep the same folder structure. Every asset path in the app is relative. No npm, build step, or audio library is needed.

The BMW MP3 is embedded in `index.html`, so Test mode works when that HTML file is opened directly. The separate MP3 is kept as an editable source copy. If you replace the MP3, update the embedded audio in `index.html` too. GPS and Home Screen installation still require hosting over HTTPS.

## Create the separate GitHub repository and push

1. On GitHub, create a **public**, empty repository named `motor-sound-app` under your account. Do not initialize it with a README, license, or `.gitignore`; those files are already in this local repository. A public repository works with GitHub Pages on GitHub Free.
2. In PowerShell, enter this folder and push the prepared `main` branch. Its `origin` remote is already configured for `hussainali-saiyed/motor-sound-app`:

   ```powershell
   cd "C:\Users\HUSSAIN ALI SAIYED\Portfolio\motor-sound-app"
   git push -u origin main
   ```

3. In that repository, open **Settings → Pages**. Choose **Deploy from a branch**, then **main** and **/(root)**, and save. GitHub will show the HTTPS site URL.
4. Open that URL in iPhone Safari, use **Share → Add to Home Screen**, and launch it from the new icon.

Only the `git push` step sends the committed files to GitHub. Publishing with Pages happens after you enable Pages in the repository settings.

## iPhone check

- Connect Bluetooth speakers and set a low starting volume.
- While parked, select **Built in · BMW exhaust** under **Sound source** and tap **Test mode**. The roughly 10-second file should repeat while its pitch follows RPM.
- Switch to **Synthesized engine** and check the V8, Inline-4, Electric whine, and Turbine profiles.
- Tap **Start GPS**, allow location access, and check speed and RPM during a safe drive. Keep the app visible in the foreground.
- If adding your own MP3 or WAV, upload from the Home Screen app. It is saved locally on that iPhone and is not added to the GitHub repository.

An earlier app can be restored by copying either file in `backups/` over `index.html` and committing that change. This standalone app has no service worker, so offline startup is not guaranteed.
