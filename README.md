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

1. **My cats (roster)** — paste your **Village Manager** page once (it's a private page, so it can't be
   auto-loaded). The tool parses the whole table into a **searchable, filterable** list saved on your device;
   click a cat to fetch and analyze it. Paste more manager views (Basic, Adventuring Levels, Day Job Bonuses,
   Active/Traveling) and their columns/filters merge into the same roster. A **Table** view shows every cat with
   all captured columns plus suggested class/jobs, and **Suggest for shown cats** computes suggestions in bulk.
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

## Hosting

GitHub **Settings → Pages → Deploy from a branch → `main` / `/ (root)`**. The hub is then at
`https://owlsomniac.github.io/owlfunstuff/` and the advisor at `…/pixelcatsend-advisor/`.
