# Example: Limit Order — Create & Cancel

Paste this prompt to the agent:

---

Test the limit order flow on the Spot trading page.

**Test cases to cover:**
1. Place a limit BUY order for BTC/USD — price $30,000, quantity 0.001 — verify success toast appears and the order shows up in the Open Orders tab
2. Cancel the order from Open Orders — verify the confirmation modal appears, confirm cancellation, verify order disappears from the list
3. Place a limit SELL order for ETH/USD — verify it appears in Open Orders with correct side and values

**Login required:** Yes
**Mocks:** Pre-fill the account balance so there's enough margin to place orders without manual top-up — return `{ "balance": 50000, "currency": "USD" }` on `GET /api/v*/accounts*`
