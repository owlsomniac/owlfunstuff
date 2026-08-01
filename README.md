# owlfunstuff

Small self-contained web tools. Everything here is a single static HTML file — no build step, no server.
The root page (`index.html`) is a simple hub linking to each tool.

## Pixel Cat's End — Adventuring Advisor (`pixelcatsend-advisor/`)

Pull a [Pixel Cat's End](https://www.pixelcatsend.com) cat's **attributes** and **personality traits** by ID,
see the **bonuses** each stat grants, and get an **adventuring class** + **day-job** recommendation from the
combined profile. All analysis runs in your browser; nothing leaves the page.

**Live** (once GitHub Pages is enabled): **https://owlsomniac.github.io/owlfunstuff/pixelcatsend-advisor/**

### Using it

Everything lives on two tabs — **🐈 My cats** and **🧬 Breeding**. The tool opens on **My cats**, which has three
collapsible rows (open one at a time):

1. **🪄 Pull My Whole Roster** — paste your **User Profile ID** (or any link that contains it) and hit **Pull my
   cats**. It crawls every Cats-page tab (Adventurers, Trainees, … + Traveling) for each cat's name, colour, pattern,
   white, genetics and real portrait, **then opens each cat's page** to add its **7 attributes (base / trinket /
   total), equipped trinkets, current day job & adventuring class, every day-job level and all 7 class levels**. All
   from public pages. A small **↻ Fetch stats & levels** button appears only if some cats still need it (a relay
   hiccup) and hides itself once they're done.
2. **🔎 Single Cat Look-Up** — paste one cat's **ID** or **page link** and press **Fetch cat** (or **Try a demo
   cat**). Routed through public CORS relays because the game blocks direct cross-site reads.
3. **✏️ Enter Manually** — start a blank sheet and type any values you know.

Single-cat lookups land on an editable **Review & edit** sheet (with a real cropped portrait), so you can fix any
mis-parse before **Analyze**. Attributes read the **effective total** (base + equipped trinkets); equipped stats show
a `base X · +N Item` breakdown.

