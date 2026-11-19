# Reward screens and UI juice

Playbook for how game screens *feel*: button feedback, the results screen
(win, lose, level complete), reward and level-up popups, chest or pack
reveals, and the feedback tier behind each one. Back to
[SKILL.md](../SKILL.md). Gameplay feel (hit-stop, camera shake on impacts,
character animation) belongs to the gameplay code, not here; this file covers
the UI layer around it.

The leading idea: **earned juice.** Feedback is information first, and its
size matches how rare and meaningful the moment is. A big response only reads
as big against quiet around it, so most of the screen stays calm and the
largest celebration is kept for the rarest event.

## Feedback tiers

Assign every feedback moment on the screen a tier before choosing effects.

| Tier | Typical moments | Channels and starting values |
|---|---|---|
| **Frequent** | Button press, tapping a cell, collecting a single coin, a tutorial step | Press scale + short sound. Optional light haptic on primary actions only. No particles, no screen effects. |
| **Occasional** | A star earned, a combo, a small level-up, an item added to inventory | Pop (scale up to ~1.2–1.3 and settle), sound with rising pitch on streaks, a small particle burst (6–12), light haptic. |
| **Rare** | 3-star clear, new personal record, boss or chapter clear, a top-rarity reveal | Anticipation beat, full pop, larger burst, color shift, medium haptic, the one moment on the screen that may move the camera or flash the background. One per screen at most. |

Every relevant event gets *some* cue, so nothing feels dead; the ladder keeps
the big ones meaningful. Exaggerate the game's one core verb more than
anything else.

## Motion and sound defaults

Starting values to tune by eye and playtest.

- **Press:** scale to 0.92–0.95 over 50–90 ms, release back with a slight
  overshoot (ease-out-back) over 150–250 ms. The action registers on release
  at the start of the animation; the animation never delays the result.
- **Disabled control:** no press animation and no sound; dimmed, with the
  reason shown on or beside it ("Need 200 coins").
- **Easing:** ease-out for things arriving, ease-in for things leaving,
  overshoot for things that should feel squishy. Linear motion is for
  mechanical movement only (a conveyor, a progress fill at constant rate).
- **Anticipation:** rare moments get a short wind-up (100–300 ms of build:
  a pulse, a glow gathering, a shake that grows) before the payoff.
- **Sound:** every visual feedback beat has a sound. Repeated sounds vary
  pitch by ±5–10% and climb in pitch across a streak (stars, coins ticking).
- **Particles:** fewer, bigger, shorter: 6–24 per burst, 0.3–0.6 s life,
  always behind the numbers they celebrate.

## Results screen: the reveal sequence

**Verdict first, actions last.** The screen tells the story in a fixed order,
one beat at a time, each beat landing before the next starts:

1. **Verdict.** Win, lose, or level complete, in the screen's largest type.
   Arrives within 300 ms of the level ending.
2. **Performance.** Stars appear one at a time, 250–400 ms apart, each with a
   higher pitch than the last. The score counts up over 0.6–1.2 s whatever
   its size (scale the step, never the duration). "New record" appears only
   when the record is real.
3. **Rewards.** Each reward pops in, then flies to where it lives: coins to
   the coin counter in the top bar, items to the inventory icon. The counter
   ticks up on arrival. A reward that lands nowhere teaches the player
   nothing about the economy.
4. **Progress.** The XP or chapter bar fills; a level-up is its own beat,
   after the fill, never on top of it. A next-unlock preview may close this
   beat.
5. **Actions.** Buttons appear last, so a tap meant to skip the animation
   never presses one. The primary action (Next, Continue) sits in the thumb
   zone at full size; secondary actions (Retry, Home) are smaller and to the
   side.

Rules that hold for every results screen:

- **Budget:** 2–3.5 s from verdict to actions for a normal win; up to ~5 s
  when a rare-tier moment is present.
- **Tap to fast-forward:** a tap anywhere jumps to the final state of the
  sequence with every value shown. The sequence is skippable from its first
  frame, every time.
- **State first, show second:** rewards and progress are saved before the
  sequence starts (`docs/portfolio/persistence.md`). Backgrounding the app
  mid-reveal loses nothing.
