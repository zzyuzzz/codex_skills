# Game Audio Engineer Reference

Use this reference for FMOD/Wwise integration, adaptive music, SFX event architecture, spatial audio, voice limits, memory budgets, and audio performance.

## Core Rules

- Route production audio through middleware events such as FMOD or Wwise unless explicitly prototyping.
- Trigger SFX via event references or named event strings, not hardcoded asset paths.
- Keep audio logic in middleware. Game systems should drive parameters such as intensity, wetness, occlusion, or health.
- Give every event a voice limit, priority, and steal mode.
- Stream music, ambience, and VO. Decompress short SFX to memory.
- Use tempo-synced music transitions unless a hard cut is an intentional design choice.
- Spatialize world-space diegetic sounds in 3D.
- Drive occlusion through raycast-based parameters.

## Workflow

1. Define sonic identity with three adjectives.
2. List gameplay states that require unique audio responses.
3. Define adaptive parameters before composition.
4. Establish event hierarchy, bus structure, VCA assignments, and platform overrides.
5. Implement SFX as randomized containers where repetition would be noticeable.
6. Test one-shots at maximum expected simultaneous count.
7. Profile CPU, memory, voice count, streaming hitches, and spatial raycasts on the lowest target platform.

## Event Naming Convention

```text
event:/[Category]/[Subcategory]/[EventName]

event:/SFX/Player/Footstep_Concrete
event:/SFX/Weapons/Gunshot_Pistol
event:/SFX/Environment/Waterfall_Loop
event:/Music/Exploration/Forest_Day
event:/UI/Button_Click
event:/VO/NPC/[CharacterID]/[LineID]
```

## Adaptive Music Parameters

```markdown
## CombatIntensity (0.0-1.0)
- 0.0: Exploration only
- 0.3: Alert state, light percussion
- 0.6: Active combat, full arrangement
- 1.0: Boss or critical state

**Source**: AI threat, health, or combat state aggregator
**Update Rate**: Every 0.5 seconds, smoothed
**Transition**: Beat-quantized
```

## Audio Budget Template

```markdown
# Audio Performance Budget - [Project]

## Voice Count
| Platform | Max Voices | Virtual Voices |
|---|---:|---:|
| PC | 64 | 256 |
| Console | 48 | 128 |
| Mobile | 24 | 64 |

## Memory
| Category | Budget | Format | Policy |
|---|---:|---|---|
| SFX | 32 MB | ADPCM | Decompress RAM |
| Music | 8 MB | Vorbis | Stream |
| Ambience | 12 MB | Vorbis | Stream |
| VO | 4 MB | Vorbis | Stream |

## CPU
- Middleware DSP: [PLACEHOLDER] ms/frame on lowest hardware.
- Spatial audio raycasts: [PLACEHOLDER] per frame, staggered.
```

## Spatial Audio Spec

```markdown
## 3D Audio Configuration

**Attenuation**: [Min distance], [Max distance], [rolloff]
**Occlusion**: Raycast listener to source; parameter `Occlusion` from 0 open to 1 blocked.
**Low-pass at max occlusion**: [PLACEHOLDER] Hz.
**Reverb Zones**:
| Zone | Pre-delay | Decay | Wet |
|---|---:|---:|---:|
| Outdoor | 20ms | 0.8s | 15% |
| Indoor | 30ms | 1.5s | 35% |
| Cave | 50ms | 3.5s | 60% |
```

## Success Metrics

- No audio-caused frame hitches on target hardware.
- No event ships with default voice/priority/steal settings.
- Music transitions feel seamless across tested state changes.
- Audio memory remains within budget at maximum content density.
- Occlusion and reverb are active for world-space diegetic sounds.
