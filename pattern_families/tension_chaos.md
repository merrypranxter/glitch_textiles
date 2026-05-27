# Tension Chaos

## Failure Mode
Warp or weft tension varies irregularly across the width of the fabric, causing threads to pack unevenly. High tension = tight, dense weave. Low tension = loose, open weave. The density ripples create visible waves of tight and loose structure.

## Visual Signature
- Alternating bands of dense and open weave running lengthwise (warp tension variation) or widthwise (weft tension)
- In patterned fabric: the pattern compresses in tight zones, expands in loose zones — same number of threads, different spatial frequency
- Visible "smiling" or "frowning" curves where threads bow toward or away from high-tension zones
- In severe cases: actual puckers, bubbles, or ripples where the fabric can't lie flat
- The fabric becomes a physical frequency map of the tension across time

## Failure Origin
Mechanical: worn tension springs, debris in the tension system, inconsistent beam winding, operator adjustments mid-run.
Environmental: humidity change causing thread contraction/expansion during weaving.

## Shader Snippet
```glsl
vec3 tension_chaos(vec2 uv, float amplitude, float frequency, float seed) {
    float tension = sin(uv.x * frequency + random(vec2(seed)) * TWO_PI) * amplitude;
    float density = 1.0 + tension; // >1 = compressed, <1 = expanded
    vec2 distorted_uv = vec2(uv.x, uv.y * density);
    return texture(pattern, fract(distorted_uv)).rgb;
}
```

## Prompt Template
> "A plain weave linen where warp tension varies across the width — alternating zones of dense tightly-packed threads and loose open-weave areas, the fabric's own structure recording the mechanical irregularity of the loom, tension as visible texture, the cloth as a seismograph"

## Anti-Drift Notes
- Tension variation affects **density**, not color — same threads, different spacing
- Warp tension variation creates **lengthwise** density bands; weft tension creates **crosswise** variation
- Severe tension chaos causes 3D surface deformation — the cloth physically cannot lie flat
