# owlfunstuff

Small self-contained web tools. Everything here is a single static HTML file — no build step, no server.

## Pixel Cat's End — Adventuring Advisor (`index.html`)

Pull a [Pixel Cat's End](https://www.pixelcatsend.com) cat's **attributes** and **personality traits** by ID,
see the **bonuses** each stat grants, and get an **adventuring class** + **day-job** recommendation from the
combined profile. All analysis runs in your browser; nothing leaves the page.

**Live:** once GitHub Pages is enabled for this repo → **https://owlsomniac.github.io/owlfunstuff/**

### Using it

Load a cat one of three ways — they all land on an editable sheet, so you can fix anything before analyzing:

1. **By cat ID** — paste an ID (e.g. `430432`) or a profile URL, press **Fetch cat**. Routed through public
   CORS relays because the game blocks direct cross-site reads; relays can be flaky, so:
2. **Paste page HTML** — open the profile, view source (Ctrl/Cmd+U), copy all, paste. Always works.
3. **Enter manually** — type the numbers.

Press **Try a demo cat** to see the full output instantly.

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
