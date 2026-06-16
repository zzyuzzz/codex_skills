# Technical Artist Reference

Use this reference for shaders, VFX, LOD chains, texture compression, asset import standards, rendering budgets, and art-to-engine pipeline work.

## Core Rules

- Define asset budgets before production starts: triangle counts, texture sizes, draw calls, particle count, overdraw, and shader complexity.
- Review assets in engine under target lighting, not only in DCC previews.
- Require LOD chains for hero assets and performance-sensitive props.
- Profile custom shaders with the engine's shader complexity tools before sign-off.
- Provide mobile-safe variants or explicit platform restrictions for custom shaders.
- Move work from pixel to vertex stage on mobile when possible.
- Use platform-specific texture overrides rather than downscaling source imports.
- Block broken pivots, scale, UVs, non-manifold geometry, and naming issues at import.

## Workflow

1. Publish budget sheets per asset category.
2. Set import presets and naming conventions before art production.
3. Prototype shaders visually, then optimize in code if needed.
4. Document exposed shader parameters with ranges and tooltips.
5. Review first import: pivot, scale, UVs, poly count, materials.
6. Validate LOD transitions in engine.
7. Profile worst-case density scenes and record before/after metrics.

## Asset Budget Template

```markdown
# Asset Technical Budgets - [Project]

## Characters
| LOD | Max Tris | Texture Res | Draw Calls |
|---|---:|---|---:|
| LOD0 | 15000 | 2048x2048 | 2-4 |
| LOD1 | 8000 | 1024x1024 | 2 |
| LOD2 | 3000 | 512x512 | 1 |
| LOD3 | 800 | 256x256 | 1 |

## Hero Props
| LOD | Max Tris | Texture Res |
|---|---:|---|
| LOD0 | 4000 | 1024x1024 |
| LOD1 | 1500 | 512x512 |
| LOD2 | 400 | 256x256 |
```

## Texture Compression Defaults

```markdown
| Type | PC | Mobile | Console |
|---|---|---|---|
| Albedo | BC7 | ASTC 6x6 | BC7 |
| Normal | BC5 | ASTC 6x6 | BC5 |
| Roughness/AO | BC4 | ASTC 8x8 | BC4 |
| UI Sprites | BC7 | ASTC 4x4 | BC7 |
```

## VFX Audit Checklist

```markdown
## VFX Effect Review: [Effect]

**Platform**: [PC / Console / Mobile]
- [ ] Worst-case particle count measured: ___
- [ ] Overdraw visualizer checked: ___ layers
- [ ] Mobile overdraw <= 3 layers, PC <= 6 layers
- [ ] Shader complexity map checked
- [ ] Particle textures use atlas where practical
- [ ] GPU frame contribution measured: ___ ms
- [ ] Effect remains readable from normal gameplay camera distances
```

## LOD Validation Logic

```python
LOD_BUDGETS = {
    "character": [15000, 8000, 3000, 800],
    "hero_prop": [4000, 1500, 400],
    "small_prop": [500, 200],
}

def validate_lod_chain(asset_name, asset_type, lod_poly_counts):
    errors = []
    budgets = LOD_BUDGETS.get(asset_type)
    if not budgets:
        return [f"Unknown asset type: {asset_type}"]
    for i, (count, budget) in enumerate(zip(lod_poly_counts, budgets)):
        if count > budget:
            errors.append(f"{asset_name} LOD{i}: {count} exceeds {budget}")
    return errors
```

## Success Metrics

- No shipped asset exceeds its LOD or texture budget.
- Rendering frame time stays within budget on the lowest target hardware.
- Custom shaders have safe variants or platform restrictions.
- VFX overdraw remains within platform limits in worst-case gameplay.
- Artists need fewer revisions because constraints were clear up front.
