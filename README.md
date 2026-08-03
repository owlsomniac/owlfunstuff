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
   hiccup) and hides itself once they're done. **Re-pulling is non-destructive to your genetics work.** A cat's genes
   never change in-game, but the game's own genetic string shows `?` for alleles it hasn't revealed — the very hidden
   recessives and tested accents you discover in the breeding sandbox and record by hand. So a pull **only ever *adds*
   resolution**: it accepts a freshly-pulled string when that string agrees with every concrete allele you already have
   and merely fills in some `?`s; if it would blank out or disagree with an allele you know, your value is kept. Hours
   of test-crossing survive every re-pull; new cats and newly game-revealed alleles still flow in.
2. **🔎 Single Cat Look-Up** — paste one cat's **ID** or **page link** and press **Add cat** to drop them straight
   into your roster. Routed through public CORS relays because the game blocks direct cross-site reads.
3. **✏️ Enter Manually** — **Add a blank cat**, which opens the ✏️ editor so you can type in whatever you know.

Every cat lives in the roster, and **all editing happens in one place — the ✏️ pencil editor** (see *Edit any cat*
below). There's no longer a separate stat sheet at the bottom of the page, and clicking a roster row doesn't jump you
anywhere — use the row's pencil.

The roster itself is one **searchable, filterable, sortable table** (zebra-striped, with full-size portraits).
**Preview, Name and ID stay on the left** (Name links to the cat's own page); every other column is grouped under a
**collapsible header** — click a group (*Basic info · Appearance · Jobs · Adventure Classes · Personality · Stats*)
to fold it away to the left. Groups are separated by clear **3px dividers**, and every column has a **1px vertical
rule** so the data reads as a clean grid; cell padding is tight so more columns fit without scrolling. The table
**sizes itself to the viewport** — its scroll region fills the space down to the bottom of the screen, with the header
row pinned, so you see the top and bottom at once without zooming out (many rows scroll *inside* the table, not the page).
A wider, collapsible **Quick View** column gives the at-a-glance summary (appearance, current job & class, a **Best Stats**
line with the cat's top three base stats abbreviated — *Str (20), Agi (18), Luck (17)* — with the base-stat total on a
**BST** line beneath it, recommended job/class, and the cat's genetics as **one click-copy block** — the whole
**Genes + Carries** section copies together:
you get the genetic string (ready to paste into Breeding) with a `Carries: …` line appended when there is one. Below the
string, a **Carries:** line lists the alleles a cat is hiding — *Longhair* (`[SL]`),
*Dilute* (`[FD]`), *Solid* (a patterned cat carrying solid, `[YN]`), *No-white* (`[YN]`), *Null (wind)* (`[NO]`/`[SO]`),
and — for **North/South** cats — the **base colour** it doesn't show. Base colour is co-dominant *and positional*: North
shows allele 1, South allele 2, so a het (`BO`/`OB`) hides and passes on the other pigment. The line reads the wind, then
names the carried colour — e.g. a **North `BO`** shows Black but *carries Red*; a **South `BO`** shows Red but
*carries Black*. (A **Trade** het shows both as a tortoiseshell, so it carries neither.) It only reports what's genuinely
known: an unrevealed allele reads `?`, so a cat with `[S?]` fur makes no claim about carrying longhair. The **ID** cell is a one-click copy too — tap it to grab the cat's numeric ID. **Click any column sub-header to
sort.** Highlights:

- **Appearance** — the coat is split into a **Color** column (just the shade — *Charcoal-Buff*, *Chocolate-Brown*,
  *Beige*) and its own **Color Type** column (*Standard · Watercolor · Tortoiseshell*), so you can sort or scan by type
  without the word cluttering every colour. Then a **White** column (e.g. *Classic, C7, Spotted Piebald*, or *None*), a
  **Density** column (the coat's colour density / dilution level, **1–4**, recovered from its colour) and an **Accent**
  column (the game shows accent only when it's visible, so cats without a revealed accent read **Unknown**). The White label respects the
  visibility gene, so a white that's **carried but not shown** (`[NN5C]`) reads *Hidden, Classic, C5, …* and one that
  **expresses white at level 0** (`[YY0C]`) reads *Classic, C0, None* — the type and level are kept instead of collapsing
  to a bare *None* (an ordinary no-white cat still just reads *None*).
- **Life stage** — young cats are drawn as their **actual stage** (the tool crops the right cell of the sprite
  sheet — beans no longer show up as adults), carry a **Bean/Kitten** badge, and get a small **Bean ▸ Adult**
  dropdown under the preview to see how they'll look grown up. Because beans have no stats yet, they're **not
  counted** by the *Fetch stats & levels* button — so a village full of beans won't nag you with a "3 left" that
  can never resolve.
- **Edit any cat** — a **✏️ pencil** on each row opens the **cat editor**, the single place all edits live. **Name,
  Species and Wind** stay at the top; below them are three collapsible sections — **Appearance**, **Stats** and
  **Personality**. **Appearance** is the full genotype: every locus is its own dropdown, in
  genome order, and the ones that can hide a recessive offer an **"X carries Y"** option: **Wind** (*North (NN)*, *North
  (carries Null) (NO)*, *South (SS)*, *South (carries Null) (SO)*, *Trade (NS)*, *Null (OO)*), **Fur** (*Shorthair (SS)*,
  *Shorthair (carries Longhair) (SL)*, *Longhair (LL)*), **Base colour** — the co-dominant **and positional** black/red pair,
  where **order matters**: *Black (BB)*, *Red (OO)*, *Black-based (BO)* and *Red-based (OB)*. `BO` vs `OB` decides which pigment is
  primary — a Trade `BO` is a black-based tortoiseshell (e.g. *Silver-Beige*) while `OB` is red-based (*Beige-Silver*), and for
  North/South it flips which allele shows. **Dilution** (*Full (FF)*, *Full (carries Dilute) (FD)*, *Dilute (DD)*), **Density** (1–4),
  **Pattern type** (the 15 named patterns, kept even under a solid coat) and **Pattern shown** (*Patterned (YY)*, *Patterned
  (carries Solid) (YN)*, *Solid (NN)*), **White type & level** and **White shown** (*White (YY)*, *White (carries No-white)
  (YN)*, *No-white (NN)*), plus **Accent** (a 10-colour dropdown that shows each colour's genotype — *Green (BY)*, *Indigo
  (BL)* … — or *Unknown*). The **derived coat shade** (e.g. *Grey*, *Black-Red tortoiseshell*, *Snow*) updates live beside
  Density so you can see what the genotype paints. The parent builder uses the **same options in the same order**, so the
  two always match. Edits flow straight into breeding predictions. This is also how you **record a hidden accent** once
  you've revealed it: a Not-cat's accent isn't on its page, so test it in the breeding sandbox against a homozygous Mercat,
  then set it here so every future cross is exact. (**Growth** has no dropdown — it's an unobservable gene, so it's always
  written as `??` rather than guessed.) The **Stats** section edits the 7 attributes and **Personality** the 5 traits;
  saving writes them to the roster and **re-runs that cat's class/job recommendation** on the spot.
- **Stats** — a **BST** column leads the group with the cat's **Base Stat Total** and its **top three** base stats
  (number + name, ranked, one stat per slot), sortable by the total. Then each attribute total is tinted by its game
  **grade** (ROYGBP pastels: Poor · Average · Good · Very Good · Excellent · Exceptional) and shows its **dice pool**
  (1d6–9d6). A trinket-adjusted stat **splits** the cell — the adjusted total on top, the base value below — and sorts
  by the (higher) adjusted number.
- **Jobs** — **Suggested jobs** leads the group, then one column per day job (alphabetized) reading **`Lv. N (+M)`**:
  its level plus its governing attribute's modifier.
- **Adventure Classes** — **Suggested class** leads (its class name over a sortable **Fit %**), then one column per
  class (Fighter … Bard) reading **`Lv: N`** / **`Fit: X%`** (level defaults to 1 when the page doesn't list it;
  Fit % is how well the cat matches that class's ideal, `0.55 × attributes + 0.45 × personality`, computed from the
  cat's stats). Each of these headers has separate sort buttons for its two values.

**Suggest for shown cats** computes recommendations in bulk.

**Your roster stays on your device** — everything you pull, paste or edit lives in the browser's local storage (no
account, nothing leaves the page). Because some setups wipe that storage on a **PC restart** (a *clear data on exit*
setting, a private window, or a shared/managed machine), a **BACKUP** bar pinned at the very top of the page keeps you
safe (it's always visible, so you can restore before loading anything): **⬇️ Export
to file** saves your whole state — cats, your pencil edits, and the last breeding pairing — to a `.json` file you keep
anywhere, and **⬆️ Import from file** restores it (replacing the current roster). On **Chrome / Edge** a **🔗 Auto-save
to file** button also appears — pick a file once and the tool writes to it automatically on every change and reconnects
to it on your next visit, so nothing is ever lost.

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
- **Paste a genetic string** directly (e.g. `[C] [NN] [SS] [BBFF4] [YYTT] [YY0C] [??] [YR]`; old dash/pipe strings work too)
  when you have one revealed. The **7th (growth) section is always `??`** — that gene can't be observed or tested in-game,
  so the tool never fabricates a value for it (old strings that carry a growth genotype still parse fine).
- **Build a parent (what-if)** — a **🛠 dropdown builder** under each parent assembles a full genotype from scratch, in
  genome order: **Species · Wind · Fur · Base colour · Dilution · Density · Pattern type · Pattern shown · White type ·
  White level · White shown · Accent** — the **same carrier controls, in the same order**, as the pencil editor (Fur
  *SS/SL/LL*, Base colour *BB/OO/BO*, Dilution *FF/FD/DD*, Pattern/White shown *YY/YN/NN*), so a cat opened in one reads
  identically in the other. A **BO** base on a Trade cat makes a tortoiseshell; the **derived shade** is shown live. Each
  change writes the string into the box and re-renders; opening the builder syncs it from whatever's already there — so
  you can tweak a picked cat or invent one to explore *"what if I bred X with Y?"*

Or work backwards with **🔎 Find a pairing for a desired kitten**: choose the traits you want — coat type/colour, pattern,
wind, fur, **white type & level (min/max)**, **colour density (min/max)**, species, accent — and it searches every pair of
your cats with known genetics for ones that could produce it, ranked by the chance per kitten (incompatible-wind pairs are
excluded). Offspring stats aren't genetically determined, so the two stat fields instead constrain the **parents** (only pair
cats whose total attributes / personality meet a minimum). Click a result to load that pair into the predictor.

Like the roster, the Breeding tab **remembers your last pairing** (both parents and every preview pick — wind / pattern /
white / pose) across reloads, so you land right back where you left off.

Either way you get each kitten's odds for **coat colour** (standard / watercolor / tortoiseshell / snow, with swatches),
**colour density** (1–4, the dilution level), **wind**, **fur length**, **pattern** (all 15 named combinations — Mackerel,
Rosette, Karpati…), **white markings** (named per level &amp; type, e.g. *Bib &amp; Boots*) — including a distinct **Hidden**
outcome for kittens that inherit a white type &amp; level but don't express it (no-white visibility), so it reads
*Hidden, Classic, C1, Locket* and its gene string records the real type (`[NN1C]`) instead of collapsing to *None* / `[NN0?]`,
just like the parents' own hidden white — **accent colour** (Ruby, Amber,
Teal…), and **species** — the result blocks are ordered to mirror the finder's inputs (Species first). Under every outcome the
possible **allele pairs** are listed (e.g. accent `[RR]` × `[LL]` → *Pink* `[RL] / [LR]`); colour alleles honour each parent's
**wind** (which slot each donates), and traits that aren't a two-allele cross (species, white type & level, density) show a short
inheritance note instead. A pattern only names its type when it's actually shown (a solid cat reads **Solid**, never a leaked
hidden type). **Accent** follows Pixel Cat's End's **co-dominant** rules — one colour ⇔ one exact allele pair — and the game only
ever *shows* it on a **Mercat** (its tail); a **Not-cat's accent is never revealed** (it lives on PCE's server), so the tool
treats it as unknown rather than inventing one. When **both** parents' accents are known, each kitten's accent is a concrete
colour with its genotype. When a parent's accent is hidden, the offspring accent stays an **honest partial** — `[L?]` or `[B?]`,
never an invented colour or a fake percentage — and a note explains that Mercat kittens are drawn with the **known parent's
colour as a placeholder** (not a prediction), plus how to **reveal** a hidden accent (breed with a homozygous Mercat —
Black/Ruby/Blue/Gold — and read the offspring colours) and record it. An **Accent picker** appears only when a pairing genuinely
has more than one outcome to choose from — labelled by colour when fully known, by genotype (`[B?]`) when partial, and
**(tail)** on a Mercat, where the pick also recolours the tail. A parent with a hidden accent reads **Accent: Unknown** on its
card. Plus
each parent's decoded phenotype (shown as **labelled facts** in the same order as the search inputs — Species / Wind / Fur /
Coat / Pattern / White / Accent — with its name/#ID linking to the cat's page when picked from your roster). Parents and
**every** possible kitten get **composited sprite previews** built from the game's own image layers, each **cropped to a single
pose** (correct per-species offsets for Not-cats and Mercats) — pick **standing / sitting / playing / sleeping / upsidedown**
from the pose selector. Above the kitten gallery a row of **dropdowns — Species · Wind · Fur · Coat · Pattern · White** (plus an **Accent**
picker whenever more than one accent is possible) — each lists **only outcomes this pairing can actually produce** (**Coat** filters by
coat type — Standard / Watercolor / Tortoiseshell / Snow; Species toggles the
previews between Not-cat and Mercat sprites); picking
any of them narrows the previews and rewrites every kitten's % to the **true overall chance** of a kitten with that coat *and*
the chosen
species/wind/pattern/white (independent loci multiply in, and a wind pick isolates the exact coat-and-wind pair). Each kitten also
carries a **click-to-copy genetic string** (small, wrapping button) that marks every allele the game keeps hidden with a
single **`?`**: a shown-dominant trait reads `[D?]` (the second copy could be a hidden recessive), a shown-recessive trait
reads `[rr]` (both copies known), and a fully-hidden slot (a North/South cat's off-wind colour allele) reads `[??]` — never a
guessed value; the final section carries the accent genotype, which stays a partial like `[L?]` (or `[??]`) whenever a parent's
accent is unknown. A collapsible
**🧬 Quick Genetics Overview** on the tab explains the homozygous
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
