# GeoCloak

One-click residential **geo · timezone · locale · WebRTC** alignment with a live posture monitor and WhoX-style self-tests.

**Status:** inject layer verified **12/12** in headless Chrome (timezone, offset, native `toString`, language, WebRTC block, geolocation, iframe TZ, probe, profile switch). Manifest and profile schema validated.

## Profiles

| City | Timezone |
|------|----------|
| Memphis, TN | America/Chicago |
| Savannah, GA | America/New_York |
| Dayton, OH | America/New_York |
| Chillicothe, OH | America/New_York |
| Chicago, Dallas, Atlanta, Denver, Seattle | (US zones) |
| London, Toronto | Europe/London, America/Toronto |

## Install (3 steps)

### Firefox
1. Clone or unzip this repo.
2. `about:debugging#/runtime/this-firefox` → **Load Temporary Add-on** → select `manifest.json`.
3. Toolbar icon → pick VPN exit city → **Start protection** → **Run tests**.

### Chrome / Edge / Brave
1. `chrome://extensions` → Developer mode → **Load unpacked** → select this folder.
2. Same Start flow as above.

### Safari (macOS)
Developer menu → **Add Temporary Extension** → select this folder → Start.

Match your **OS timezone** once to the city shown in the popup (Copy button).

## What is verified

| Layer | Covered |
|-------|---------|
| Date / `Intl` timezone | Yes |
| `getTimezoneOffset` coherence | Yes |
| Native-shaped function `toString` | Yes |
| `navigator.language` / `languages` | Yes |
| Geolocation coords | Yes |
| iframe realm timezone | Yes |
| WebRTC constructor block | Yes |
| Live HUD + score badge | Yes |
| JA4T / TCP SYN OS fingerprint | **No** (network layer — see `VPN-ALIGNMENT.md`) |

## Daily use

1. Connect residential VPN.
2. Open GeoCloak → city matches exit → **Start protection**.
3. **Run tests** (or rely on monitoring).
4. Score 80+ = solid JS alignment.

## Develop / self-test

```bash
# Syntax
node --check background.js content.js inject.js popup.js options.js hud.js

# Browser inject E2E (needs Chrome)
python3 -m http.server 8765 --directory . &
# open tests/inject-e2e.html
```

## Limits (honest)

No browser extension can rewrite **JA4T** (TCP SYN) or exit ASN. Use a residential VPN whose exit city matches the selected profile, and set the OS timezone to that city.

## License

MIT
