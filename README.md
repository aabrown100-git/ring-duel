# Ring Duel

A this-or-that game for finding an engagement ring style. You see two drawn rings at a time and pick the one you'd rather wear. After 20, 30 or 40 picks, the game narrows in on your style and shows a final-four bracket, then your winning ring with a jeweler-style spec card.

## How to play

Play online: [Ring Duel](https://aabrown100-git.github.io/ring-duel/).

On the start screen you can set:

- **Skin tone:** Choose from six tones to preview rings on an illustrated hand. Your choice is saved on this device and does not affect the preference model.
- **Picks:** 20, 30 or 40 (default 30). More picks give a more accurate result.
- **Timer:** 5s, 10s, 15s or Off (default 10s).

## What it varies

| Trait | Options |
|---|---|
| Stone shape | Round, oval, emerald, cushion, pear, marquise, princess |
| Setting | Solitaire, halo, three-stone, bezel, cluster |
| Metal | 18k yellow gold, platinum, 18k rose gold |
| Band | Thin, pavé, twisted, wide |
| Accents | None, tapered baguettes, hidden halo |
| Prongs & details | Four prongs, six prongs, double claw, milgrain |

## How pairs are chosen

Each option has a hidden "appeal" weight, estimated with a Bayesian logistic (Bradley–Terry) choice model.

1. **Mapping (first 40% of picks):** from 300 random candidate pairs that differ in 1–3 traits, it shows the one with the highest expected information (Bayesian D-optimal design). This favors near coin-flip pairs.
2. **Homing in (the rest):** her current best-guess ring vs. that ring with one trait swapped, picking the most informative swap.
3. **Final four:** the best-guess ring plus three alternatives drawn from the model's uncertainty, in an untimed bracket.

Before each round, both rings are drawn offscreen and compared pixel by pixel, so two rings that look the same are never shown together.

Comparison rings are drawn with the HTML canvas. The winning ring also gets a 3D studio preview with reflective metal, faceted stones, and geometry matching its selected traits. Use the results-screen button to switch between the studio view and the original illustration.

The studio preview loads Three.js 0.170.0 from esm.sh on demand and requires internet access and WebGL. If it cannot load, the illustration and results still work. Google Fonts is also loaded externally. The preview is illustrative, not a manufacturing model.

## Interactive 3D model

On the results screen, drag the ring to rotate it and scroll or pinch to zoom. Keyboard users can focus the model and use arrow keys to rotate, plus/minus to zoom. Reset view restores the original camera angle. Download 3D model saves a GLB file with the ring geometry, materials, and selected traits for use in a 3D viewer or editor. The model uses illustrative proportions and sizing; it is not production CAD or a print-ready jewelry design.

## Export a Blender brief

After choosing the winner, click **Export Blender brief**. This downloads one self-contained Markdown file containing a ready-to-use Codex prompt, the exact selected traits as JSON and readable specifications, and the Python source of the earlier Blender prototype. Attach the file to a new Codex chat and ask it to follow the brief. No API key, backend, WebGL, or internet connection is needed for the export.

The Python source is an oval-halo example, not a generator for all designs. The prompt instructs Codex to adapt it to the actual winner, document unspecified dimensions, render and inspect the result, and deliver a `.blend`, `.glb`, preview, and reproducible script. Exporting does not start a Codex session or run Blender automatically.

Ring comparisons, the final-four bracket, and the winning illustration use the selected hand tone. The separate interactive 3D view shows the ring alone. The Blender brief includes the hand-preview color for an optional on-hand render.
