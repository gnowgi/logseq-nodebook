# logseq-nodebook

Write knowledge as readable **Controlled Natural Language** in a ` ```nodeBook ` code fence — get an interactive knowledge graph in your Logseq notes.

````
```nodeBook
# Water [Substance]
boiling_point: 100 *C*;
<part of> Ocean;

## frozen
    state: solid;
```
````

## Features

- **Interactive concept maps** — drag nodes, pan, zoom; light/dark theme follows Logseq.
- **Inspector panel** — click a node to see its role, attributes, and relations.
- **Morphs** — polymorphic node states (`## frozen`); switch them live from the inspector.
- **Inference** — derived facts (transitive `is_a`, membership inheritance) appear as dashed purple edges with proof tooltips.
- **Containment view** — the *Nest* button draws class hierarchies as boxes-within-boxes.
- **Process simulation** — transitions (`[Transition]`) with `has prior_state` / `has post_state` arcs render in Petri-net notation (vertical bars, flow-directed arcs); click an enabled transition to fire it and watch tokens move. Great for chemistry, biology, and ecology:

````
```nodeBook
# Combustion of Methane [Transition]
<has prior_state> 2 O2;
<has prior_state> CH4;
<has post_state> CO2;
<has post_state> 2 H2O;
```
````

- **Toolbar** — fit, layout picker, PNG export, and an *Edit* button back to the CNL source.
- `/nodeBook graph` slash command inserts a starter fence.

The full CNL syntax is documented in the [nodeBook CNL specification](https://github.com/gnowgi/hedgedoc-nb/blob/main/docs/nodebook-cnl-spec.md).

## Install

From the Logseq **Marketplace**: search for “nodeBook”.

Manual / development install:

```bash
npm install
npm run build
```

then Logseq → Settings → Advanced → Developer mode → Plugins → **Load unpacked plugin** → select this directory.

## How it's built

This plugin is a thin integration of the published [`@nodebook/dom`](https://www.npmjs.com/package/@nodebook/dom) renderer (Cytoscape.js) and [`@nodebook/core`](https://www.npmjs.com/package/@nodebook/core) CNL engine. It registers a fenced-code renderer via `logseq.Experiments.registerFencedCodeRenderer`, runs on Logseq's own React, and loads the renderer into the host page once via `loadScripts`. Development happens in the [hedgedoc-nb monorepo](https://github.com/gnowgi/hedgedoc-nb) (`apps/logseq-nodebook`); this repository tracks the standalone releases.

## License

AGPL-3.0-only — see [LICENSE](LICENSE).
