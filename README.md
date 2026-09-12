# Tiny house Malý gurmán — aplikace pro hosty

Jednostránkový průvodce pobytem. Bez sestavování, bez závislostí — statické soubory.

## Nasazení

Repozitář je napojený na Cloudflare Workers (služba `tiny-house-app`).
Po commitu do větve `main` se sestavení spustí samo a nová verze je za pár desítek sekund živá na
https://tiny-house-app.dejv93.workers.dev

## Soubory

| soubor | co dělá |
|---|---|
| `index.html` | celá aplikace: HTML, styly, skript i fotky (WebP v base64) |
| `manifest.webmanifest` | umožní přidat appku na plochu telefonu s vlastní ikonou |
| `sw.js` | offline režim — po první návštěvě appka funguje i bez signálu |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | ikony na ploše |
| `apple-touch-icon.png` | ikona pro iPhone |

## Aktualizace obsahu

Všechen text i fotky jsou v `index.html`. Po úpravě zvyšte verzi cache v `sw.js`
(`const CACHE = 'malygurman-v1'` → `v2`), jinak se hostům se starou verzí v telefonu
nemusí změna hned projevit.

## Co appka potřebuje ze sítě

- **Open-Meteo** (`api.open-meteo.com`) — živé počasí, bez klíče a zdarma. Offline se pruh skryje.
- **Google Fonts** — písma Fraunces a Work Sans. Servisní skript je ukládá, takže po první
  návštěvě fungují i offline.

## Wi-Fi údaje

Název sítě a heslo se mění na jednom místě, na začátku `<script>` na konci `index.html`
(konstanta `WIFI`). Po změně je potřeba přegenerovat i oba QR kódy.
