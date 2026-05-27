# Misregistration

## Failure Mode
In multi-layer printing (screen print, rotary print, digital textile print), separate color layers are applied sequentially. Misregistration occurs when one or more layers shift position relative to the others — the layers no longer align at their intended coordinates.

## Visual Signature
- Color halos around pattern edges: the color that should be inside the outline has slid outside
- Gaps of unprinted ground fabric where two adjacent color layers have moved apart
- Double outlines: one layer of the outline is correct, a ghost outline appears offset by the shift distance
- In multi-color prints: each layer's offset is independent — some colors left, some right, some both
- Registration marks (crop marks, corner dots) visibly misaligned — the internal evidence of the error

## Failure Origin
Screen printing: screen not locked into registration stops; screen stretched unevenly.
Rotary printing: rollers not synchronized; fabric stretching inconsistently under different roller tensions.
Digital printing: print head passes misaligned due to paper/fabric feed error.

## Shift Directions
| Shift Type | Visual |
|------------|--------|
| Single layer translates | Color halo on one side, gap on opposite |
| Rotation | Color halo curves around the motif |
| Scale error | Color halo is uniform around all edges |
| Multiple layer shifts | Complex overlapping halos, multiple colors visible at edges |

## Shader Snippet
```glsl
vec3 misregistration(vec2 uv, vec2 layer1_shift, vec2 layer2_shift) {
    vec3 base = texture(layer_base, uv).rgb;
    vec3 layer1 = texture(layer_color1, uv + layer1_shift).rgb;
    vec3 layer2 = texture(layer_color2, uv + layer2_shift).rgb;
    return blend_print_layers(base, layer1, layer2);
}
```

## Prompt Template
> "A screen-printed floral textile where the red layer has shifted 4mm to the right and the blue layer 2mm upward — red halos on the right side of every stem, blue halos above every petal, gaps of white fabric where the layers separated, the registration marks in the selvedge visibly misaligned"

## Anti-Drift Notes
- Misregistration shows **halos on one side and gaps on the other** — not uniform outlines
- The shift distance is **consistent** across the entire fabric width within a single print run
- Each color layer shifts **independently** — not all layers shift together
