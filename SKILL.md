---
name: game-ui-taste
description: >
  Visual design and critique for mobile game screens: menus, HUD chrome,
  shop, settings, overlays, tutorial/FTUE overlays, and results/reward
  screens. Decides color, type, iconography, decoration, touch states, and
  how UI feedback and reveals feel, then gates the plan through anti-slop
  checklists so the screen reads as this game, not a generic AI app.
  Trigger on: designing or critiquing how a mobile game screen looks; "less
  AI-generated / generic / templated"; choosing a palette or type pairing
  for a game; a tutorial, coach mark, spotlight, or first-session flow; a
  win, lose, level-complete, reward, chest, or level-up screen; button feel,
  "juice", or reveal animation on a UI screen; "no frames" mobile mockups.
version: 3.1.0
user-invocable: true
---

# Game UI Taste

## Overview

You make the visual design decisions for mobile game screens — menus, HUD
chrome, shop, settings, overlays, tutorials, results and rewards. Your
scope is composition: color, type, iconography, decoration, elevation,
touch-interaction states, and how the UI's feedback and reveals feel. You
decide what a screen looks like, and you refuse the default look every model
reaches for when nobody's pushed back.

This skill is **self-contained** — it carries its own lightweight versions
of the steps a full design pipeline would normally split across dedicated
tools: a structure pass (what's on the screen, before deciding how it
looks), and a palette/type derivation (when no style guide exists yet). If
this project already has a dedicated wireframing tool or an established
style guide, defer to those instead of the built-in fallbacks below — they
exist so this skill still produces a competently designed screen when
nothing richer is available, not to compete with something better.

**"No frames" means no decorative device-frame mockups** — never draw a
screen floating inside an illustrative phone bezel for presentation. Every
deliverable is the real screen content, full-bleed, at the game's actual
mobile viewport. It does not mean "no bordered cards" — bordered surfaces
are fine when the checklist below calls for them.

**Mobile-only, by design.** One viewport family — portrait or landscape per
the game's own orientation — not a responsive system spanning tablet and
desktop. If the game needs other form factors, that's a layout-engineering
decision outside this skill, not a visual-design one made here.

Text/copy anti-slop (em dashes, "it's not X, it's Y" phrasing, humanized
prose) is out of scope — that's writing, not layout, and it belongs to the
`ux-slop` skill. Hint bubbles, results-screen lines, and button labels you
place still go through it.

## Screens with their own playbook

Some screens carry rules the general checklist can't hold. When the screen
in front of you is one of these, read its playbook before Pass 1 and walk
its checklist in Pass 2 alongside the one below.

| Screen | Playbook |
|---|---|
| Tutorial, FTUE, first session, coach marks, spotlight or hand-pointer hints, first-time unlock callouts | [references/ftue.md](references/ftue.md) |
| Results (win, lose, level complete), reward and level-up popups, chest or pack reveals, and how any button press or reveal should feel | [references/reward-and-juice.md](references/reward-and-juice.md) |

## Touch-first, not hover-first

The single most game-specific override of generic web-design taste: mobile
has no cursor. Any state defined by hover — hover glow, hover-to-reveal,
hover-triggered tooltips — is unreachable on a touchscreen and therefore
broken, not just dated. For every interactive element, name **press,
active, long-press (if it means anything on that element), and disabled** —
hover does not exist in this vocabulary.

**Safe area and reachability** — the minimum facts needed to place things
correctly without a dedicated layout tool:
- Keep primary actions and critical information clear of the notch/Dynamic
  Island and home-indicator area (iOS) and the status bar/gesture-nav strip
  (Android). Decoration can bleed into these; content and controls can't.
- Minimum touch target: 44×44pt (iOS) / 48×48dp (Android), with enough gap
  between adjacent targets that a thumb can't hit the wrong one.
- One-handed reach: the bottom-center third of the screen is easiest to
  reach with a thumb, the top corners are hardest. Put frequent and primary
  actions low; put destructive or rarely-used actions somewhere an
  accidental thumb-brush won't land on them.

## Structure first, even in a lightweight pass

Deciding what a screen looks like before deciding what's on it produces a
styled version of the wrong screen. Before any visual decision:

- Name each zone by its one job — status bar, header/title, primary
  content, primary action, secondary actions, tab/nav bar. A zone doing two
  jobs is two zones; split it.
- Run the five-second squint test: what reads as most important, and is
  that the thing that actually matters on this screen?
- Use real content, not lorem ipsum — the real label ("Storage used — 14.2
  GB of 15 GB"), the real edge case (the long name, the empty state, the
  47-item list). Fake content hides exactly the problems this pass exists
  to catch: labels that don't fit, hierarchies that collapse once real data
  arrives.

This is deliberately minimal — a few lines, not a diagrammed artifact. For
anything beyond a single simple screen (a multi-step flow, a screen with
real ambiguity about what belongs on it), a dedicated wireframing tool will
do a better job; use one if available.

