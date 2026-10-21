# Patchit

An algorithm research repository for small, reproducible labs on lightweight
adversarial-patch detection and defense for object detectors.

The ideas come from
[轻量级扰动检测调研](chatgpt-conversation://6ad58bb4-dab8-83ec-81b9-c5355c6a3152).
The central question is whether we can distinguish an adversarial patch from an
ordinary sticker or occlusion using its effect on the detector, then locate and
handle it with little additional computation.

**Status:** documentation initialized; no Python labs or measured results yet.
Research directions below are hypotheses to test.

## Candidate labs

| Direction | Question to test |
| --- | --- |
| Patch–detector relationship | Do task responses and intermediate features reveal harmful patch effects beyond texture or feature magnitude? |
| Foreground/background mechanisms | Under matched sticker and occlusion controls, does a patch reduce useful context, disturb foreground evidence, or affect localization and post-processing? |
| Paired supervision | Can clean, ordinary-sticker, and adversarial-patch examples teach a small detection/localization head to predict task impact and generalize to unseen patches? |
| Lightweight repair | With the same patch mask and detector, how much detection recovery do simple filling and repair methods provide per added millisecond? |
| Progressive adversarial training | As a separate training direction, does scheduling patch difficulty improve robustness over fixed-strength training at the same training budget? |

Start with a small mechanism experiment and a simple baseline. Keep the repair
backend fixed while comparing patch detectors. Evaluate detection/localization,
clean-image false positives, final object-detection quality, and full-pipeline
latency separately. Strong localization alone does not establish effective defense.

## Python workflow

Use [uv](https://docs.astral.sh/uv/) and its local `.venv` for all Python work.
The repository currently has no Python project configuration. When adding the
first Python lab, run from the repository root:

```bash
uv init --bare --name patchit
uv venv .venv
uv sync
```

Commit the resulting `pyproject.toml` and `uv.lock`. Add `.venv/` and Python caches
to `.gitignore` when initializing the environment. Once the project configuration
exists, a fresh checkout only needs `uv sync` to create or update `.venv`.

Add only the dependencies needed for the current lab with `uv add PACKAGE`, or
`uv add --dev PACKAGE` for development tools. Run Python through `uv run`:

```bash
uv run python --version
```

Select `.venv/bin/python` in editors and notebooks. Do not install repository
dependencies globally or manage a separate environment with pip or Conda. Each
lab must document its actual `uv run` commands, inputs, and expected outputs.

## Organization

Create these directories only when there is content for them:

```text
labs/<lab_name>/       A focused experiment, its code, and a README.md
docs/                 Shared research notes, derivations, and decisions
src/patchit/          Helpers genuinely shared by multiple labs, if needed
tests/                Small correctness checks for algorithms, if needed
```

Keep experiments easy to read and run. Avoid building a framework before the
experiments need one. Store large datasets, weights, and generated outputs outside
Git, and document their locations and reproduction steps.

## Lab notes

Use this outline for each lab's `README.md`. Update it as the experiment changes,
including negative results and failed runs.

```markdown
# Lab: <name>

## Question and hypothesis
What are we testing? What result would support or reject the hypothesis?

## Method and controls
Describe the algorithm, baseline, assumptions, and controlled variables.
Separate offline analysis inputs from information available at inference time.
Link source papers or official implementations; distinguish claims from hypotheses.

## Reproduce
Record the code revision, exact uv run commands, configuration, random seed,
dataset version/splits, model/checkpoint, attack settings, and environment.
Include data/artifact locations, input preparation, and hardware used for timing.

## Results
Record measured metrics, units, sample counts, and timing scope.
Include clean/sticker controls, failures, and links or paths to supporting outputs.
Mark anything not run explicitly; keep patch presence separate from attack success.

## Interpretation and next step
What did we learn? What remains uncertain? What should we test next?
```

For generalization studies, separate source images/videos and patch identities
across splits and hold out attack methods where appropriate. For deployment
results, do not assume access to clean pairs, true boxes, or true patch masks.
Record extra forward/backward passes and all repair costs in the latency budget.

## Lab index

No labs yet. Add a link and short status here when the first lab is implemented.

## Repository rules

- Use uv and `.venv` for Python development.
- Write simple, understandable code and make minimal, focused edits.
- Keep good Markdown notes and reproducible experiment records.
- Do not leave Office documents in this repository, even as ignored or temporary
  files: no PowerPoint, Word, Excel, OpenDocument, or RTF files. Put any required
  exports outside the repository.

See [AGENTS.md](AGENTS.md) for contributor and coding-agent instructions.
