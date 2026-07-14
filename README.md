# Swarmscape

A tiny artificial-life toy. A few hundred colored particles, a randomized
matrix of attraction and repulsion between colors, and nothing else — yet the
swarm organizes itself into orbits, membranes, chases, and slow-drifting
colonies that no one designed on purpose.

This is [particle life](https://en.wikipedia.org/wiki/Particle_life), a class
of simulation where complexity emerges from a rule as simple as *"each pair
of colors either likes or dislikes each other, at some distance."* Every time
you hit **New rules**, that matrix is re-rolled and the swarm finds a
completely different way to behave.

**[Live demo →](https://fuskio64.github.io/swarmscape/)**

## Running it locally

No build step, no dependencies. Just open `index.html` in a browser.

```
git clone https://github.com/fuskio64/swarmscape.git
cd swarmscape
# open index.html
```

## Controls

| Control | Effect |
|---|---|
| **species** | how many colors are in play |
| **particles** | how many dots are simulated |
| **speed** | simulation speed multiplier |
| **trails** | how quickly old frames fade (low = long ghostly trails) |
| **style** | how the rulebook is generated — `balanced` (self-repelling species, good default), `orderly` (asymmetric pairs, tends to chase/orbit), `chaotic` (fully random, original behavior) |
| **wrap edges** | off makes particles bounce off the screen edges instead of wrapping around |
| **rulebook grid** | live view of the attraction matrix — red = repel, blue = attract. **Drag a cell up/down** to bend that relationship in real time |
| **🎲 shuffle** | re-randomize the attraction matrix, keep positions |
| **↺ reset** | re-randomize rules *and* scatter particles fresh |
| **🔗 link** | copy a permalink that reproduces this exact universe, including any cells you've hand-edited |
| **📸 save frame as PNG** | download the current canvas as an image |
| click / drag canvas | stir the swarm with your cursor |
| `space` | pause / resume |
| `R` | reset (fresh seed + scattered particles) |
| `N` | shuffle rules only (fresh seed, keep positions) |

Your last universe is also remembered automatically (via `localStorage`), so
reopening the page without a link picks up where you left off.

## How it works

Each particle belongs to a species (a color). For every pair of species
`(a, b)` there's a coefficient in `[-1, 1]` and a random interaction radius.
On every frame, each particle sums up a force from every nearby particle:
attract if the coefficient for that pair is positive, repel if negative,
nothing beyond the radius. On top of that, every particle also keeps a
small universal personal-space bubble (~14px) that repels *any* other
particle regardless of species — without it, strongly-attracting species
just collapse into an overlapping smear; with it, clusters settle into
crisp membranes and cells. A neighbor grid keeps all of this cheap enough
to run thousands of particles at 60fps in a browser tab.

The whole rulebook — the NxN matrix of coefficients — is drawn as a small
colored grid in the panel, and it's live: dragging a cell edits that force
in real time, so you can nudge an emergent pattern instead of only
re-rolling the dice. Everything (the random seed, the sliders, and any
hand-edits to the matrix) round-trips through the **🔗 link** button, so a
specific universe can be bookmarked or sent to someone else.

## License

MIT
