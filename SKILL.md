# SKILL: TRAC Time Machine

**Version:** 1.0  
**App:** TRAC Time Machine  
**Fork of:** https://github.com/Trac-Systems/intercom

---

## Overview

This skill enables Intercom agents to perform **historical wallet analytics** on the TRAC Network. Agents can look up past wallet balances, compute growth metrics, and deliver formatted time-comparison reports.

---

## Trigger Phrases

The agent activates this skill when it detects phrases like:

- `"Show my wallet [N months/weeks/days] ago"`
- `"What was my balance in [month/year]?"`
- `"How much did my [TOKEN] grow?"`
- `"TRAC time machine"`
- `"Historical balance for [address]"`
- `"Compare my wallet now vs [period]"`

---

## Input Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `wallet` | string | ✅ | TRAC-compatible wallet address |
| `token` | string | ✅ | Token ticker (TRAC, TNK, PIPE, POLS, etc.) |
| `period` | string | ✅ | Time period: "1m", "3m", "6m", "1y", "2y" |
| `format` | string | ❌ | Output format: "summary" (default), "full", "share" |

---

## Agent Instructions

### Step 1 — Parse the Request

Extract wallet address, token, and time period from natural language:

```
User: "Show my wallet 6 months ago"
→ period = "6m"
→ token = (default to TRAC or last used token)
→ wallet = (from session context or ask user)
```

### Step 2 — Fetch Historical Data

Via Intercom sideChannel, query TRAC ledger for:

```json
{
  "action": "wallet_history",
  "wallet": "<address>",
  "token": "<TOKEN>",
  "from_block": "<block_at_past_date>",
  "to_block": "<current_block>"
}
```

Fields to retrieve:
- `balance_at_start` — balance at the beginning of the period
- `balance_now` — current balance
- `peak_balance` — highest balance in window
- `low_balance` — lowest balance in window
- `tx_count` — number of transactions
- `tx_list` — array of transaction objects (type, date, amount)

### Step 3 — Compute Metrics

```
diff = balance_now - balance_at_start
growth_pct = (diff / balance_at_start) * 100
avg_monthly = diff / months_in_period
```

### Step 4 — Format Response

**Default (summary) format:**
```
⏳ TRAC Time Machine — [WALLET_SHORT]

📅 [PAST_DATE]:  [PAST_BALANCE] [TOKEN]
📅 Now:          [NOW_BALANCE] [TOKEN]
📈 Growth:       [+/-][PCT]%

💎 Peak:   [PEAK] [TOKEN]
📉 Low:    [LOW] [TOKEN]
🔄 Txs:    [TX_COUNT]
📊 Avg/Mo: [AVG_MONTHLY] [TOKEN]

[NARRATIVE_SENTENCE]
```

**Full format:** Include full transaction list in addition to above.

**Share format:** One-liner for social sharing:
```
6 months ago: 1,200 TNK → Now: 2,050 TNK (+70.8%) via TRAC Time Machine ⏳
```

---

## Example Conversations

**User:** `Show my wallet 6 months ago`  
**Agent:**
```
⏳ TRAC Time Machine

📅 Aug 20, 2025:  1,200 TNK
📅 Feb 20, 2026:  2,050 TNK
📈 Growth:        +70.8% (+850 TNK)

💎 Peak:   2,340 TNK
📉 Low:    1,100 TNK
🔄 Txs:    31
📊 Avg/Mo: +141.6 TNK/month

Strong accumulation pattern over this window. 
```

**User:** `Compare my TRAC over the last year`  
**Agent:** *(fetches 12-month window and returns same format)*

---

## Error Handling

| Error | Response |
|---|---|
| Invalid wallet | "⚠ Wallet address not recognized on TRAC Network." |
| No history found | "⚠ No transaction history found for this address in this period." |
| Period too far back | "⚠ Requested period exceeds available historical data (max 2 years)." |
| Network timeout | "⚠ Time jump failed. TRAC Network unreachable. Retry in a moment." |

---

## Notes for Agents

- Always shorten wallet addresses in output: `bc1p...xyz` (first 4 + last 3 chars)
- Default token is TRAC if user doesn't specify
- If wallet has zero history, prompt user to double-check address
- The app UI at `index.html` can be used for visual rendering of results

---

## Related Skills

- `wallet_balance` — current balance only (no history)
- `token_swap` — IntercomSwap trading skill
- `p2p_timestamp` — TracStamp certification skill
