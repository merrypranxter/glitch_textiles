# Channel Swap

## Failure Mode
RGB channels in the textile color program are remapped in the wrong order. Red reads green data, green reads blue, blue reads red — or any permutation thereof. The result is a fabric where every color is plausible but nothing is correct.

## Visual Signature
- Familiar pattern geometry; completely alien color relationships
- Traditional palette signature (e.g., indigo/cream tartan) replaced by its channel-swapped equivalent (e.g., orange/magenta)
- Colors shift coherently across the entire fabric — this is not noise, it's a systematic wrong answer
- Pattern structure fully intact; only hue relationships are broken

## Failure Origin
A lookup table (LUT) or color profile was applied in the wrong channel order during loom programming. Common when converting between RGB and CMY dye systems without proper mapping.

## Possible Channel Permutations
| Swap | Result |
|------|--------|
| R↔G | Red areas become green and vice versa |
| R↔B | Warm tones become cool |
| G↔B | Greens become blues, cyans become magentas |
| RGB→GBR | Full rotation, everything wrong |
| RGB→BRG | Full rotation opposite direction |

## Shader Snippet
```glsl
vec3 channel_swap(vec3 color, int mode) {
    if (mode == 0) return color.grb; // R↔G
    if (mode == 1) return color.bgr; // R↔B
    if (mode == 2) return color.rbg; // G↔B
    if (mode == 3) return color.gbr; // RGB→GBR
    return color.brg;                // RGB→BRG
}
```

## Prompt Template
> "A traditional indigo and cream herringbone where the RGB channels have been swapped — indigo areas now render as orange, cream as cyan, the pattern geometry perfect but every color wrong, systematic color inversion as textile error"

## Anti-Drift Notes
- Channel swap is **global and consistent** — not random per thread
- The pattern must still read as a recognizable pattern family (plaid, herringbone, etc.)
- Do not confuse with palette swap (which is intentional/artistic) — channel swap is a pure technical error
