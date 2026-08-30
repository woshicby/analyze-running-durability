# Analyze Running Durability

[中文说明](README.zh-CN.md)

An OpenAI skill for analyzing how well a runner preserves output during repeated long runs. It combines heart-rate–output decoupling, RPE, fueling, weather, terrain, the sequence of reported symptoms, and 24–48 hour recovery to identify the most plausible current limiter and the next useful training experiment.

## What it does

- Designs a four-week durability field test with three comparable long runs.
- Normalizes speed or running-power efficiency, carbohydrate and fluid intake, RPE, and onset timing.
- Checks whether sessions are comparable before interpreting trends.
- Separates observed data, plausible explanations, competing explanations, confidence, and the next discriminating test.
- Supports road, trail, marathon, and ultra contexts without treating one decoupling value as a diagnosis or universal threshold.
- Produces a concise coaching report and identifies symptoms that should stop performance interpretation.

## Repository structure

```text
analyze-running-durability/
├── SKILL.md
├── agents/openai.yaml
├── assets/icon.svg
├── references/
│   ├── data-schema.md
│   └── interpretation.md
└── scripts/summarize_durability.py
```

`SKILL.md` is the entry point. The reference files contain the data schema and interpretation framework. The Python script provides deterministic CSV normalization; it does not make a diagnosis or select training on its own.

## Install

### ChatGPT

Download this repository as a ZIP file and import the skill folder through ChatGPT's Skills interface. Keep the directory structure intact.

### Codex

Clone the repository into the local skills directory:

```bash
git clone https://github.com/SrJackCM/analyze-running-durability.git \
  ~/.codex/skills/analyze-running-durability
```

Restart or refresh Codex if the skill is not discovered immediately.

## Use

Invoke the skill explicitly:

```text
Use $analyze-running-durability to compare my last four long runs, identify what deteriorated first, and recommend the next four-week training emphasis.
```

Useful input includes duration, first- and second-half heart rate plus speed or power, RPE, carbohydrate and fluid intake, conditions, route and elevation, the first meaningful change and its onset, and recovery at 24 and 48 hours. Missing data should be reported rather than invented.

### CSV helper

Python 3.9 or later is sufficient; the script uses only the standard library.

```bash
python3 scripts/summarize_durability.py long-runs.csv > summary.md
```

Use `--metric speed` or `--metric power` to require one output type. See [the data schema](references/data-schema.md) for supported columns.

## Interpretation and safety

- A decoupling percentage is one summary of the heart-rate–output relationship, not a complete durability score.
- Route, weather, altitude, stops, sensor quality, pacing, fueling, illness, pain, and recovery can change the interpretation.
- The skill is for performance analysis and coaching support, not medical diagnosis.
- Chest pain, fainting, neurological symptoms, severe breathing difficulty, dark urine with severe muscle pain, gastrointestinal bleeding, inability to keep fluids down, acute injury, gait-changing pain, or persistent worsening symptoms warrant appropriate clinical evaluation.

## Contributing

Issues and focused pull requests are welcome. Please preserve the evidence-first interpretation model and avoid introducing universal pass/fail thresholds without strong support.
