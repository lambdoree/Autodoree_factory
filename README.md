# Autodoree Factory

`Autodoree_factory` composes Autodoree with Flowdoree Extend Factory.

This repository is the top-level factory integration layer. It should contain
factory behavior that requires both Autodoree host/effect orchestration and the
Flowdoree Extend factory composition layer.

## Topology

```text
flowdoree
  -> flowdoree_extend
  -> flowdoree_factory
flowdoree_extend + flowdoree_factory
  -> flowdoree_extend_factory

Autodoree + flowdoree_extend_factory
  -> Autodoree_factory
```

## Submodules

```text
external/Autodoree                 Autodoree host/effect layer
external/flowdoree_extend_factory  Flowdoree Extend Factory layer
```

Initialize dependencies with:

```sh
git submodule update --init --recursive
```

## Boundary

- May depend on `Autodoree`.
- May depend on `flowdoree_extend_factory`.
- Must not make lower layers depend back on Autodoree Factory.
- Should own only factory integration semantics that require both Autodoree
  orchestration and Flowdoree Extend factory projection.
