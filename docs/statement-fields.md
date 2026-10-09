# Statement Fields Checklist

Practical checklist for product and engineering teams designing **digital wallet statement history** and exports.

## 1. Minimum fields per line

| Field | Required | Notes |
|-------|----------|-------|
| `transaction_id` | Yes | Unique, stable, shareable with support |
| `posted_at` | Yes | UTC stored; local display labelled |
| `type` | Yes | e.g. CASH_IN, P2P, MERCHANT, FEE, REVERSAL |
| `amount` | Yes | Minor units or decimal with currency code |
| `currency` | Yes | ISO code |
| `direction` | Yes | DEBIT / CREDIT (or signed amount) |
| `status` | Yes | COMPLETED, FAILED, PENDING, REVERSED |
| `balance_after` | Optional | Useful for customers; confirm auditor expectation |
| `counterparty_label` | Recommended | Masked MSISDN, merchant name, or "Bank transfer" |
| `channel` | Recommended | App, USSD, agent, API |
| `external_ref` | When available | Bank, switch, or partner reference |
| `parent_transaction_id` | For reversals | Links correction to original |

## 2. Customer UI filters worth shipping early

- [ ] Date range (presets: 7 / 30 / 90 days)
- [ ] Type (payments, transfers, cash-in/out, fees)
- [ ] Status (completed / failed / pending)
- [ ] Search by amount or transaction ID
- [ ] Clear empty states when no matches

## 3. Export checklist

- [ ] Same columns in CSV as summarised in the UI help text
- [ ] UTF-8 with BOM if Excel users are common
- [ ] Filename includes wallet/account id fragment and date range
- [ ] Signed, time-limited download URL
- [ ] Audit log: who exported, when, which range
- [ ] Cap row count or stream large exports asynchronously

## 4. Dispute support hooks

- Surface "Report a problem" on a line only when status and age allow it
- Pass `transaction_id` into the case system automatically
- Freeze related evidence (receipt, device, channel) for the retention window of the case

## Related

See the main [README](../README.md). Product context: [wallet cash-in, cash-out, transfers and reversals](https://evdsystem.com/evd-software/wallet-cash-in-out-transfers-and-reversals/).
