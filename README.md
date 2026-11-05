# Personal projects

Shaun Finch's side projects, moved out of the design portfolio (`Shaun-Finch/Design`) in November 2026. Both are works in progress.

Live at **https://shaun-finch.github.io/personal-projects/** once GitHub Pages is switched on (Settings → Pages → Deploy from a branch → `main`, `/ (root)`).

```
index.html                 Landing page for the two projects
ventryx.html               Ventryx: opening-bell breakouts, long-term ideas, backtests, crypto, Polymarket, free books, weekly news video
xovern.html                Xovern: AI security dashboard (sanctions screening, prompt-injection firewall, code checks)
data/sanctions.json        Sanctions data for Xovern, refreshed daily
scripts/                   Data builders, backtests, paper-trading bot and the Nova news video
.github/workflows/         Scheduled jobs (see below)
og/                        Link-preview images
```

## Secrets and settings to add (Settings → Secrets and variables → Actions)

Secrets don't move with the code, so these need adding again here:

- `ALPACA_KEY_ID` and `ALPACA_SECRET_KEY`: Alpaca **paper** trading keys for the bot. Without them the bot simply doesn't trade.
- `ANTHROPIC_API_KEY`: for the weekly news video script and the bot's optional news check.
- Optional repository variables, only if you set them before: `ALPACA_LIVE` (live trading switch; leave unset for paper) and `BOT_PAUSED`.

## Scheduled jobs

- `markets-data.yml`: every 15 minutes in US market hours, plus after the close. Writes `markets.json`, `fundamentals.json`, `bot.json` and `orb_history.json` to the `market-data` branch, which `ventryx.html` reads.
- `weekly-news.yml`: Sundays at 08:07 UTC. Renders the Nova weekly video to the `news-video` branch.
- `sanctions-data.yml`: daily at 06:17 UTC. Refreshes `data/sanctions.json` from the UK Sanctions List (FCDO) and the OFAC SDN list.
- `check-book-links.yml`: Mondays. Checks every free books link on `ventryx.html` still opens.
- `backtest.yml` and `avatar-probe.yml`: run by hand from the Actions tab. Backtests go to the `research-data` branch.

Data and articles come from Yahoo Finance via yfinance and may be delayed. Ventryx shows ideas only, never financial advice.
