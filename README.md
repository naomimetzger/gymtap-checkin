# GymTap Check-in

Static GymTap demo: passport home and NFC check-in flow.

## Pages

| URL | Purpose |
|-----|---------|
| `/` | Passport home — onboarding & stamp book |
| `/checkin.html` | Check-in flow (geolocation + selfie stamp) |
| `/passport.html` | Redirects to `/` (legacy URL) |

## NFC stickers

NTAG stickers open a URL in the phone browser — that **is** the NFC tap. Program each sticker with:

```
https://gymtap-checkin.vercel.app/checkin.html?nfc=1&step=selfie
```

From passport (iOS fallback — sticker opens check-in while passport waits):

```
https://gymtap-checkin.vercel.app/checkin.html?nfc=1&step=selfie&from=passport
```

Per-gym coordinates (optional):

```
https://gymtap-checkin.vercel.app/checkin.html?nfc=1&step=selfie&gym=PureGym%20Leicester&lat=52.6369&lng=-1.1398
```

**Legacy stickers** pointing at `/?nfc=1&…` still work — Vercel redirects those query params to `/checkin.html`.

### Passport tap-in flow

1. Open [the passport](https://gymtap-checkin.vercel.app/) and tap **Tap in**
2. **Android Chrome**: Web NFC listens for the chip (`NDEFReader.scan()`)
3. **iPhone**: hold phone to sticker — Safari opens the check-in URL above
4. Selfie → stamp → check-in saved to `localStorage` (`gymtap-checkins`)

When `nfc=1` (or `from=nfc` / `source=nfc`):

- Geofence is skipped (physical tap = proof of presence)
- With `step=selfie` or `#selfie`, lands directly on selfie capture (`capture="user"`)
- Stamp shows **NFC tap confirmed**

## Geofence (manual visits)

Without `nfc`, the app uses `navigator.geolocation` and compares your position to the gym coordinates (default: PureGym Leicester, 150 m radius).

Override via query params: `?gym=Name&lat=52.63&lng=-1.14&radius=150`

Demo without location: `?demo=1`

## Deploy

```bash
vercel --prod
```
