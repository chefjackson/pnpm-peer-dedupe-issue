# Peer Dedupe Issue

## Structure

```
pacakges:
  a:
    dependencies:
      - b
      - c
      - react
      - viem
      - wagmi

  b:
    dependencies:
      - react
      - viem
      - wagmi
      - react-dom

  c:
    dependencies:
      - react
      - viem
      - wagmi
      - zod

```

## Issue

All the packages share the same `react`, `viem` and `wagmi` version. `react-dom` and `zod` are both optional transitive peer dependency lower in the dependency graph.

The expected behavior with `dedupe-peer-dependents` on is, there should be only one `wagmi` instance, as there's no conflicting peer dependencies. However, according to the generated lock file, `c` is referring to a duplicate instance.
