# Glitch Textiles

Corrupted looms. Datamoshed plaids. Broken beauty.

This repository documents textile aesthetics derived from **system failure** — what happens when looms, printers, digital systems, and generative algorithms fail in visually interesting ways.

## The Core Principle

Glitch textiles exploit the tension between:
- **The expected pattern**: Regular, repeating, controlled
- **The failure mode**: Shifted, corrupted, broken, transformed

The glitch reveals the underlying system. The error becomes the art.

## The Glitch Families

### Digital / Pixel Errors
- [Datamoshed plaid](pattern_families/datamoshed_plaid.md) — color channels shifted horizontally in woven repeat
- [Pixel-weave](pattern_families/pixel_weave.md) — screen pixels trying to be threads
- [Channel swap](pattern_families/channel_swap.md) — RGB textile where colors are misaligned
- [Compression artifact fabric](pattern_families/compression.md) — JPEG blocks on cloth
- [Bitrot lace](pattern_families/bitrot_lace.md) — missing nodes, broken connections

### Loom / Weave Errors
- [Corrupted jacquard](pattern_families/corrupted_jacquard.md) — wrong punch card / wrong pixel in digital loom
- [Broken repeat](pattern_families/broken_repeat.md) — repeat unit shifts mid-fabric
- [Dropped thread](pattern_families/dropped_thread.md) — single thread missing creating streak
- [Tension chaos](pattern_families/tension_chaos.md) — irregular density across width
- [Misaligned warp](pattern_families/misaligned_warp.md) — warp threads offset creating moiré-like error

### Print / Dye Errors
- [Misregistration](pattern_families/misregistration.md) — color layers sliding apart
- [Color palette swap](pattern_families/palette_swap.md) — acid substitutions in traditional patterns
- [Wrong dye lot](pattern_families/wrong_dye.md) — abrupt color change mid-roll
- [Bleed error](pattern_families/bleed_error.md) — excessive dye diffusion destroying crisp edges

### Generative / AI Errors
- [AI hallucination textile](pattern_families/ai_hallucination.md) — plausible but impossible structures
- [Bad generative embroidery](pattern_families/bad_embroidery.md) — path errors, thread tangles
- [GAN artifact fabric](pattern_families/gan_artifact.md) — weird textures from discriminator failure
- [Style transfer bleed](pattern_families/style_transfer.md) — pattern bleeding across garment seams

### Analog / Physical Decay
- [Scanline weave](pattern_families/scanline.md) — CRT artifacts translated to thread
- [Tape decay](pattern_families/tape_decay.md) — oxide shedding as pigment loss
- [Sun fade](pattern_families/sun_fade.md) — selective UV degradation creating ghost patterns
- [Water damage](pattern_families/water_damage.md) — tide lines, mineral deposits on fabric

## Shader Translation: Glitch Textile Parameters

| Parameter | What It Controls | Range | Notes |
|-----------|---------------|-------|-------|
| `channel_shift` | RGB misalignment | 0.0–0.1 | UV space offset |
| `scanline_freq` | CRT line density | 10–500 | Lines per unit |
| `scanline_depth` | Visibility of lines | 0.0–1.0 | 1.0 = heavy banding |
| `block_size` | Compression artifact scale | 0.01–0.1 | JPEG 8×8 block equivalent |
| `dropout_rate` | Percentage of missing data | 0.0–0.5 | 0.5 = half missing |
| `noise_amplitude` | Random corruption strength | 0.0–1.0 | Higher = more chaos |
| `glitch_frequency` | How often glitch appears | 0.0–1.0 | 0.1 = sparse, 1.0 = everywhere |
| `error_seed` | Randomization seed | 0–10000 | Reproducible chaos |

## Glitch-to-Shader Logic

### Channel Shift
```glsl
vec3 channel_shift(vec2 uv, float offset, int channel) {
    vec3 color;
    color.r = texture(base, uv + vec2(offset * float(channel == 0), 0.0)).r;
    color.g = texture(base, uv + vec2(offset * float(channel == 1), 0.0)).g;
    color.b = texture(base, uv + vec2(offset * float(channel == 2), 0.0)).b;
    return color;
}
```

### Scanline Bands
```glsl
float scanline(vec2 uv, float freq) {
    float line = sin(uv.y * freq * PI);
    return smoothstep(0.0, 0.1, line);
}
```

### Compression Blocks
```glsl
vec2 block_uv(vec2 uv, float block_size) {
    vec2 block = floor(uv / block_size) * block_size;
    return block + (fract(uv / block_size) > 0.5 ? block_size * 0.5 : 0.0);
}
```

### Data Dropout
```glsl
float dropout(vec2 uv, float rate, float seed) {
    float noise = random(uv + seed);
    return step(rate, noise); // 1.0 = keep, 0.0 = drop
}
```

## Prompt Templates

### Datamoshed Plaid
> "A datamoshed tartan where red and green color channels have shifted horizontally by 3 threads, creating RGB-split woven bands, some thread intersections showing impossible color combinations, digital corruption of traditional textile"

### Corrupted Jacquard
> "A corrupted digital jacquard output with missing pixels in the pattern program, creating broken floral motifs and sudden repeat resets, dropped threads where the loom skipped beats, industrial textile error as aesthetic"

### Scanline Weave
> "A woven fabric with CRT scanline artifacts translated to thread — horizontal bands of varying thickness where the 'electron beam' hit the cloth, phosphor glow colors, retro-digital textile"

## Anti-Drift: Glitch Textile Specific

- **Glitch must reference a "correct" pattern**: The error needs a baseline to deviate from
- **Channel shift only works on multi-color patterns**: Monochrome can't RGB-shift
- **Compression blocks are square**: If blocks aren't square, it's not compression artifact
- **Dropped threads create vertical streaks**: Warp errors = vertical; weft errors = horizontal
- **AI hallucinations are plausible but wrong**: The structure looks almost right but violates physics

---

*This repo treats failure as a generative system. The bug is the feature. The error is the pattern. The crash is the design.*
