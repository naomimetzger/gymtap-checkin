# GymTap Check-in

Static GymTap demo: NFC check-in flow and passport app.

## Pages

| URL | Purpose |
|-----|---------|
| `/` | Check-in flow (geolocation + selfie stamp) |
| `/passport.html` | Full passport onboarding & stamp book |

## NFC stickers

NTAG stickers open a URL in the phone browser — that **is** the NFC tap. Program each sticker with:

```
https://gymtap-checkin.vercel.app/?nfc=1
```

Per-gym coordinates (optional):

```
https://gymtap-checkin.vercel.app/?nfc=1&gym=PureGym%20Leicester&lat=52.6369&lng=-1.1398
```

When `nfc=1` (or `from=nfc` / `source=nfc`):

- Geofence is skipped (physical tap = proof of presence)
- Check-in auto-starts on page load
- Stamp shows **NFC tap confirmed**

## Geofence (manual visits)

Without `nfc`, the app uses `navigator.geolocation` and compares your position to the gym coordinates (default: PureGym Leicester, 150 m radius).

Override via query params: `?gym=Name&lat=52.63&lng=-1.14&radius=150`

Demo without location: `?demo=1`

## Deploy

```bash
vercel --prod
```