The roster itself is one **searchable, filterable, sortable table** (zebra-striped, with full-size portraits).
**Preview, Name and ID stay on the left** (Name links to the cat's own page); every other column is grouped under a
**collapsible header** — click a group (*Basic info · Appearance · Jobs · Adventure Classes · Personality · Stats*)
to fold it away to the left. Groups are separated by clear **3px dividers** so they never run together when expanded.
A collapsible **Quick View** column gives the at-a-glance summary (appearance, current job & class, recommended
job/class). **Click any column sub-header to sort.** Highlights:

- **Appearance** — a single **White** column (e.g. *Classic, C7, Spotted Piebald*, or *None*), a **Density** column
  (the coat's colour density / dilution level, **1–4**, recovered from its colour) and an **Accent** column (the game
  shows accent only when it's visible, so cats without a revealed accent read **Unknown**).
- **Stats** — each total is tinted by its game **grade** (ROYGBP pastels: Poor · Average · Good · Very Good ·
  Excellent · Exceptional) and shows its **dice pool** (1d6–9d6). A trinket-adjusted stat **splits** the cell — the
  adjusted total on top, the base value below — and sorts by the (higher) adjusted number.
- **Jobs** — **Suggested jobs** leads the group, then one column per day job (alphabetized) reading **`Lv. N (+M)`**:
  its level plus its governing attribute's modifier.
- **Adventure Classes** — **Suggested class** leads (its class name over a sortable **Fit %**), then one column per
  class (Fighter … Bard) reading **`Lv: N`** / **`Fit: X%`** (level defaults to 1 when the page doesn't list it;
  Fit % is how well the cat matches that class's ideal, `0.55 × attributes + 0.45 × personality`, computed from the
  cat's stats). Each of these headers has separate sort buttons for its two values.

**Suggest for shown cats** computes recommendations in bulk.

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
  genetic string, so the tool **derives the genotype from what the game displays** — for cats pulled from your Cats page
  that means reading the rendered avatar's description (main + trade colours, pattern, white level & type, fur, species),
  which pins the coat genetics down accurately; it fills the editable string box and notes any hidden recessives it had
  to assume. Parents picked from the roster show their **real in-game portrait**.
- **Paste a genetic string** directly (e.g. `[C] [NN] [SS] [BBFF4] [YYTT] [YY0C] [BA] [YR]`; old dash/pipe strings work too)
  when you have one revealed.

Or work backwards with **🔎 Find a pairing for a desired kitten**: choose the traits you want — coat type/colour, pattern,
wind, fur, **white type & level (min/max)**, **colour density (min/max)**, species, accent — and it searches every pair of
your cats with known genetics for ones that could produce it, ranked by the chance per kitten (incompatible-wind pairs are
excluded). Offspring stats aren't genetically determined, so the two stat fields instead constrain the **parents** (only pair
cats whose total attributes / personality meet a minimum). Click a result to load that pair into the predictor.

Either way you get each kitten's odds for **coat colour** (standard / watercolor / tortoiseshell / snow, with swatches),
**colour density** (1–4, the dilution level), **wind**, **fur length**, **pattern** (all 15 named combinations — Mackerel,
Rosette, Karpati…), **white markings** (named per level &amp; type, e.g. *Bib &amp; Boots*), **accent colour** (Ruby, Amber,
Teal…), and **species**. Under every outcome the possible **allele pairs** are listed (e.g. accent `[RR]` × `[LL]` →
*Pink* `[RL] / [LR]`); colour alleles honour each parent's **wind** (which slot each donates), and traits that aren't a
two-allele cross (species, white type & level, density) show a short inheritance note instead. A pattern only names its
type when it's actually shown (a solid cat reads **Solid**, never a leaked hidden type), and an **unknown accent stays
unknown** rather than defaulting to Ruby. Plus each parent's decoded phenotype (shown as **labelled facts** — Coat /
Pattern / Wind / Fur / White / Accent / Species — with its name/#ID linking to the cat's page when picked from your roster). Parents and **every** possible kitten get **composited sprite previews** built from the
game's own image layers, each **cropped to a single pose** (correct per-species offsets for Not-cats and Mercats) — pick
**standing / sitting / playing / sleeping / upsidedown** from the pose selector. Above the kitten gallery a row of three
**dropdowns — Wind · Pattern · White** — each lists **only outcomes this pairing can actually produce**; picking any of them
narrows the previews and rewrites every kitten's % to the **true overall chance** of a kitten with that coat *and* the chosen
wind/pattern/white (independent loci multiply in, and a wind pick isolates the exact coat-and-wind pair). Each kitten also
carries a **click-to-copy full genetic string** (small, wrapping button) that marks every allele the game keeps hidden with a
single **`?`**: a shown-dominant trait reads `[D?]` (the second copy could be a hidden recessive), a shown-recessive trait
reads `[rr]` (both copies known), and a fully-hidden gene (a North/South cat's off-wind colour slot, an unrevealed accent)
reads `[??]` — never a guessed value. A collapsible **🧬 Quick Genetics Overview** on the tab explains the homozygous
assumption for un-revealed cats, the `?` convention, and how gene pairs pass down (`[rr] × [rr]` → `[rr]`; `[D?] × [DD]` →
`[DD]`/`[D?]`; `[D?] × [D?]` → `[DD]`/`[D?]`/`[??]`), with the reminder that outcomes are a close approximation. A missing
layer falls back to a colour swatch. (Accent is only ever asserted when actually revealed — a cat's roster data is the
authority, so a stale cached string can never make one up.)
The genetics engine follows the Not-Wiki's [Genetics](https://pixelcatsend.miraheze.org/wiki/Genetics) rules (Mendelian
inheritance, recessive dilute/no-white/longhair, number-range colour density &amp; white level, positional colour by wind) with
the pattern/accent/white-marking name tables from Apocracy's community *Cat Genetics 6* spreadsheet, and is unit-tested against
the wiki's own worked Punnett examples. Percentages are exact per kitten; colour swatches approximate the coat (the game
renders the real layered sprite).

## Hosting

GitHub **Settings → Pages → Deploy from a branch → `main` / `/ (root)`**. The hub is then at
`https://owlsomniac.github.io/owlfunstuff/` and the advisor at `…/pixelcatsend-advisor/`.
