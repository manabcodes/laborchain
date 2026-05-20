# LaborChain

**An Ontological Framework for Tracing and Documenting Labor Exploitation Provenance in AI Training Lineages**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> *"Entre los individuos, como entre las naciones, el respeto al derecho ajeno es la paz."*  
> — Benito Juárez

---

## What is LaborChain?

LaborChain is an OWL ontology for modeling and tracing the labor exploitation conditions embedded in AI training lineages. Just as model cards track data provenance and bias inheritance, LaborChain tracks the *labor conditions* underneath a model — who moderated its training data, under what conditions, at what wage, in what jurisdiction, and whether they could refuse — and how those conditions propagate when one model is fine-tuned from another.

The central claim: labor exploitation provenance is not a representational artifact that can be corrected through post-hoc mitigation. It is a historical fact about production. You cannot fine-tune away the conditions under which workers were paid $1.32 an hour to review child sexual abuse material. The blood does not wash out.

---

## Repository Contents

| File | Description |
|------|-------------|
| `laborchain.ttl` | OWL ontology in Turtle format — schema + Sama/OpenAI instance data |
| `cq03.sparql` | Was adequate psychological support provided? |
| `cq06.sparql` | What is the wage ratio between labor and deploying jurisdictions? |
| `cq07.sparql` | Was labor located in a low-regulation jurisdiction? |
| `cq08.sparql` | How many subcontracting layers separate the lead company from workers? |
| `cq10.sparql` | Does the deploying jurisdiction have stronger labor protections? |
| `cq11.sparql` | Which fields are populated from self-disclosure vs third-party sources? |
| `cq12.sparql` | In which jurisdiction did the labor occur? |
| `cq15.sparql` | Which base models does this model inherit exploitation provenance from? |
| `cq16.sparql` | Full lineage of exploitation provenance inheritance with depth |
| `cq18.sparql` | Which models carry exploitation provenance from a documented case? |
| `cq20.sparql` | Were workers able to organize without retaliation? |

---

## Namespace

```
@prefix lc: <https://manabcodes.github.io/laborchain#>
```

---

## Core Classes

| Class | Description |
|-------|-------------|
| `AIModel` | Any trained model — foundation, fine-tuned, or distilled |
| `TrainingDataset` | Dataset used in training, including RLHF feedback datasets |
| `LaborUnit` | A cohort of workers engaged in a specific training labor task |
| `LaborTask` | Type of training labor (DataLabeling, ContentModeration, RLHFAnnotation, etc.) |
| `Contractor` | The AI company directly contracting labor (e.g. OpenAI) |
| `Subcontractor` | The company employing workers (e.g. Sama, Remotasks) |
| `Jurisdiction` | Legal jurisdiction in which labor occurs |
| `ExploitationRecord` | Documented instance of labor exploitation conditions |
| `ModelLineage` | Chain of inheritance relationships between models |

---

## Running the SPARQL Validation Suite

Requires [Apache Jena](https://jena.apache.org/) (`brew install jena` on Mac):

```bash
# Run a single query
sparql --data laborchain.ttl --query cq06.sparql

# Run all queries
for f in cq*.sparql; do echo "=== $f ==="; sparql --data laborchain.ttl --query $f; done
```

---

## The LaborChain Model Card

The ontology supports generation of **LaborChain Model Cards** — structured artifacts documenting labor exploitation conditions for any AI model. Cards record:

- Who produced the training data and under what conditions
- Wage ratio between labor jurisdiction and deploying company jurisdiction
- Psychological harm indicators
- Labor rights conditions (unionization, consent, coercion)
- Model lineage and inherited exploitation provenance
- What the company disclosed vs what required investigative journalism

**Try it:** [LaborTrail — The Trail of Your Blood on Circuits](https://huggingface.co/spaces/sage-lollipop/laborchain) — enter any HuggingFace model ID to generate a LaborChain Model Card.

---

## Proof of Concept

The repository includes instance data for two documented cases:

**OpenAI/Sama** — Wage ratio: 0.09. Traumatic content processed. Psychological harm documented. Unionization suppressed (260 workers terminated). Company disclosure: None. Source: Perrigo, B. *TIME Magazine*, January 2023.

**GPT Family Lineage** — Exploitation provenance from the Sama labor unit propagates through GPT-3.5 (depth 1), ChatGPT and GPT-4 (depth 2), GPT-4o (depth 3), and any GPT-4 fine-tune (depth 3+).

---

## Citation

If you use LaborChain in your research, please cite:

```
@inproceedings{anonymous2026laborchain,
  author    = {Anonymous},
  title     = {{LaborChain}: An Ontological Framework for Tracing and Documenting Labor Exploitation Provenance in {AI} Training Lineages},
  booktitle = {Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society (AIES 2026)},
  year      = {2026}
}
```

---

## License

Ontology and SPARQL queries: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
