# Wrong Dye Lot

## Failure Mode
A dye lot change occurs mid-fabric roll. Different production batches of the same dye color produce slightly (or dramatically) different shades. When the roll switches from one lot to another, an abrupt color step appears across the full width of the fabric.

## Visual Signature
- A horizontal line (perpendicular to selvedge) where one shade of a color becomes another
- Both sides of the line show the same pattern, texture, and structure — only the color value changes
- The shift can be subtle (same hue, slightly different value) or dramatic (different hue family)
- Multiple lot changes = multiple horizontal color bands, like geological strata
- Selvedge stamps/lot numbers in the edge may show the transition

## Failure Origin
Dye supplier changed formulation; natural dye variation from harvest to harvest; production batch exhausted mid-run; operator switched dye tanks at wrong moment.

## Lot Change Frequency
| Industry | Typical Lot Size | Change Visibility |
|----------|-----------------|-------------------|
| Fashion fabric | 50–200m | High if visible garment color |
| Upholstery | 100–500m | Medium |
| Industrial | 500m+ | Low, controlled closely |
| Natural dye | 2–10m | Very high, intentional variation |

## Shader Snippet
```glsl
vec3 wrong_dye_lot(vec2 uv, float break_y, vec3 color_a, vec3 color_b, float softness) {
    float t = smoothstep(break_y - softness, break_y + softness, uv.y);
    vec3 pattern_mask = texture(pattern, uv).rgb;
    vec3 lot_a = mix(background_a, color_a, pattern_mask.r);
    vec3 lot_b = mix(background_b, color_b, pattern_mask.r);
    return mix(lot_a, lot_b, t);
}
```

## Prompt Template
> "A continuous roll of navy herringbone tweed where a dye lot change at the 2-meter mark shifts the navy from a blue-navy to a purple-navy — the pattern identical on both sides of the line, the weave structure identical, only the precise color of the dye different, a geological stratum in cloth"

## Anti-Drift Notes
- Wrong dye lot creates a **horizontal line** (weft direction) across the full width
- Both colors are **valid production colors** — not errors in the dye, just different batches
- The pattern **continues unchanged** through the lot break
