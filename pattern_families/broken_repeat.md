# Broken Repeat

## Failure Mode
The pattern's repeat unit shifts mid-fabric — the tile that tiles cleanly for 40 cm suddenly offsets by half a repeat width, then continues tiling from that new position. The seam is abrupt and geometrically jarring.

## Visual Signature
- Clean tiling for a section, then a hard horizontal or vertical line where the repeat resets
- After the break, the pattern continues correctly — but now misaligned with what came before
- If multiple breaks occur, the fabric has a staircase of misaligned tiles
- At the break line: two half-repeats forced together, creating an impossible chimera motif

## Failure Origin
Digital: the repeat offset counter in the loom control software reset mid-run (integer overflow, operator error, file seek error).
Mechanical: fabric shifted on the beam during a re-start after a thread break, losing position.

## Shader Snippet
```glsl
vec3 broken_repeat(vec2 uv, float break_pos, float offset) {
    vec2 shifted_uv = uv;
    if (uv.y > break_pos) {
        shifted_uv.x += offset;
    }
    return texture(pattern, fract(shifted_uv)).rgb;
}
```

## Prompt Template
> "A geometric woven repeat — small diamond tiles — that suddenly shifts half a repeat width at the 60% mark, creating a seam where two half-diamonds are forced together into an impossible shape, the pattern continuing perfectly on both sides of the break but irreconcilably misaligned"

## Anti-Drift Notes
- The break is a **hard edge**, not a gradient — the shift is instantaneous
- Both sides of the break show **correct pattern** — only the relationship between them is wrong
- Repeat breaks are **horizontal** (weft direction) for beam displacement; **vertical** (warp direction) for reed misalignment
