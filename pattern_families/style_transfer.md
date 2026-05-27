# Style Transfer Bleed

## Failure Mode
Neural style transfer applied to a garment image causes the learned style to bleed across seam boundaries — the algorithm doesn't respect the physical joins between panels. Style from one fabric panel leaks into adjacent panels; structural seams become zones of style contamination.

## Visual Signature
- Style textures that cross seam lines without respecting the physical join
- Different fabric panels that should be distinct now share leaked stylistic elements
- Seam areas show the highest contamination: a gradient of style bleed fading with distance from the seam
- Pattern elements from one panel appear as ghosts in adjacent panels
- The garment reads as a single image rather than assembled pieces — seam structure erased by style

## Failure Origin
The style transfer algorithm was applied to a flat photograph of the assembled garment, treating it as a single image. Seam boundaries were not masked or respected as panel boundaries.

## Bleed Patterns
| Panel Configuration | Bleed Behavior |
|--------------------|----------------|
| Bodice → sleeve | Style texture crosses shoulder seam |
| Front → back | Back picks up front panel's style characteristics |
| Collar → bodice | Collar style saturates into neckline area |
| Lining → shell | Interior style bleeds through to exterior in photographs |

## Shader Snippet
```glsl
vec3 style_bleed(vec2 uv, float seam_pos, vec3 style_a, vec3 style_b, float bleed_radius) {
    float dist_to_seam = abs(uv.x - seam_pos);
    float bleed_factor = exp(-dist_to_seam / bleed_radius);
    vec3 local_style = uv.x < seam_pos ? style_a : style_b;
    vec3 foreign_style = uv.x < seam_pos ? style_b : style_a;
    return mix(local_style, foreign_style, bleed_factor * 0.4);
}
```

## Prompt Template
> "A blazer where neural style transfer has been applied — the houndstooth pattern of the main body bleeds across the shoulder seam into the sleeve, the sleeve's herringbone style contaminating the collar area, seams invisible because the style transfer treats the whole garment as one canvas, patterns leaking through physical joins"

## Anti-Drift Notes
- Style bleed is **strongest at seam boundaries** and fades with distance
- The bleed is **bidirectional** — both panels contaminate each other
- Seam structure becomes **invisible** under heavy bleed — this is the key diagnostic
