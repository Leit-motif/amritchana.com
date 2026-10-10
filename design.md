# amritchana.com design language

Extracted from `index.html` as published at `d96a257` ("The Crossing v4"). Nothing here is a new look:
it names what the page already does so new sections can match it. Where the page breaks its own rule,
the rule wins and the break is listed at the end.

The page in one line: a pinned landscape (ice → ridge → valley → forest) with words on glass scrolling over
it, then a conventional offer screen of cream cards.

## 1. Tokens

### Colour: the 13 custom properties in `:root`

| Token | Value | Used for |
|---|---|---|
| `--ink` | `#f4f3ed` | Text on dark glass and photos |
| `--card-ink` | `#203329` | Text on cream cards |
| `--card-muted` | `#43574a` | Secondary text on cream cards |
| `--gold` | `#e8cf83` | Gold fills: CTA, card highlight, "Me" badge, bullet dots |
| `--gold-text` | `#f1d77d` | Gold words on dark glass |
| `--gold-ink` | `#1e2a20` | Text on a gold fill |
| `--glass` | `rgba(8,14,11,.76)` | Caption glass |
| `--sans` | Schibsted Grotesk | Everything that is a sentence |
| `--mono` | IBM Plex Mono | Eyebrows and labels only |
| `--gutter` | `clamp(20px,4.5vw,68px)` | Page side margin |
| `--maxw` | `1420px` | Content width |
| `--scene-min` | `560px` (`620px` ≤560px wide) | Shortest a landscape screen may be |
| `--card-pad` | `19px` (`15px` ≤560px wide) | Inner padding of cards and panels |

Literal colours in use that new work should treat as tokens (promote them when a section is rebuilt):

| Literal | Meaning |
|---|---|
| `#101711` / `#111812` | Page and world background (forest black) |
| `rgba(244,243,234,.97)` | Cream card |
| `#c9ad55` | Gold rule: the ring on "Best first project", the border of gold chips |
| `#f2d779`, `#fff4c5` | Focus ring (page) and focus ring (on cards and the CTA) |
| `#a9c2d1` | Cool: the before-state (ridge bullets) |
| `#c9dbe6` | Cool text: the ridge eyebrow |
| `#eceee8`, `#eef0e9` | Body text on glass |

### Type scale actually used

Two families, no others. Sizes are the ones in the CSS; nothing in between.

| Step | Size (desktop → phone) | Line height | Weight / tracking | Where |
|---|---|---|---|---|
| Label | 12px mono (13px in the header) | 1.25–1.3 | 500, `.06em` labels / `.13em` eyebrows, uppercase | Eyebrows, card labels, who-badges, "Example · no client data" |
| Small | 14px | 1.35–1.45 | 400; 600 for terms | Card body, footer, small notes |
| Note | 15px | 1.42–1.5 | 400–500 | Care note, after-steps, queue steps |
| Body | 17px → 16px | 1.42–1.55 | 400; `strong` 650 | Captions, page body |
| Card title | `clamp(19px,1.45vw,22px)` → 20px | 1.12 | 700, `-.025em` | Offer card `h3` |
| Panel title | `clamp(21px,1.7vw,26px)` / `clamp(22px,2vw,28px)` | 1.06–1.1 | 700, `-.03em` | After-box, queue card |
| Price | `clamp(25px,2vw,30px)` → 26px | 1.05 | 700, `-.035em` | Offer price |
| Section | `clamp(32px,3.1vw,44px)` → 31px | 1 | 700, `-.045em` | Ridge and valley `h2` |
| Offer head | `clamp(38px,5vw,64px)` → `clamp(34px,9.4vw,42px)` | .99 | 700, `-.048em` | Screen-three `h2` |
| Display | `clamp(48px,7.6vw,100px)` → `clamp(40px,11.4vw,54px)` | .99 | 700, `-.055em` | Hero `h1` |

Display and section heads use `text-wrap:balance`; sentences use `text-wrap:pretty`.

### Radii

10px glass caption and `.panel` · 8px cards, header bar, footer · 7px guard box · 6px CTA and notes ·
5px small tiles (queue steps) · 4px badges and labels · 50% dots.

### Shadows

| Name | Value | On |
|---|---|---|
| Rest | `0 8px 22px rgba(4,12,7,.16)` | Cream cards |
| Lifted | `0 16px 28px rgba(4,12,7,.25)` | Cream card on hover/focus |
| Float | `0 18px 44px rgba(0,0,0,.2)` | Glass caption |
| Button | `0 7px 18px rgba(5,12,7,.2)` | CTA |
| Gold ring | `0 0 0 1px #c9ad55` (added to Rest) | The recommended card |

Text over photos gets a soft text-shadow (`0 1px 8–12px rgba(0,0,0,.45–.55)`), never an outline.

### Glass and scrims (content over landscape)

