# Changelog

## 1.2.0

`/vitafin:setup` walks a new user through accounts, statements, cards, loans, people and
recurring bills one question at a time. Skill rules added: fees, fines and interest are
recorded as fees, never inside a payment; keep Uncategorized small with `learn_category`;
use the mailbox when a mail connector is available; `chart` for pictures.

## 1.1.0

`/vitafin:card-statement`: read a credit-card statement and record it with
`record_card_statement` — the closing balance anchors the ledger, card terms come off the
statement, and each line carries a kind (charge, payment, fee, interest, instalment…) so fees
and interest show in spending while instalments and payments do not.

## 1.0.0

First release: Vitafin connector, the `vitafin` skill, setup guide, and the log / spent /
due / networth / reconcile commands.
