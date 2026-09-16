# Vitafin plugin for Claude

Track all your money by chat. This plugin connects Claude to [Vitafin](https://vitafin.io),
a complete personal money tracker: accounts, cards, loans, investments, budgets, upcoming
bills and the money between you and other people.

## What it adds

- **Connector**: the Vitafin MCP server at `https://vitafin.io/mcp` (61 tools, OAuth sign-in
  with an emailed code, no API keys).
- **Skill** `vitafin`: how Claude keeps your records the way the app expects: exact
  currencies, transfers versus spending, the review queue, what not to do.
- **Commands**: `/vitafin:log`, `/vitafin:spent`, `/vitafin:due`, `/vitafin:networth`,
  `/vitafin:reconcile`.
- **Setup**: guides the first sign-in.

## Install

Claude Code (this repository is also its own marketplace):

```
/plugin marketplace add hakki123mrk/vitafin-plugin
/plugin install vitafin@vitafin
``` The first Vitafin tool call opens the
sign-in page; enter your email and the 6-digit code. A new email creates an account with a
14-day trial; after that Vitafin is one monthly plan priced for your country.

## Privacy Policy

Vitafin stores your financial records on servers operated by Vitafin (AWS, Mumbai). It does
not sell or share your data, does not use it to train models, and does not read your bank
accounts; nothing enters Vitafin unless you enter it, import it, or ask Claude to. Full
policy: https://vitafin.io/support/privacy/ · Terms: https://vitafin.io/support/terms/ ·
Contact: davudul.hakeem@vitafin.io

This plugin contains no code that runs on your machine: only the connector definition,
a skill and command prompts.

## License

MIT
