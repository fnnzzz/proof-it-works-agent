# Demo Agent Memory

Persistent learnings across QA sessions. Updated automatically at the end of each session.

---

## Selectors

- Coin asset page sections: `[data-test="coin-additional-info-sections-technology-header"]` / `-team-header` / `-roadmap-header` etc. — stable data-test attributes on section buttons (2026-02-24)
- Tags expand button: `[data-test="coin-additional-info-sections-metadata-tags-toggle"]` — stable (2026-02-24)
- Accordion section expanded state: button has `[expanded]` and `[active]` attributes in snapshot when open (2026-02-24)
- Coin page scrollable container: `.coin__body` — must scroll this element, not window, to reveal sections below the chart (2026-02-24)

---

## Timing

- Coin asset page (BTC, BNB, USDT): wait 3s after navigation before taking snapshot — page renders fully within that time (2026-02-24)
- Sections accordion responds immediately to clicks — no delay needed between click and assertion (2026-02-24)

---

## Test Data

- BTC coin page: Overview/Technology/Tokenomics/Roadmap/Team all present; Tags has 35 total (+31 bubble shows first 4); Website: bitcoin.org; Socials: Reddit, GitHub, Message Board (2026-02-24)
- BNB coin page: All CMC sections present; Contracts section shows 1 Ethereum address (0xb8c7...1bdd52); Tags has 14 total (+10 bubble shows first 4) (2026-02-24)
- USDT coin page: All CMC section buttons present (Overview/Technology/Tokenomics/Roadmap/Team); No Contracts section in right panel (no XBO DP/WD contracts); Tags has 19 total (+15 bubble) (2026-02-24)
- BTC circulating/total supply in header: 19.99M BTC (2026-02-24)
- BNB circulating/total supply in header: 136.35M BNB (2026-02-24)
- USDT circulating supply: 183,738.73M USDT; total supply: 187,952.73M USDT (2026-02-24)

---

## Known Quirks

- Coin asset page layout uses a fixed-size chart area with `.coin__body` as the only scrollable element — `window.scrollBy` does nothing; must use `document.querySelector('.coin__body').scrollTop` (2026-02-24)
- Header label says "Circular supply" not "Circulating supply" — possible cosmetic typo; not blocking (2026-02-24)
- Overview section is open/expanded by default when landing on a coin page — all others collapsed (2026-02-24)
- Contracts section in right panel only appears if the token has DP/WD contracts registered on XBO — no "empty" placeholder is shown when absent (2026-02-24)
- Tags "+N" bubble is a button that expands all remaining tags inline (not a modal) (2026-02-24)

---

## API Patterns

- Coin info page: `/platform/coin/{SYMBOL}` — e.g. /platform/coin/BTC, /platform/coin/BNB, /platform/coin/USDT (2026-02-24)
- No API errors observed during CMC data rendering for BTC/BNB/USDT pages (2026-02-24)