- **One tier per beat:** a 1-star clear runs at the occasional tier; only a
  3-star clear or a record earns the rare tier.

### Rewarded ads and interstitials on this screen

Following `docs/portfolio/monetization.md`:

- A "×2 with ad" or similar offer appears with the actions in beat 5, as a
  secondary, opt-in button, never larger than the free Continue and never
  replacing it. The reward it doubles is already credited and visible.
- An interstitial plays only after the player taps Continue, never over the
  reveal and never before rewards are credited.
- The top banner strip stays clear; the verdict and the top-bar counters sit
  below it.

### Lose screen

- Lead with progress: what the run achieved (distance, % of the level,
  best combo), then the verdict. The player reappraises the run instead of
  quitting.
- Retry is the primary action, in the thumb zone.
- A revive offer (rewarded ad or currency) shows its cost plainly, gives at
  least 5 s to decide, and has a dismiss control the same size class as the
  offer. Declining is one tap.
- Calm tier throughout: no shake, no red flashing.

## Reward popups and queues

Level-ups, achievements, daily rewards, and unlocks often fire together.
**One popup at a time**, in priority order (progress before cosmetics), each
dismissed before the next appears. Combine same-kind rewards into one popup
("+3 items") instead of three. A popup arriving during gameplay waits for the
next natural break.

## Chest, pack, and gacha reveals

- **Anticipation scales with rarity:** 0.5–1 s of build for a common item,
  longer and stronger for higher tiers. The build itself tells the player
  something good is coming.
- **Rarity reads without color alone:** frame shape, a label ("Epic"), and
  particle intensity carry it alongside the color.
- **Skip:** tapping during the build jumps to the result; a multi-item pack
  offers "reveal all".
- **Odds:** paid random rewards show their drop odds before purchase, as the
  App Store and Google Play require.

## Accessibility and restraint

- Flashes stay at 3 per second or fewer, and avoid saturated red flashes.
- Settings carry toggles for screen shake, haptics, and reduced motion; the
  system reduced-motion setting turns the reveal into fades with the final
  state shown immediately.
- Information never lives only in motion, sound, or color: every value the
  animation celebrates is also printed on screen.
- Particles and effects stay behind numbers and buttons.

## Checklist

Walk every row against the plan; each gets an explicit pass or fail.

| Avoid | Instead |
|---|---|
| Every element animating in at once | One beat at a time: verdict, performance, rewards, progress, actions |
| The same fanfare for 1 star and 3 stars | Tier matched to the result; rare tier only for the rare result |
| Confetti or particles on every screen | Particles reserved for occasional and rare moments |
| A score count-up that takes longer for bigger numbers | 0.6–1.2 s fixed duration, bigger steps for bigger numbers |
| Rewards shown in the middle and then vanishing | Rewards fly to their counter in the top bar and tick it up |
| Buttons visible during the reveal, catching skip taps | Actions appear last, after the sequence |
| An unskippable reveal | Tap anywhere fast-forwards to the final state |
| "×2 with ad" larger than Continue, or replacing it | Opt-in secondary button beside a full-size free Continue |
| Interstitial over the reveal | Interstitial after the player taps Continue |
| Popups stacked on popups | One popup at a time, queued by priority |
| Linear tweens on feedback | Ease-out in, ease-in out, overshoot for squish |
| A silent visual effect | A sound on every feedback beat, pitch-varied |
| Lose screen leading with failure in red | Progress first, calm tier, Retry as primary |
| Generic praise ("AWESOME!!", "Amazing!") | A specific line from the result, written through `ux-slop` |
| Disabled button that still bounces and clicks | No feedback on disabled controls; the reason shown instead |

## Sources

Principles drawn from Steve Swink's *Game Feel*, Jesse Schell's *The Art of
Game Design*, Celia Hodent's *The Gamer's Brain*, Vlambeer's "The Art of
Screenshake" talk, and the juice material in `m4bwav/game-juice` (MIT) and the
`game-juice` skill in `JSON-OBJECT/claude-code`. Wording and the results-screen
sequence here are original.
