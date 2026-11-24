# game-ui-taste

An agent skill for designing and critiquing **mobile game screens** so they read
as *this* game, not a generic AI-generated app.

It covers menus, HUD chrome, shop, settings, overlays, tutorial/FTUE overlays,
and results/reward screens. It decides color, type, iconography, decoration,
touch states, and how UI feedback and reveals feel. Every plan goes through a
plan-then-critique gate against anti-slop checklists before anything is built.

## What's inside

| File | Covers |
|---|---|
| [`SKILL.md`](SKILL.md) | Touch-first rules, safe area and reachability, the structure pass, palette/type derivation from the game's world, the plan → critique → build → render process, ranked critique of existing screens, and the main anti-slop checklist |
| [`references/ftue.md`](references/ftue.md) | First-session time budget, step anatomy, spotlight / hand pointer / arrow / bubble hints, hint timing, input gating, skip, progressive unlocks, FTUE checklist |
| [`references/reward-and-juice.md`](references/reward-and-juice.md) | Feedback tiers (frequent, occasional, rare), press and easing defaults, the results-screen reveal sequence, lose screens, popup queues, chest and pack reveals, accessibility, reward checklist |

The two reference files are playbooks: `SKILL.md` sends the agent to them only
when the screen is a tutorial or a results/reward screen.

## Install

### Claude Code, for every project

```bash
git clone https://github.com/vitorverrone/game-ui-taste ~/.claude/skills/game-ui-taste
```

### Claude Code, for one project

```bash
git clone https://github.com/vitorverrone/game-ui-taste .claude/skills/game-ui-taste
```

Other agents that read the Agent Skills format can use the same folder; point
them at `SKILL.md`.

## Use

Claude picks the skill up on its own when you ask for a game screen's look, a
tutorial overlay, a results or reward screen, or "make this less generic".
You can also call it by name:

```
/game-ui-taste design the level-complete screen
/game-ui-taste critique src/screens/Shop.tsx
```

It works best with the game's world in a sentence or two (genre, setting, the
feeling it's going for) and, if one exists, a style guide.

## Scope

Owned here: visual composition, touch states, FTUE overlays, and the UI layer
of feedback (press feel, reveal sequences, popup queues).

Left to other tools: player-facing copy (a copy-review skill such as
`ux-slop`), engine-level layout and scaling, gameplay feel such as hit-stop and
impact shake, art production, and tablet/desktop layouts.

## Credits

All text is original. Ideas draw on Steve Swink's *Game Feel*, Jesse Schell's
*The Art of Game Design*, Celia Hodent's *The Gamer's Brain*, Vlambeer's "The
Art of Screenshake", and these skills:
[`m4bwav/game-juice`](https://github.com/m4bwav/game-juice) (MIT),
[`omer-metin/skills-for-antigravity`](https://github.com/omer-metin/skills-for-antigravity)
(Apache-2.0), [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable)
(Apache-2.0), [`felipebasurto/unslop-ui`](https://github.com/felipebasurto/unslop-ui)
(MIT), [`diego3g/craft`](https://github.com/diego3g/craft) (MIT), and the
`ftue` and `game-juice` skills published on skills.lc.

## License

[MIT](LICENSE)
