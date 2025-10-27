# Resume Screening

A Jupyter Notebook-based project for resume (CV) screening and shortlist automation. This repository contains exploratory data analysis, feature engineering, and prototype model(s) to help parse, score, and rank candidate resumes for a given job description. The goal is to provide a reproducible, explainable pipeline that can be extended and productionized.

Table of contents
- Project overview
- Key features
- Repository structure
- Notebooks and workflow
- Installation & environment
- Usage examples
- Data & privacy
- Model, evaluation & interpretation
- Reproducing experiments
- Contributing
- License & contact

## Project overview

Resume Screening is intended to help hiring teams accelerate the early stage of recruitment by:
- Extracting structured attributes from semi-structured resumes (education, skills, experience, etc.)
- Matching candidate profiles against job requirements
- Producing ranked shortlists and human-readable explanations for rankings

This repository focuses on the investigatory and prototyping phase (not a production-ready pipeline). It is implemented primarily with Jupyter Notebook(s) for transparency and reproducibility.

## Key features

- Resume parsing and basic normalization
- Rule-based and ML-assisted feature extraction
- Simple matching and scoring against job descriptions
- Evaluation metrics for ranking and classification
- Notebook-driven, step-by-step demonstration and visualization

## Repository structure

- README.md — this file
- notebooks/ — primary Jupyter Notebook(s) demonstrating the pipeline and experiments
  - 00_introduction.ipynb (example) — walkthrough of the approach
  - 01_data_preparation.ipynb — ingestion, cleaning and parsing
  - 02_feature_engineering.ipynb — extracting skill/education/experience features
  - 03_modeling_and_scoring.ipynb — scoring logic, models, evaluation
  - 04_analysis_and_visualization.ipynb — results, charts, insights
- data/ (optional, not committed) — placeholder for dataset (see Data & privacy)
- requirements.txt — Python dependencies (if present)
- environment.yml — conda environment specification (optional)

Note: Not all files may exist in the repo — the list above provides an expected structure and recommended notebook split.

## Notebooks and workflow

A typical investigative workflow in this repository follows these steps:
1. Load example resumes and job descriptions (notebooks/01_data_preparation.ipynb)
2. Parse resumes to extract structured fields (name, contact, education, experience, skills)
3. Clean and normalize skill tokens and job titles
4. Engineer features useful for matching (skill overlap, years of experience, degree match)
5. Implement scoring function(s) — rule based and simple ML models
6. Evaluate candidate ranking using metrics (precision@k, MAP, AUC for binary labels)
7. Visualize results and inspect failure cases

All notebooks include narrative sections, code cells, and visualization to help understand each step.

## Installation & environment

Recommended: Use a virtual environment (venv) or conda environment to isolate dependencies.

Using pip + venv:
1. Create and activate a virtual environment
   - python3 -m venv .venv
   - source .venv/bin/activate  (macOS / Linux)
   - .venv\Scripts\activate     (Windows PowerShell)
2. Upgrade pip
   - pip install --upgrade pip
3. Install dependencies
   - pip install -r requirements.txt
   If the repository doesn't have a requirements.txt, the notebooks commonly need:
   - pandas, numpy, scikit-learn, spacy, nltk, jupyterlab, matplotlib, seaborn, python-docx, pdfminer.six (depending on parsing approach)

Using conda (if environment.yml provided):
- conda env create -f environment.yml
- conda activate resume-screening

Set Jupyter kernel to the created environment:
- python -m ipykernel install --user --name resume-screening --display-name "Resume Screening"

## Usage examples

Start Jupyter:
- jupyter lab
- or jupyter notebook

Open the notebooks in the `notebooks/` directory in the running server and run cells sequentially. Notebooks are written to be run top-to-bottom.

Command-line run (exporting to static HTML or running end-to-end with nbconvert):
- jupyter nbconvert --to html notebooks/03_modeling_and_scoring.ipynb
- jupyter nbconvert --execute --to notebook --inplace notebooks/01_data_preparation.ipynb

If you have a script wrapper (notebooks converted to scripts), you can run them with:
- python scripts/run_pipeline.py --config config.yaml

## Data & privacy

This repository is structured for research and demonstration. Resumes and other personal data are sensitive. Before using real candidate data:

- Ensure you have permission to process personal data.
- Apply anonymization or synthetic data when sharing or publishing.
- Follow your organization's data retention and access policies.

Sample or synthetic datasets should be stored in the `data/` folder. Do not commit real resumes or PII to public repositories.

## Model, evaluation & interpretation

This project is intentionally lightweight and prioritizes explainability:

- Rule-based scoring: deterministic functions that score skill matches, education and experience.
- Simple ML baselines: logistic regression, decision trees, or ranking models (where labeled data exists).
- Evaluation metrics:
  - Precision@k (how many of the top-k are relevant)
  - Mean Average Precision (MAP) for ranking quality
  - ROC-AUC or F1 for binary screening decisions

Explainability practices:
- Provide feature importances for model-based approaches
- Emit readable score breakdown per candidate (e.g., skill_match: 0.6, experience_score: 0.3)

## Reproducing experiments

To reproduce the analyses in the notebooks:
1. Install dependencies as described.
2. Place the prepared sample data (or real data) into the `data/` directory.
3. Open notebooks in order and execute cells.
4. For deterministic results, set random seeds inside modeling notebooks:
   - numpy, random, scikit-learn seeds should be fixed.

If results differ between runs, ensure you are using the same package versions; pinning them in requirements.txt or environment.yml is recommended.

## Extending & productionizing

Suggested next steps for production:
- Replace notebook parsing with a well-tested parser module (extract to Python package)
- Add robust resume file-type handling (.pdf, .docx), OCR where necessary
- Persist intermediate outputs to a database or data lake
- Containerize the processing pipeline and add orchestration (Airflow, Prefect, or similar)
- Add a REST API front-end for scoring batches of resumes
- Add end-to-end tests and CI/CD checks

## Contributing

Contributions are welcome. Please follow these guidelines:
- Create an issue describing the feature or bug
- Work on a feature branch: git checkout -b feature/your-feature
- Keep notebooks clean and include narrative text explaining changes
- If adding data or models, prefer synthetic or anonymized examples
- Submit a pull request with a clear description and testing steps

## License

Specify a license for the project (e.g., MIT, Apache-2.0). If no license file exists in the repo, add one to make reuse terms explicit.

Example (add a LICENSE file):
- MIT License — see LICENSE file for details.

## Contact

Maintainer: alishanihsan

For questions, issues, or collaboration requests, please open an issue in this repository or contact the maintainer via their GitHub profile.

---

Thank you for using this repository. If you would like, I can:
- Create a recommended requirements.txt or environment.yml based on the notebooks,
- Convert the Jupyter notebooks into runnable Python scripts,
- Add a sample synthetic dataset and an example `config.yaml`.

Tell me which of these you'd like next and I'll proceed.
