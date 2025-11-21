# Website App

An Electron Forge wrapper that turns any static website into a desktop application. Drop your pre-built site into the project, tweak the branding assets, and ship cross-platform packages via Electron.

## Prerequisites

- macOS, Windows, or Linux with Node.js 18+ and npm 9+
- Git (optional, but recommended)
- Bundled static website output (HTML/CSS/JS) ready to embed

## Getting Started

1. Install dependencies:
   ```bash
   npm install
   ```
2. Run the app in development mode with live reload:
   ```bash
   npm start
   ```

## Packaging a Static Website

Follow these steps every time you want to bundle a new static site build into the Electron shell:

1. **Copy your site into `dist/`:**
   - Build your static site with your favorite framework (Next.js, Vite, Astro, etc.).
   - Remove any previous contents inside `dist/` in this repository.
   - Paste the latest build artifacts (HTML, CSS, JS, assets) directly under `dist/`.

2. **Replace branding assets under `assets/`:**
   - Update `assets/icon.png` (and other icon sizes if present) with your app icon.
   - Swap the background artwork files (for example `assets/background.png`) so installer windows and splash screens show the correct branding.
   - Keep file names and dimensions consistent unless you also update the Electron Forge maker configuration.

3. **Update metadata in `package.json`:**
   - Change `name`, `productName`, and `description` to match the new project.
   - Optionally adjust `author`, `version`, and any custom fields you surface in auto-updaters or installers.
   - Save the file so Electron Forge uses the latest metadata when creating distributables.

## Build & Distribution Commands

- `npm run package` – Creates unpacked builds for the current platform.
- `npm run make` – Produces installers/DMGs/ZIPs based on the makers configured in `forge.config.js`.
- `npm run make-universal` (macOS only) – Produces a universal binary for Apple Silicon and Intel.
- `npm run publish` – Runs the publish pipeline defined in Electron Forge (configure targets before use).

Artifacts appear under the `out/` directory. Always test the generated installer on a clean machine or VM before distributing.

## Customization Tips

- Adjust Electron main process behavior in `src/index.js` and preload logic in `src/preload.js`.
- Review `forge.config.js` to tweak makers, DMG backgrounds, Squirrel settings, or code-signing hooks.
- Consider wiring your CI/CD pipeline to run `npm ci && npm run make` so releases remain reproducible.

## Troubleshooting

- If the app launches but shows a blank window, ensure your static files exist under `dist/` and that the entry `index.html` path matches what `src/index.js` loads.
- When icons appear pixelated, provide higher-resolution PNG/ICNS files in `assets/` and update the Forge makers accordingly.
- For signing or notarization issues on macOS, integrate your Apple Developer credentials into the Forge configuration or use `electron-osx-sign` hooks.
