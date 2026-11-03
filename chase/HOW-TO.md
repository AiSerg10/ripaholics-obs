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
