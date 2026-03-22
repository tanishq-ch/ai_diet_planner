# 🥗 AI-NutriCare: AI Diet Planner

**Status:** Under Development  
**Author:** Tanishq Chauhan  
**Developed Under:** Infosys Springboard Internship  

---

## 📌 Overview

**AI-NutriCare (AI Diet Planner)** is an advanced, privacy-first AI/ML-based system designed to analyze medical reports—such as blood tests, lab reports, and doctor prescriptions—to automatically generate highly personalized dietary plans tailored to an individual's unique health profile.

Medical reports are often filled with complex numeric values, jargon, and unstructured notes, making it difficult for average individuals to correlate their lab results with their daily diet. AI-NutriCare bridges this gap by combining **Optical Character Recognition (OCR)**, **Local Large Language Models (LLMs)**, and rigorously defined **Rule-Based Nutritional Logic**. This allows the system to extract meaningful metrics (e.g., glucose levels, blood pressure, cholesterol, BMI) and unstructured physician advice directly from uploaded documents, subsequently converting these granular insights into structured, actionable, multi-day meal plans.

*This project was conceptualized and developed as part of the **Infosys Springboard Internship**, showcasing the practical application of Machine Learning, OCR, and Generative AI in the Healthcare Domain.*

---

## 🎯 Objectives

The main objectives of the AI-NutriCare project are:
1. **Automate Unstructured Medical Data Parsing:** Utilize OCR and localized LLMs to read and interpret unstructured PDF lab reports or scanned prescription images.
2. **Translate Medical Metrics to Health Risk Assessments:** Map granular laboratory values to identified health risks (e.g., Pre-diabetes, Hypertension, Low Hemoglobin).
3. **Generate Actionable Dietary Interventions:** Provide users with personalized, AI-generated meal plans that explicitly include recommended foods while excluding contraindicated items based on their detected medical conditions.
4. **Ensure Data Privacy:** Employ locally-hosted AI inference (via Ollama) ensuring that sensitive medical data and user health metrics never leave the local environment or get transmitted to third-party cloud APIs.

---

## ✨ Key Features

- **Automated Medical Report Extraction (No Manual Data Entry):**
  - Direct upload for **PDFs** and Scanned **Images** (JPEG/PNG).
  - Uses `pdfplumber` and `pytesseract` to scan raw text seamlessly, preserving context and numeric values.
- **AI-Powered Metrics Parsing & Analysis:**
  - Instructs local LLMs (via Ollama) to sift through raw lab reports and intelligently extract critical markers (e.g., HbA1c, Fasting Glucose, LDL, HDL, Triglycerides, Hemoglobin, Creatinine).
  - Automatically captures, interprets, and parses unstructured **Doctor Notes** and advice found at the bottom of prescriptions.
- **Intelligent Health Risk Assessment:**
  - Evaluates extracted metrics against established medical thresholds automatically.
  - Detects complex interacting conditions such as **Type 2 Diabetes, Hypertension, Obesity/Overweight, High Cholesterol, Anemia, Thyroid Disorders, and Kidney Disease**.
- **Personalized Diet Generation Engine:**
  - Generates highly specific, safe, multi-tier meal plans (Vegetarian or Non-Vegetarian) completely dynamically.
  - Automatically calculates basal metabolic rate (BMR) and caloric targets based on age, gender, weight, and detected health goals (e.g., caloric deficit for obesity, glycemic control for diabetes).
  - Features robust fallback daily meal plans for high resilience during generation phases.
- **Privacy-First Local Processing:**
  - Utilizes **Ollama** for running fast, private LLMs (`gemma3:1b`, `qwen2.5:1.5b`, `phi3.5`, etc.) completely offline.
- **Beautiful, Interactive UI:**
  - Built with **Streamlit**, featuring a highly customized, responsive, visually appealing, and intuitive interface with informative step-by-step progress tracking.
- **Export & Download:**
  - Download structured dietary data as **JSON** for digital records.
  - Export beautifully formatted, patient-ready **PDF Reports** customized with medical disclaimers using `reportlab`.

---

## 🧱 Complete Project Structure

```text
AI-NutriCare/
│
├── diet_plan_module/               # Main Application Module (Modern UI + GenAI)
│   ├── app2.py                     # Streamlit web application & Frontend UI
│   ├── diet_engine.py              # Core logic: LLM integration, metric extraction, rules, PDF gen
│   ├── rules/                      # Rule-based logic algorithms and dataset loading
│   ├── ocr/                        # OCR integrations for targeted text extraction
│   └── medical/                    # Medical logic and biomarker threshold analysis modules
│
├── main.py                         # Modular CLI orchestrator for basic file reading (Legacy/CLI view)
├── input_handlers/                 # Parsers to clean data from Image, PDF, or text contexts
│   ├── image_reader.py
│   ├── pdf_reader.py
│   └── text_reader.py
│
├── parsers/                        # Prescription and medical entity parsing logic (Regex/NLP)
│   ├── prescription_parser.py
│   └── text_cleaner.py
│
├── diet_engine/                    # (CLI module) Dataset loaders and basic ML recommendation logic
│   └── meal_selector.py
│
├── Datasets/                       # Datasets for traditional ML (Pima Diabetes, Nutrition, etc.)
│   ├── nutrition.xlsx
│   └── (Other CSV datasets)
│
├── Outputs/                        # Application generated assets (JSON outputs, PDF plans)
├── requirements.txt                # Python dependencies
└── README.md                       # Comprehensive Documentation
```

