# Narrative Designer Reference

Use this reference for story systems, branching dialogue, character voice, lore architecture, environmental storytelling, and story-gameplay integration.

## Core Rules

- Every line should sound like a real person in that situation, not like exposition.
- Give every dialogue node a dramatic function: reveal, establish relationship, create pressure, or deliver consequence.
- Define character voice pillars before drafting dialogue.
- Make choices differ in kind, not just tone or degree.
- Map branches before writing lines to avoid dead ends.
- Let the player feel consequences, even when subtle.
- Keep critical path story understandable without optional lore.
- Ensure environmental storytelling, dialogue, and world bible facts do not contradict.

## Workflow

1. Define the central thematic question.
2. Align narrative pillars with game design pillars.
3. Map acts, turning points, branches, and consequence timing.
4. Create voice pillar docs for speaking characters.
5. Draft in engine-ready formats such as Ink, Yarn, Twine, or the project's custom syntax.
6. Revise in passes: function, voice, brevity.
7. Test branches for convergence and consequence visibility.

## Character Voice Pillars Template

```markdown
## Character: [Name]

**Role in Story**: [Role]
**Core Wound**: [What shaped their worldview]
**Desire**: [Conscious want]
**Need**: [Actual need]

### Voice
- **Vocabulary**: [Formal/casual, technical/colloquial]
- **Sentence Rhythm**: [Short, clipped, winding, lyrical]
- **Avoided Topics**: [What they avoid saying directly]
- **Verbal Tics**: [Specific habits]
- **Subtext Default**: [Direct or indirect]

### Never Say
- [Line that would be wrong] - [Why]

### Reference Lines
- "[Approved line]" - [What it demonstrates]
```

## Dialogue Node Template

```text
// Scene: [Scene name]
// Tone: [Emotional pressure]

[CHARACTER]: "[Opening line]"
-> [Choice prompt]
    + "[Choice A]" [Intent tag]
        [CHARACTER]: "[Response]"
        -> [state_a]
    + "[Choice B]" [Intent tag]
        [CHARACTER]: "[Response]"
        -> [state_b]

= [state_a]
[Consequence or convergence]
-> scene_continue
```

## Lore Tier Template

```markdown
# Lore Tiers: [World]

## Tier 1: Surface
Critical path facts every player needs.

## Tier 2: Engaged
Optional NPCs, notes, side quests, and discoverable scenes.

## Tier 3: Deep
Hidden connections, secrets, and inference-heavy material.

## World Bible Guardrails
- **Timeline**: [Key events]
- **Factions**: [Goals and relationships]
- **Rules of the World**: [What is possible]
- **Banned Retcons**: [Facts that cannot be contradicted]
```

## Story-Gameplay Matrix

```markdown
| Story Beat | Gameplay Consequence | Player Feeling | Validation |
|---|---|---|---|
| Ally betrayal | Vendor unavailable | Loss, recalibration | Player notices within 2 beats |
| Truth revealed | New area unlocked | Realization, urgency | Objective changes immediately |
| Choice to spare | Reputation shift | Agency | NPC dialogue updates |
```

## Success Metrics

- Players identify major character personalities from dialogue alone.
- Branching choices produce observable consequences within two scenes or beats.
- Critical path story works without optional lore.
- Reviews find no "as you know" exposition.
- Environmental story beats are inferred without explicit text.
