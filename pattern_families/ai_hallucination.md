# AI Hallucination Textile

## Failure Mode
An AI model generates a textile pattern that is visually plausible — it looks like a real fabric — but contains structures that are physically impossible. The pattern describes a weave that cannot be woven, a print that cannot be printed, or a construction that violates the physics of thread behavior.

## Visual Signature
- Warp and weft threads that pass through each other rather than interlacing correctly
- Thread count that changes mid-pattern without a structural break
- Shadows and highlights suggesting 3D depth that is structurally impossible for flat cloth
- Pattern elements that suggest they belong to two different weave structures simultaneously
- Symmetry that is "almost" correct but breaks in ways no mechanical process would produce
- Colors that imply a dye affinity impossible for the fiber type shown

## Impossible Structures
| Hallucination | Why It's Impossible |
|--------------|---------------------|
| Thread passing through thread | Threads occupy physical space |
| Gradient warp in plain weave | Plain weave can't produce smooth gradients |
| Perfectly smooth curve at thread scale | Threads are discrete, not continuous |
| Knot that is also an intersection | A knot and an interlace are different structures |
| Shadow on flat cloth suggesting deep relief | Flat cloth does not cast that shadow |

## The Uncanny Valley of Cloth
AI hallucination textiles occupy a specific zone: convincing enough at thumbnail scale to pass as real fabric, but revealing their impossibility at close inspection. This is the textile uncanny valley.

## Prompt Template
> "An AI-generated silk damask that looks completely convincing in the thumbnail — warp-faced satin ground with supplementary weft florals — but on close inspection the threads pass through each other at the transition zones, the weave structure changes thread count without a structural break, shadows suggesting impossible relief, plausible but unweave-able"

## Anti-Drift Notes
- AI hallucination must be **plausible at first glance** — obvious nonsense is not a hallucination
- The impossibility must be **structural** — not just aesthetically wrong
- The pattern should sit in the **uncanny valley**: not clearly wrong, not quite right
