
# Pigmentary

A lightweight, serverless SVG color palette gallery hosted on GitHub Pages. Pigmentary indexes AI-generated SVG color strips so you can inspect swatches, download raw `.svg` files, copy clean one-hex-per-line color lists, and extract embedded prompt text with zero backend infrastructure.

**Live Gallery:** [pigmentary.github.io](https://pigmentary.github.io)  
**Companion Generator:** [Gemini Palette Studio](https://share.gemini.google/h0fmiHOGVHBW)

---

## Companion Gemini App

Pigmentary is paired with a custom [Gemini Palette Studio](https://share.gemini.google/h0fmiHOGVHBW) web app built to generate structured color palettes from natural-language prompts and export them as clean vector swatches.

* **Prompt-to-Palette Generation:** Enter any mood, scene, or theme (such as *watercolor landscape kit* or *1970s retro desert*) to generate cohesive 2- to 8-color palettes with descriptive color names.
* **Color Locking & Refinement:** Lock up to 2 favorite swatches to preserve anchor colors while regenerating the rest of the palette.
* **Direct Vector & Hex Export:** Copy hex codes immediately or export the palette directly as an `.svg` file with embedded prompt metadata ready to upload into Pigmentary.

---

## Gallery Features

* **Two-Column Strip Feed:** Displays full-bleed SVG color strips side by side with horizontal palette titles and quick actions.
* **Popup Swatch Inspector:** Click any strip or palette name to preview the full SVG, inspect detected color counts and prompt metadata, and trigger actions.
* **One-Click Exports:**
  * **Download SVG:** Saves the original `.svg` file directly from browser memory.
  * **Copy Hexes:** Extracts unique hex values in appearance order and copies them in a clean one-hex-per-line format.
  * **Copy Prompt:** Parses prompt text from SVG IDs, classes, or `data-prompt` attributes (`#prompt`, `.prompt`, `#prompt-text`, `.prompt-text`, `[data-prompt]`).
* **Serverless GitHub Publishing:** Built-in `Add SVG` drawer commits new entries straight to `palettes.json` via the GitHub REST API using a browser-stored Fine-Grained Personal Access Token.

---

## Repository Structure

```text
pigmentary.github.io/
├── index.html      # Single-file gallery UI, SVG parser, and GitHub API uploader
├── palettes.json   # Auto-generated JSON store of uploaded SVG palettes
└── README.md       # Project documentation

```

---

## Setup & Deployment

1. **Create the Repository:**
Create a public repository named `pigmentary.github.io` under the `Pigmentary` GitHub account and upload `index.html`.
2. **Enable GitHub Pages:**
Go to **Settings > Pages**, set the source to **Deploy from a branch**, and select `main` (`/ (root)`).
3. **Verify Repository Config in `index.html`:**
Ensure `GITHUB_CONFIG` in `index.html` matches your repository details:
```javascript
const GITHUB_CONFIG = {
  owner: "Pigmentary",
  repo: "pigmentary.github.io",
  branch: "main",
  dataPath: "palettes.json",
  storageKey: "pigmentary_gh_pat",
};

```



---

## Publishing New SVG Palettes

1. Generate and export an `.svg` palette from the [Gemini Palette Studio](https://share.gemini.google/h0fmiHOGVHBW).
2. Create a **Fine-Grained Personal Access Token** on GitHub scoped exclusively to `pigmentary.github.io` with **Contents: Read and write** permission.
3. Open pigmentary.github.io and click **Add SVG**.
4. Paste your token once (saved locally in `localStorage` so you do not need to re-enter it on subsequent visits), choose your `.svg` file, enter a palette name, and click **Add to list**.
5. Pigmentary commits the updated `palettes.json` to `main`, and GitHub Pages refreshes automatically within 30–60 seconds.

---

## Developer

Built and maintained by [Saurabh Gayali](https://github.com/saurabhgayali).

