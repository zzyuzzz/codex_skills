# Level Designer Reference

Use this reference for level layout, spatial flow, encounter pacing, grey-box/blockout plans, navigation readability, and environmental storytelling.

## Core Rules

- Keep the critical path visually legible unless disorientation is an explicit design goal.
- Use lighting, color, silhouette, landmarks, and geometry to guide attention.
- Give every junction a clear primary path and a readable optional path.
- Design difficulty spatially before increasing stats.
- Avoid enemies damaging the player before being readable, except telegraphed ambushes.
- Playtest grey boxes before art dressing. Art should reinforce readable layouts, not rescue unclear ones.
- Document layout changes with the playtest observation that caused them.

## Workflow

1. Write the level's emotional arc and one memorable moment.
2. Sketch a top-down flow with critical path, optional branches, encounter nodes, and pacing beats.
3. Build a grey box with untextured geometry.
4. Validate navigation without minimap reliance.
5. Tune encounters in isolation before connecting them.
6. Annotate art handoff constraints: gameplay-critical geometry, lighting intent, safe reshaping zones.
7. Run a final fresh-player playtest and measure confusion points.

## Level Design Document Template

```markdown
# Level: [Name/ID]

## Intent
**Player Fantasy**: [What the player should feel]
**Pacing Arc**: [Tension > Release > Escalation > Climax > Resolution]
**New Mechanic**: [How it is taught spatially]
**Narrative Beat**: [Story moment carried by the level]

## Layout Specification
**Shape Language**: [Linear / Hub / Open / Labyrinth]
**Estimated Playtime**: [X minutes]
**Critical Path**: [Meters, node count, or room list]
**Optional Areas**: [Area and reward]

## Encounter List
| ID | Type | Enemy Count | Tactical Options | Fallback Position |
|---|---|---:|---|---|
| E01 | [Ambush/Arena/Patrol] | [N] | [Flank/Cover/Verticality] | [Safe retreat] |
```

## Pacing Chart Template

```markdown
| Time | Activity | Tension | Notes |
|---|---|---:|---|
| 0:00 | Exploration | Low | Establish mood and landmark |
| 1:30 | Small encounter | Medium | Teach mechanic |
| 3:00 | Reward/exploration | Low | Release and world-building |
| 4:30 | Major encounter | High | Apply mechanic under pressure |
| 6:00 | Resolution | Low | Exit read and payoff |
```

## Blockout Room Spec

```markdown
## Room: [ID] - [Name]

**Dimensions**: [W]m x [D]m x [H]m
**Primary Function**: [Combat / Traversal / Story / Reward]
**Entry Read**: [What the player understands in the first 3 seconds]
**Cover/Traversal**: [Positions, height, risks]
**Lighting**: [Primary guide, secondary contrast, objective accents]
**Entry/Exit**: [Visibility and affordance]
**Environmental Story Beat**: [What happened here and what the player infers]
```

## Readability Checklist

- Exit or next goal is identifiable within 3 seconds of entering a room.
- Critical path is brighter, cleaner, or more strongly framed than optional paths.
- Dead ends do not look like exits.
- Enemies are readable before engagement.
- At least two tactical options are viable from entry.
- Optional rewards are visible from the choice point.

## Success Metrics

- Fresh players navigate the critical path without assistance.
- Actual pacing matches chart within about 20%.
- Each encounter shows at least two observed successful tactics.
- Environmental story is inferred by most playtesters without text prompts.
