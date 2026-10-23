# Ring Duel

A this-or-that game for finding an engagement ring style. You see two drawn rings at a time and pick the one you'd rather wear. After 20, 30 or 40 picks, the game narrows in on your style and shows a final-four bracket, then your winning ring with a jeweler-style spec card.

## How to play

Open `index.html` in any browser. There's nothing to install or build.

On the start screen you can set:

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

Rings are drawn with the HTML canvas. The only outside resource is Google Fonts.
