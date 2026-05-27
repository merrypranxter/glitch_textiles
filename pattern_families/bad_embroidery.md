# Bad Generative Embroidery

## Failure Mode
A generative algorithm or machine embroidery path planner produces invalid stitch sequences: path errors, impossible geometries, thread tangles, machine crashes mid-design. The machine faithfully executes the bad path, producing physical evidence of algorithmic failure.

## Visual Signature
- Long "jump threads" crossing the design where the machine moved without cutting thread
- Stitching that loops back on itself, creating knots and raised nodules
- Incomplete motifs where the machine stopped mid-path (power failure, buffer overflow)
- Overlapping stitch areas where the fill algorithm revisited the same zone multiple times
- Path ghosts: thread lines showing the routing algorithm's decision process, not just the intended motif
- Machine crash artifacts: a spray of random stitches as the machine lost position and continued stitching

## Error Types
| Error | Cause | Visual |
|-------|-------|--------|
| Jump thread | No cut command between path segments | Thread strings crossing motif |
| Over-stitch | Fill algorithm overlap | Dense, raised, possibly burnt areas |
| Path ghost | Routing stitches not trimmed | Faint structural lines beneath design |
| Crash spray | Machine lost position | Random radiating stitches from a point |
| Incomplete fill | Algorithm terminated early | Half-filled shapes, abrupt end |

## Shader Snippet
```glsl
// Simulate jump threads as line artifacts
float jump_thread(vec2 uv, vec2 from, vec2 to, float thread_width) {
    vec2 line_dir = normalize(to - from);
    vec2 to_point = uv - from;
    float along = dot(to_point, line_dir);
    float perp = length(to_point - line_dir * clamp(along, 0.0, length(to - from)));
    return 1.0 - smoothstep(0.0, thread_width, perp);
}
```

## Prompt Template
> "A machine embroidered portrait where the path algorithm failed — long jump threads crossing the face like spiderwebs, one eye only half-filled where the routine terminated early, a spray of random stitches in the upper right where the machine crashed and kept running, the intended portrait visible beneath the evidence of its own production failure"

## Anti-Drift Notes
- Jump threads are **straight lines** — they connect two path endpoints directly
- Over-stitch areas are **raised** — physical accumulation of thread, not just dark color
- Machine crash sprays radiate from a **single point** (the position at time of crash)
