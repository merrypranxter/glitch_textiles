# Datamoshed Plaid

## Failure Mode
Color channels (RGB) are shifted horizontally by a fixed number of threads within a woven repeat. The glitch originates from treating the fabric's color data as a raw pixel buffer and displacing one or two channels independently.

## Visual Signature
- Red and/or green channels offset from blue by 2–8 thread widths
- Thread intersections show impossible color combinations (magenta warp over cyan weft where the pattern says it should be white)
- The plaid grid remains structurally intact; only the color registration is broken
- Fringe zones at channel-shift boundaries where three palettes briefly overlap

## Failure Origin
Datamosh-style: the motion-compensation frame from one color plane is applied to a different plane. In textile terms: the loom's color program was loaded with a per-channel memory offset.

## Shader Parameters
| Parameter | Suggested Value |
|-----------|----------------|
| `channel_shift` | 0.03–0.07 |
| `glitch_frequency` | 0.4–0.8 |
| `error_seed` | any |

## Shader Snippet
```glsl
vec3 datamosh_plaid(vec2 uv, float shift) {
    float r = texture(plaid, uv + vec2(shift, 0.0)).r;
    float g = texture(plaid, uv - vec2(shift * 0.5, 0.0)).g;
    float b = texture(plaid, uv).b;
    return vec3(r, g, b);
}
```

## Prompt Template
> "A datamoshed tartan where red and green color channels have shifted horizontally by 3 threads, creating RGB-split woven bands, some thread intersections showing impossible color combinations, digital corruption of traditional textile"

## Anti-Drift Notes
- Channel shift **only works on multi-color patterns** — monochrome plaids cannot exhibit this glitch
- The plaid structure (crossing bands) must still be legible; total chaos is not datamoshing, it's noise
- Shift direction is always horizontal (weft direction); vertical shifts indicate a different error class