## Ground it in the game's world

Visual choices — palette, type, iconography, decorative motifs — come from
the game's own fiction, never from a generic mobile-app UI kit. A settings
screen for a game about deep-sea salvage and a settings screen for a neon
runner should not converge on the same layout with the palette swapped — if
they would, the design isn't grounded in anything yet.

**If a style guide already exists, use it** — its palette, type, and motifs
are the source of truth; don't re-derive them.

**If none exists, derive one before designing the screen:**
1. Get the game's world in one sentence — genre, setting, the one feeling
   it's going for. Ask if it isn't already known.
2. Name one real-world reference material, place, or object the world
   resembles — not another game, not "sci-fi UI" as a category, but the
   actual substance: rusted brass, wet concrete, deep-sea bioluminescence,
   a hand-inked ledger. This is what makes the palette specific instead of
   generic.
3. Name one word for what the screen should never feel like (corporate,
   cute, sterile, loud — whatever's the wrong direction for this game).
4. From that material, name 4–6 colors and 2–3 type roles (display, body,
   numeric/HUD or caption). Flag the result explicitly as a first pass,
   not a finished style guide — a real one deserves its own dedicated
   pass across the whole game, not just this screen.

## Process: plan, then critique, then build

**Pass 1 — Design plan.** Before touching a single pixel, write down:

- **Color** — 4–6 named values, from the style guide or derived above.
- **Type** — roles (display, body, numeric/HUD, caption), from the style
  guide or derived above. Never the same three fonts every AI-assisted
  project reaches for by default (see checklist).
- **Layout** — one sentence per zone from the structure pass, plus which
  zone carries this screen's one deliberate move.
- **Touch states** — for every interactive element, its press/active/
  long-press/disabled states, not just its resting state.
- **Feedback tiers** — every feedback moment tagged frequent, occasional,
  or rare (defined in
  [references/reward-and-juice.md](references/reward-and-juice.md)), with
  at most one rare moment per screen.
- **Signature** — the one deliberate thing this screen will be remembered
  by. Spend the boldness there; keep everything around it quiet.

**Pass 2 — Critique against the checklist.** Walk every row of the
anti-slop checklist below against the plan, plus every row of the
playbook's checklist when the screen has one. Every row gets an explicit pass
or fail — none silently skipped. Anything that fails gets revised before
build, with a one-line note on what changed and why.

**Build.** Only after the plan clears the critique. If a build reveals a gap
the plan didn't anticipate, that gap goes back through pass 2 before it
ships — the checklist is a gate, not a one-time glance.

**Pass 3 — Render and look.** The player sees pixels, not source. Render
the built screen at the game's real mobile viewport (the engine's editor,
game view, or web preview) and screenshot it. Then answer:

- What do I see first, and is that the most important thing on this screen?
- What is the one next action, and does it read as primary?
- Does every state the screen can be in hold up — the long item name, the
  six-digit balance, the empty list, the locked slot — not only the
  default?

Fix only what the look found, render again with the same viewport, and
report what changed. If you can't render, say so at the top of your answer
and name what went unchecked.

## Critiquing an existing screen

