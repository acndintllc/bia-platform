# Brand assets

Drop files straight into the folder for each mark. Specification and usage
rules live in [`docs/BRAND.md`](../../docs/BRAND.md).

## Naming

`<mark>-<variant>.svg` for vector, `<mark>-<variant>-<size>.png` for raster.

Variant is `gold` or `mono`. Size is the pixel width.

```
assets/brand/
├── bia/
│   ├── bia-crest-gold.svg      bia-crest-mono.svg
│   ├── bia-badge-gold.svg      bia-badge-mono.svg
│   └── bia-seal-gold.svg       bia-seal-mono.svg
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

Twelve marks in total: three BIA lockups plus five applications, each in
gold and mono.

SVG is preferred. If a mark only exists as raster, export the largest
version you have and generate the smaller sizes down from it — never scale
up. The seal needs at least 200px to keep its ring text legible; below
that, use the badge instead.

Keep the background transparent where the tool allows it, so marks sit on
any surface.
