# RimRunnerNewHampshire

Unofficial New Hampshire HS boys basketball ratings. Not affiliated with the NHIAA or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerNewHampshire/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
88 teams: the NHIAA (New Hampshire Interscholastic Athletic Association) 2026-27 Boys Basketball Divisional Alignment (NHIAA Handbook 2026-27,
By-Law Article XVI Sect. 11): Division I 22, Division II 20, Division III 20, Division IV 26 (new cutoffs for the 2026-28 cycle: I 850+, II 550-849,
III 281-549, IV 1-280; petitioned: Bishop Guertin and Trinity to I; Pelham, Sanborn, St. Thomas Aquinas and Bishop Brady to II; Inter-Lakes to III).
Every listed school has a MaxPreps team. No Other (non-NHIAA) programs met the 8-game rule (no non-NHIAA New Hampshire program on MaxPreps played an NHIAA team in 2025-26).
Conferences: New Hampshire basketball has no conferences or leagues - schools schedule within their NHIAA division and the NHIAA posts standings
by division - so the four divisions are the conferences.

## Season rule
NHIAA 2026-27 Corresponding Dates: first date to play Fri Dec 11, 2026 for Divisions I-III (first practice Nov 30 for I-II, Nov 23 for III) and
Fri Dec 4, 2026 for Division IV (first practice Nov 16). Finals: D-III Feb 27 (Keene State), D-IV Mar 6 (Colby-Sawyer), D-I and D-II Sun Mar 14, 2027 (UNH).
Games involving an NHIAA team before its division's first date to play are left out (schedule build and nightly updater); games between two
non-NHIAA schools are kept. Duplicate next-day listings of one game are removed (shared tournament-repeat rule, tested on both seasons).

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 06:30 and 14:00 UTC (1:30 am / 9:00 am Eastern standard time) and
on manual dispatch. Before `SEASON_START` in index.html (Fri Dec 4, 2026) the script makes no requests. From then on it reads boys basketball
finals for the last 3 days from the MaxPreps New Hampshire scores-by-date page (team-page fallback), matches them to the schedule by MaxPreps team
id + date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo from those finals.
It commits only when data changed; GitHub Pages updates from the commit.
