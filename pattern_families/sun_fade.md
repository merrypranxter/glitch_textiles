# Sun Fade

## Failure Mode
Selective UV degradation causes differential color loss across a fabric. Some dyes fade faster than others under UV exposure; if part of the fabric was shielded (folded, covered, in shadow), ghost patterns of the original color remain while exposed areas have shifted.

## Visual Signature
- A ghost of the original color in protected areas; faded, bleached version in exposed areas
- The ghost pattern corresponds to whatever physical object shielded the fabric (fold crease, another fabric panel, furniture leg, window frame)
- Non-photostable dyes fade first: turquoise, magenta, yellow often before navy, black, red
- The fade gradient follows light geometry — most fade at window side, least at interior
- Where multiple dyes were mixed: one component fades, shifting the color toward the survivor

## Fade Vulnerability by Dye Class
| Dye Type | UV Resistance | Fade Behavior |
|----------|--------------|---------------|
| Reactive dyes (cellulosics) | Medium | Even fade, preserves hue |
| Acid dyes (protein fibers) | Variable | Certain hues fade faster |
| Direct dyes | Low | Rapid bleaching |
| Vat dyes (indigo) | High | Slow, characteristic desaturation |
| Discharge print | Very low | Discharged areas may yellow |

## Ghost Pattern Types
| Shield Object | Ghost Shape |
|--------------|-------------|
| Fold crease | Parallel lines with sharp edges |
| Stacked cloth | Rectangle with straight edges |
| Object placed on cloth | Silhouette of the object |
| Window shadow | Architectural shadow pattern |
| Furniture | Curved or geometric silhouette |

## Shader Snippet
```glsl
vec3 sun_fade(vec2 uv, sampler2D shield_mask, float fade_amount, float dye_stability) {
    float shield = texture(shield_mask, uv).r; // 1.0 = protected, 0.0 = exposed
    float exposure = (1.0 - shield) * fade_amount;
    vec3 original = texture(pattern, uv).rgb;
    vec3 faded = mix(original, vec3(dot(original, vec3(0.3, 0.59, 0.11))), exposure * (1.0 - dye_stability));
    return mix(faded, original * 0.95, shield * 0.05); // Slight yellowing in protected zone
}
```

## Prompt Template
> "A vintage indigo-dyed cotton curtain with sun fade — exposed areas have shifted from deep navy to steel grey-blue, but where the curtain was pleated, dark navy ghost lines remain, the pleat geometry making a pattern that was never designed, UV decay revealing the fabric's history as a light record"

## Anti-Drift Notes
- Sun fade creates **ghost patterns** from shielding objects, not from the original design
- The fade follows **light geometry** — the light source's angle is readable from the fade pattern
- Differential fade means the color **shifts**, not just lightens — blue may become grey-green as yellow component bleaches
