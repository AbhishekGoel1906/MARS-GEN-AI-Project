# MARS-GEN-AI-Project

# 📄 Automated Metadata Generator 🧠

This project provides a web-based tool to automatically generate rich metadata for unstructured documents. By uploading a file (`PDF`, `DOCX`, or `TXT`), users can instantly receive a structured JSON output containing a summary, keywords, named entities, and word count.

This tool enhances document discoverability, classification, and analysis by producing consistent, scalable, and semantically meaningful metadata.

https://huggingface.co/spaces/abhishek1211/MARS_Project

---

## 🚀 Features

-   **Multi-Format Support**: Process `.pdf`, `.docx`, and `.txt` files seamlessly.
-   **Automated Text Extraction**: Utilizes Optical Character Recognition (OCR) with Tesseract for PDFs, ensuring text is extracted even from scanned documents.
-   **📄 AI-Powered Summarization**: Generates a concise summary of the document's content using a Hugging Face Transformers model.
-   **🔑 Semantic Keyword Extraction**: Identifies the most relevant keywords and keyphrases using KeyBERT, which leverages sentence embeddings for contextual relevance.
-   **🧠 Named Entity Recognition (NER)**: Extracts key entities like persons, organizations, locations, and dates using a pre-trained spaCy model.
-   **🔢 Word Count**: Provides a quick count of the total words in the document.
-   **Structured Output**: Delivers all metadata in a clean, machine-readable JSON format.
-   **Intuitive Web UI**: A simple and user-friendly interface built with Gradio for easy document uploading and metadata viewing.

---

## ⚙️ How It Works

The automated generation process follows these steps:
1.  **File Upload**: The user uploads a supported document through the Gradio web interface.
2.  **Content Extraction**: The backend determines the file type:
    -   For **PDFs**, `pdf2image` converts each page into an image, and `Tesseract OCR` extracts the text from each image.
    -   For **DOCX** files, the `python-docx` library is used to extract all text.
    -   For **TXT** files, standard Python I/O is used.
3.  **Metadata Generation**: The extracted text is then passed to a series of NLP models:
    -   The text (trimmed to a manageable length) is fed into a `Hugging Face Summarization Pipeline`.
    -   The text is analyzed by `KeyBERT` to extract the top 5 most relevant keywords.
    -   `spaCy` processes the text to identify and list named entities.
    -   The total number of words is calculated.
4.  **Display Results**: The generated metadata is compiled into a dictionary and returned to the user as a formatted JSON object in the UI.

---

## 🛠️ Tech Stack

This project is built with a combination of powerful open-source libraries:

-   **Web Framework & UI**: [Gradio](https://www.gradio.app/)
-   **NLP & Machine Learning**:
    -   [Hugging Face Transformers](https://huggingface.co/transformers) (for summarization)
    -   [KeyBERT](https://github.com/MaartenGr/KeyBERT) (for keyword extraction)
    -   [Sentence-Transformers](https://www.sbert.net/) (as the backend for KeyBERT)
    -   [spaCy](https://spacy.io/) (for Named Entity Recognition)
    -   [NLTK](https://www.nltk.org/) (for tokenization)
-   **File & Text Processing**:
    -   [Pytesseract](https://github.com/madmaze/pytesseract) (OCR engine)
    -   [PDF2Image](https://github.com/Belval/pdf2image) (PDF to image conversion)
    -   [python-docx](https://python-docx.readthedocs.io/en/latest/) (for reading `.docx` files)
-   **Deployment**: [Hugging Face Spaces](https://huggingface.co/spaces)

---

## 🖥️ Local Setup and Installation

To run this application on your local machine, follow these steps:

### 1. Prerequisites

You must have Tesseract OCR and Poppler installed on your system.

**On macOS (using Homebrew):**
```bash
brew install tesseract
brew install poppler
```

**On Debian/Ubuntu:**
```bash
sudo apt-get update
sudo apt-get install tesseract-ocr
sudo apt-get install poppler-utils
```

**On Windows:**
-   Install Tesseract from the [official UB Mannheim repository](https://github.com/UB-Mannheim/tesseract/wiki). Make sure to add the Tesseract installation directory to your system's `PATH`.
-   Download and extract the [Poppler binaries for Windows](https://github.com/oschwartz10612/poppler-windows/releases/). Add the `bin/` directory to your system's `PATH`.

### 2. Clone the Repository
```bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```
*(Remember to replace `your-username/your-repository-name` with your actual GitHub repo URL)*

### 3. Create a Virtual Environment (Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

### 4. Install Python Dependencies
Install all the required Python libraries using the `requirements.txt` file.
```bash
pip install -r requirements.txt
```

### 5. Download NLP Models
The first time you run the app, it will automatically download the necessary NLTK and spaCy models. You can also do this manually:
```bash
python -m spacy download en_core_web_sm
python -c "import nltk; nltk.download('punkt')"
```

### 6. Run the Application
```bash
python app.py
```
The application will start, and you can access it in your browser at `http://127.0.0.1:7860`.

---

## ⚠️ Limitations and Future Improvements

-   **Large File Handling**: The application, especially when running on free, shared hardware, may struggle with very large files (over ~3-5 MB), particularly PDFs. The OCR process is memory- and CPU-intensive.
-   **OCR Accuracy**: The accuracy of text extraction from PDFs depends entirely on the quality of the document (scan resolution, text layout). Poor quality scans may result in inaccurate metadata.
-   **Language Support**: The current models are optimized for English. Future versions could include language detection and support for multilingual models.
-   **Summarization Length**: The summary is generated from the first 2000 characters to ensure performance. For long documents, this may not capture the full context.

---

Created with ❤️ by [Abhishek](https://huggingface.co/abhishek1211).
```
