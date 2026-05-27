# Scanline Weave

## Failure Mode
CRT cathode ray tube artifacts — the horizontal scanline structure — are translated directly into woven thread. The electron beam's alternating pass pattern becomes an alternating thick/thin weft sequence. Phosphor persistence becomes thread density variation. The weave records the CRT as physical structure.

## Visual Signature
- Alternating bands of slightly different density running horizontally (weft direction)
- "Even" picks: normal density, representing beam-lit lines
- "Odd" picks: slightly lighter/lower density, representing dark between-scan lines
- At fabric edges: the scanline rhythm subtly interrupts the selvedge structure
- Under raking light: the alternating bands shimmer as alternating surface angles catch light differently
- High scanline frequency: the variation is too fine to see individually, but creates a visual texture
- Low scanline frequency: broad bands of heavy and light weave are clearly visible

## CRT-to-Thread Mapping
| CRT Property | Textile Translation |
|-------------|---------------------|
| Horizontal scanline | Weft pick density variation |
| Phosphor glow | Slight thread halation / loose tension |
| Beam intensity | Weft thread count (picks per cm) |
| Interlace pattern | Even/odd pick alternation |
| Persistence | Gradual density fade between lines |

## Shader Parameters
| Parameter | Suggested Value |
|-----------|----------------|
| `scanline_freq` | 50–200 |
| `scanline_depth` | 0.1–0.4 |
| `glitch_frequency` | 0.3–0.7 |

## Shader Snippet
```glsl
float scanline_weave(vec2 uv, float freq, float depth) {
    float scan = sin(uv.y * freq * PI) * 0.5 + 0.5;
    float phosphor_glow = smoothstep(0.4, 0.6, scan);
    return 1.0 - depth * (1.0 - phosphor_glow);
}
// Apply as density multiplier to weave texture
```

## Prompt Template
> "A woven fabric with CRT scanline artifacts translated to thread — horizontal bands of varying thickness where the 'electron beam' hit the cloth, phosphor glow colors of green and amber, alternating picks of different density creating a shimmering horizontal rhythm, retro-digital textile, the TV screen made cloth"

## Anti-Drift Notes
- Scanlines are **horizontal** — always weft direction. Vertical scanlines would be a vertical sync error, different artifact class.
- The variation is **density**, not color — same thread, different pick count per band
- High-frequency scanlines may only be visible as a surface shimmer, not individual lines
