# TreppenliftVergleich MCP server

Stairlift and home lift data for Germany, from [treppenliftvergleichsportal.de](https://treppenliftvergleichsportal.de), for ChatGPT, Claude and any MCP client. The tools use the same calculators and the same fact register as the website, so every figure comes with its source and the date it was checked. Answers are in German.

- **Website:** [treppenliftvergleichsportal.de](https://treppenliftvergleichsportal.de)
- **Documentation:** [treppenliftvergleichsportal.de/ki-assistenten](https://treppenliftvergleichsportal.de/ki-assistenten)
- **Endpoint:** `https://treppenliftvergleichsportal.de/mcp` (MCP Streamable HTTP, public, no authentication, no API key)
- **MCP Registry:** `de.treppenliftvergleichsportal/treppenlift`

## Tools

| Tool | What it answers |
|---|---|
| `treppenlift_kosten_schaetzen` | Price range including installation for a seat stairlift, standing lift, platform lift, vertical lift, home lift or stair climber, by stair shape and floors, minus the long-term care insurance subsidy (up to 4,180 EUR per eligible person, § 40 (4) SGB XI) |
| `foerderung_finden` | Federal options with current status (care insurance, KfW grant 455-B closed since 01.08.2026, KfW loan 159, § 35a tax reduction), the programme of each of the 16 federal states and known city programmes, plus the order in which to apply |
| `treppe_pruefen` | Whether a stairlift fits a staircase of a given width: rule-of-thumb widths, DIN 18065, the 60 cm remaining width next to a moving lift (MVV TB), how to measure, alternatives |
| `treppenlift_stoerung` | What to check when a stairlift beeps, stops or gets stuck, brand notes (Lifta, Acorn, TK Home Solutions, Handicare, HIRO, Stannah) and documented Acorn T700 codes |
| `reparieren_oder_ersetzen` | Whether a repair quote is still worth it, by the age of the lift and the new price |
| `treppenlift_fakten` | Sourced facts by topic: prices, price index, subsidies, KfW, tax, running costs, stair width rules, home lift prices and building code, tests |

All tools are read-only and stateless. The server asks for no personal data, stores nothing it receives, recommends no providers and contains no affiliate links.

## Connect

Any MCP client that supports remote servers:

```json
{
  "mcpServers": {
    "treppenlift": {
      "type": "streamable-http",
      "url": "https://treppenliftvergleichsportal.de/mcp?src=mcp"
    }
  }
}
```

Claude Code:

```bash
claude mcp add --transport http treppenlift https://treppenliftvergleichsportal.de/mcp
```

Quick test:

```bash
curl -s -X POST 'https://treppenliftvergleichsportal.de/mcp?src=mcp' -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

## Deutsch

Treppenlift-Kosten, Förderung je Bundesland, Treppenbreite, Störungshilfe und Reparatur-Rechner von TreppenliftVergleich im KI-Assistenten. Beschreibung, Datenschutz und Nutzungsbedingungen: [treppenliftvergleichsportal.de/ki-assistenten](https://treppenliftvergleichsportal.de/ki-assistenten).

This repository holds the listing metadata only. The server itself is a hosted service run by the TreppenliftVergleich website; see the documentation link above for privacy ([Datenschutz 6a](https://treppenliftvergleichsportal.de/datenschutz#ki-assistenten)) and [terms](https://treppenliftvergleichsportal.de/nutzungsbedingungen).
