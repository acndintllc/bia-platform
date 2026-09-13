# Brand assets

Drop files straight into the folder for each mark. Specification and usage
rules live in [`docs/BRAND.md`](../../docs/BRAND.md).

## Naming

`<mark>-<variant>.svg` for vector, `<mark>-<variant>-<size>.png` for raster.

Variant is `gold` or `mono`. Size is the pixel width.

**The BIA mother marks are gold only** — there is no mono crest, badge or
seal. The five application marks have both.

```
assets/brand/
├── bia/                        gold only
│   ├── bia-crest-gold.*        shield + fist
│   ├── bia-badge-gold.*        crest in a ring, "BIA" above
│   ├── bia-seal-gold.*         full institutional seal
│   └── bia-lockup-gold.*       seal with the five apps orbiting
├── blackgpt/    blackgpt-gold.svg     blackgpt-mono.svg
├── blackbook/   blackbook-gold.svg    blackbook-mono.svg
├── blackgram/   blackgram-gold.svg    blackgram-mono.svg
├── blackflix/   blackflix-gold.svg    blackflix-mono.svg
└── blackboard/  blackboard-gold.svg   blackboard-mono.svg
```

PNG exports sit alongside the SVG in the same folder:

```
blackgpt-gold-512.png
blackgpt-gold-256.png
blackgpt-gold-128.png
blackgpt-gold-64.png
blackgpt-gold-32.png
```

## What each size is for

| Size | Use |
|---|---|
| SVG | Anything that scales — web, print, app headers |
| 512 | Social profile images, README headers |
| 256 | App icons, cards |
| 128 | Small UI, list rows |
| 64 | Nav bars, compact headers |
| 32 | Favicons |

## Notes

Fourteen files in total: four BIA marks in gold only — crest, badge, seal
and the system lockup — plus five application marks in gold and mono.

Current assets are raster (PNG/JPEG) at roughly 1200–1700px. SVG versions
do not exist yet; trace them when a mark needs to scale cleanly. Only
`bia-badge-gold.png` has a transparent background — the rest carry their
black field, so they need a dark surface or a re-export to sit elsewhere.

SVG is preferred. If a mark only exists as raster, export the largest
version you have and generate the smaller sizes down from it — never scale
up. The seal needs at least 200px to keep its ring text legible; below
that, use the badge instead.

Keep the background transparent where the tool allows it, so marks sit on
any surface.
