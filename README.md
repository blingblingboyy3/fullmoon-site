# 🌕 FullMoon Website — Treasury Tracker & Home Page

One self-contained file (`index.html`) — no server, no build tools.
It reads the donation wallet straight from the Solana blockchain in
each visitor's browser.

**Security model:** this site NEVER holds keys or funds. The wallet
lives in your Phantom; the site only watches its public address —
the same thing anyone can do on Solscan, just prettier.

## Setting up the donation wallet (do this before launch)

1. Open Phantom → click the account menu → **Add / Connect Wallet** →
   **Create a new wallet/account**. Name it "FullMoon Donations".
   Keep it SEPARATE from your personal wallet — clean books matter
   when you're preaching transparency.
2. Write the recovery phrase on paper. Never digital, never shared.
   Anyone with the phrase owns the treasury.
3. Copy the wallet's **public address** (the ~44-character string).

## Configuring the site

Open `index.html`, find the `CONFIG` block near the bottom
(clearly marked — it's the only part you edit):

- `WALLET_ADDRESS` — paste the public address. Until you do, the site
  shows a "wallet goes live at launch" notice (with a scam warning).
- `GOAL_SOL` — the "next donation at X SOL" target. After each
  donation, bump it or leave it for the next round.
- `RPC_URLS` — works out of the box on Solana's public endpoint. For
  faster/more reliable reads, paste your Helius URL as the first
  entry (same key as the buy bot).
- `DONATIONS` — the receipts wall. Each time the pack donates, add
  one entry: date, amount, Solscan tx link, foundation receipt link.
  This is your proof archive — keep it current.
- `LINKS` — Telegram + X links for the footer.

## The donation flow (how the transparency loop works)

1. People send SOL to the address → live tracker climbs.
2. Treasury hits `GOAL_SOL` → you donate to the American Wolf
   Foundation. If they don't accept crypto directly: convert to USD,
   donate on their site, screenshot the confirmation.
3. Add the entry to `DONATIONS` (tx link + receipt) → commit → the
   receipts wall updates. Reset/raise `GOAL_SOL` as you like.

## Hosting (when you're ready — GitHub Pages, free)

1. New GitHub repo (e.g. `fullmoon-site`) — **Public** this time
   (Pages requires it on free accounts, and it's just a website).
2. Upload `index.html` → Commit.
3. Repo **Settings → Pages** → Source: "Deploy from a branch" →
   Branch: `main`, folder `/ (root)` → Save.
4. Two minutes later your site is live at
   `https://YOURUSERNAME.github.io/fullmoon-site/`.
5. Custom domain later: buy one (e.g. Namecheap), add it in the same
   Pages settings screen, follow the DNS instructions shown there.

Updates forever after: edit `index.html` on GitHub (pencil icon) →
Commit → live in ~1 minute.

## Notes

- The live feed shows recent incoming donations with Solscan links;
  on the free public RPC it may occasionally rate-limit — adding your
  Helius URL fixes that.
- SOL→USD price comes from CoinGecko's free API.
- Everything degrades gracefully: if an API is down, the page still
  looks good and shows the last known numbers.
