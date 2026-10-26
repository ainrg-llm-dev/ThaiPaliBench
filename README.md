# 🪷 ThaiPaliBench Dataset

🌐 **Project page:** https://ainrg-llm-dev.github.io/ThaiPaliBench/ · 📄 *Findings of EMNLP 2026*

## Overview

**ThaiPaliBench** is a benchmark dataset designed for evaluating large language models on Pali written in Thai script. It enables systematic assessment of grammatical knowledge, reading comprehension, natural language inference, and translation understanding.

The dataset contains **4,000 instances**, evenly distributed across four task types:

- 🧩 **Grammar** — 1,000 instances  
- 📚 **Reading Comprehension (RC)** — 1,000 instances  
- 🌐 **Translation** — 1,000 instances  
- 🔎 **Natural Language Inference (NLI)** — 1,000 instances

## Dataset Design

The dataset is organized into nine proficiency levels (L1–L9), reflecting increasing linguistic and cognitive complexity.

### Grammar
- Focused on foundational levels L1–L3  
- Emphasizes morphology and syntax  
- **Total: 1,000 items**

### Reading Comprehension, Translation, and NLI
- Span all levels L1–L9  
- 125 items per level for each task  
- **Total per task: 1,000 items**

This structured distribution enables evaluation of both foundational linguistic knowledge (L1–L3) and advanced comprehension across all nine levels.

## Dataset Statistics

| Level | Grammar | RC  | Translation | NLI | Total |
|-------|---------:|----:|------------:|----:|------:|
| L1–2  | 500      | 125 | 125         | 125 | 875   |
| L3    | 500      | 125 | 125         | 125 | 875   |
| L4    | —        | 125 | 125         | 125 | 375   |
| L5    | —        | 125 | 125         | 125 | 375   |
| L6    | —        | 125 | 125         | 125 | 375   |
| L7    | —        | 125 | 125         | 125 | 375   |
| L8    | —        | 125 | 125         | 125 | 375   |
| L9    | —        | 125 | 125         | 125 | 375   |
| **Total** | **1,000** | **1,000** | **1,000** | **1,000** | **4,000** |

## Data Format

The dataset is provided in **JSON Lines (.jsonl)** format. There are two primary data structures depending on the task type.

---

### 1. Multiple-Choice Tasks  
(Grammar, Reading Comprehension, Translation)

Each item contains a question with five answer options.

**Fields**
- `filename` — Source document filename  
- `โจทย์` — Question text  
- `ก, ข, ค, ง, จ` — Multiple-choice options  
- `เฉลย` — Correct answer key  
- `อธิบาย` — Explanation of the correct answer

**Example**
```json
{
  "filename": "12-PW-23.pdf",
  "โจทย์": "\"\"มาน\"\" ปัจจัย (กิริยากิตก์) จะเป็น \"\"กัมมวาจก\"\" ได้เมื่อใด?",
  "ก": "เมื่อเป็นปัจจัยของอานที่ไม่มีอิ อาคม",
  "ข": "เมื่อมี อ ปัจจัย (และอิ อาคม) แต่ไม่มี ย ปัจจัย",
  "ค": "เมื่อมี ย ปัจจัย (และอิ อาคม)",
  "ง": "เมื่อไม่มี ย ปัจจัยแต่มี ส ปัจจัยที่เป็นอิ อาคม",
  "จ": "เมื่อเป็นธาตุสกัมมกะที่ไม่มีอิ อาคม",
  "เฉลย": "ค",
  "อธิบาย": "ถ้ามี ย ปัจจัย (ซึ่งลงในกรรม) เป็นกัมมวาจก"
}
```
## 2. Natural Language Inference (NLI)

This task evaluates the semantic relationship between:

- A **Pali premise**
- A **Thai hypothesis**

### Fields

- `pali` — Premise sentence (Pali)  
- `thai` — Hypothesis sentence (Thai)  
- `label` — Numerical label (0, 1, 2)  
- `type` — Text label (`entailment`, `neutral`, `contradiction`)

### Label Definitions

| Label | Type | Description |
|-------|------|------------|
| 0 | entailment | The hypothesis is definitively true given the premise |
| 1 | neutral | The hypothesis may or may not be true |
| 2 | contradiction | The hypothesis is definitively false given the premise |

### Example

```json
{
  "pali": "ปณฺฑิตปุริสา หิ ปุญฺญํ กโรนฺตา วิวฏมุขภาชนํ วิย อุทเกน อนุปุพฺเพน ปุญฺเญน ปูรนฺติเยวาติ วตฺวา อนุสนฺธึ ฆเฏตฺวา ธมฺมํ เทเสนฺโต อิมํ คาถามาห",
  "thai": "เหล่าบัณฑิตสะสมบุญจนเต็มเปี่ยมเหมือนภาชนะเปิดปากรับน้ำ และพระพุทธองค์ทรงแสดงธรรมนี้ ณ เชตวันมหาวิหาร",
  "label": 1,
  "type": "neutral"
}
```

---

## Usage

ThaiPaliBench can be used for:

- Benchmarking large language models (LLMs)
- Evaluating Thai–Pali translation systems

---

## Total Size

**4,000 instances** — Balanced across task types and systematically distributed across proficiency levels.

---

## Data Source

The dataset is constructed from past papers of the Royal Pali Examination (Parian Tham), administered by the Office of the Sanam Luang Pali Examination under the Sangha Supreme Council of Thailand. Scanned exam papers (1986–2025) were obtained from the public archive [สถิติข้อสอบบาลีสนามหลวง](https://www.pariyat.com/education/%E0%B8%9A%E0%B8%B2%E0%B8%A5%E0%B8%B5-%E0%B8%9A%E0%B8%B2%E0%B8%A5%E0%B8%B5%E0%B8%A8%E0%B8%B6%E0%B8%81%E0%B8%A9%E0%B8%B2/%E0%B8%AA%E0%B8%96%E0%B8%B4%E0%B8%95%E0%B8%B4%E0%B8%82%E0%B9%89%E0%B8%AD%E0%B8%AA%E0%B8%AD%E0%B8%9A%E0%B8%9A%E0%B8%B2%E0%B8%A5%E0%B8%B5%E0%B8%AA%E0%B8%99%E0%B8%B2%E0%B8%A1%E0%B8%AB%E0%B8%A5%E0%B8%A7%E0%B8%87) on pariyat.com.

## License

Released under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) — non-commercial use only. See [LICENSE](LICENSE).

## Citation

If you use ThaiPaliBench, please cite:

```bibtex
@inproceedings{phetsri-etal-2026-thaipalibench,
    title     = "{T}hai{P}ali{B}ench: Benchmarking Large Language Models on {T}hai-Script {P}ali Understanding",
    author    = "Phetsri, Nobpharat and Saeoueng, Anon and Kongyoung, Sarawoot and Viriyavit, Waranrach",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2026",
    year      = "2026",
    address   = "Budapest, Hungary",
    publisher = "Association for Computational Linguistics"
}
```

## Acknowledgments

We thank Kun Kerdthaisong and Chaianun Damrongrat.

## Contact

Sarawoot Kongyoung — sarawoot.kon@nectec.or.th