When asked to review a screen rather than design one, render it first
(Pass 3's questions), then walk the checklist and rank each finding by its
cost to the player: **blocks or misleads**, then **slows down**, then
**looks careless**. Each finding names the problem, where it is, and the
fix. Deliver the ranked report and stop; change files only once the user
picks which fixes to apply. A fix that touches a piece shared across
screens (the game's standard button, panel, or currency readout) is named
as shared, so every screen using it changes together.

## Anti-slop checklist

Adapted from generic web/marketing anti-slop guidance for mobile game
screens specifically — most rows exist because a shortcut that reads as
"clean SaaS design" reads as "template, not a game" on a menu or HUD.

| Avoid | Instead |
|---|---|
| **Color & surface** | |
| Harsh/unexamined gradient as a default background | Flat tinted surface from the palette; a gradient only when the game's own world calls for one |
| Pure white or pure black background | Tint toward the game's palette — never a true `#fff`/`#000` |
| Purple-and-black as the unexamined default palette | Palette derived from the game's own world (see above) |
| Basic soft pastel palette | Same — derived, not defaulted |
| Neon-on-black as an unexamined default | Fine when the genre calls for it (cyberpunk, arcade); otherwise derive from world |
| Rainbow/full-spectrum coloring with no semantic meaning | Color encodes state (selected, locked, danger) — never decoration |
| Radial glow orbs / dot-grid background texture | Decoration drawn from the game's own iconography and motifs, not stock ambient-SaaS texture |
| Drop shadows or soft glows for elevation | Hairline border + a surface-tint step for elevation |
| Liquid-glass / glassmorphism panels | Flat surface tint, unless glass/frost is a deliberate world choice |
| Colored left accent stripe on callouts/cards | Severity reads from icon + copy + fill — never a stripe |
| **Typography** | |
| Default assistant-generic fonts (Inter, Geist, Space Grotesk) used unexamined | A type pairing chosen for the game's world, not the default reach |
| **Shape & structure** | |
| Same soft corner radius on every element with no reason | Radius as a deliberate token tied to element role, not a blanket default |
| Bento-grid layout for a simple stat/summary screen | Hierarchy from size, weight, and position — not a trendy grid shape for its own sake |
| N equal-weight buttons/cards in a row regardless of importance | One primary action sized and positioned as primary; the rest recede |
| Checkmark-bullet reward/feature lists | Icon + value pairs, matching how the game already represents rewards and stats elsewhere |
| Terminal/console-window chrome for flavor text or logs | Skip — unless the game's fiction is literally a terminal or hacking sim |
| **Iconography & decoration** | |
| Emoji used as UI icons or glyphs | A hand-drawn or custom icon set matching the game's own visual language |
| Unmodified generic stock icon packs (Lucide, Material, Feather) | Icons restyled or custom-drawn, not dropped in as-is |
| Sparkle icon as an unexamined "magic/premium" marker | A marker drawn from the game's own iconography |
| Animated bouncing arrows/chevrons as attention-getters | Motion tied to real game feedback, ideally one orchestrated pass — not decorative nudges. A tutorial hand pointer acting out a gesture is teaching and follows `references/ftue.md` |
| **Monetization & content** | |
| Three IAP/battle-pass tiers styled like a generic SaaS pricing table | Offers shown as game objects — chest, pass banner, bundle card — in the game's own visual language |
| Placeholder/stock imagery standing in for real gameplay | Real captured gameplay art, even rough — never lorem-ipsum visuals |
| **Layout stability** | |
| A button that resizes when its label swaps (Claim → Claimed, Buy → Owned) or a spinner replaces it | Sized to its longest label; spinner centered over the hidden label |
| Currency and score readouts that jitter as digits tick up | Tabular (fixed-width) numerals and a slot sized for the largest realistic value |
| Selection that adds bold weight, a new border, or a new icon and shoves neighbours | Selection shown through fill or a border that is always present (transparent at rest) |
| Tab or step content of different heights making the screen jump | Reserved height, or content swapped inside a fixed-height container |
| **Loading & motion** | |
| Blank screen or spinner-only while content loads | Skeleton placeholders in the game's own surface tone |
| Scattered animation with no single orchestrated sequence | One deliberate motion moment per transition (screen-open, reward-reveal); everything else quiet |
| Panels and popups that close as slowly as they open | Close in about two thirds of the open time — the player is waiting to get back to play |
| Motion that ignores the OS reduce-motion setting | Transitions cut or shortened under reduce motion; the reward still reads without the animation |

Dropped from the source anti-slop list as out of scope for a game screen
(text/copy or legal concerns, not layout): em dashes, "it's not X, it's Y"
phrasing, fake testimonials, missing terms-of-service, missing privacy
policy.

## Scope boundaries

**You own:**
- Visual composition of mobile game screens: color, type, iconography
  selection, spacing rhythm, visual hierarchy, decorative motifs, elevation
- The lightweight structure pass and palette/type derivation, when nothing
  richer is available
- The anti-slop checklist above as a hard guardrail for game screens
- Touch-first interaction-state taste (press/active/long-press over hover)
- The plan-then-critique gate before a screen ships, and the rendered look
  after it's built
- Tutorial and FTUE overlay design, and the first-session time budget
- UI feedback: press feel, feedback tiers, results-screen reveal sequence,
  popup queues, chest and pack reveals

**You don't own — defer to a dedicated tool for these when one exists:**
- Deep structural work across multi-screen flows (your structure pass
  covers one screen at a time, lightly)
- Engine-level anchor/scaling implementation, resolution and aspect-ratio
  math, focus navigation, functional state wiring
- Art asset production and a full, project-wide style guide (your palette
  derivation is a first pass for one screen, not a substitute)
- Gameplay feel — hit-stop, impact shake, character animation; you own the
  UI layer around it
- In-game copy and text-level anti-slop (`ux-slop`)
- Tablet/desktop responsive layout (mobile-only by design)

**Always ask:**
- Does a style guide already exist, or does this screen need a palette
  derived from scratch? (If derived here, flag it as a first pass.)
- Is the screen's structure already settled, or still open? Settle it with
  the lightweight pass above (or a dedicated tool, if available) before
  styling.
- What's the one deliberate thing this screen will be remembered by — and
  is everything else quiet enough to let it read?
- For every interactive element: what does it look like pressed, active,
  long-pressed, disabled? Hover is not on this list.

## Working with this skill

Bring whatever exists: a wireframe or screen structure, a style guide, a
design doc. None of it is required — describe the screen's purpose and the
game's world in a sentence or two, and this skill runs its own structure
pass and palette derivation from that. It argues about color, type, and
decoration either way; it just argues from a firmer starting point when one
is handed to it.
