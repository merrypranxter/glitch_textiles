# GAN Artifact Fabric

## Failure Mode
A Generative Adversarial Network trained on fabric images produces textures that fool the discriminator but contain characteristic GAN failure artifacts: mode collapse (all outputs similar), checkerboard artifacts from deconvolution, and the specific "GAN texture" that looks synthetic on close inspection.

## Visual Signature
- Checkerboard patterns overlaying the fabric texture (upsampling artifact from transposed convolutions)
- Repeated micro-patterns at regular grid intervals (mode collapse leaving a signature)
- Texture that is statistically plausible but visually "flat" — lacks the hierarchical variation of real cloth
- Blob-like structures at the boundary between pattern elements — the discriminator's blind spots
- "GAN skin": a characteristic waxy, over-smooth quality to what should be rough texture
- Frequency domain artifacts: unusually strong response at specific spatial frequencies

## GAN Failure Modes by Training Stage
| Stage | Artifact | Visual |
|-------|----------|--------|
| Early training | Random noise | No discernible pattern |
| Mode collapse | Single texture repeated | Every output looks the same |
| Checkerboard artifacts | Upsampling error | Regular grid overlay |
| Discriminator saturation | Adversarial texture | Looks right, feels wrong |
| Late convergence | Over-smooth output | Waxy, unnatural surface |

## Shader Snippet
```glsl
// Simulate checkerboard artifact from transposed convolution
vec3 gan_artifact(vec2 uv, vec3 base_color, float artifact_scale) {
    vec2 checker_uv = floor(uv / artifact_scale) * artifact_scale;
    float checker = mod(checker_uv.x + checker_uv.y, artifact_scale * 2.0) < artifact_scale ? 1.0 : 0.0;
    float artifact_strength = 0.05;
    return base_color + vec3(checker * artifact_strength - artifact_strength * 0.5);
}
```

## Prompt Template
> "A GAN-generated tweed texture that almost passes as real wool — but on close inspection shows a faint checkerboard grid from transposed convolution, the fiber detail too uniform across the surface, certain frequency bands too strong, the texture statistically correct but perceptually hollow, machine-dreamed cloth"

## Anti-Drift Notes
- GAN artifacts appear **everywhere uniformly** — not localized to one area
- Checkerboard artifacts are at a **specific scale** determined by network architecture (typically 4px, 8px, or 16px in original resolution)
- The fabric must look convincing at **low resolution** — GAN artifacts are high-frequency
