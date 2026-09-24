# OMANISHA Data Dictionary

This document describes the schema, fields, and label inventory for the OMANISHA dataset file [`dataset.csv`](dataset.csv).

**Dataset name:** OMANISHA (Online Misogynistic Annotated Natural-language Instances for Sentiment and Hate Analysis)  
**Instances:** 7,017  
**File format:** CSV (comma-separated), UTF-8 with BOM  
**Header row:** Yes (first row)  
**Missing values:** None (all fields are non-empty for every row)  
**License:** MIT (see [`LICENSE`](LICENSE))

---

## File schema

| Column name | Data type | Required | Description |
|-------------|-----------|----------|-------------|
| `Final annotation` | string (categorical) | Yes | Final gold label after dual annotation and disagreement resolution. One of four predefined misogyny categories (see [Label inventory](#label-inventory)). |
| `Text` | string (Bengali, Unicode) | Yes | Original Bengali instance. Includes formal and informal register. Constructed by the authors; not verbatim social-media text. |
| `English Translation` | string (English) | Yes | Parallel English translation of `Text`, provided for cross-lingual accessibility and comparative NLP use. |

### Column details

#### `Final annotation`
- **Role:** Target / class label for supervised classification and evaluation.
- **Cardinality:** 4 classes (see counts below).
- **Canonical values (use these exact strings):**
  - `Non Misogynistic`
  - `Stereotype`
  - `Derogation`
  - `Sexual Harassment`
- **Notes:** Labels are case-sensitive. Prefer the Title Case forms listed above when filtering or training.

#### `Text`
- **Role:** Primary input feature (Bengali source text).
- **Language:** Bengali (Bangla), Unicode / UTF-8.
- **Content policy:** Samples were independently constructed by the authors after reviewing public online discourse patterns. The file does not contain verbatim or directly paraphrased social media comments.

#### `English Translation`
- **Role:** Auxiliary parallel text for accessibility, inspection, and cross-lingual research.
- **Language:** English.
- **Alignment:** One translation per Bengali `Text` row (row-aligned).

---

## Label inventory

| Label | Count | Share | Definition |
|-------|------:|------:|------------|
| `Non Misogynistic` | 2,420 | 34.5% | Text that does not express, endorse, or imply hostility, prejudice, or abuse toward women. Neutral, supportive, or otherwise non-misogynistic content. |
| `Stereotype` | 1,744 | 24.8% | Text that assigns fixed, generalized, or reductive traits, roles, or expectations to women (or girls) as a group, without necessarily using overt insults. |
| `Derogation` | 1,527 | 21.8% | Text that demeans, belittles, ridicules, or otherwise expresses contempt toward women, including appearance-based or character-based insults. |
| `Sexual Harassment` | 1,326 | 18.9% | Text that sexualizes, objectifies, or directs unwanted sexual attention, propositions, or sexually abusive language toward women. |
| **Total** | **7,017** | **100%** | |

**String hygiene:** One row currently uses lowercase `stereotype` instead of `Stereotype`. Treat it as `Stereotype` when training or evaluating (normalize with `.str.strip()` / case-folding to the canonical list above).

### Label design notes
- Categories are **mutually exclusive** at the instance level: each row has exactly one `Final annotation`.
- Unlike binary misogyny datasets, OMANISHA supports **fine-grained** (category-level) modeling.
- Pairwise Jaccard similarity among classes in the paper/analysis ranges from **0.12 to 0.21**, indicating taxonomic separation across labels.

---

## Annotation process (summary)

| Item | Detail |
|------|--------|
| Annotators | Two native Bengali annotators per sample, drawn from a pool of four annotators with diverse gender, religious, ethnic, and geographical backgrounds |
| Disagreement resolution | Structured consultation with a third annotator |
| Agreement | Cohen’s Kappa κ = 0.76; Krippendorff’s Alpha α = 0.75 (substantial agreement) |
| Preprocessing | Duplicate removal, text normalization, and coherence checking |

---

## Example rows

| Final annotation | Text (Bengali) | English Translation |
|------------------|----------------|---------------------|
| `Non Misogynistic` | *(Bengali source in CSV)* | Apu is successful as a first-generation female entrepreneur. |
| `Derogation` | *(Bengali source in CSV)* | This girl’s eyebrows are so thick that they look like a black dam. |
| `Stereotype` | *(Bengali source in CSV)* | It is better for the family to marry girls off early. |

Full Bengali strings are stored in `dataset.csv`; open the file in a UTF-8–aware editor or load with `encoding="utf-8-sig"` in Python.

---

## Recommended loading (Python)

```python
import pandas as pd

df = pd.read_csv("dataset.csv", encoding="utf-8-sig")
assert list(df.columns) == ["Final annotation", "Text", "English Translation"]
assert df.isna().sum().sum() == 0
```

Canonical class list for modeling:

```python
CLASSES = [
    "Non Misogynistic",
    "Stereotype",
    "Derogation",
    "Sexual Harassment",
]
```

---

## Related files

| File | Purpose |
|------|---------|
| [`dataset.csv`](dataset.csv) | Full annotated dataset |
| [`README.md`](README.md) | Dataset overview and motivation |
| [`LICENSE`](LICENSE) | MIT license terms |
| [`data_analysis_source.ipynb`](data_analysis_source.ipynb) | Analysis / visualization source |
