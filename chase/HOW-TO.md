# Chase cards - how to add a new break's set

1. Put card images in `chase/img/<slug>/` (jpg/png, portrait card shape ~731x1024 is ideal).
   `<slug>` = short lowercase name, e.g. `2026-bowman-chrome`.
2. Create `chase/<slug>.json`:
```json
{
  "name": "2026 Bowman Chrome",
  "league": "mlb",
  "entries": [
    {"team":"LAD","player":"Player Name","card":"Superfractor /1","format":"hobby","img":"img/2026-bowman-chrome/lad-player.jpg"}
  ]
}
```
   - `team` = the board abbreviation (LAD, NYY, KC, WSH, ... same as the tile).
   - `format` = `hobby`, `retail`, or `both` (shows HOBBY / RETAIL / HOBBY + RETAIL tag).
   - `img` is relative to the `chase/` folder.
   - Only list real chase cards. Don't add pack odds.
   - `"sample": true` adds an EXAMPLE badge - leave it out for real sets.
3. Add the set to `chase/index.json` so it shows in the control-bar dropdown:
   `{"slug":"2026-bowman-chrome","name":"2026 Bowman Chrome","league":"mlb"}`
4. Commit + push. GitHub Pages updates in ~1-10 min.
5. On the board control bar: pick the set in the **Chase set** dropdown (saved per league), and make sure **Chase: ON**.
   Or use the URL: `team-board.html?league=mlb&chase=2026-bowman-chrome`

## Which cards show
- Only teams that are still OPEN cycle; a team drops out the moment it sells.
- Format comes from the **Opening** text: hobby/jumbo/breaker/case -> HOBBY cards; retail/blaster/mega/hanger/value -> RETAIL cards; anything else -> all.
  `both` cards always match. Override with the **Format** dropdown (Auto / Hobby / Retail / All).
- Hidden when the board is FILLED, chase is OFF, or no set is selected.

## Extra tiles (college spots)
- A set can add extra tiles with `"extra":"college"` (NFL only): adds a COLLEGE group with SEC, BIG10, BIG12, ACC, OTHER.
  They appear while that set is selected; normal 32-team NFL is unchanged otherwise.
- URL override: `&extra=college` forces them on, `&extra=none` forces them off (saved per league).
- An entry without `img` shows a styled text card (player + card name) instead of a picture.
- `"label"` (optional) = short set name printed on text cards, e.g. "2026 Topps Update" (falls back to `name`).

## Team Chase Sheet (optional `"sheet"` key)

On the team board, **long-press a team tile** (or turn on **Chase View** in the control bar, then click a tile) to open that team's full chase sheet: ROOKIES / STARS / LEGENDS. Close with ✕, Esc, or a click outside. It closes by itself when a reveal fires. Normal click and right-click selling are unchanged while Chase View is OFF.

Add a top-level `"sheet"` object to the set JSON, keyed by team abbreviation:

```json
"sheet": {
  "LAA": [
    {"id":"laa-1","tier":"rookie","player":"Walbert Ureña","card":"1952 Rookie Image Variation Auto (US16) · /10 · Black w/ Gold Ink 1/1","format":"both"},
    {"id":"laa-5","tier":"star","player":"Mike Trout","card":"Flagship Auto Patch (TFAPU-MT) · /50 · Platinum 1/1","format":"hobby","img":"img/2026-topps-update/trout.jpg"}
  ]
}
```

- `tier`: `rookie` | `star` | `legend`
- `format`: `hobby` | `retail` | `both` (shown as HOBBY / RETAIL / HOBBY + RETAIL)
- `img`: optional, relative to `chase/`. Without it, a text card is drawn.
- Cards from the same player go next to each other. Aim for 4–10 per team.
- If a team has no `sheet` entry, the sheet falls back to that team's `entries` (grouped by `tier` when present).
- `sheet` does not affect `entries` or the peek card.
