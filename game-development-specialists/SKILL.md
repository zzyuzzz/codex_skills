---
name: game-development-specialists
description: Role-based game development guidance distilled from specialist briefs for game design, level design, narrative design, game audio, technical art, and Godot 4 engineering. Use when Codex needs to design or review gameplay systems, GDD sections, mechanics, economies, onboarding, levels, encounters, environmental storytelling, dialogue branches, lore, adaptive audio, FMOD/Wwise integration, shaders, VFX, asset budgets, LODs, art-to-engine pipelines, Godot GDScript/C# gameplay architecture, Godot multiplayer, or Godot shader work.
---

# Game Development Specialists

Use this skill as a lightweight game development expert system. Select the needed discipline, read only the matching reference file, then produce buildable design guidance with concrete constraints, deliverables, and validation criteria.

## Discipline Router

- Gameplay systems, mechanics, economy, progression, onboarding, player psychology, GDD sections: read `references/game-designer.md`.
- Level layout, pacing, encounter design, grey-box/blockout specs, navigation readability, environmental story through space: read `references/level-designer.md`.
- Dialogue, branching story, character voice, lore tiers, world bible, story-gameplay consequences: read `references/narrative-designer.md`.
- FMOD/Wwise, adaptive music, SFX events, bus structure, spatial audio, audio budgets, voice limits: read `references/game-audio-engineer.md`.
- Shaders, VFX, LODs, texture compression, asset import rules, rendering budgets, art pipeline checks: read `references/technical-artist.md`.
- Godot 4 gameplay code, GDScript 2.0, C# interop, signal architecture, Autoload hygiene, scene composition: read `references/godot-gameplay-scripter.md`.
- Godot 4 networking, MultiplayerAPI, RPCs, authority, MultiplayerSpawner, MultiplayerSynchronizer, ENet/WebRTC: read `references/godot-multiplayer-engineer.md`.
- Godot 4 CanvasItem/Spatial shaders, VisualShader, renderer compatibility, post-processing, shader performance: read `references/godot-shader-developer.md`.

If a request spans several disciplines, read the smallest set of references that covers the work. Combine their outputs through shared design pillars, production constraints, and testable acceptance criteria.

## Working Process

1. Identify the game context: genre, target platform, engine, player fantasy, production stage, and requested output.
2. Select the relevant discipline reference files. If key context is missing, make conservative assumptions and label them.
3. Lead with player experience and production constraints before implementation detail.
4. Produce practical artifacts: specs, tables, checklists, diagrams, tuning variables, or implementation notes.
5. Mark untested numbers as `[PLACEHOLDER]` and define how to validate them.
6. Include edge cases, failure states, dependencies, and handoff notes when the work crosses disciplines.

## Output Standards

- Make every recommendation actionable by designers, artists, engineers, writers, or audio implementers.
- Prefer measurable budgets, named parameters, and explicit pass/fail checks over vague advice.
- Separate observation, design intent, and implementation suggestion.
- Treat all numbers as hypotheses until playtested or profiled.
- Tie narrative, audio, visuals, levels, and mechanics back to gameplay state and player emotion.

## Common Multi-Discipline Handoffs

- For a new feature: start with game design, then add technical art or audio constraints as needed.
- For a level: start with level design, then layer narrative beats, audio zones, and performance budgets.
- For a story quest: start with narrative design, then add gameplay consequences and level/environmental requirements.
- For a polished combat beat: combine game design, level design, audio, and technical art.
- For a Godot implementation task: combine the design reference with the matching Godot engineering reference.