| Surface | Fill | Blur | Edge | Radius |
|---|---|---|---|---|
| Caption glass | `var(--glass)` = `rgba(8,14,11,.76)` | 8px | 1px `rgba(244,243,237,.17)` | 10px, Float shadow |
| Panel | `rgba(7,15,10,.72)` | 6px | none | 10px |
| Note | `rgba(7,15,10,.66)` | 4px | none | 6px |
| Bar (header, footer) | `rgba(7,15,10,.62)` | 4px | none | 8px |
| Hero scrim | horizontal `rgba(6,10,13,0→.5→.44→0)` gradient, masked top and bottom | none | none | none |
| Scene shade | bottom-up `rgba(7,11,13,.22–.55)` gradient | none | none | none |

The landscape must stay visible around and through every surface. Never darken a plate to near-black.

### Layout

Breakpoints at 560px (phone), 1000px and 1180px. Phone gutters are 20px, so a phone panel is 350px wide at
390px. Tap targets are at least 44px tall (the CTA is 52px on phone).

## 2. Motion: one feel

**One curve.** `--ease: cubic-bezier(.2,.75,.25,1)`, "settle": it leaves quickly and lands softly, with no
overshoot. Every time-based transition and animation uses it. No springs, no bounce, no `linear` except
for scroll-scrubbed progress.

**Three durations.**

| Token | Value | For |
|---|---|---|
| `--dur-respond` | 200ms | Anything that answers a pointer, focus or tap: colour, lift, tilt, press |
| `--dur-change` | 480ms | One item changes state or place: turns over, slides into a lane, rewrites, a gate opens |
| `--dur-beat` | 960ms | The pace of a sequence that runs by itself: one step of a flow, the pause before an item comes back |

Siblings in a sequence start `calc(var(--dur-change) / 6)` (80ms) apart. Nothing takes longer than one beat.

**Scroll-scrubbed motion has no duration.** The visitor's scroll supplies the timing; progress is mapped
through smoothstep (`t*t*(3-2*t)`), as the landscape crossfade already does. An ease-out on a scrub would
feel like lag.

**Distances are small.** Lifts are 2–5px, tilts at most 6°, slides 8–40px. Motion is there to show cause
and effect, never to decorate.

**Reduced motion** (`prefers-reduced-motion: reduce`, the `.reduced` class):
- No pinned world: the page renders the static stacked screens, as with no JS.
- No tilt, lift, turn, slide or autoplay. State changes still happen when the visitor asks, as an instant
  swap or an opacity fade no longer than `--dur-respond`.
- Sequences show their end state. Nothing moves on its own.

**No JS:** every section shows its finished, readable state. Controls that need JS are hidden, not dead.

## 3. Meaning rules

