# Misaligned Warp

## Failure Mode
Warp threads are systematically offset from their intended positions — shifted laterally in groups or individually. The weft interlaces correctly with each warp thread, but the threads are not where the pattern assumes they should be. The result is a moiré-like interference pattern between intended and actual structure.

## Visual Signature
- Pattern appears to "drift" or "swim" laterally across the width
- Moiré interference where the intended repeat and the actual thread positions have different spatial frequencies
- Groups of warp threads shifted together create visible "bands" of offset pattern
- At points where intended and actual positions coincide: pattern looks correct; between these points: maximum distortion
- Optical shimmer effect under raking light as the two grids interact

## Failure Origin
Reed misalignment: the denting (threading through reed slots) was done with the reed shifted.
Threading error: warp threads sleyed through wrong reed dent positions.
Beam winding error: threads crossed or shifted during warping.

## Moiré Parameters
| Warp Offset | Interference Period | Visual |
|-------------|---------------------|--------|
| 1 thread | Equal to repeat width | Pattern disappears into moiré |
| 0.5 thread | 2× repeat width | Gentle drift bands |
| 0.1 thread | 10× repeat width | Subtle shimmer |

## Shader Snippet
```glsl
vec3 misaligned_warp(vec2 uv, float offset_freq, float offset_amp) {
    float warp_offset = sin(uv.x * offset_freq) * offset_amp;
    vec2 displaced_uv = vec2(uv.x + warp_offset, uv.y);
    return texture(pattern, fract(displaced_uv)).rgb;
}
```

## Prompt Template
> "A woven geometric pattern where the warp threads have been systematically offset, creating a moiré interference between intended and actual thread positions, the pattern swimming and shifting across the width, optical shimmer where the two grids interact, weaving error as optical art"

## Anti-Drift Notes
- Misaligned warp creates **moiré** because two regular grids are out of phase — not random noise
- The error is in the **warp direction** (vertical); weft misalignment is a different error class
- The pattern remains **locally correct** — each thread interlaces correctly, just in the wrong column
