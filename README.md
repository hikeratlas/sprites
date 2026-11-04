# sprites

Generate sprite .json and .png files in SDF format, suitable for use
on vector maps with MapLibre GL.

`temaki` and `maki` are added as submodules.

## Usage

```bash
./build
```

## Patterns

`patterns/` holds full-colour fill and line patterns, built into a separate
non-SDF sheet, `output/patterns`. MapLibre can't use SDF images as patterns,
and one sheet can't mix SDF and non-SDF images. The basemap style lists both
sheets, and refers to patterns as `patterns:<name>`.

| Pattern | Used for |
|---|---|
| `scree` | `natural=scree` |
| `rock` | `natural=bare_rock` |
| `cliff`, `cliff2` | `natural=cliff` lines; `cliff2` is the larger one, for close zooms |

They come from [openstreetmap-carto](https://github.com/gravitystorm/openstreetmap-carto)'s
`symbols/` (`generating_patterns/scree.svg`, `generating_patterns/rock.svg`,
`cliff.svg`, `cliff2.svg`), which are CC0. Changes from the originals:

- Recoloured: scree is `#3f3f46` at 55% opacity, rock `#52525b` at 18%, and
  cliffs `#52525b`.
- Cliffs are flipped vertically, with a transparent 1px row added top and
  bottom. MapLibre puts the bottom of a `line-pattern` image on the left of the
  line, and OSM draws cliffs with the drop on the right. Without the padding,
  the tick tips wrap onto the far edge.
