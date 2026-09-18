---
name: vitafin
description: How to keep a user's money records in Vitafin. Use whenever the user wants to log spending or income, ask what they spent, check balances, net worth, budgets or what is due, reconcile a bank statement, record a credit-card statement, split a bill, or manage accounts, cards, loans, investments and recurring payments through the Vitafin MCP tools.
---

# Working with Vitafin

Vitafin is the user's complete money tracker. The `vitafin` MCP server exposes the same
records the app uses. Follow these conventions so what you record matches what the user
expects to see in the app.

## Ground rules

- **Currencies are exact and never mixed.** Every account has one currency; an amount you
  log is in that account's currency. Never add figures across currencies. Summary tools
  return one block per currency; present them that way. Only `net_worth` restates into one
  currency, and it says which rate and date it used: call that an estimate.
- **Negative is money out.** `log_transaction` takes major units (`-850` is an expense of
  850, `120000` is income). Ask when the direction is unclear.
- **Everything you log lands in the user's review queue.** Say so briefly after logging;
  do not ask the user to confirm every line first.
- **Pick the account before logging.** Call `list_accounts` once per conversation and
  match the user's words ("my ICICI card", "the AED account") to an account id. If it is
  ambiguous, ask.
- **Categories come from `list_categories`.** Prefer a specific sub-category
  (`food.delivery`, `transport.taxi`) over a parent. When you omit `category_id`,
  Vitafin suggests one from the merchant; that is fine for everyday spending.
- **Transfers are not spending.** Moving money between the user's own accounts (paying a
  card bill, funding a broker) is `create_transfer`, never two transactions.
- **Not everything out is spending.** A payment made on someone's behalf, a refundable
  deposit or a reimbursement should be logged with `excluded: true`: the balance moves,
  insights do not count it.
- **Do not give financial advice or predictions.** Vitafin records and reports. If asked
  whether to buy, sell or invest, answer without calling tools and say the app only
  tracks.

## Common tasks

| The user says | Do |
| --- | --- |
| "Log 850 for groceries on the ICICI card" | `list_accounts` → `log_transaction` (amount -850, merchant if given) |
| "What did I spend this month?" | `spending_summary` with the month's `from`/`to`; present per currency, then by category |
| "How am I doing on budgets?" | `budget_status` |
| "What's due soon?" / "next 30 days" | `upcoming` |
| "What's my net worth?" | `net_worth`; quote the base currency, the four lines and the rate date |
| "Here's my bank statement" (pasted or attached) | `reconcile_statement` dry-run first; report matched / missing in app / missing on statement; only `commit` when the user agrees |
| "Here's my credit-card statement" | `record_card_statement` dry-run first (closing balance, due date, minimum, every line with its `kind`); the ledger is anchored to the bank's figure; `commit` on agreement, oldest statement first |
| "Split dinner with Ravi and Priya" | `log_transaction` then `split_transaction`; `people_balances` to report |
| "Ravi paid me back 1,600" | `record_settlement` |
| "Paid the card bill from HDFC" | `create_transfer` |
| "Bought 10 Reliance at 2,850" | `record_lot` (with the cash-side account if the user names one) |
| "Rent is 28,000 on the 3rd every month" | `add_recurring_rule` |
| "Remind me about insurance on the 28th" | `add_reminder` |
| "That was actually 950, not 850" | `correct_transaction` (amount/date) or `update_transaction` (category, merchant, note) |
| "Delete that" | Confirm which row, then `delete_transaction` |

## Reporting style

- Use the formatted amounts the tools return (they carry the right symbol and locale).
- Round nothing. Do not convert. Do not total across currencies.
- After a write, one short line: what was recorded, on which account, and that it is in
  the review queue. No restating of every field.
- When a tool returns an error about the trial or subscription, tell the user to open
  Settings → Plan in the Vitafin app.

## Not available here

Vitafin does not connect to banks or move money. Bank alerts arrive because the user
forwards or imports them. If the user wants a bank linked, say that Vitafin works from
statements and alerts they provide.
