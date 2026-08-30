# EnviroCheck AI

An AI agent that calculates and classifies Indonesia's official Air Pollutant Standard Index (ISPU) — built so that the LLM reasons about *which* numbers to use, but never does the arithmetic itself.

Capstone project for **IBM SkillsBuild University Education x Hacktiv8 Indonesia** — Health track (AI Agent for Healthcare).

## Why a "no-calculation" agent?
ISPU conversion isn't a single formula — it depends on which pollutant you're measuring (PM10, SO2, CO, O3, NO2), each with its own measurement window (24h, 8h, or 1h) and its own threshold table. Getting it right means: matching a raw concentration to the correct table row, running an interpolation formula, then comparing across pollutants to find the one driving the overall air quality rating.

LLMs are fluent but not reliable at that kind of multi-step arithmetic — they'll produce a plausible-looking number that's simply wrong. EnviroCheck AI is designed around that weakness: the agent decides *what* to calculate and *which values* to use, but every actual computation is delegated to a Calculator tool, so the final index number is verifiable rather than guessed.

## What's in this repo
| File | Purpose |
|---|---|
| `EnviroCheck_AI_ISPU.json` | Langflow export of the complete agent pipeline |
| `referensi_ispu.md` | ISPU threshold tables, interpolation formula, and health category definitions (loaded as the agent's reference context) |

## Pipeline
```
Chat Input → Read File (ISPU reference) → Prompt Template → Agent (Gemini + Calculator tool) → Chat Output
```

Step by step:
1. User enters pollutant concentration values in chat.
2. A Read File node loads the ISPU reference document (thresholds, formula, category definitions).
3. A Prompt Template turns that reference into the agent's standing instructions.
4. The Agent identifies which parameters were provided, looks up the matching threshold bounds, builds the interpolation expression `I = ((IA - IB) / (XA - XB)) x (Xx - XB) + IB`, and calls the Calculator tool to evaluate it — manual computation by the LLM is explicitly disallowed in its instructions.
5. Once every parameter is scored, the agent identifies the dominant pollutant, assigns the final ISPU category, and returns a short plain-language interpretation.
6. If the input is incomplete, the agent asks for clarification instead of assuming values.

## Running it
1. Install [Langflow](https://www.langflow.org/).
2. Import `EnviroCheck_AI_ISPU.json`.
3. Point the Read File node to `referensi_ispu.md`.
4. Add your Gemini API key in the Agent node.
5. Open the Playground and enter pollutant readings to get a classification.

## Stack
Langflow · Gemini · Calculator tool (for verified ISPU interpolation)
