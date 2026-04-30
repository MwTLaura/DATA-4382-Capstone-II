# DATA-4382 Capstone II

# AI-Powered Environmental Health Literature Extraction Pipeline

> Automated extraction of environmental exposures and health outcomes from scientific literature using a structured 3-layer taxonomy and large language models.

---

## 1. Business Problem

Environmental health research depends on systematic literature reviews to identify relationships between exposures (e.g., air pollution, heavy metals, diet) and health outcomes (e.g., cardiovascular disease, respiratory function, cognitive decline).

This process is manual, time-intensive, and difficult to scale across hundreds of publications.

This project develops an AI pipeline that automatically extracts structured exposure-outcome relationships from scientific text, enabling faster and more consistent analysis.

---

## 2. Project Overview

|                           |                                                                         |
| ------------------------- | ----------------------------------------------------------------------- |
| **Goal**                  | Extract exposures and outcomes from scientific abstracts and full texts |
| **Approach**              | 3-layer taxonomy + LLM extraction                                       |
| **Models**                | GPT-3.5 (baseline), GPT-4o (production)                                 |
| **Validation Data**       | 86 papers (Phase 4), 121 PDFs (Phase 5)                                 |
| **Best Performance (F1)** | 96%+ (Layer 1, aggressive matching)                                     |
| **Coverage**              | 100% of papers processed                                                |

---

## 3. Data

**Ground Truth Dataset**

* Source: VA Normative Aging Study
* Link: https://github.com/MwTLaura/DATA-4382-Capstone-II/blob/main/CohortNetwork_ES%26T_SI_B_Main.xlsx
* Type: Expert-curated exposure-outcome annotations
* Size: 428 records across 121 papers

**Production Corpus**

* 121 full-text PDFs
* Topics: air pollution, lead exposure, diet, cardiovascular and respiratory outcomes

**Taxonomy**

* 3-layer hierarchy (114 fine-grained categories)

---

## 4. Data Preprocessing

* API-based abstract retrieval (PubMed, Google Scholar)
* Selenium-based full-text detection
* PDF extraction using pdfplumber
* Cleaning: normalization, noise removal, deduplication

---

## 5. Exploratory Data Analysis

**Key Observations**

* Strong concentration of air pollution and lead exposure studies
* Cardiovascular and respiratory outcomes dominate
* Increasing sparsity at deeper taxonomy layers

### Example Dataset Distribution

<img width="1076" height="796" alt="Image" src="https://github.com/user-attachments/assets/0c50456f-44a9-4381-b9ef-a9ff5caa3f74" />

---

## 6. Modeling Approach

### Baseline Model

**GPT-3.5 (Abstract-based)**

* Fast and cost-efficient
* Limited by incomplete text

### Advanced Model

**GPT-4o (Full PDF-based)**

* Higher accuracy and reasoning ability
* Uses full document context

---

## 7. Model Comparison

| Model   | Input     | Strengths      | Limitations     | Key Results       |
| ------- | --------- | -------------- | --------------- | ----------------- |
| GPT-3.5 | Abstracts | Fast, low cost | Limited context | 61.4% L1 accuracy |
| GPT-4o  | Full PDFs | High accuracy  | Higher cost     | 96%+ F1           |

---

## 8. Model Training

* Prompt engineering with structured taxonomy
* Deterministic output via low temperature
* Fuzzy matching optimization (threshold = 0.75)

---

## 9. Results

### Phase 4 (Validation)

* 61.4% Layer 1 accuracy
* Performance decreases with taxonomy depth

### Phase 5 (Production)

* 100% paper coverage
* High precision and recall under flexible matching

### Example Output

<img width="1489" height="810" alt="Image" src="https://github.com/user-attachments/assets/38eec67c-7bfa-43ca-8375-620fb17a0f47" />


### Performance Summary
Phase 4 Results
<img width="498" height="463" alt="Image" src="https://github.com/user-attachments/assets/06de1be9-f3e5-4b2d-bb96-3bf33431011f" />

Phase 5 Results
<img width="741" height="263" alt="Image" src="https://github.com/user-attachments/assets/a9a78438-0b69-4473-9e15-a08be085ca0b" />
<img width="1199" height="231" alt="Image" src="https://github.com/user-attachments/assets/27480457-cc5c-4041-844b-56c6d461d80b" />


---

## 10. Model Interpretation

Predictions are driven by:

* Semantic similarity to taxonomy categories
* Keyword detection
* Contextual reasoning

**Strengths**

* Accurate when terminology is explicit
* Handles multi-exposure papers well

**Limitations**

* Sensitive to synonyms
* Struggles with implicit exposures

---

## 11. Key Insights

* Taxonomy-guided prompting significantly improves consistency
* Evaluation method strongly affects measured performance
* Full-text input is a major performance driver
* Automation reduces analysis time from ~20–30 hours to under 2 hours

---

## 12. Conclusion

This project demonstrates that LLM-based systems can reliably automate structured extraction from scientific literature.

The pipeline is production-ready and scalable to other research domains.

---

## 13. Future Work

* Expand taxonomy
* Add confidence scoring
* Improve synonym handling
* Build a web interface

---

## 14. How to Run

1. Clone this repository

2. Install dependencies:
 !pip install -r requirements.txt

3. Set up your OpenAI API key:
 Create a .env file in the root directory:
 OPENAI_API_KEY=your_key_here

4. Run the notebooks in order:
 Phase1 → Phase5

---

## 15. Repository Structure

```
env-health-extraction/
├── README.md                        # This file
├── requirements.txt                 # Python dependencies
├── data/
│   └── CohortNetwork_ES%26T_SI_B_Main.xlsx      # 3-layer taxonomy (428 records, 114 Layer 3 terms)
├── notebooks/
│   ├── Phase1.ipynb                 # Proof of concept & Google Scholar collection
│   ├── Phase_2_PubMed.ipynb         # PubMed integration & scaling
│   ├── Phase3.ipynb                 # Full-text access assessment (Selenium)
│   ├── Phase_4.ipynb              # Semantic extraction & accuracy validation
│   └── Phase5.ipynb                 # Production PDF pipeline (GPT-4o)
├── important results/
│   ├── aggressive_semantic_extraction_20260311_163232.csv       
│   ├── aggressive_semantic_outcomes_20260311_161726.csv
│   ├──  Phase5_extraction_results.csv
│   ├── Phase5_extraction_results_metrics.csv
│   ├── Phase5_extraction_results_with_strategies.csv
│   └── Phase5_extraction_results_with_strategies_metrics.csv
```

---

## 16. Requirements

```bash
pip install -r requirements.txt
```

---

## Tech Stack

* Python
* OpenAI API
* Selenium, BeautifulSoup
* pdfplumber
* pandas

---

*Developed by Laura Tambwe Mwibashiye and Byrnes Mulumbeni*
*DATA 4382 Capstone, University of Texas at Arlington, Spring 2026*
*Advisor: Dr. Yike Shen*

---


