# AI-Resume-Analyzer

**Repository:** `UjwalBagalkoti/AI-Resume-Analyzer`  
**Short description:** A tool that uses NLP and ML to automatically parse, score, and generate insights for resumes — matching candidates to job descriptions, extracting skills/experience, and producing recruiter-friendly summaries.

---

## Table of contents
- [About](#about)
- [Features](#features)
- [Demo](#demo)
- [Tech stack](#tech-stack)
- [Installation](#installation)
- [Usage](#usage)
  - [Command-line example](#command-line-example)
  - [Python API example](#python-api-example)
- [Model / Data](#model--data)
- [Evaluation](#evaluation)
- [Project structure](#project-structure)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)
- [Contact](#contact)

---

## About
`AI-Resume-Analyzer` automates resume processing for hiring pipelines. It extracts structured fields (name, contact, education, experience, skills, certifications), matches resumes to job descriptions (semantic similarity + rule-based boosts), scores candidates on customizable rubrics, and can generate short summaries or interview question suggestions for hiring teams.

---

## Features
- Resume parsing (PDF, DOCX, TXT).
- Named-entity extraction: contact info, education, work history, skills, certifications.
- Skill normalization (maps synonyms / variants).
- Job-resume matching with similarity scores.
- Customizable scoring rules and weighting.
- Exportable output: JSON, CSV, and recruiter-friendly summaries (Markdown / PDF).
- Optional UI (simple web dashboard) and REST API.
- Batch processing for large candidate sets.

---

## Demo
Example output (JSON):
```json
{
  "name": "Jane Doe",
  "email": "jane@example.com",
  "skills": ["python", "nlp", "tensorflow"],
  "experience_years": 4.5,
  "match_score": 87,
  "highlights": [
    "Led NLP project reducing annotation time by 30%",
    "Experience with Transformer-based models"
  ]
}
```

---

## Tech stack
- Python 3.9+
- NLP: spaCy / NLTK / transformers
- Model training: PyTorch / Hugging Face Transformers
- CLI: Click / argparse
- Optional web UI: FastAPI + React (or Streamlit for quick demos)
- Data storage: SQLite / JSON / CSV for lightweight use

---

## Installation
```bash
git clone https://github.com/UjwalBagalkoti/AI-Resume-Analyzer.git
cd AI-Resume-Analyzer

python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows

pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

---

## Usage

### Command-line example
```bash
python bin/parse_resume.py --input resumes/jane_doe.pdf --output out/jane_doe.json
python bin/batch_process.py --input-folder resumes/ --output-folder out/
python bin/match.py --resume out/jane_doe.json --job-spec jobs/data_scientist.md
```

### Python API example
```python
from ai_resume_analyzer import Analyzer, JobSpec

an = Analyzer(config_path="config.yml")
result = an.parse_resume("resumes/jane_doe.pdf")
job = JobSpec.from_file("jobs/data_scientist.md")
match = an.match_resume_to_job(result, job)
print(match.summary())
```

---

## Model / Data
- Default models: lightweight spaCy models for parsing + a small transformer (optional) for semantic similarity.
- Training pipeline (if you wish to improve scoring/matching):
  - `data/` should contain labeled resumes and job pairs.
  - Training script: `scripts/train_matcher.py`
- Provide your own datasets in `data/custom/` and configure `config.yml`.

---

## Evaluation
- Pre-built metrics:
  - Field extraction: Precision / Recall / F1.
  - Matching: ROC-AUC or ranking metrics (MRR, NDCG) on labeled job-resume pairs.
- Evaluation scripts: `scripts/evaluate.py`

---

## Project structure
```
AI-Resume-Analyzer/
├── bin/                    # CLI entrypoints
├── ai_resume_analyzer/     # core library
│   ├── parser.py
│   ├── matcher.py
│   ├── scoring.py
│   └── utils.py
├── config/                 # config templates
├── data/                   # sample data and labeled pairs
├── docs/                   # screenshots, demo notes
├── scripts/                # training / evaluation scripts
├── requirements.txt
├── README.md
└── LICENSE
```

---

## Contributing
Contributions welcome!

1. Fork the repo.
2. Create a feature branch: `git checkout -b feat/your-feature`
3. Implement changes and add tests where relevant.
4. Run tests and linters.
5. Open a Pull Request with a clear description of changes.

---

## Roadmap
- Improve skill normalization with a knowledge-base.
- Add multi-language parsing.
- Build a hosted web dashboard with bulk-upload and filtering.
- Add anonymization mode for blind screening.

---

## License
MIT License — see LICENSE file.

---

## Contact
Created by **UjwalBagalkoti** — GitHub: `@UjwalBagalkoti`.
