# 🩺 Medical NLP Pipeline – Physician–Patient Conversation Analysis

## 📌 Project Overview

This project implements a Medical Natural Language Processing (NLP) pipeline to analyze physician–patient conversation transcripts and automatically generate structured clinical insights.

The project is divided into three core components:

1.  **Medical NLP Summarization**
2.  **Sentiment & Intent Analysis**
3.  **SOAP Note Generation (AI-assisted – Bonus Task)**

The objective is to demonstrate how rule-based NLP, transformer-based models, and large language models (LLMs) can be combined to solve real-world healthcare documentation problems in a safe, explainable, and structured manner.

## 📁 Project Format

This project is implemented as a Jupyter Notebook (`.ipynb`).

**File name:** `Medical_NLP_Project_Emitrr.ipynb`

Because the project is notebook-based:
*   It can be run using Jupyter Notebook, JupyterLab, Google Colab, or VS Code
*   Users can download the notebook and run it locally using an IDE and terminal
*   All code, explanations, and outputs are contained in a single file

## ⚙️ System Requirements

### ✅ Python Version (Important)

This project uses **spaCy**, which currently has compatibility limitations with newer Python versions.

**✔ Supported Python versions:**
*   Python 3.11
*   Python 3.12

**❌ Not supported:**
*   Python 3.13 and above (spaCy models will fail to install or load)

**⚠️ Please ensure you are using Python 3.11 or 3.12 before installing dependencies.**

##  Libraries & Tools Used

This project intentionally uses different NLP tools for different tasks, based on what is most reliable and appropriate for each problem.

### 🔹 Part 1: Medical NLP Summarization

**Tools Used:**
*   `spaCy`
*   `en_core_web_sm`
*   `spaCy Matcher`
*   `json`

**Why spaCy here?**
Rule-based extraction is deterministic and safe for medical information. It avoids hallucination and is ideal for extracting:
*   Symptoms
*   Diagnosis
*   Treatment
*   Prognosis

**Techniques Applied:**
*   Pattern-based Named Entity Recognition (NER)
*   Custom matcher rules
*   Canonical normalization (e.g., “ten sessions” → “10 physiotherapy sessions”)
*   Structured JSON output

### 🔹 Part 2: Sentiment & Intent Analysis

**Tools Used:**
*   `transformers`
*   `facebook/bart-large-mnli`
*   `Zero-shot classification`
*   `Lightweight rule-based correction`

**Why transformers here?**
*   Sentiment and intent are semantic and contextual.
*   Zero-shot classification allows:
    *   No labeled dataset requirement
    *   Flexible label definitions
    *   Suitable for emotional and intent inference

**Detected Outputs:**
*   **Sentiment:** Anxious / Neutral / Reassured
*   **Intent:** Seeking reassurance / Reporting symptoms / Expressing concern

**Stabilization:**
Rule-based overrides for common clinical patterns (e.g., “worried” + “hope” → Seeking reassurance).

### 🔹 Part 3: SOAP Note Generation (Bonus – AI Model)

**Tools Used:**
*   `google-generativeai`
*   `Gemini 2.5 Flash`
*   `Prompt-engineered JSON generation`
*   `Regex-based cleanup`
*   `json`

**Why Gemini (LLM) here?**
SOAP note generation requires long-context understanding and clinical summarization. This task explicitly requires an AI model, and LLMs are well-suited for document drafting tasks.

**Design Choice:**
*   **AI** generates SOAP content
*   **Code** enforces:
    *   Strict JSON schema
    *   Parsing safety
    *   Output validation

This mirrors real-world clinical documentation systems, where AI assists drafting but structure and safety are programmatically enforced.

## Installation Instructions

### 1️⃣ Create a Virtual Environment (Recommended)
```bash
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
```

### 2️⃣ Install Required Libraries
```bash
pip install spacy transformers torch google-generativeai
```

### 3️⃣ Install spaCy Model
```bash
python -m spacy download en_core_web_sm
```

### 4️⃣ Google Gemini Setup (For SOAP Generation)
This project uses **Google Generative AI (Gemini)**. You must provide a valid Google API Key.

In **Google Colab**, the key is accessed using:
```python
from google.colab import userdata
userdata.get("GOOGLE_API_KEY")
```

For **local usage**, you may set it as an environment variable.

## 🚀 Running the Project

### Option 1: Google Colab
1.  Upload the `.ipynb` file
2.  Add your Google API Key to Colab secrets
3.  Run cells sequentially

### Option 2: Local IDE (VS Code / Jupyter)
```bash
jupyter notebook
```
1.  Open: `Medical_NLP_Project_Emitrr.ipynb`
2.  Ensure:
    *   Correct Python version selected
    *   Virtual environment activated

## 🧠 Project Architecture Summary

| Component | Approach | Reason |
| :--- | :--- | :--- |
| **Medical Summarization** | Rule-based spaCy | Deterministic & safe |
| **Sentiment & Intent** | Transformer (Zero-shot) | Semantic understanding |
| **SOAP Generation** | LLM (Gemini) | Structured clinical drafting |

This hybrid architecture balances:
*   Accuracy
*   Explainability
*   Practical deployability
