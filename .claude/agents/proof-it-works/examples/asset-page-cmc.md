# Example: Asset Page — CoinMarketCap Sections

Paste this prompt to the agent:

---

Test the asset detail page for BTC. The page should show several dynamic sections pulled from CoinMarketCap: an overview/about section describing the coin, a Technology section, a Team section (if available), and links to the project's website and social media accounts.

All data is dynamic — verify that these sections actually render with real content and aren't empty or broken. Also check that switching to a different coin (e.g. ETH) updates the sections correctly.

**Test cases to cover:**
1. Open the BTC asset page — all CMC sections render with content (overview, technology, links)
2. Open the ETH asset page — sections update and show ETH-specific data
3. Check a coin that may have minimal CMC data (e.g. a smaller altcoin) — verify graceful fallback, no broken layout

**Login required:** No
**Mocks:** None
