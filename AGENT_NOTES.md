# Agent notes — JS-Image-Classifier

Background for anyone (or any agent) editing this repo. Read this before opening a PR.

## Status

This repo is mid-pivot. The 2019 build is still in place — an HTML5 UP template with a TensorFlow.js KNN classifier sketch and credits from a Siraj Raval tutorial. The plan to finish it as **RPS vs the Browser** lives in [issue #1](https://github.com/warrenrross/JS-Image-Classifier/issues/1).

Don't add features to the old scaffolding. The current work is to strip it back to a minimal page and build the game on top.

## Where this repo fits

Two sibling repos share an interest in browser-side hand work and webcam ML. They are deliberately separate, not merged:

| Repo | Role |
| --- | --- |
| **JS-Image-Classifier** (this repo) | Train-your-own webcam classes. Play Rock-Paper-Scissors against what you just taught. |
| [`Hand_AI`](https://github.com/warrenrross/Hand_AI) | A fixed gesture vocabulary as a control surface. Already shipped. |

The split is documented in [ADR-0002](https://github.com/warrenrross/warrenrross.github.io/blob/master/docs/adr/0002-two-sibling-hand-classifier-repos.md) in the personal-site repo. The short version: one is a learning toy, the other is a controller. Keeping them separate stops either one from accreting features that belong in the other.

## Research repo — background for the open design questions below

Deeper research on hand-gesture model choices — lineage from earlier projects, dataset survey, open-weight model survey, transfer-learning surface for each option — lives at:

**[warrenrross/gesture-detect-research](https://github.com/warrenrross/gesture-detect-research)** — see its [RESEARCH.md](https://github.com/warrenrross/gesture-detect-research/blob/main/RESEARCH.md).

It's directly relevant to Open Design Question 1 below (MediaPipe vs TF.js MobileNet + KNN). §6.2 of RESEARCH.md inventories both options as pretrained surfaces; §4 surveys what others have built on top of MediaPipe landmarks specifically.

The research repo is Phase-1-only right now — a survey, not a recommendation. The RPS-vs-the-browser direction here is one of its potential consumers, alongside Hand_AI.

## Open design questions

These are not decided yet. Pick one and write it up in an ADR (or just here) when you do.

1. **MediaPipe Hand Landmarker, or stay on TF.js MobileNet + KNN?** MediaPipe aligns with the sibling repo. KNN over MobileNet embeddings is what the 2019 code already does. Either can work for three classes. Picking MediaPipe makes the two repos share a model; picking TF.js keeps the demo about "you can train a classifier from raw image features" rather than "you trained MediaPipe to map landmarks." Both are legitimate angles for a portfolio piece. See [gesture-detect-research/RESEARCH.md §6.2](https://github.com/warrenrross/gesture-detect-research/blob/main/RESEARCH.md#62-pretrained-open-weight-models-suitable-for-transfer-learning) for the two options side by side.
2. **Where the shared ML plumbing lives.** Webcam plumbing and a tiny landmark/embedding wrapper could be vendored as a small ESM module to avoid drift between this repo and Hand_AI. Worth doing only if the two repos actually need to share code, not preemptively.
3. **Round structure.** Best-of-N? First-to-N? Countdown timing? Show the model's confidence per round? These are gameplay calls, not technical ones — pick what's fun.

## Pointers

- **Plan and checklist:** [issue #1](https://github.com/warrenrross/JS-Image-Classifier/issues/1).
- **Cross-repo decisions:** [`docs/adr/`](https://github.com/warrenrross/warrenrross.github.io/tree/master/docs/adr) in the personal-site repo. Especially ADR-0002.
- **Sibling repo to look at first:** [`Hand_AI`](https://github.com/warrenrross/Hand_AI). Its `AGENT_NOTES.md` covers the in-browser MediaPipe setup, the gesture classifier shape, and the "no backend, no upload" rule. Most of those apply here too.

## What to leave alone

- The LICENSE file. Keep it.
- The repo name. The display name on the portfolio card is "RPS vs the Browser"; the repo stays `JS-Image-Classifier` because URLs are sticky.

## What to remove

- The HTML5 UP template scaffolding and styles.
- The Siraj-tutorial credit block in the README.
- Anything in `index.html` and `assets/` that's there because the 2019 template put it there, not because the game needs it.
