# Boundary

`Autodoree_factory` is the top factory integration layer.

Use it for behavior that combines:

- Autodoree host/effect, state, provider, service, native orchestration, or
  generated artifact context.
- Flowdoree Extend Factory projection, playback, layout, and inspection
  contracts.

Do not push this integration logic down into `flowdoree`, `flowdoree_extend`,
`flowdoree_factory`, or `flowdoree_extend_factory`.
