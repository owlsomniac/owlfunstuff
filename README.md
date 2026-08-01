# owlfunstuff

Small self-contained web tools. Everything here is a single static HTML file — no build step, no server.
The root page (`index.html`) is a simple hub linking to each tool.

## Pixel Cat's End — Adventuring Advisor (`pixelcatsend-advisor/`)

Pull a [Pixel Cat's End](https://www.pixelcatsend.com) cat's **attributes** and **personality traits** by ID,
see the **bonuses** each stat grants, and get an **adventuring class** + **day-job** recommendation from the
combined profile. All analysis runs in your browser; nothing leaves the page.

**Live** (once GitHub Pages is enabled): **https://owlsomniac.github.io/owlfunstuff/pixelcatsend-advisor/**

### Using it

Load a cat one of four ways — they all land on an editable sheet, so you can fix anything before analyzing:

1. **My cats (roster)** — two ways to build it:
   - **Fastest — from your profile:** type your **profile ID or link** and hit **Pull my cats**. It reads your
     *public* profile through a relay and grabs every cat it links to (no pasting). Then click a cat to fetch its
     full stats, or **Suggest for shown cats** to do them all.
   - **Most complete — Village Manager:** paste that page's **HTML** once (it's a private, logged-in page, so it
     can't be auto-loaded, and pasting the *address* won't work — you need the page **source**). Grab it with
     **Ctrl+U → Ctrl+A → Ctrl+C** (⌘+⌥+U on Mac), or use the one-click **bookmarklet** in that tab. This is the only
     source for traveling cats and class/job levels. Paste more views (Basic, Adventuring Levels, Day Job Bonuses,
     Appearances, Active/Traveling) and their columns/filters merge into the same roster. (A profile page pasted
     here also works.)

   Either way the roster is a **searchable, filterable** list saved on your device. A **Table** view shows every cat
   with all captured columns plus suggested class/jobs — **click any column header to sort** (numeric-aware, click
   again to reverse) — and **Suggest for shown cats** computes suggestions in bulk.
2. **By cat ID** — paste an ID (e.g. `430432`) or a profile URL, press **Fetch cat**. Routed through public
   CORS relays because the game blocks direct cross-site reads; relays can be flaky, so:
3. **Paste page HTML** — open the profile, view source (Ctrl/Cmd+U), copy all, paste. Always works.
4. **Enter manually** — type the numbers.

Press **Try a demo cat** to see the full output instantly. Attributes read the **effective total** (base +
equipped trinkets) from the cat's stat boxes, and equipped stats show a `base X · +N Item` breakdown.

### What it computes

| Trait | Effect |
|-------|--------|
| **Bravery** | `+min(5, floor(v/2))` to mental-fortitude pools and Spite defense. |
| **Benevolence 8+** | up to **+5 Benevolence** (Befriend / cooperative rolls); unlocks caring day jobs. |
| **Benevolence 0–1** | **+5 Spite** (Intimidate, Bluff, Hiss…); resisted by the target's Bravery. |
| **Energy / Extroversion / Dedication** | Situational *exploration* advantages only — no combat dice bonus. |

Class fit = `0.55 × attribute-fit + 0.45 × personality-fit` across Fighter, Guardian, Thief, Ranger, Medic, Scout, Bard.
Day jobs come from the strongest attributes; high Benevolence/Bravery surface specialty roles (Caregiver, Doctor,
Diplomat/Spite Bard, Adventurous Mayor).

Fan-made; not affiliated with Pixel Cat's End. Bonus rules follow the supplied Adventuring Guide; attribute/job/class
data cross-checked against the community [Not-Wiki](https://pixelcatsend.miraheze.org/wiki/Attributes).

### Breeding predictor (🧬 Breeding tab)

Predict a litter **two ways**:

- **Pick each parent from your cats** by name or `#ID` (autocompletes from your roster). Most cats never reveal their
  genetic string, so the tool **derives a best-effort genotype from their visible traits** — colour, pattern, wind, fur,
  white markings, accent — filling the editable string box and telling you which hidden recessives it had to assume.
  Load cats in **🐈 My cats** first (the **Appearances** manager view carries the richest data).
- **Paste a genetic string** directly (e.g. `[C] [NN] [SS] [BBFF4] [YYTT] [YY0C] [BA] [YR]`; old dash/pipe strings work too)
  when you have one revealed.

Either way you get each kitten's odds for **coat colour** (incl. tortoiseshell / watercolor / snow, with swatches), **wind**,
**fur length**, **pattern** (all 15 named combinations — Mackerel, Rosette, Karpati…), **white markings** (named per level &amp;
type, e.g. *Bib &amp; Boots*), **accent colour** (Ruby, Amber, Teal…), and **species** — plus each parent's decoded phenotype.
The genetics engine follows the Not-Wiki's [Genetics](https://pixelcatsend.miraheze.org/wiki/Genetics) rules (Mendelian
inheritance, recessive dilute/no-white/longhair, number-range colour density &amp; white level, positional colour by wind) with
the pattern/accent/white-marking name tables from Apocracy's community *Cat Genetics 6* spreadsheet, and is unit-tested against
the wiki's own worked Punnett examples. Percentages are exact per kitten; colour swatches approximate the coat (the game
renders the real layered sprite).

## Hosting

GitHub **Settings → Pages → Deploy from a branch → `main` / `/ (root)`**. The hub is then at
`https://owlsomniac.github.io/owlfunstuff/` and the advisor at `…/pixelcatsend-advisor/`.
