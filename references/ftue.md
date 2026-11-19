# FTUE and tutorial overlays

Playbook for the first session and every guided-teaching surface: spotlight
overlays, coach marks, hand pointers, hint bubbles, first-time unlock callouts.
Back to [SKILL.md](../SKILL.md). Every hint string also goes through `ux-slop`.

The leading idea: **the level is the tutorial.** The player learns by doing the
real action on the real control in the real game, one concept at a time. Text
supports the action; it never replaces it.

## Time budget for the first session

Measure from the moment the first-launch splash ends.

| Milestone | Budget |
|---|---|
| Title to playing, first launch | 1 tap (or none: drop straight into level 1) |
| Player's first input | ≤ 5 s |
| First success with feedback | ≤ 30 s |
| Core loop completed once | ≤ 60 s |
| Guided steps in the whole tutorial | ≤ 7, one concept each |
| A natural stopping point with a reason to return | ≤ 3 min |

The **hand-the-phone test** is the completion bar for any FTUE design: a
non-gamer given the phone with no explanation plays correctly within 30
seconds. Walk the plan through that person's eyes, step by step, before
building.

## Step anatomy

Each guided step runs the same loop:

1. **One concept.** The core verb first (tap, swipe, drag), then the goal,
   then what makes it hard. Secondary systems wait (see Progressive unlocks).
2. **Guided action** on the live control, with the smallest hint that works.
3. **Guaranteed success.** The tutorial level is simplified so the first
   attempt cannot fail: fewer elements, no timer, no loss state.
4. **Feedback** at the *frequent* tier from
   [reward-and-juice.md](reward-and-juice.md). Save the bigger celebration
   for finishing the tutorial as a whole.
5. **Hand-off.** The final step has no hint: the player does it alone and the
   overlay fades out.

## Hint vocabulary

Pick the lightest tool that teaches the step; escalate only when the player
stalls.

| Tool | Use for | Rules |
|---|---|---|
| **Spotlight** | Pointing at one interactive element | Dim layer at 50–70% opacity, tinted from the palette's darkest tone. Cutout matches the target's shape with ≥ 8 pt padding, stays inside the safe area, and avoids the top banner-ad strip. |
| **Hand pointer** | Teaching a gesture | Animates the gesture itself: a press-bounce for tap, a trail for swipe, the full path for drag. It approaches from the side and stops short of the target so the finger image never hides what the player has to see. |
| **Arrow** | Direction or off-screen target | One arrow at a time, pointing at the target edge. |
| **Bubble** | The one fact the action can't show | ≤ 8 words, verb first, in the game's own terms ("Drag a crate onto the dock"). Placed beside the target, never over it. Text scales with the system font size (`docs/portfolio/font-scale.md`). |

## Timing

- **Let them try first.** The first hint waits ~2 s of idle after the step
  starts. A player who acts correctly before that skips the hint entirely.
- **Escalate on stall.** After ~5 s more of idle, strengthen the hint one
  level (bubble, then spotlight, then hand). Keep the same hint on screen
  instead of re-popping it.
- **Dismiss on success.** The hint disappears the moment the correct action
  lands, then the success feedback plays.
- **Respect action in progress.** A hint waits until the player's current
  gesture ends.

## Input gating

- **Soft step (default):** input passes through everywhere and the hint only
  guides. Use it whenever a wrong tap is harmless.
- **Forced step:** taps outside the cutout are absorbed. Use it only when a
  wrong tap would break the lesson or spend something irreversible. The
  cutout exposes the real control in its real position, so the lesson
  transfers to normal play.
- **Escape hatch:** a "Skip" control is visible from the first step, small,
  in a top corner, away from where the thumb rests. Skipping finishes the
  tutorial state cleanly: rewards granted, flags set, nothing left half-taught.

## Returning players and replays

- A persisted first-run flag (`docs/portfolio/persistence.md`) decides whether
  the tutorial runs. It runs once.
- Settings offers "Replay tutorial" for anyone who wants it back.
- After a reinstall with restored progress, the restored flag wins: no
  tutorial for a player who has already finished it.

## Progressive unlocks (after the core tutorial)

Secondary systems (shop, upgrades, daily reward, events) are taught
**just in time**: the first time each one becomes relevant, with one coach
mark on its entry point and nothing else. One new system per moment; if two
unlock together, queue the second for the next natural break.

- A locked feature shows its unlock condition on the locked element itself
  ("Reach level 5").
- The first visit to a newly unlocked screen gets one soft hint on its
  primary action, then the screen behaves normally.

## Monetization during the FTUE

Follow `docs/portfolio/monetization.md`: no interstitials during the first
session, and the top banner strip stays outside every spotlight and bubble.
The first session shows no IAP offer and no rewarded-ad prompt until the
core tutorial is finished. The first reward is free and lands in the HUD so
the player sees the economy before being asked to spend in it.

## Accessibility

- With reduced motion on, the hand pointer becomes a static hand plus an
  arrow, and the dim layer fades in instead of sliding.
- Every hint works without sound and without color: the spotlight's shape and
  the bubble's text carry the instruction.
- Bubble text meets 4.5:1 contrast against its own background, never against
  the dimmed game.

## Checklist

Walk every row against the plan; each gets an explicit pass or fail.

| Avoid | Instead |
|---|---|
| A text wall or slideshow before the first input | The first input within 5 s, rules taught by doing |
| A tour of every menu button on first launch | Each system taught when it first becomes relevant |
| A failable tutorial level | A simplified level where the first attempt succeeds |
| Hint on screen the instant the step starts | ~2 s of idle first; skip the hint for players who already acted |
| The same hint re-popping every few seconds | One hint that escalates one level on stall |
| Spotlight on a picture or copy of the control | The cutout exposes the live control in its real position |
| Hand pointer covering the target | Pointer approaches from the side and stops short |
| Skip hidden until the end, or missing | Skip visible from step one, in a top corner |
| Tutorial replaying on every launch | Persisted first-run flag; replay lives in Settings |
| Explaining what the screen already says ("Tap Continue to continue") | No hint where the control's own label teaches it |
| Full fanfare on every tutorial step | Frequent-tier feedback per step; one bigger beat at the end |
| Tutorial popup stacked over a reward or level-up popup | One overlay at a time, queued |
| Spotlight or bubble overlapping the top banner strip or a notch | Everything inside the safe area, below the banner |
| Dimming the text the player needs to read | Hint text on its own surface with full contrast |
| IAP or rewarded-ad prompt before the tutorial ends | Monetization appears after the first free reward has landed |

## Sources

Ideas drawn from Nintendo's teach-by-doing level design as described in game
UX practice, Celia Hodent's *The Gamer's Brain*, and the onboarding material
in `omer-metin/skills-for-antigravity` (`player-onboarding`, Apache-2.0) and
the `ftue` skill from `wolfgames/temp-colagame`. Wording here is original.
