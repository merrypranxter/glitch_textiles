# Corrupted Jacquard

## Failure Mode
The Jacquard loom's punch card (or digital equivalent) contains wrong data: a pixel is flipped, a row is shifted, or a card is inserted out of sequence. The resulting fabric weaves exactly what the corrupted program says — faithfully producing the wrong pattern.

## Visual Signature
- Floral or figurative motifs with sudden pixel-level inversions — a black dot where white should be
- Repeat resets mid-motif: the pattern abruptly starts over at the wrong position
- Horizontal bands of garbled pattern where an entire card row was corrupted
- Mirror errors: half a motif correct, the other half running backwards
- Single-thread errors creating fine vertical lines through an otherwise intact design

## Failure Origin
Mechanical: a physical punch card hole is in the wrong position, or a card is loaded inverted/out-of-order.
Digital: a bit flip in the loom's pattern memory, or a file corruption in the `.jcd` pattern file.

## Error Types
| Error | Cause | Visual |
|-------|-------|--------|
| Single pixel flip | One wrong hole in card | Single thread error, vertical stripe |
| Row shift | Card inserted one position off | Horizontal band of offset pattern |
| Card inversion | Card loaded upside-down | Upside-down section in repeat |
| Card swap | Two cards exchanged | Two pattern sections swapped |
| Missing card | Card not loaded | Blank (all warp up or all warp down) band |

## Prompt Template
> "A corrupted digital jacquard output with missing pixels in the pattern program, creating broken floral motifs and sudden repeat resets, dropped threads where the loom skipped beats, industrial textile error as aesthetic"

## Anti-Drift Notes
- Jacquard corruption is **structured**, not random — it follows the grid of the punch card
- Each corrupted pixel creates a **consistent vertical stripe** through every repeat of that card row
- The non-corrupted areas of the pattern are **perfectly correct** — the contrast is key
