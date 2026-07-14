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
| **🎲 New rules** | re-randomize the attraction matrix, keep positions |
| **↺ Reset** | re-randomize rules *and* scatter particles fresh |
| click / drag | stir the swarm with your cursor |
| `space` | pause / resume |

## How it works

Each particle belongs to a species (a color). For every pair of species
`(a, b)` there's a random coefficient in `[-1, 1]` and a random interaction
radius. On every frame, each particle sums up a force from every nearby
particle: attract if the coefficient for that pair is positive, repel if
negative, nothing beyond the radius. A neighbor grid keeps this cheap enough
to run thousands of particles at 60fps in a browser tab.

That's the entire model. No global rules, no fitness function, no seed
values you have to hand-tune — just a random matrix and physics doing the
rest.

## License

MIT
