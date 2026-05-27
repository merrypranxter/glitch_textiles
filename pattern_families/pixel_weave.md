# Pixel-Weave

## Failure Mode
Screen pixels attempt to become threads. The mapping from 2D pixel grid to over/under warp-weft interlacement is imperfect — pixels are square, threads are not. The collision produces a fabric that looks simultaneously woven and digital, where neither system fully wins.

## Visual Signature
- Hard-edged pixel blocks visible within the woven structure
- "Thread" crossings that are too perfect, too square — revealing their pixel origin
- Aliasing at diagonal lines: the weave attempts curves the pixel grid can't represent
- Flickering color at high-DPI boundaries where pixel and thread pitch mismatch

## Failure Origin
A digital-to-loom translation error. The source image's pixel grid was mapped 1:1 to loom heddle positions without accounting for the aspect ratio difference between pixel (1:1) and thread crossing (typically 1:1.3–1.5 warp:weft).

## Shader Parameters
| Parameter | Suggested Value |
|-----------|----------------|
| `block_size` | 0.02–0.05 |
| `noise_amplitude` | 0.1–0.3 |
| `glitch_frequency` | 0.6–1.0 |

## Shader Snippet
```glsl
vec3 pixel_weave(vec2 uv, float pixel_size, float thread_ratio) {
    vec2 pixel_uv = floor(uv / pixel_size) * pixel_size;
    vec2 thread_uv = pixel_uv * vec2(1.0, thread_ratio);
    return mix(texture(base, pixel_uv).rgb, texture(base, thread_uv).rgb,
               fract(uv.y / pixel_size));
}
```

## Prompt Template
> "A woven fabric where the source pattern is clearly a pixel grid — square blocks of color arranged in a strict digital grid, but rendered as actual threads, the pixel boundaries visible as doubled thread lines, screen artifacts in cloth form"

## Anti-Drift Notes
- Pixel-weave shows **both** pixel structure AND thread structure simultaneously
- The pixel grid must be square; irregular blocks indicate compression artifacts, not pixel-weave
- Diagonals will always staircase — smooth diagonals mean the pixel origin has been lost