### Module Breakdown
- **`diet_plan_module`**: This is the heart of the modern application. It utilizes Streamlit for a web interface (`app2.py`) and offloads complex LLM inference, medical reasoning, and PDF generation to `diet_engine.py`.
- **`input_handlers` & `parsers`**: These folders form the extraction pipeline that attempts to sanitize chaotic OCR text into clean, tokenizable text before passing it to parsing logic or an LLM.

---

## 🛠️ Technology Stack

**Frontend & User Interface:**
- `streamlit`

**AI, Machine Learning & NLP:**
- `ollama` (Local LLM Server handling inference)
- Open Source LLMs (Gemma3, Qwen2.5, Phi3.5)
- `pandas`, `numpy` (For dataset analytics and data manipulation)

**Document Processing & OCR:**
- `pdfplumber` (For parsing digital PDFs)
- `pytesseract` & `pillow` (For Optical Character Recognition on images)
- `opencv-python` (Image processing enhancements)

**Data Export & Report Generation:**
- `reportlab` (Dynamic PDF assembly)
- `json`

---

## 🚀 Getting Started

Follow these steps to set up the project on your local machine. Because this application processes text locally using LLMs, you must install Ollama.

### 1. Prerequisites

You must have **Ollama** installed on your system to run the local AI models.
- Download and install Ollama from: [https://ollama.com/](https://ollama.com/)

Once installed, open a terminal and pull a lightweight, fast model. The system works best with these fast models:
```bash
ollama pull gemma3:1b
ollama pull qwen2.5:1.5b
```

### 2. Environment Setup

Make sure you have Python 3.9+ installed. It is highly recommended to use a virtual environment.

```bash
# Clone the repository
git clone https://github.com/your-username/AI-NutriCare.git
cd AI-NutriCare

# Create and activate a Virtual Environment (Windows)
python -m venv venv
venv\Scripts\activate

# Install the dependencies
pip install -r requirements.txt
```

*(Note: Depending on your system, `pytesseract` may also require you to install Tesseract-OCR software natively on your OS and add it to your system PATH).*

---

## 💡 How to Use the Project

1. **Launch the Engine:**
   Ensure Ollama is running in the background. Then, start the Streamlit application:
   ```bash
   cd diet_plan_module
   streamlit run app2.py
   ```

2. **Configure the AI (Sidebar):**
   - Use the sidebar to select your preferred Local Model (e.g., `gemma3:1b`).
   - Click "Test Connection" to ensure the AI bridge is active.
   - Select the desired Diet Preference (Vegetarian/Non-Vegetarian) and the Plan Duration.

3. **Step 1: Patient Information:**
   - Input basic demographics (Name, Age, Gender) used for BMR and caloric calculations.

4. **Step 2 & 3: Health Metrics & Doctor Notes:**
   - **Upload Tab:** Upload a lab report (PDF/Image). The OCR will extract text, and the LLM will parse out the medical values and doctor notes completely automatically.
   - **Manual Tab:** If you don't have a report, manually enter known values (Fasting Glucose, Blood Pressure, LDL, etc.).

5. **Step 4: Generate Diet Plan:**
   - Review the AI-identified conditions (displayed as badges).
   - Click "Generate Diet Plan". The local LLM will generate daily meals adhering to specific restrictions.

6. **Review & Export:**
   - View your day-by-day plan directly in the beautiful UI.
   - Download the raw data via **"Download JSON"** or get a pristine PDF document by clicking **"Generate PDF"**.

---

## 🔮 Future Enhancements

- **Deep Image-Based Food Recognition:** Integrate computer vision to allow users to take a picture of their meals to retroactively analyze whether they adhered to their generated ML diet plan.
- **Expanded Nutritional Ontology:** Add deeper integrations with extensive regional recipes mapping out macro and micro-nutrients across hundreds of localized Indian cuisines.
- **Conversational RAG Chatbot:** Provide the patient with an interactive AI chat window natively within the app, allowing them to ask context-aware questions about the generated diet plan (e.g., "Can I substitute the paneer for tofu?").
- **Wearable API Integrations:** Connect directly with Google Fit and Apple Health to pull real-time metabolic and activity data to adjust daily caloric targets dynamically.

---

## ⭐ Support & Acknowledgments

*A special thanks to the **Infosys Springboard Internship** program for the guidance and opportunity to innovate in the HealthTech domain.*

If you find this project useful, consider giving it a ⭐ on GitHub!
