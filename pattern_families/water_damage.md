# Water Damage

## Failure Mode
Water contacts fabric, carrying dissolved minerals, dye particles, or soil. As it evaporates, it deposits its cargo at the evaporation front, creating tide lines — rings of concentrated deposit at the boundary between wet and dry zones.

## Visual Signature
- Tide line rings: darker or lighter curves following the wet-front geometry
- Mineral deposits: white or rust-colored crystalline residue at the tide lines
- Dye migration: color bleeds toward the wet front and concentrates there
- Halo effect: the area within the water zone is lighter (dye migrated out); the tide line is darker (dye concentrated)
- Multiple flood events = concentric rings, like tree rings or geological strata
- At center of water contact point: sometimes cleaner than surrounding area if clean water diluted existing soil

## Water Damage Patterns by Water Type
| Water Type | Deposit | Visual |
|------------|---------|--------|
| Hard tap water | Calcium carbonate | White mineral ring |
| Rust water | Iron oxide | Orange-brown ring |
| Seawater | Salt crystals + mineral | White crystalline ring |
| Flood (soil) | Clay + organic | Dark brown tide line |
| Coffee/tea | Tannin | Warm brown graduated ring |
| Clean water on dyed fabric | Migrated dye | Lighter center, darker ring in fabric's own color |

## Shader Snippet
```glsl
vec3 water_damage(vec2 uv, vec2 center, float inner_r, float outer_r, vec3 deposit_color) {
    float dist = length(uv - center);
    float in_zone = smoothstep(outer_r, inner_r, dist); // 1.0 inside water zone
    float at_tide_line = exp(-pow((dist - outer_r) / 0.02, 2.0)); // Gaussian at tide line
    vec3 base = texture(pattern, uv).rgb;
    vec3 bleached = mix(base, base * 0.7 + vec3(0.1), in_zone * 0.5); // Lighter inside
    return mix(bleached, deposit_color, at_tide_line * 0.6); // Deposit at ring
}
```

## Prompt Template
> "A linen tablecloth with water damage from a vase — a perfect oval tide line marking the evaporation front, the interior slightly bleached where the water diluted the linen's natural color, a concentrated ring of mineral deposit at the boundary, concentric ghost rings from previous water events, the cloth as a record of liquid history"

## Anti-Drift Notes
- Tide lines follow the **evaporation front geometry** — not the fabric structure
- The area **inside** the water zone is typically **lighter** (dye migrated out); the ring is **darker**
- Multiple events create **concentric rings** — the fabric as a chronological record
