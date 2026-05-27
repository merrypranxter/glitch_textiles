# Bitrot Lace

## Failure Mode
Data decay in the lace pattern file: individual bits flip over time (or during transmission), turning thread nodes ON→OFF or OFF→ON. The lace structure develops holes, phantom connections, and orphaned thread segments where no node exists to anchor them.

## Visual Signature
- Missing nodes where thread intersections should exist — holes in the lattice
- Ghost threads connecting non-adjacent nodes across empty space (bit 0→1 in wrong position)
- Orphaned thread segments ending mid-air with no anchor
- Corrupted symmetry: one quadrant of a repeating motif is correct, others show increasing decay
- Entropy gradient: early bits intact, late bits mostly flipped — the decay pattern follows bit position

## Failure Origin
File system bitrot or storage medium degradation affecting the binary lace pattern file. Each flip toggles a single heddle position between raised/lowered.

## Decay Progression
| Bit Error Rate | Visual Result |
|----------------|---------------|
| 0.001 | Occasional missing node, pattern largely intact |
| 0.01 | Noticeable holes, some orphaned threads |
| 0.05 | Pattern partially legible, significant gaps |
| 0.1 | Pattern barely recognizable, structural collapse beginning |
| 0.2+ | Ghost lattice only, original pattern unrecoverable |

## Shader Snippet
```glsl
float bitrot_lace(vec2 uv, float error_rate, float seed) {
    float node = lace_pattern(uv);
    float flip = step(1.0 - error_rate, random(floor(uv * 64.0) + seed));
    return abs(node - flip); // XOR via abs(a - b) for binary values
}
```

## Prompt Template
> "A Venetian needle lace with bitrot decay — some bobbin intersections missing where bits flipped to zero, phantom thread connections appearing where zeros became ones, the lattice structure partially intact but increasingly corrupted toward the border, digital entropy in handmade lace"

## Anti-Drift Notes
- Missing nodes create **holes**, not tears — the surrounding threads remain intact
- Ghost threads have valid start/end nodes but wrong path (the connection exists, the route is wrong)
- Bitrot is **random** in position but follows a **density pattern** based on decay rate
