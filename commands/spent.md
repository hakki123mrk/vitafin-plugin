---
description: Spending summary for a period, per currency and by category
argument-hint: [this month | last month | YYYY-MM | from..to]
---

Summarise the user's spending in Vitafin for: ${ARGUMENTS:-this month}

Use `spending_summary` with the right `from` (inclusive) and `to` (exclusive) ISO dates.
Present one block per currency: spent, received, then the top categories with amounts and
share. Mention budgets only if `budget_status` shows one over 80%.
