# Alpenglow bounty scope watcher

Polls `anza-xyz/agave` master every 30 minutes for new commits touching the
Alpenglow bug-bounty in-scope surface (per `RULES.md` section 3 on
`anza-xyz/alpenglow`), and pings a Telegram bot when it finds one. Scope is a
moving window on master during the submission window, so a fix landing on a
bug you're about to report costs you the race — this is early warning.

State (last-checked timestamp + seen commit SHAs) lives in `state/` and is
committed back by the workflow itself, so restarts don't replay history.

## Setup

Add two repository secrets (Settings → Secrets and variables → Actions →
New repository secret):

- `TELEGRAM_BOT_TOKEN` — from [@BotFather](https://t.me/BotFather)
- `TELEGRAM_CHAT_ID` — the chat/user ID the bot should message

No other config needed. `GITHUB_TOKEN` (auto-provided by Actions) is used to
call the GitHub API and to push the state file back to this repo.

## Manual run

Actions tab → "Alpenglow bounty scope watcher" → Run workflow. First run
only seeds state (no notification) so it doesn't replay old history.

## Scope surface

Regex lives in `.github/workflows/watch.yml`, mirrored from
`docs/scope.md`/`RULES.md` in the audit workspace. Re-sync if scope changes.
