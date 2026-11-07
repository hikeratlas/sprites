# sprites

Generate sprite .json and .png files in SDF format, suitable for use
on vector maps with MapLibre GL.

`temaki` and `maki` are added as submodules.

## Usage

```bash
./build
```

## Our own icons

`icons/` holds icons drawn for Hiker Atlas, built into the SDF sheet with
maki's and temaki's (and winning a name clash). Draw them 15×15, in black.

| Icon | Used for |
|---|---|
| `ridgeline` | peaks: a jagged outline, unlike the campsite's triangle (hikeratlas/website#44) |

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
| `wetland` | `natural=wetland` (horizontal dashes) |
| `scrub` | `natural=scrub` (scattered shrubs) |
| `sand` | `natural=beach`, `natural=sand` (grains) |

They come from [openstreetmap-carto](https://github.com/gravitystorm/openstreetmap-carto)'s
`symbols/` (`generating_patterns/scree.svg`, `generating_patterns/rock.svg`,
`generating_patterns/wetland.svg`, `generating_patterns/scrub.svg`,
`generating_patterns/beach.svg`, `cliff.svg`, `cliff2.svg`), which are CC0. Changes from the originals:

- Recoloured: scree is `#3f3f46` at 55% opacity, rock `#52525b` at 18%,
  wetland `#0d9488` at 60%, cliffs `#52525b`, scrub `#3f7a50` at 50%, and sand
  `#8a6a2e` at 55%, drawn at twice the size.
- Cliffs are flipped vertically, with a transparent 1px row added top and
  bottom. MapLibre puts the bottom of a `line-pattern` image on the left of the
  line, and OSM draws cliffs with the drop on the right. Without the padding,
  the tick tips wrap onto the far edge.
