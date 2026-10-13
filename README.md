# WomSakhi Mobile

The WomSakhi mobile app for Android and iOS. WomSakhi is a women-only Indian platform for work, circles, shops, learning and support. This app is the second door to the same account as the web app at **app.womsakhi.com**.

## The decision this repo follows

These were decided on 29 Sep 2026:

- **One account, two doors.** Every feature goes in the app. Nothing is hidden to push her to the web. The web app stays for shared shop links, computers and staff.
- **The app is the login key for computers.** She signs in on a computer by scanning a QR code or typing a 30-second code from the app. SMS is the backup.
- **Stack:** Phase 1 is a Trusted Web Activity. Phase 2 is **Expo (React Native) + TypeScript**. Do not use Capacitor, Flutter or a bare WebView wrapper. Google Play rejects a bare wrapper, and UPI payment intents fail inside a WebView.

## Phases

| Phase | What | Notes |
|---|---|---|
| **1. Trusted Web Activity on Play** | Wrap app.womsakhi.com as a TWA (~1 MB). Add `/.well-known/assetlinks.json` on the web app. | 1–2 weeks. Also needs live chat with notifications. |
| **1. Backend support** | Trusted devices, one-time "open web" links, token refresh for the app | Tokens last 30 min and `/auth/refresh` is cookie-only today, so a native client cannot renew. This must be fixed in the main repo first. |
| **2. Expo native screens** | Shop, circles, chat, the login key (QR / 30 s code), app lock | Reuse the TypeScript types, API client and wording from the web app |

## How it connects

| Thing | Where |
|---|---|
| API | `https://api.womsakhi.com` (FastAPI). Source: `prakmas-global/womsakhi` → `womencrafts-backend/backend` |
| Web app (reference for screens, types, API calls) | `prakmas-global/womsakhi` → `womencrafts-frontend/frontend` (`src/lib/*-api.ts`) |
| Brand | Berry `#9b1d50`, deep plum, cream. Playfair Display + DM Sans. Pill buttons. |
| Language | English at launch. Telugu and Hindi later, so no hard-coded strings. |

## Rules that are not negotiable

- **Women's safety first.** Phone numbers are hidden by default, an exact address is shown only after a booking, and every screen has a quick way to report.
- **Never invent data.** If something isn't there, show an honest empty state, not sample numbers.
- **WomSakhi never holds money.** Pay goes person to person over UPI, so open UPI apps by intent, never inside a WebView.
- **Small and light.** Each extra ~6 MB of APK costs about 1% of installs. Many users are on low-storage phones and are using a smartphone for the first time.
- **Secrets** never go in this repo. Use `.env` files kept out of git and EAS secrets.

## Working in this repo

1. Create a branch from `main`: `feat/<short-name>` or `fix/<short-name>`.
2. Commit and push your branch.
3. Open a **pull request to `main`**. Direct pushes to `main` are blocked, and only the owner reviews and merges.
4. Resolve every review comment before merge.

## Status

New repository, created 13 Oct 2026. No app code yet; Phase 1 starts here.
