# 📊 Resume Skill Gap Analyzer

[![Python](https://img.shields.io/badge/Python-3.9%20%7C%203.10%20%7C%203.11-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-FF4B4B?logo=streamlit&logoColor=white)](https://streamlit.io/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.3+-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![NLTK](https://img.shields.io/badge/NLTK-3.8+-green?logo=nltk&logoColor=white)](https://www.nltk.org/)
[![Plotly](https://img.shields.io/badge/Plotly-5.15+-3F4F75?logo=plotly&logoColor=white)](https://plotly.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end AI/ML-powered career intelligence tool that parses resumes, calculates multi-feature job compatibility, pinpoints skill gaps, visualizes career insights, and drafts tailored resumes with one-click PDF & Text export.

---

## 🌟 Key Features

- **📄 Resume Ingestion & Parsing**:
  - Direct text paste or `.txt` file upload with real-time word, character, and skill counts.
  - Text normalization pipeline: lowercasing, punctuation stripping, regex cleaning, NLTK stopwords elimination, and WordNet lemmatization.

- **🤖 Hybrid Machine Learning Matching**:
  - **Feature Engineering Engine**: Extracts a 3-dimensional feature vector combining **TF-IDF Cosine Similarity**, **Skill Overlap Count**, and **Job Title Match Score**.
  - **Supervised Compatibility Classifier**: Trained Logistic Regression model estimating probability calibration scores for candidate-job relevance.
  - **Information Retrieval (IR) Ranking**: Evaluated against metrics like NDCG (Normalized Discounted Cumulative Gain), MAP (Mean Average Precision), Precision, Recall, and F1-score.

- **🔍 Automated Skill Gap Identification**:
  - Scans target job descriptions across top matching opportunities to isolate matched vs. missing skills.
  - Automated recommendations with curated learning paths (direct links to tutorials on Coursera, YouTube, Microsoft Learn, and W3Schools).

- **📊 Interactive Analytics & Visualizations**:
  - Plotly-powered dynamic charts:
    - **Job Compatibility Scores**: Horizontal bar chart comparing ranked job roles.
    - **Skills Breakdown**: Distribution breakdown of matched, missing, and candidate skills.
    - **Compatibility vs. Similarity**: Dual grouped bar comparison of semantic text similarity vs. machine-learned compatibility.

- **🎯 One-Click Tailored Resume Generator**:
  - Automatically drafts a targeted resume summary and emphasizes matched keywords for any selected job role.
  - Instant in-app preview and `.txt` download.

- **📑 Multi-Format Report Export**:
  - Download complete analysis reports in formatted plain text (`.txt`) or structured PDF (`.pdf`) generated via ReportLab.

- **🛡️ Resilience & Demo Mode**:
  - Built-in graceful fallbacks: handles pickle version mismatches and provides interactive demo mode simulation if dataset files are unavailable.

---

## 🏗️ System Architecture & Workflow

```
┌─────────────────┐      ┌───────────────────────────┐
│ Candidate Resume│      │ Job Listings Dataset      │
│  (Text / Upload)│      │ (cleaned_jobs_deduped.csv)│
└────────┬────────┘      └─────────────┬─────────────┘
         │                             │
         ▼                             ▼
┌────────────────────────────────────────────────────┐
│             NLP Preprocessing Pipeline             │
│  (Lowercasing • Regex • Stopwords • Lemmatizer)   │
└────────────────────────┬───────────────────────────┘
                         │
                         ▼
┌────────────────────────────────────────────────────┐
│            Feature Engineering Engine              │
│  1. TF-IDF Cosine Similarity                       │
│  2. Skill Set Token Overlap                        │
│  3. Job Title Alignment Score                      │
└────────────────────────┬───────────────────────────┘
                         │
                         ▼
┌────────────────────────────────────────────────────┐
│             Pre-trained ML Classifier              │
│       (Logistic Regression / Best Model)           │
│         Outputs Compatibility Probabilities        │
└────────────────────────┬───────────────────────────┘
                         │
         ┌───────────────┴───────────────┐
         ▼                               ▼
┌─────────────────────────┐    ┌─────────────────────────┐
│    Ranked Job Matches   │    │   Skill Gap Analysis    │
│  & Top Recommendations  │    │ (Matched vs. Missing)   │
└────────┬────────────────┘    └────────────┬────────────┘
         │                                  │
         └────────────────┬─────────────────┘
                          │
                          ▼
┌────────────────────────────────────────────────────────┐
│                   Streamlit Web App                    │
│  • Interactive Visualizations (Plotly)                 │
│  • Curated Learning Path Recommendations               │
│  • One-Click Resume Tailor Draft                       │
│  • Exportable Reports (PDF / TXT via ReportLab)        │
└────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Category | Tools & Libraries |
| :--- | :--- |
| **User Interface** | [Streamlit](https://streamlit.io/), [Plotly Express](https://plotly.com/python/), [Plotly Graph Objects](https://plotly.com/python/graph-objects/) |
| **NLP & Text Processing** | [NLTK](https://www.nltk.org/) (Punkt, Stopwords, WordNet), [Regular Expressions (re)](https://docs.python.org/3/library/re.html) |
| **Machine Learning** | [scikit-learn](https://scikit-learn.org/) (TfidfVectorizer, LogisticRegression, LinearRegression, KNeighborsClassifier/Regressor, SVC) |
| **Data Manipulation** | [Pandas](https://pandas.pydata.org/), [NumPy](https://numpy.org/) |
| **Model Serialization** | [Joblib](https://joblib.readthedocs.io/), [Pickle](https://docs.python.org/3/library/pickle.html) |
| **Document Generation** | [ReportLab](https://www.reportlab.com/) (PDF generation), Python `io.BytesIO` |
| **Container & Cloud** | DevContainer (`.devcontainer/devcontainer.json`), Render (`render.yaml`) |

---

## 📁 Repository Structure

```text
resume-skill-gap-analyzer/
├── .devcontainer/
│   └── devcontainer.json        # VS Code Remote Container / Codespaces config
├── app.py                       # Main Streamlit web application & UI
├── train_model.py               # Model training, validation, and evaluation pipeline
├── convert_pickles.py           # Compatibility utility to convert old pickle files
├── create_samples.py            # Generates synthetic sample dataset & mock models
├── best_model.pkl               # Trained classification model (Logistic Regression)
├── tfidf_vectorizer.pkl         # Fitted TF-IDF vectorizer artifact
├── linear_regression_model.pkl  # Trained Linear Regression model artifact
├── knn_regression_model.pkl     # Trained KNN Regression model artifact
├── cleaned_jobs.pkl             # Serialized preprocessed job listings
├── cleaned_jobs_deduped.csv     # Deduplicated and cleaned job listings dataset
├── cleaned_resumes.csv          # Preprocessed resume dataset
├── resumes.csv                  # Raw resume collection
├── manual_test_set.csv          # Annotated test set for IR & ranking evaluation
├── sample_resume1.txt           # Sample resume: Data Analyst
├── sample_resume2.txt           # Sample resume: Software Engineer
├── sample_resume3.txt           # Sample resume: Machine Learning Engineer
├── render.yaml                  # Render deployment blueprint
├── requirements.txt             # Python package dependencies
└── README.md                    # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9, 3.10, or 3.11 installed
- Git
- `pip` or a virtual environment manager (`venv` / `conda`)

### 1. Clone the Repository

```bash
git clone https://github.com/shresth2308/resume-skill-gap-analyzer.git
cd resume-skill-gap-analyzer
```

### 2. Create and Activate a Virtual Environment

```bash
# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate

# Windows (Command Prompt)
python -m venv .venv
.venv\Scripts\activate

# Windows (PowerShell)
.venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

> **Note:** The application will automatically check for and download required NLTK corpora (`punkt`, `stopwords`, `wordnet`) on first run.

### 4. Run the Streamlit Application

```bash
streamlit run app.py
```

Open your browser at `http://localhost:8501` to use the application.

---

## 🧪 Testing with Sample Resumes

Sample resumes are provided out-of-the-box in the root folder:

| File | Domain / Profile |
| :--- | :--- |
| `sample_resume1.txt` | **Data Analyst** (SQL, Tableau, Power BI, Pandas, Statistics) |
| `sample_resume2.txt` | **Software Engineer** (Python, Django, React, Docker, PostgreSQL) |
| `sample_resume3.txt` | **Machine Learning Engineer** (PyTorch, TensorFlow, NLP, Scikit-Learn) |

Paste the contents of any sample file into the app's input area or upload the text file to see immediate matching and skill gap insights!

---

## 🔬 Model Training & Evaluation

To re-train or fine-tune models on your own datasets:

```bash
python train_model.py
```

### Training Pipeline Details

1. **Preprocessing**: Normalizes raw job listings and resumes by removing HTML artifacts, digits/symbols, and applying lemmatization.
2. **Feature Extraction**:
   - `tfidf_sim`: Cosine similarity over a 3,000-feature TF-IDF matrix.
   - `skill_overlap`: Exact vocabulary overlap between candidate and job profile skills.
   - `title_match`: Lexical intersection with target job titles.
3. **Model Benchmarking**:
   Evaluates multiple classification and regression architectures:
   - **Logistic Regression** (with class weight balancing)
   - **K-Nearest Neighbors (KNN)**
   - **Support Vector Classifier (SVC)** (linear kernel with probability estimates)
4. **Ranking & Classification Metrics**:
   Outputs comprehensive metrics including:
   - **Accuracy, Precision, Recall, F1-Score**
   - **MAP (Mean Average Precision)**
   - **NDCG (Normalized Discounted Cumulative Gain)**
5. **Artifact Export**: Saves `best_model.pkl`, `tfidf_vectorizer.pkl`, and regression models using `joblib`.

---

## 🔧 Utilities & Troubleshooting

### Pickle / Scikit-Learn Version Compatibility

If you encounter deserialization warnings or version mismatch errors with `.pkl` files across different Python/scikit-learn installations, use the included conversion utility:

```bash
python convert_pickles.py
```

This utility attempts deserialization across multiple protocols (`latin1`, standard pickle, joblib) and re-saves compatible artifacts.

### Synthetic Data Generation

If you need to generate quick mock datasets and baseline weights for development or CI tests:

```bash
python create_samples.py
```

---

## ☁️ Deployment

### Deploy to Render

This repository contains a pre-configured `render.yaml` for one-click deployment:

1. Link your GitHub repository to [Render](https://render.com/).
2. Create a new **Web Service** or select **Blueprints**.
3. Render automatically reads `render.yaml`:
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `streamlit run app.py --server.port $PORT --server.address 0.0.0.0`

### Run in GitHub Codespaces / Dev Containers

A `.devcontainer/devcontainer.json` configuration is included:
1. Open this repository in **GitHub Codespaces** or VS Code using the **Remote - Containers** extension.
2. The environment automatically sets up Python 3.11, installs dependencies, forwards port `8501`, and opens the preview.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
