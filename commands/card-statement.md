---
description: Record a credit-card statement (PDF, image or pasted text) — balance anchored to the bank, card terms set, fees and interest visible
argument-hint: <card name> then attach or paste the statement(s)
---

Record the credit-card statement(s) the user provides against the Vitafin card: $ARGUMENTS

1. Find the card with `list_accounts` (type `card`); if there is none, `create_account` with
   type `card` and the statement's currency.
2. Read off each statement: the **statement date** (closing date of the period), the **closing
   balance** — printed as "current balance", "closing balance" or "total outstanding" (never
   "minimum due" or "total payment due") — the previous balance, credit limit, payment due
   date ("immediate" if the bank says so), minimum payment due, and the monthly interest rate
   × 12 as `apr_percent` when stated.
3. List every transaction line with a `kind`: `charge` for purchases · `payment` for
   "PAYMENT RECEIVED / THANK YOU" credits · `refund` for merchant credits · `fee` for late,
   over-limit, annual and VAT-on-fee lines · `interest` for finance charges · `instalment`
   for a monthly EMI / IPP line (the billed instalment, not the remaining principal) ·
   `conversion` for a purchase moved onto a plan and shown as a credit. Amounts are always
   positive as printed.
4. Call `record_card_statement` with `commit: false`. Show the closing balance, the lines to
   be added, the adjustment (should be small — a large one means a line was missed or a kind
   is wrong), the arithmetic check and the card terms. If the arithmetic fails, re-read the
   statement before going on.
5. On the user's go-ahead call it again with `commit: true`. Several statements: oldest first,
   one call each; finish with the balance at each statement date and any hints the tool
   returned (over limit, arrears, what to pay by when).
