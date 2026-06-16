# Game Designer Reference

Use this reference for gameplay systems, mechanics, economies, progression, onboarding, GDD authorship, and balance work.

## Core Rules

- Document every mechanic with purpose, player experience goal, inputs, outputs, edge cases, failure states, tuning levers, and dependencies.
- Design from player motivation outward, not from a feature list inward.
- Avoid complexity unless it adds meaningful choice.
- Treat all numerical values as hypotheses. Mark untested numbers `[PLACEHOLDER]`.
- Build tuning spreadsheets or tables alongside design docs.
- Define what "broken" means before playtesting.

## Workflow

1. Define 3 to 5 design pillars and the player fantasy.
2. Identify the fun hypothesis: the one interaction that must feel good.
3. Sketch the core loop before implementation.
4. Write mechanics from the player's perspective first, then add implementation notes.
5. Define tuning levers, target curves, and failure thresholds.
6. Run paper simulations or simple prototypes before production integration.
7. Separate playtest observation from interpretation.

## Mechanic Spec Template

```markdown
## Mechanic: [Name]

**Purpose**: [Why this mechanic exists]
**Player Fantasy**: [What emotion or power it delivers]
**Input**: [Button, trigger, timer, event]
**Output**: [State/resource/world change]
**Success Condition**: [What correct behavior looks like]
**Failure State**: [What happens when it goes wrong]
**Edge Cases**:
- [Simultaneous event or conflicting state]
- [Min/max resource condition]
**Tuning Levers**: [Variables controlling feel or balance]
**Dependencies**: [Systems this touches]
```

## Core Loop Template

```markdown
# Core Loop: [Game Title]

## Moment-to-Moment
- **Action**: [Player verb]
- **Feedback**: [Visual/audio/haptic response]
- **Reward**: [Resource/progression/intrinsic payoff]

## Session Loop
- **Goal**: [Objective]
- **Tension**: [Risk/resource pressure]
- **Resolution**: [Win/fail state and consequence]

## Long-Term Loop
- **Progression**: [Unlock/meta-progression]
- **Retention Hook**: [Reason to return]
```

## Balance Table Template

```markdown
| Variable | Base | Min | Max | Rationale | Test |
|---|---:|---:|---:|---|---|
| Player HP | 100 | 50 | 200 | [PLACEHOLDER] baseline survivability | Time-to-death test |
| Enemy Damage | 15 | 5 | 40 | [PLACEHOLDER] level 5 pressure | Damage intake simulation |
| Ability Cooldown | 8s | 3s | 15s | [PLACEHOLDER] prevents spam | Feel test at low/high skill |
```

## Onboarding Checklist

- Introduce the core verb within the first 30 seconds of control.
- Guarantee first success in the initial tutorial beat.
- Introduce each new mechanic in a safe, low-stakes context.
- Let the player discover at least one mechanic through play rather than instruction text.
- End the first session with an unlock, cliffhanger, or "one more try" hook.

## Success Metrics

- Every mechanic has an unambiguous spec.
- Playtests produce concrete tuning changes.
- Economy has no infinite sources, dead-end sinks, or dominant path.
- Onboarding can be completed without designer assistance.
- Core loop is fun before secondary systems are added.
