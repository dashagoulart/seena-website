# Photo upload guidelines

Any photo added to this folder (or `product_images/`, `specialist_images/`, etc.) must be resized and compressed before committing. Raw exports from phones/cameras run 10-16MB at 4000-6000px — far more than any page displays them at — and that's what was making the gallery slow to load.

## Before adding a new photo

1. Resize so the longest edge is **1800px** (plenty for retina displays at the sizes we display images on this site — hero banners aside, see below).
2. Re-compress as JPEG at **quality 75**.
3. Confirm the result is roughly **200-500KB**. If it's still over ~800KB, drop quality a bit further (65-70) before adjusting dimensions.

One command does both steps:

```bash
sips -Z 1800 --setProperty formatOptions 75 your-photo.jpg
```

`-Z 1800` resizes so the longest side is 1800px (preserves aspect ratio). Run it in place — it overwrites the file.

## If a photo needs to display larger than usual (e.g. a full-bleed hero)

Use `-Z 2400` instead of `1800`, still at quality 75. Don't go beyond 2400px on this site — nothing here displays a photo wide enough to need it.

## Also do this in the HTML

- Add `loading="lazy" decoding="async"` to every `<img>` except the first one visible on page load (that one should stay `loading="eager"` so it doesn't delay the initial paint).
- Keep the `gallery-*`, naming pattern consistent with existing files (descriptive, kebab-case, prefixed by section).

## Why this matters

A single unoptimized photo (10-16MB) can take several seconds to load on mobile data, and the gallery carousel showed a related bug (blank gap on the last slide) that was easier to spot with slow-loading images. See commit `684570d` for the fix and reasoning.
