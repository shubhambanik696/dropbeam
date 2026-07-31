# DropBeam

**Share instantly. Store nothing.**

DropBeam is a serverless, open-source tool for sharing files and text — with no
accounts, no servers, and no tracking. It's a single HTML file.

- **Beam** — send files, text, and a live-synced clipboard directly between your
  own devices (laptop, phone, tablet) over an end-to-end encrypted peer-to-peer
  connection. Everything burns after use.
- **Collect** — sign in with your own Google account, show a QR code, and let
  anyone upload files straight into *your* Google Drive — no app, no account
  needed on their end.

Nothing is ever stored on a server. Closing the tab wipes everything.

## How it works

The entire product is one file, `index.html`. Transfers use WebRTC (via PeerJS)
so data travels directly between browsers. The QR generator is embedded inline.
Collect mode uses Google's Drive API with the narrow `drive.file` scope; the
organiser's token never leaves their browser.

## Run it

**Beam mode works immediately — just host the file over HTTPS.**

1. Drop `index.html` onto [Netlify Drop](https://app.netlify.com/drop), or push
   to GitHub Pages / Cloudflare Pages.
2. Open the URL. Try **Beam** right away.

**Collect mode** needs a Google OAuth Client ID (one-time setup):

1. Copy `config.example.js` to `config.js`.
2. Paste your Google Client ID into `config.js`.
3. Deploy `index.html` **and** `config.js` together.

`config.js` is git-ignored, so your Client ID never lands in the repo. Full
step-by-step (including creating the Google Client ID) is in
[`SETUP.md`](./SETUP.md).

## A note on the Google Client ID

OAuth Client IDs are **not secrets** — they're meant to be visible in
client-side code. Their security comes from the *Authorized JavaScript Origins*
allowlist you configure in Google Cloud Console, not from being hidden. We keep
it in a git-ignored `config.js` only so that forks don't accidentally use the
original project's OAuth app and quota — not because exposure would be a breach.

DropBeam has **no server-side secrets of any kind** (no API keys, no database),
which is what makes it safe to open-source as-is.

## Files

| File | Committed? | Purpose |
|---|---|---|
| `index.html` | yes | the entire app |
| `config.example.js` | yes | template for your config |
| `config.js` | **no** (git-ignored) | your real Client ID, local only |
| `SETUP.md` | yes | full hosting + Google setup guide |
| `.gitignore` | yes | keeps `config.js` out of the repo |

## Privacy & Terms

The app includes built-in Privacy Policy and Terms of Use pages (linked in the
footer). They're general-purpose templates — for anything high-stakes, have a
lawyer review them and fill in your contact details and jurisdiction.

## License

MIT — see [`LICENSE`](./LICENSE).
