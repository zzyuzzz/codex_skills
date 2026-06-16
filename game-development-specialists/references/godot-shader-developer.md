# Godot Shader Developer Reference

Use this reference for Godot 4 CanvasItem, Spatial, particles, VisualShader, renderer compatibility, post-processing, and shader performance work.

## Core Rules

- Godot shading language is not raw GLSL. Use Godot built-ins such as `TEXTURE`, `UV`, `COLOR`, and `FRAGCOORD`.
- Declare `shader_type` at the top of every shader: `canvas_item`, `spatial`, `particles`, or `sky`.
- Use `texture()`, not Godot 3-era `texture2D()`.
- In `spatial` shaders, treat `ALBEDO`, `METALLIC`, `ROUGHNESS`, and `NORMAL_MAP` as outputs.
- Identify renderer target before implementation: Forward+, Mobile, or Compatibility.
- Avoid `SCREEN_TEXTURE` on mobile unless the effect explicitly justifies the framebuffer copy.
- Count fragment texture samples; they are usually the primary cost.
- Expose artist-facing values as `uniform` with hints such as `hint_range`, `source_color`, or `hint_normal`.
- Avoid dynamic fragment loops on mobile.
- Use VisualShader for artist-extensible graphs; use code shaders for complex or performance-critical work.

## Workflow

1. Define the visual target with a reference or concise effect description.
2. Choose shader type: `canvas_item` for 2D/UI, `spatial` for 3D, `particles` for particle behavior.
3. Determine renderer requirements before writing code.
4. Prototype in VisualShader if artist iteration is important.
5. Port to code shader when performance or maintainability requires it.
6. Add uniform hints and document renderer restrictions in comments.
7. Profile draw calls, material changes, shader compile time, and GPU frame cost.

## CanvasItem Outline Shader

```glsl
shader_type canvas_item;

uniform vec4 outline_color : source_color = vec4(0.0, 0.0, 0.0, 1.0);
uniform float outline_width : hint_range(0.0, 10.0) = 2.0;

void fragment() {
    vec4 base_color = texture(TEXTURE, UV);
    vec2 texel = TEXTURE_PIXEL_SIZE * outline_width;
    float alpha = 0.0;
    alpha = max(alpha, texture(TEXTURE, UV + vec2(texel.x, 0.0)).a);
    alpha = max(alpha, texture(TEXTURE, UV + vec2(-texel.x, 0.0)).a);
    alpha = max(alpha, texture(TEXTURE, UV + vec2(0.0, texel.y)).a);
    alpha = max(alpha, texture(TEXTURE, UV + vec2(0.0, -texel.y)).a);

    vec4 outline = outline_color * vec4(1.0, 1.0, 1.0, alpha * (1.0 - base_color.a));
    COLOR = base_color + outline;
}
```

## Spatial Dissolve Shader

```glsl
shader_type spatial;

uniform sampler2D albedo_texture : source_color;
uniform sampler2D dissolve_noise : hint_default_white;
uniform float dissolve_amount : hint_range(0.0, 1.0) = 0.0;
uniform float edge_width : hint_range(0.0, 0.2) = 0.05;
uniform vec4 edge_color : source_color = vec4(1.0, 0.4, 0.0, 1.0);

void fragment() {
    vec4 albedo = texture(albedo_texture, UV);
    float noise = texture(dissolve_noise, UV).r;

    if (noise < dissolve_amount) {
        discard;
    }

    ALBEDO = albedo.rgb;
    float edge = step(noise, dissolve_amount + edge_width);
    EMISSION = edge_color.rgb * edge * 3.0;
    METALLIC = 0.0;
    ROUGHNESS = 0.8;
}
```

## Shader Audit Checklist

```markdown
## Godot Shader Review: [Effect]

**Shader Type**: [canvas_item / spatial / particles]
**Renderer Target**: [Forward+ / Mobile / Compatibility]
- [ ] `shader_type` declared
- [ ] Renderer requirements documented
- [ ] Fragment texture sample count: ___
- [ ] All uniforms have hints
- [ ] No unbounded dynamic loops in fragment stage
- [ ] `SCREEN_TEXTURE` use justified or absent
- [ ] Mobile opaque shader avoids unnecessary `discard`
- [ ] Effect measured in Rendering Profiler
```

## Success Metrics

- Shaders compile in the stated Godot 4 renderer target.
- Artist-facing uniforms have useful hints.
- Mobile-targeted shaders pass Compatibility or Mobile renderer constraints.
- `SCREEN_TEXTURE` and `DEPTH_TEXTURE` uses are documented and justified.
- Visual output matches the reference within the target performance budget.
