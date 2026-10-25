<h1 align="center">Football Rule Cite</h1>

[Portfolio case study](https://ompatnaik.com/projects/football-rule-cite/) · [Static sample preview](https://ompatnaik.com/Football-Rule-Cite/)

**Describe an incident and a referee’s call, then inspect an explanation linked to retrieved IFAB law excerpts.**

[Demo or published artifacts](https://ompatnaik.com/Football-Rule-Cite/)

Python and local Ollama. Source PDF downloads separately. Hosted page is a sample preview; live explanations require the local server.

By Om Patnaik · repository created July 2026.

[![License: MIT](https://img.shields.io/badge/license-MIT-176b75?style=flat-square)](LICENSE)

## Install

| Platform / path | Start here |
| --- | --- |
| Python | `pip install -r requirements.txt` in a virtual environment |
| Preview | [Open the static sample](https://ompatnaik.com/Football-Rule-Cite/) |

Run `python -m src.cli ingest`, then `python -m src.cli serve` and open http://127.0.0.1:8765. Start Ollama with the configured model (`qwen3.6:27b` by default). The hosted sample needs no model download.

```bash
python -m src.cli ingest
python -m src.cli serve
```

## Why

You want to understand which law might explain a call, with the source passage available to inspect. Football Rule Cite retrieves page-labelled text from the IFAB Laws before asking Ollama for an explanation. The stated call is input; this is not an expert referee-decision benchmark.

## Inspect a cited explanation

Use `explain --call` for a stated decision or `ask` for a direct question. Review retrieved laws and uncertainties rather than treating the generated text as a ruling.

## Read recorded evaluation

Both July 8 runs passed 10/10 seed scenarios for expected-law coverage and required uncertainty presence. Extra law numbers did not fail the scorer; model digests and PDF hashes were not captured. [Full answers and scoring limits](eval/README.md).

## Notes from building it

I kept the source excerpts and citations visible instead of relying on an unsupported model answer. Rescoring the saved runs clarified that passing meant law coverage, not decision correctness. I would add expert-reviewed grounding checks and pinned runtime metadata before making stronger claims.

## Commands

```bash
python -m src.cli ingest        # download and index the source
python -m src.cli serve         # serve the local interface
python -m src.cli explain --call 'Penalty kick' 'A defender trips an attacker inside the penalty area.'  # explain a call
python -m src.cli ask 'An offside attacker interferes with a defender.'  # ask about an incident
python -m src.cli eval --save    # run seed scenarios; requires Ollama
```

## Verify it yourself

```bash
python -m compileall -q src
python -m src.cli eval --save
```

Compilation checks syntax; evaluation needs the ingested source and installed Ollama model. The ten-case scorer checks expected laws and uncertainty presence, not clause accuracy or expert judgment; saved-run rescoring is documented in `eval/README.md`.

## Credits, license and pointers

Source: IFAB Laws of the Game 2026/27. Built with Python, PDF extraction, and Ollama/Qwen; dependency details are in `requirements.txt`. [MIT](LICENSE); IFAB material retains its own terms.

[Full setup, original notes, and project history](README-DETAILS.md).