**Gold = a person decides.** Gold marks a human judgment: the person who approves ("A person approves
anything that needs judgment"), Amrit's recommendation ("Best first project"), Amrit as the person who
does the work (the "Me" badge), and the visitor choosing (card highlight, focus ring, the CTA). Work a
machine does is never gold. If a pattern needs an accent for something automatic, it uses cream or cool.

**Cool = the before.** The ridge uses blue-grey (`#a9c2d1` dots, `#c9dbe6` eyebrow). Cool marks the old
way: work done by hand, waiting, repeating. It never appears in the after-state.

**Cream = something you can take.** Offers and the example workflow are cream cards with dark ink. In the
story sections cream marks work that is handled.

**Mono eyebrow = where you are in the story.** One per section, above the heading, mono 12px uppercase
`.13em`: "AI consulting · Chicago" → "Where you are" → "Where I take you" → "A practical way to get time
back". Cool on the ridge, gold once the story turns to what a person does, near-white on the hero. Mono
also labels things (card labels, who-badges, a clock in a pattern). It never carries a sentence.

**Glass panel = content over landscape.** Words over a photo sit on caption glass or a scrim. A pattern
lives inside a glass panel: the glass is the stage, the pattern is what moves on it.

**Every scroll position shows readable words.** At 390×844 the longest scroll with no readable content
text stays under half a screen. Interaction adds delight; it never hides the content. Each section reads
completely at rest, without a tap.

**Honest content.** No invented numbers, clients, logos or testimonials. Clocks and days in a pattern are a
frame for the story, not a statistic.

## 4. Pattern catalog

Each pattern shares the tokens, the curve and durations, and the gold meaning, and uses a **different
interaction mechanic**. Coherence comes from shared physics and meaning; no pattern repeats another's
mechanic. Patterns 2–6 are proposals for the two story sections (prototypes in `/lab/`); only pattern 1
is live.

### 1. Tilt card (live: the offer ladder)

*Mechanic: the card follows the pointer.*

- Rectangular cream card (`rgba(244,243,234,.97)`, 1px `rgba(255,255,255,.45)` edge, 8px radius,
  17px × `--card-pad` padding, Rest shadow) holding one offer: mono label, title, price, terms, one sentence.
- Fine pointer only (`(hover:hover) and (pointer:fine)`, JS on): the card tilts toward the cursor, at most
  5° on X and 6° on Y with 900px perspective, and lifts 5px. Leaving resets it.
- Hover or keyboard focus turns the card gold (`--gold` fill, `#f7e7aa` edge, Lifted shadow). Focus gets a 3px
  `#fff4c5` outline and the colour change, no tilt. The visitor is choosing, so gold is right.
- The recommended card carries the gold ring and a dark label chip with gold text ("Best first project").
- Touch gets no tilt and no hover state; the whole card is one link.
- `--dur-respond`, `--ease`. Reduced motion: colour change only, no lift or tilt.

### 2. Scrub: your scroll is the clock

*Mechanic: scroll position drives a sequence while its glass panel is pinned.*

- The panel pins (sticky, vertically centred) for at most 0.8 of a screen. Scrolling forward advances the
  sequence; scrolling back reverses it exactly. No timers.
- The heading and the first item are on screen when the pin starts, and every item has reached its end
  state by 85% of the pin, so stopping anywhere shows a readable panel.
- Progress maps through smoothstep. Each item takes its own slice of the progress; slices overlap by
  about a third so the motion never stalls.
- Shows the before-state, so it uses cool and paper colours, never gold.
- Skins: **Pile** (paper slips land crooked on a stack; each landing jolts the pile 2px) and **Week clock**
  (a mono clock runs MON 09:00 → FRI 17:00 and a week grid fills).
- Reduced motion and no JS: no pin; the end state.

### 3. Recur: clear it and it comes back

*Mechanic: tap one item to clear it; the page undoes it.*

- A list of jobs, each with a real ✓ button (44px target, Enter/Space). Tapping strikes the item, and it
  leaves (`--dur-change`). One beat later (`--dur-beat`) it returns on top, tagged "Again" in cool mono.
  The list never empties: that is the joke and the point.
- Runs once on its own when the panel is centred, so a visitor who only scrolls sees it, then hands over.
- No gold. Reduced motion: the item swaps in place with a 200ms fade. No JS: a plain list, no buttons.

### 4. Gate: work flows, a person opens the gate

*Mechanic: a sequence runs by itself, and only a tap on gold lets judgment items through.*

- A track with one stop per job. A marker moves down it, one stop per `--dur-change`; at each stop the job
  straightens and rewrites from its before-line to its after-line (cool slip → cream).
- Jobs that need judgment also get a gold gate: a gold barrier and a button naming the human action
  ("Approve", "Pick up"). The flow never waits for a gate; held items wait for a person. Only a tap opens a
  gate (no auto-approve). The arm lifts (`--dur-change`) and the chip reads "Approved".
- Gold is only on gates. The guard line closes the panel.
- Reduced motion: the end state; gates open instantly on tap. No JS: the end state, gates shown as gold
  "Waits for a person" labels without buttons.

### 5. Flip: tap to turn it over

*Mechanic: tap or Enter turns one tile between its before and after faces.*

- Each topic is one tile with two faces in the same grid cell, so the tile is as tall as its taller face
  and nothing reflows. Before face: cool paper. After face: cream; the person part of an after-line is gold.
- When the panel is centred, tiles turn from before to after on their own, 80ms apart (`--dur-change`
  each, rotateY 180° with 1000px perspective). After that, tapping a tile shows its before; tapping again
  turns it back.
- Each tile is a `button` with `aria-pressed`. A one-line mono hint says what tapping does.
- Reduced motion: an opacity crossfade instead of the turn. No JS: the after face.

### 6. Sort: one tap files it

*Mechanic: one button re-files the whole set into lanes.*

- Starts as one mixed list (the inbox). "Sort it" moves every item to its lane with a FLIP animation
  (`--dur-change`, 80ms stagger) while each line rewrites to its after-line.
- Lanes: "Handled" (cream) and "A person decides" (gold). The gold lane is the only gold; the button is
  neutral, because sorting is the machine's work.
- Runs once on its own a beat after the panel is centred if nobody taps. Tapping again un-sorts, so the
  visitor can compare.
- Reduced motion: instant re-layout with a 200ms fade. No JS: the sorted state.

### Adding a pattern

Before adding a seventh: name its mechanic in one line and check it differs from all six; use only the
tokens above; use `--ease` and the three durations (or scrub through smoothstep); keep gold for a person
deciding; make the resting state readable without interaction; give it reduced-motion and no-JS states;
check 390×844 touch and keyboard.

## 5. Where the live page breaks its own rules

- The valley caption ("What changes") gives every after-line a gold dot and gold topic word, though most
  of that work is automatic. By the gold rule only the person part should be gold. The sections-v5
  concepts fix this.
- The ridge and valley captions are bullet lists of full sentences (6 × 8–16 words). Each item should
  read in about a second; the concepts cut them to 3–6 words.
