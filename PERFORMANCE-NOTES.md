# Em Poertner Portfolio — Performance Pass

## High-impact changes

- Removed `imagesLoaded` from Masonry initialization. The portfolio layout now relies on intrinsic image dimensions instead of forcing every portfolio image to load before layout.
- Converted the 35 unique live portfolio images to resized WebP assets (max 1240px wide).
- Added `width`, `height`, `loading="lazy"`, and `decoding="async"` to the 33 visible portfolio thumbnails.
- Changed all 35 images inside hidden project popups from `src` to `data-src`; `main.js` assigns `src` only when the popup opens.
- Converted the desktop and mobile hero images to resized WebP and added media-specific preload hints.
- Removed the full-screen preloader, so useful content can paint immediately.
- Removed unused `jquery.validate.js`, `imagesloaded.pkgd.js`, and `jquery.mb.YTPlayer.js` from the production folder.
- Replaced the two live Ionicons glyphs with inline SVG and removed the Ionicons font files.
- Reduced the Google Fonts request to weights used by the current CSS and enabled `display=swap`.
- Made the core local stylesheets normal render-blocking stylesheets; only popup CSS and web fonts remain deferred.
- Normalized active portfolio image paths while rewriting them to WebP.
- Removed `.git`, `.DS_Store`, `.vscode`, `to_delete`, and unused alternate hero/source images from this production package.

## Measured source-size changes

These numbers are file sizes from the supplied source and optimized production folder; they are not Lighthouse transfer-size measurements.

- Unique live portfolio image assets: **27.33 MB → 3.51 MB** (~87% smaller)
- Desktop hero: **2,208 KB → 341 KB** (~85% smaller)
- Mobile hero: **2,669 KB → 293 KB** (~89% smaller)
- Active JavaScript set: **337 KB → ~280 KB** raw/uncompressed
- Production folder (excluding the original repo's Git history): **~42 MB → ~7.2 MB**
- Hidden popup images requested on initial HTML parse: **35 → 0** (`data-src` until popup open)

## Files changed

- `index.html`
- `css/basic.css`
- `css/layout.css`
- `js/main.js`
- Portfolio image assets under `images/works`, `images/pages`, and `images/marketing`
- Hero assets `images/topper3.webp` and `images/topper6.webp`

## Files removed from production

- `js/imagesloaded.pkgd.js`
- `js/jquery.validate.js`
- `js/jquery.mb.YTPlayer.js`
- Ionicons font files / `fonts/`
- Original live portfolio JPG/PNG files replaced by WebP
- Original `topper3.jpg` and `topper6.jpg` replaced by WebP
- Unused alternate hero images and repository-only files/directories listed above

## Validation performed

- All active local HTML/CSS/JS/image references resolve to files in this folder.
- All 35 popup images have `data-src` and no initial `src`.
- All 33 visible portfolio thumbnail images use WebP, native lazy loading, async decoding, and intrinsic dimensions.
- Project/filter/popup counts match the supplied HTML (33 projects / 33 popups).
- Visible page text matches the supplied page after removing only the preloader.
- `main.js` and `masonry-filter.js` pass Node syntax checks.

## Hosting-side follow-up

The static code cannot set origin/CDN response headers. On the production host, enable Brotli/gzip compression and long-lived caching for versioned images, CSS, JS, and fonts. After deployment, run Lighthouse/PageSpeed Insights against the live URL and tune LCP/cache settings using real production response headers and network latency.
