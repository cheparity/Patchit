# Repository instructions

## Purpose

Patchit is an algorithm research repository for small, reproducible labs based on
[轻量级扰动检测调研](chatgpt-conversation://6ad58bb4-dab8-83ec-81b9-c5355c6a3152).
The main focus is lightweight adversarial-patch detection and localization for
object detectors, including mechanism studies and lightweight repair experiments.
Read `README.md` and the relevant lab notes before making changes.

## Python development

- Use `uv` and the repository-local `.venv` for all Python development.
- Use tmux if you need to run long-time training works.
- Manage dependencies with `uv add`, `uv add --dev`, and `uv remove`; synchronize
  the environment with `uv sync`. Do not use system Python, global installs,
  standalone `pip`, or Conda for repository work.
- Run scripts and tools with `uv run`. If an editor or notebook needs an
  interpreter, select `.venv/bin/python`.
- When the first Python lab is added, initialize `pyproject.toml` and the uv
  environment as described in `README.md`. Track `pyproject.toml` and `uv.lock`;
  keep `.venv` and Python caches out of Git.
- Add dependencies only when a lab needs them. Record Python and relevant
  accelerator/runtime versions for reproducible experiments.

## Keep implementation simple

- Make the smallest change that implements the requested idea. Avoid unrelated
  refactoring, formatting, dependency upgrades, and speculative features.
- Prefer straightforward functions, descriptive names, and explicit data flow.
  Avoid unnecessary class hierarchies, registries, wrappers, and frameworks.
- Start with one clear baseline and one runnable experiment. Share code only
  when multiple labs actually need it; do not build a general experiment platform.
- Comment on mathematical assumptions and non-obvious choices. Keep formulas,
  tensor shapes, units, and metric definitions clear where they matter.
- Run a small check appropriate to the change. For algorithm changes, check a
  known case or baseline before a large run. Report what was checked and any
  checks that could not be run; never invent results.

## Notes and research records

- Keep documentation in Markdown. Each lab should have a `README.md` with its
  question, hypothesis, method, exact run commands, results, and limitations.
  Use the lab-note template in the repository `README.md`.
- Record dataset source/version and splits, model/checkpoint, attack settings,
  seed, configuration, code revision, and relevant hardware/software details.
- Distinguish literature claims, hypotheses, and measured findings. Link primary
  papers or official implementations when using their methods. Treat the source
  conversation as research context, not proof of correctness or novelty.
- Record failed runs and negative results, with enough context to avoid repeating
  mistakes. Update affected docs alongside code and maintain the README lab index.
- Keep offline analysis separate from deployment evaluation: document whether a
  method uses clean image pairs, labels, true patch masks, gradients, or extra
  detector passes. Do not silently use unavailable information at inference time.
- Use matched ordinary-sticker and occlusion controls where relevant. Keep patch
  presence labels separate from attack success, prevent train/test leakage, and
  report clean-image false positives alongside attacked-image performance.
- Measure full-pipeline latency when claiming a method is lightweight, including
  patch detection, repair, and any repeated object-detector passes.

## Repository hygiene

- **Do not create, download, or leave Office documents anywhere in this repo**,
  including ignored or temporary directories. This includes `.ppt`, `.pptx`,
  `.doc`, `.docx`, `.xls`, `.xlsx`, their macro/template variants, `.odt`, `.ods`,
  `.odp`, and `.rtf`. Put any required external exports outside the repository.
- Keep notes and reports as Markdown; use small text formats such as JSON, CSV,
  or TOML for configurations and result summaries.
- Keep datasets, model weights, generated media, and large run artifacts outside
  Git. Record their locations and how to obtain or reproduce them in lab notes.
  Add appropriate ignore rules when introducing generated local files.
- Create directories and tooling only as needed. Preserve unrelated user work.
