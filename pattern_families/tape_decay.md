# Tape Decay

## Failure Mode
Magnetic tape oxide shedding translated to textile: as magnetic tape degrades, iron oxide particles shed from the binder, causing dropout — local signal loss. When the audio/video signal was controlling a textile printing or weaving system, these dropouts appear as missing color, missing pattern, missing structure.

## Visual Signature
- Horizontal streaks of signal dropout — areas where the pattern simply isn't there
- Dropout appears as either the base fabric color (signal = 0) or maximum signal (signal = 1)
- The dropouts are sharp-edged horizontally (time axis = x axis on tape) but may flutter vertically
- Neighboring dropouts often cluster (oxide sheds in patches, not uniformly)
- Magnetic tape timecode artifacts: brief flashes of the wrong pattern from head switching
- Shed oxide creates a secondary texture — the dropout debris itself becomes visible

## Tape Decay Properties
| Decay Stage | Visual Signature |
|-------------|-----------------|
| Early shedding | Occasional small horizontal dropout |
| Active decay | Regular clusters of dropout, pattern disruption |
| Advanced | Large zones of missing signal, head-switching errors |
| End of life | Only the strongly-magnetized areas survive — high-contrast patterns, fine detail gone |

## Shader Parameters
| Parameter | Suggested Value |
|-----------|----------------|
| `dropout_rate` | 0.05–0.3 |
| `noise_amplitude` | 0.3–0.6 |
| `glitch_frequency` | 0.3–0.6 |

## Shader Snippet
```glsl
vec3 tape_decay(vec2 uv, float dropout_rate, float seed) {
    float dropout = step(1.0 - dropout_rate, random(vec2(floor(uv.x * 200.0), floor(uv.y * 2.0)) + seed));
    vec3 pattern_color = texture(pattern, uv).rgb;
    vec3 dropout_color = vec3(0.0); // Base fabric showing through
    return mix(pattern_color, dropout_color, dropout);
}
```

## Prompt Template
> "A digitally-printed textile where the control signal came from a degrading magnetic tape — horizontal dropout streaks where the oxide shed, the pattern disappearing in horizontal bands of varying width, the base fabric showing through in the signal-loss zones, the texture of magnetic decay translated to cloth, tape hiss made visible"

## Anti-Drift Notes
- Tape dropout follows the **horizontal (time) axis** — always horizontal streaks, never vertical
- Dropout shows **base fabric** (signal loss = no information = no dye), not random color
- Dropout **clusters** — areas near previous dropout are more likely to drop out again
