# McdSaving Expert (麦麦省钱官)

> An AI money-saving assistant built on McDonald's China **official MCP** — upgrading from *"teach you how to judge a good price"* to *"compute the real cost for you with live official data"*.

🇨🇳 **中文说明请见 [README.md](README.md)**

---

## Introduction

Anyone who orders takeout shares the same confusion: **"Is this actually expensive? Am I wasting money again?"**

Most money-saving assistants give you **advice** — "compare prices", "grab a coupon first", "pick up in store". But advice isn't a bill. What you really want to know is: **for this exact order, right now, what do I pay and how much do I save.**

Hand-searched "deals" are really just **experience ranges** — they expire, contradict each other, and sometimes mislead. The only authoritative answers — *this store's current prices, how many coupons you actually own, the real total of this order* — come from one place: the official data source.

## What It Does

Three jobs, done in one pass:

1. **Claim coupons** — grab every currently available coupon in one shot, then tell you how many you actually hold
2. **Compute the real bill** — item price, discounts, delivery fee, final total, all itemized
3. **Decide** — pickup vs. delivery, combo vs. single, using real prices and real nutrition data

### One-line pitch

**Other assistants give you "advice". McdSaving gives you "the finished bill".**
Because every price, coupon and order comes from McDonald's official MCP live data — never guessed.

---

## Installation

### Prerequisites

- WorkBuddy client
- A McDonald's China MCP Token ([free to apply](https://open.mcd.cn/mcp))

### Steps

**1. Configure the MCP connector**

In WorkBuddy: 【Experts · Skills · Connectors】→【Connectors】→ top-right【Custom Connector】→【Configure MCP】, then paste:

```json
{
  "mcpServers": {
    "mcd-mcp": {
      "type": "streamablehttp",
      "url": "https://mcp.mcd.cn",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_TOKEN"
      }
    }
  }
}
```

⚠️ Replace `YOUR_MCP_TOKEN` with your real token, then click **Save**.

**2. Enable the connector**

Back in【Custom Connector】, set `mcd-mcp` to **Enabled**.

**3. Install the Skill**

Put this repo's `SKILL.md` and `references/` folder into your Skill directory, or simply reference this repo inside the conversation.

---

## Usage Examples

### Example 1 — What coupons can I claim today?

> **You**: What coupons can I claim right now?
>
> **Assistant**: Let me claim everything available first — `available-coupons` to list claimable coupons → `auto-bind-coupons` to claim them all → `query-my-coupons` to verify what you actually hold
>
> **Result**: Claimed 4 coupons; 7 usable coupons in your wallet now. Most recent:
> - Big Mac combo −8 CNY (on orders over 45 CNY)
> - McChicken single −5 CNY
> - Afternoon-tea coupon (14:00–17:00)
> - Free delivery coupon × 2
>
> Note: 2 free-delivery coupons expire in 3 days — use them this week.

### Example 2 — What does this order actually cost?

> **You**: Is there a McDonald's nearby? How much is a Big Mac combo?
>
> **Assistant**: `query-nearby-stores` → `query-meals` → `query-meal-detail` → `calculate-price` for the real payable amount
>
> **Result**: **Qiongshan Fengxiang East Rd store**, 1.2 km away, open now.
> Big Mac Value Combo (Big Mac + medium fries + cola):
> - List price: 45.0 CNY
> - Coupon: −8 CNY
> - Delivery fee: 3.0 CNY
> - **Payable: 40.0 CNY**
>
> Tip: pickup saves the 3 CNY delivery fee → about **37.0 CNY**.

### Example 3 — Pickup or delivery?

> **You**: Which is cheaper, pickup or delivery?
>
> **Assistant**: Compute both scenarios — `create-order` (pickup) vs. McDelivery — then compare
>
> **Result**:
> | Mode | Food | Discount | Delivery | Payable |
> |---|---|---|---|---|
> | Pickup | 45.0 | −8 | 0 | **37.0 CNY** |
> | McDelivery | 45.0 | −8 | 3.0 | **40.0 CNY** |
>
> **Verdict**: Pickup saves 3 CNY, and the store is only 1.2 km away.

### Example 4 — Ordering while cutting calories

> **You**: Can I eat McDonald's while losing fat? Build me a 500-kcal order.
>
> **Assistant**: `list-nutrition-foods` for real nutrition data → compose a combo and total the calories
>
> **Result**:
> - Big Mac alone: ~520 kcal → too high; switch to McChicken (~500 kcal) or grilled chicken
> - Medium corn cup: ~80 kcal, high fiber, good carb alternative
> - Skip sugary drinks; go with diet cola
>
> ⚠️ Not medical or nutritional advice. Follow your doctor's guidance for special dietary needs.

---

## Target Users

| Who | Typical scenario | Typical saving |
|---|---|---|
| Office workers | 3–5 orders/week, peak-hour delivery fees | 5–15 CNY/order |
| Budget students | Tight budget, torn between pickup and delivery | 3–8 CNY/order |
| Fitness-focused | Wants McDonald's without blowing the calorie budget | Peace of mind + calorie control |
| Coupon hoarders | No idea how many coupons are quietly expiring | Zero waste |

---

## Project Structure

```
mcd-saving-expert/
├── SKILL.md                      # Skill entry point
├── README.md                     # Chinese README (primary)
├── README_EN.md                  # This file (English)
├── CONTEST_DECLARATION.md        # Contest declaration (official original)
├── MCP_INTEGRATION.md            # MCP tool mapping and call flows
├── mcp-config.example.json       # Sanitized config sample
├── workbuddy.md                  # WorkBuddy development context
├── docs/
│   └── mcp-proof.jpg             # Screenshot of a real MCP call
└── references/
    ├── 省钱方法论总纲.md          # Core decision framework (zh)
    ├── 券叠加与失效预警.md        # Correct coupon stacking order (zh)
    ├── 自提与外送决策.md          # Pickup saving logic (zh)
    ├── 凑单陷阱识别.md            # Fake-markup & add-on traps (zh)
    └── 营养搭配参考.md            # Real nutrition data combos (zh)
```

> Reference docs are in Chinese; the Skill itself is designed for Chinese-language users.

---

## Design Principles

1. **Official data first** — prices, coupons and nutrition always come from the McDonald's MCP, never guessed or invented
2. **Say so when unsure** — failed lookups are reported honestly; no fake numbers
3. **Freshness matters** — coupons and prices change constantly; cached results always carry their query timestamp
4. **Stay in bounds** — not medical/nutritional advice; the purchase decision stays with the user

---

## Proof of Real MCP Usage

This project has **really called McDonald's official MCP** — a live "nearby stores + available coupons" query. Screenshot: [docs/mcp-proof.jpg](docs/mcp-proof.jpg) (5 stores near Qiongshan District, Haikou, plus claimable coupons, returned live by `mcd-mcp` — not fabricated). Submitted as the contest's "real usage" evidence.

---

## Acknowledgments

- McDonald's China for opening the MCP capability
- WorkBuddy for the development and runtime platform
