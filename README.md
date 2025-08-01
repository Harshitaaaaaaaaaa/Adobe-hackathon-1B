# 📄 Adobe Challenge 1B – PDF Heading and Section Extractor

This project processes PDF documents to extract **titles**, **headings**, and **section contents**, then ranks them by relevance to a given task. It supports:

- Extracting document outlines
- Detecting title and heading hierarchy
- Ranking sections based on a query (e.g., a job-to-be-done)
- Docker-based deployment for ease of use

---

## 📁 Project Structure

adobe_challange_02/
├── input/
│ ├── input_pdfs/ ← input PDF files
│ ├── outlines/ ← output outlines (generated)
│ └── test_input.json ← input JSON (task + document list)
├── output/ ← final output JSON (generated)
├── script.py ← full pipeline (extract, rank, analyze)
├── title_heading.py ← fast title & heading extractor
├── requirements.txt ← Python dependencies
├── Dockerfile ← Docker setup
├── .dockerignore ← Docker ignore rules
└── README.md ← this file

yaml
Copy
Edit

---

## 🧪 Example `test_input.json`

This file tells the system what task to process and which PDFs to use:

```json
{
  "persona": {
    "role": "student"
  },
  "job_to_be_done": {
    "task": "Understand the history and culture of South France."
  },
  "documents": [
    { "filename": "South of France - History.pdf" },
    { "filename": "South of France - Traditions and Culture.pdf" }
  ]
}
🚀 Quick Start with Docker
1️⃣ Build the Docker Image
Open a terminal inside the adobe_challange_02/ folder:

bash
Copy
Edit
docker build -t adobe_challenge .
2️⃣ Run the Full Pipeline (script.py)
Processes all PDFs, extracts sections, ranks them by query, and outputs results.

bash
Copy
Edit
docker run --rm -v "${PWD}:/app" adobe_challenge
Input: input/input_pdfs/ and input/test_input.json

Output: output/final.json and per-PDF outlines in input/outlines/

3️⃣ Run Just the Outline Extractor (title_heading.py)
If you want fast heading/title JSONs without ranking:

bash
Copy
Edit
docker run --rm -v "${PWD}:/app" adobe_challenge \
  python title_heading.py input/input_pdfs input/outlines
🧠 Output Files
output/final.json – ranked section results

input/outlines/*.json – outlines per document:

json
Copy
Edit
{
  "title": "South of France - History",
  "outline": [
    { "level": "H1", "text": "Ancient Times", "page": 1 },
    { "level": "H2", "text": "Roman Influence", "page": 2 }
  ]
}
🛠️ Developer Notes
Python Version:
Python 3.10 (via Docker)

Required Python Libraries:
See requirements.txt:

nginx
Copy
Edit
pymupdf
spacy
scikit-learn
numpy
Also includes:

SpaCy model: en_core_web_md

🔐 .dockerignore
To reduce image size and build time, the following are excluded:

dockerignore
Copy
Edit
__pycache__/
*.pyc
*.pyo
*.pyd
*.DS_Store
.env
.vscode/
output/
input/outlines/
input/input_pdfs/
🧪 Example Test Command (Without Docker)
If you're running locally (not recommended for prod):

bash
Copy
Edit
pip install -r requirements.txt
python -m spacy download en_core_web_md
python script.py input/input_pdfs input/test_input.json output/final.json
📝 License
This project was built for an Adobe Challenge and is provided for learning/demo purposes.

