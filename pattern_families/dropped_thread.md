# Dropped Thread

## Failure Mode
A single warp thread breaks or a single weft thread is missing from a pick. The loom continues weaving; the missing thread leaves a gap that propagates through the entire fabric length (warp break) or creates a single horizontal streak (weft break).

## Visual Signature
**Warp break (most common):**
- A single vertical streak from selvedge to selvedge (or from break point to end of fabric)
- The streak color is the background: wherever that warp thread would have been on top, the weft shows through
- Width of streak: exactly one thread (typically 0.2–0.5mm)
- Surrounding threads may crowd slightly into the gap, creating a subtle density variation

**Weft break:**
- A single horizontal line — one pick missing across the full width
- Visible as a slight gap or a doubled thread if the shuttle passed without tension

## Failure Origin
Thread exhausted on bobbin mid-run; thread break from tension, knot, or defect; operator failed to notice break before restarting loom.

## Shader Snippet
```glsl
float dropped_thread(vec2 uv, float thread_pos, float thread_width) {
    float dist = abs(uv.x - thread_pos);
    return 1.0 - smoothstep(0.0, thread_width, dist) * 0.8;
}
// Apply: multiply against warp color, revealing weft at that column
```

## Prompt Template
> "A dense twill weave with a single dropped warp thread creating a fine vertical streak from top to bottom of the cloth, the surrounding threads barely compensating for the gap, the streak color revealing the weft layer underneath, a single thread's absence marking the whole cloth"

## Anti-Drift Notes
- **Warp breaks = vertical streaks**; weft breaks = horizontal lines. This is non-negotiable weave physics.
- The streak is the width of exactly one thread — not a gap, not a tear, just an absence
- The streak runs the **full remaining length** of the fabric from the point of failure
