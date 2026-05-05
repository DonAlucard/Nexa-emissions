# Nexa Emission Schedule

A community-built, factually grounded explorer for Nexa's emission schedule, halving cadence, and live network state.

Live: https://emissions.nexa.org (or https://nexaemissions.netlify.app)

## What it is

A single-file web app that visualises every aspect of Nexa's deterministic emission schedule:

- **Halving countdown** to the next era boundary, anchored to known ETAs
- **Schedule scrubber** — drag through 116 years of supply emission, era by era
- **Emission curve chart** with seven overlay-able metrics: cumulative, remaining, per-era, % of cap, block reward, annual inflation, and stock-to-flow
- **Network state** — live block height, hash rate, difficulty, supply emitted
- **Live blocks** — recent block tiles streamed from a public Nexa Rostrum endpoint, with real on-chain transaction counts, sizes, timestamps, and per-block details (nonce, merkle root, ancestor hash, tx filter, chain work, pool fee, confirmations, time since previous)
- **Block art** — every block hash deterministically maps to a sacred-geometry mandala (32 visual parameters drawn from the 32 hash bytes; eight palette themes; downloadable as 1200×1200 PNG)
- **Sounds of Nexa** — every block hash maps to a chord locked to a musical scale, with eight selectable genres (Classical, Rock, Techno, Dubstep, Ambient, 8-Bit, Jazz, Cinematic, Lo-fi), genre-appropriate drums, and a 16-step melody bench you can compose with and share
- **Era summary** + side-by-side era comparison with thirteen metrics including stock-to-flow and inflation rate deltas
- **Date explorer calendar** — pick any date between Genesis and 2138 and see the network state for that day
- **Coin race** — interactive 2-to-6-chain throughput animation
- **Globe transaction demo** — stylised propagation visualisation between user-chosen cities
- **Live market data** from the CoinGecko public API

## Data sources

Everything on the page is either pulled live from on-chain data or computed deterministically from the canonical schedule. Specifically:

- **Schedule values** (block heights, era rewards, halving years) — from the official [Nexa Emission Schedule spreadsheet](https://docs.google.com/spreadsheets/d/1LmKRhChSDMldWGqycC0kkfH6WDICBLJNkUobUb-HrJg)
- **Live blocks** — `wss://electrum.nexa.org:20004` Rostrum endpoint, parsed with the canonical Nexa block header layout
- **Header parser** — verified against the libnexa-ts `BlockHeader._fromBufferReader` source
- **Difficulty calculation** — Bitcoin-compatible compact target encoding per [spec.nexa.org/mining/proof-of-work](https://spec.nexa.org/mining/proof-of-work/)
- **Unit conversions** — 1 NEXA = 100 satoshis (Nexa Tokenomics)
- **Market data** — CoinGecko `/coins/markets` endpoint
- **Inflation rate, stock-to-flow** — pure arithmetic on the schedule × `BLOCKS_PER_YEAR = 365.25 × 86400 / 120 ≈ 262,800`

## Tech stack

- Single HTML file, no build step
- React 18 (CDN, with Babel-standalone for JSX)
- Chart.js 4 for the emission curve
- D3 + topojson for the globe
- Tone.js 14 for the sound engine
- WebSocket client for Rostrum (Electrum 1.4.3 + Nexa extensions)
- All state in React; no backend

To run locally, just open `index.html` in a browser. No build, no install.

## Deploying

The site is a single static HTML page. Drop `index.html` and `og-image.png` into any static host:

- **Netlify** — drag-and-drop deploy via [app.netlify.com/drop](https://app.netlify.com/drop)
- **Cloudflare Pages** — direct upload
- **Vercel** — drag-and-drop
- **GitHub Pages** — enable on this repo's Settings → Pages

## Built by

The Nexa community, working under [Bitcoin Unlimited](https://www.bitcoinunlimited.info/).

The Nexa protocol is fair-launched, open-source, and developed in the open at [gitlab.com/nexa](https://gitlab.com/nexa).

## License

MIT — see [LICENSE](./LICENSE).
