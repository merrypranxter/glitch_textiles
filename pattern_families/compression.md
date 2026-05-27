# Compression Artifact Fabric

## Failure Mode
JPEG/DCT compression artifacts — the characteristic 8×8 block structure of lossy compression — are translated directly onto woven cloth. The fabric records the compression error as a physical texture.

## Visual Signature
- Visible 8×8 (or scaled equivalent) grid overlaying the woven pattern
- Ringing artifacts at high-contrast thread boundaries: dark halos, ghost edges
- Color banding within each block where smooth gradients quantize to steps
- Mosquito noise at fine pattern edges — flickering fringe of wrong-colored threads
- Block boundaries visible as slight density changes in the weave

## Failure Origin
The loom program source image was saved at extreme JPEG compression (quality 1–20) before conversion to thread data. The compression artifacts were interpreted as actual color information.

## Shader Parameters
| Parameter | Suggested Value |
|-----------|----------------|
| `block_size` | 0.04–0.08 |
| `noise_amplitude` | 0.2–0.5 |
| `glitch_frequency` | 0.8–1.0 |

## Shader Snippet
```glsl
vec3 compression_artifact(vec2 uv, float block_size) {
    vec2 block_uv = floor(uv / block_size) * block_size;
    vec3 block_color = texture(base, block_uv + block_size * 0.5).rgb;
    float ringing = sin(length(uv - block_uv) / block_size * PI * 4.0) * 0.05;
    return block_color + vec3(ringing);
}
```

## Prompt Template
> "A woven fabric where JPEG compression artifacts are physically woven into the cloth — visible 8×8 block grid overlaying the pattern, ringing at thread boundaries, color banding within each block, the texture of extreme lossy compression made textile"

## Anti-Drift Notes
- Compression blocks are **always square** — rectangular blocks indicate a different error
- Ringing artifacts appear **at edges**, not in flat areas
- The underlying pattern must still be identifiable — if no pattern survives, compression is too extreme
