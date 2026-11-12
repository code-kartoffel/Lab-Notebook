# Lab notebook (iPad web app)

An offline electronic lab notebook for the iPad. Entries are written on the iPad and exported as `.eln` files
(the open ELN file format) for import into [eLabFTW](https://www.elabftw.net/).

This repository only hosts the app. **The page is encrypted**: without the password it shows a password prompt and
nothing else. Templates and other content of the app are inside the encrypted file.

## Where the data is

- **Entries are stored only on the device** (browser storage of the Home Screen app). Nothing you write is sent to
  GitHub or anywhere else.
- Exports (`.eln` files) are saved wherever you choose, e.g. a cloud folder, and imported into eLabFTW from there.
- The browser storage is not a backup: export regularly.

## Files

| File | Purpose |
|---|---|
| `index.html` | the app, encrypted with [StatiCrypt](https://github.com/robinmoisson/staticrypt) (AES-256, password-derived key) |
| `sw.js` | service worker: keeps a copy of the app for offline use |
| `manifest.webmanifest`, `icon-*.png` | name and icon for the Home Screen |
| `.nojekyll` | tells GitHub Pages to serve the files as they are |

## Setup

1. **GitHub Pages:** upload these files to the repository root, then *Settings → Pages* → *Deploy from a branch*,
   branch `main`, folder `/ (root)`. The address appears there after about a minute.
2. **iPad:** open the address in Safari, enter the password (optionally tick *Remember me*), then
   *Share → Add to Home Screen*.
3. **Always open the app from the Home Screen icon.** A Safari tab has separate storage, so entries made there do not
   appear in the Home Screen app.
4. In the app: *Settings → Request persistent storage*, and fill in the author details used in the exports.

## Updating

Build and encrypt the new version with the same password, then upload the new files over the old ones. The iPad uses
the new version from the second start, because the offline copy updates in the background. Entries on the iPad are kept.

## Security notes

- The encryption is only as strong as the password: anyone can download `index.html` and try passwords offline. Use a
  long password.
- *Remember me* stores a salted hash of the password on the device for a limited time.
- Never upload the unencrypted build or source files to this repository.
