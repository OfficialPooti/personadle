# Personadle

A daily-style guessing game for **Persona 5 Royal**. You get one persona to find and unlimited attempts — every guess is compared against the answer across seven attributes, and the colours tell you how close you are.

Inspired by [Loldle](https://loldle.net/) and [HKDLE](https://kaosi21.github.io/HKDLE/Index.html), built with the real Royal compendium data.

> **[▶ Play it here](#)** — replace this link with your GitHub Pages URL

## How to play

1. Type a persona name — the dropdown filters as you type and shows arcana and level next to each entry.
2. Pick one with the arrow keys and <kbd>Enter</kbd>, or click it.
3. The row reveals cell by cell. Read the colours, guess again, narrow it down.

### Reading the board

| Colour | Meaning |
| --- | --- |
| 🔴 Red | Exact match |
| 🟡 Gold | Partial — shares at least one weakness, or the level is within 8 |
| ⬛ Grey | No match |
| ▲ / ▼ | The answer's level is higher / lower than your guess |

### The seven columns

| Column | What it tells you |
| --- | --- |
| **Persona** | Your guess |
| **Arcana** | Fool through Councillor, including Royal's Faith |
| **Level** | Base level, with a higher/lower arrow |
| **Affinity** | Inheritance type — Fire, Electric, Curse, Ailment, Healing, Almighty… |
| **Weak to** | Elemental weaknesses; partial matches count |
| **Mementos area** | Qimranut, Aiyatsbus, Kaitul, Akzeriyyuth, Sheriruth, Adyeshach, Chemdah, Da'at — or *Not in Mementos* for palace, special and DLC personas |
| **Type** | Standard / Special fusion / Treasure demon / DLC |

### Hints

Hints unlock as your guess count climbs, so they never shortcut an easy round:

- **4 guesses** — reveal the persona's trait
- **8 guesses** — reveal the first letter
- **10 guesses** — give up and show the answer

The **Skip DLC and treasure demons** toggle keeps the pool to the 198 personas you actually fuse during a normal playthrough. Untick it for all 232.

---

## Running it locally

There is no build step and no dependencies. Clone and open the file:

```bash
git clone https://github.com/<your-username>/personadle.git
cd personadle
open personadle-royal.html      # or just double-click it
```

Everything — markup, styles, data and game logic — lives in that single HTML file, so it works from `file://` and deploys to GitHub Pages by pushing it to the repo root.

### Deploying to GitHub Pages

1. Rename the file to `index.html` (or add one that redirects to it).
2. **Settings → Pages → Source: Deploy from a branch**, pick `main` and `/ (root)`.
3. It goes live at `https://<your-username>.github.io/personadle/`.

---

## The data

The `DATA` array at the top of the script holds all 232 Royal personas. Each entry is a flat array:

```js
["Pixie", "Lovers", 2, "Electric", ["Gun","Ice","Curse"], ["Elec","Bless"],
 "Qimranut / Aiyatsbus", "Standard", "Static Electricity"]
```

| Index | Field | Notes |
| --- | --- | --- |
| 0 | Name | |
| 1 | Arcana | |
| 2 | Base level | |
| 3 | Affinity | Inheritance type |
| 4 | Weaknesses | Array, may be empty |
| 5 | Resistances | Includes null / repel / absorb; shown on the reveal card |
| 6 | Mementos area | `"-"` when the persona doesn't appear in Mementos |
| 7 | Type | `Standard` · `Special` · `Treasure` · `DLC` |
| 8 | Trait | Used by the 4-guess hint |

Editing a value or adding a persona is a one-line change — no rebuild needed.

### Where it came from

The stat table was derived from the data files behind [chinhodado/persona5_calculator](https://github.com/chinhodado/persona5_calculator), an excellent Persona 5 / Royal fusion calculator (Apache-2.0). Levels, arcana, inheritance types, resistance tables, Mementos areas and traits are the real in-game values, which is what makes the higher/lower arrows trustworthy.

---

## Tweaking it

| Want to change | Where |
| --- | --- |
| Reveal speed | `const STEP = 190;` above `guess()` — milliseconds between cells |
| Level tolerance for a gold cell | `Math.abs(diff) <= 8` inside `guess()` |
| When hints unlock | `updateCount()` — the `n < 4` / `n < 8` / `n < 10` checks |
| Colours | The CSS variables in `:root` |

The layout respects `prefers-reduced-motion`: with it enabled, rows appear instantly instead of flipping.

---

## Roadmap

- [ ] Daily mode — one shared persona per day, seeded from the date
- [ ] Skill mode — guess the persona from its skill list
- [ ] Stat mode — five bars for St / Ma / En / Ag / Lu, no name
- [ ] Shareable result grid
- [ ] Streak tracking

---

## Credits and disclaimer

Persona, Persona 5 and Persona 5 Royal are trademarks of **ATLUS** / **SEGA**. This is an unofficial fan project, not affiliated with or endorsed by them, and it uses no game assets — only factual stat data. Made for fun.

Data groundwork by [chinhodado](https://github.com/chinhodado/persona5_calculator). Format inspiration from Loldle and HKDLE.

## License

Released under the [MIT License](LICENSE) — the code, not the underlying game data.
