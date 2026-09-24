# Data Dictionary — OMANISHA

**Resource:** OMANISHA (Online Misogynistic Annotated Natural-language Instances for Sentiment and Hate Analysis)  
**Data file:** [`dataset.csv`](dataset.csv)  
**N:** 7,017 instances  
**Format:** Comma-separated values (CSV); UTF-8 with BOM; header in row 1  
**Unit of analysis:** One row = one Bengali text instance with a single gold category label and an English translation  
**Licence:** MIT ([`LICENSE`](LICENSE))

This dictionary specifies the variables released in `dataset.csv`, their admissible values, and the operational meaning of each annotation category.

---

## 1. Variable catalogue

| Variable | Position | Type | Missing | Description |
|----------|----------|------|---------|-------------|
| `Final annotation` | 1 | Nominal (string) | None | Gold-standard category assigned after independent dual annotation and adjudication. Exactly one label per instance. |
| `Text` | 2 | String (Bengali) | None | Source text in Bengali. Formal and informal registers are both present. Instances were authored for this release; they are not copied from public platforms. |
| `English Translation` | 3 | String (English) | None | Sentence-aligned English rendering of `Text`. |

Delimiter: `,` (comma). Fields that contain commas are quoted in the usual CSV manner. There are no blank cells in the released file.

### 1.1 `Final annotation`

Supervised target. Four mutually exclusive categories. Values are stored as plain strings and are case-sensitive. The admissible labels are:

1. `Non Misogynistic`
2. `Stereotype`
3. `Derogation`
4. `Sexual Harassment`

One record in the current release is labelled `stereotype` (lowercase). For analysis it should be mapped to `Stereotype`.

### 1.2 `Text`

Primary linguistic field. Encoding is Unicode Bengali. Preprocessing applied before release comprised duplicate removal, orthographic normalisation, and a coherence check.

### 1.3 `English Translation`

Parallel English text corresponding to the same row’s `Text`. Intended for inspection and for work that benefits from an English reference; the authoritative annotation target remains `Final annotation` on the Bengali `Text`.

---

## 2. Category definitions

Labels follow a four-way scheme. An instance receives the category that best characterises its dominant communicative intent toward women.

| Label | Operational definition |
|-------|------------------------|
| `Non Misogynistic` | The text does not convey hostility, prejudice, or abuse directed at women. Content may be neutral, descriptive, or affirmative. |
| `Stereotype` | The text attributes fixed traits, roles, capacities, or social expectations to women (or girls) as a class. Insult need not be present; generalisation is the defining feature. |
| `Derogation` | The text demeans, ridicules, or otherwise expresses contempt toward women, including attacks on appearance, character, ability, or social worth. |
| `Sexual Harassment` | The text sexualises or objectifies women, or expresses unwanted sexual attention, propositioning, or sexually abusive language. |

Each instance carries only one label. Pairwise Jaccard similarity among the four classes in the accompanying analysis falls between 0.12 and 0.21.

### 2.1 Class frequencies

| `Final annotation` | Frequency | Proportion |
|--------------------|----------:|-----------:|
| `Non Misogynistic` | 2,420 | 0.345 |
| `Stereotype` | 1,744 | 0.249 |
| `Derogation` | 1,527 | 0.218 |
| `Sexual Harassment` | 1,326 | 0.189 |
| Total | 7,017 | 1.000 |

Frequencies for `Stereotype` treat the single lowercase `stereotype` token as belonging to that class.

---

## 3. Annotation procedure (release summary)

| Item | Specification |
|------|----------------|
| Annotator pool | Four native Bengali speakers, varied by gender, religion, ethnicity, and region |
| Labelling protocol | Two independent annotations per instance |
| Disagreement | Resolved by consultation with a third annotator |
| Agreement | Cohen’s κ = 0.76; Krippendorff’s α = 0.75 |

---

## 4. Example rows

One instance from each class (taken from `dataset.csv`):

| Final annotation | Text | English Translation |
|------------------|------|---------------------|
| Non Misogynistic | আপু প্রথম প্রজন্মের নারী উদ্যোক্তা হিসেবে সফল | Apu is successful as a first-generation female entrepreneur. |
| Stereotype | মেয়েদের বিয়ে তাড়াতাড়ি দেওয়াই পরিবারের জন্য ভালো | It is better for the family to marry girls off early. |
| Derogation | এই মেয়ের ভ্রু দুটো এত মোটা যে একটা কালো বাঁধের মতো দেখায় | This girl’s eyebrows are so thick that they look like a black dam. |
| Sexual Harassment | মামুনি তোমাকে ব্রা ছাড়াই সুন্দর লাগছে | Sweetie, you look beautiful even without a bra. |

---

## 5. Reading the file

```python
import pandas as pd

df = pd.read_csv("dataset.csv", encoding="utf-8-sig")
# columns: Final annotation, Text, English Translation
```

Admissible class names for filtering and evaluation:

```text
Non Misogynistic | Stereotype | Derogation | Sexual Harassment
```

---

## 6. Companion files

| File | Contents |
|------|----------|
| [`dataset.csv`](dataset.csv) | Annotated data |
| [`README.md`](README.md) | Dataset description |
| [`LICENSE`](LICENSE) | Licence text |
| [`data_analysis_source.ipynb`](data_analysis_source.ipynb) | Analysis notebook |
