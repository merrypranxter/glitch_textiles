# Bleed Error

## Failure Mode
Excessive dye diffusion causes color to migrate beyond its intended boundaries into adjacent areas. The dye "bleeds" through the fabric's capillary structure, destroying crisp edges and creating soft, undefined color zones.

## Visual Signature
- Hard-edged pattern elements become soft and blurred
- Color appears to radiate outward from its intended area like ink on wet paper
- Where two bleeding colors meet: an unexpected mix zone (tertiary color) forms at the boundary
- Fine detail is the first to disappear — thin lines become blobs, sharp corners become rounded
- The center of a color field remains strongest; edges trail off into the adjacent ground color

## Failure Origin
Excess dye applied; binder/resist not properly set before steaming; fabric too wet during application; wrong fabric fiber (high dye affinity fibers wick aggressively); temperature too high during fixation.

## Bleed Types
| Type | Cause | Visual |
|------|-------|--------|
| Capillary bleed | Wet fabric before printing | Soft, organic edges |
| Steaming bleed | Too much steam/too long | Uniform softening of all edges |
| Migration bleed | Dye moved after setting | Halo at distance from original mark |
| Color mixing bleed | Adjacent wet colors meet | Tertiary zone between two colors |

## Shader Snippet
```glsl
vec3 bleed_error(vec2 uv, float radius, sampler2D pattern_tex) {
    vec3 sum = vec3(0.0);
    for (int i = 0; i < 16; i++) {
        vec2 offset = vec2(cos(float(i) * PI / 8.0), sin(float(i) * PI / 8.0)) * radius;
        sum += texture(pattern_tex, uv + offset).rgb;
    }
    return sum / 16.0; // Approximates radial bleed via averaged samples
}
```

## Prompt Template
> "A traditional block-printed floral where all the dye has bled excessively — petals that should have crisp black outlines now have soft 3mm halos, red flowers bleeding into white ground creating pink zones, adjacent colors mixing where they touch, the pattern readable only from a distance, detail destroyed"

## Anti-Drift Notes
- Bleed error creates **soft edges**, not hard offsets — contrast with misregistration
- Fine details are **disproportionately affected** — thick lines survive, thin lines disappear
- Where bleeding colors meet, a **third color** is created — not just the two originals blurring
