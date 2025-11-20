# Justify

**Justify** is an AI-powered legal assistant that helps users understand legal documents instantly.
It supports PDF ingestion, conversational Q&A, translation, voice input, source citation, glossary extraction, and contextual question suggestions — all backed by a RAG (Retrieval-Augmented Generation) pipeline.

## Key Features

* **PDF-based RAG System**
  → Upload one or more PDFs and ask questions directly from the content.

* **Conversational Q&A**
  → Uses a retrieval-augmented chain to deliver accurate, context-aware legal answers.

* **Voice Input (Speech-to-Text)**
  → Speak your question using the built-in mic recorder.

* **Translation Support**
  → Translate AI responses into multiple languages (Spanish, French, German, Hindi).

* **Read-Aloud (Text-to-Speech)**
  → Listen to answers using integrated speech synthesis.

* **Legal Glossary Extraction**
  → Auto-detects legal terms (Acts, Authorities, Dates, Sections, Concepts).

* **Contextual Suggested Questions**
  → Dynamically generates useful questions based on uploaded document content.

* **Source Transparency**
  → Shows top source pages used to generate each answer.

* **Chat History + Download**
  → Full conversation preserved across turns with export support.

## Tech Stack

* **Frontend/UI:** Streamlit
* **NLP & RAG:** LangChain, FAISS, HuggingFace Transformers
* **Models:**

  * *Flan-T5 Small* (LLM)
  * *all-MiniLM-L6-v2* (Embeddings)
  * Helsinki Opus MT (Translation)
* **NER:** spaCy
* **Audio:** SpeechRecognition, pydub, streamlit-mic-recorder

## Project Structure

```
.
├── app.py                  # Main Streamlit UI + logic
├── rag_pipeline.py         # RAG pipeline, embeddings, QA chain, glossary, suggestions
├── requirements.txt        # Dependencies
└── README.md
```

## Setup Instructions

### **Create Virtual Environment**

```bash
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
```

### **Install Dependencies**

```bash
pip install -r requirements.txt
```

### **Install spaCy Model**

```bash
python -m spacy download en_core_web_sm
```

### **Install FFmpeg (Required for Audio)**

Ubuntu:

```bash
sudo apt-get install ffmpeg
```

Mac:

```bash
brew install ffmpeg
```

Windows:

* Download from: [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)
* Add to PATH.

### **Run the App**

```bash
streamlit run app.py
```

App opens at:
**[http://localhost:8501](http://localhost:8501)**


## How It Works (RAG Pipeline)

1. **Upload PDFs**
   → Extract pages → Split into chunks → Embed using MiniLM.

2. **FAISS Vector Store**
   → Enables fast semantic retrieval.

3. **ConversationalRetrievalChain**
   → Combines retrieved chunks + user question → LLM generates answer.

4. **Post-processing**

   * Translation
   * Read-aloud
   * Source extraction
   * Glossary tagging
   * Suggested questions


## Core Functionalities

###  Asking Questions

* Use text input
* Click a suggested question
* Use microphone to ask via speech

###  Translation

Choose a language from sidebar:

* Spanish
* French
* German
* Hindi

###  Legal Glossary Extraction

Automatically identifies legal entities (Acts, Authorities, Dates, Sections, Concepts) from each PDF.

###  Suggested Questions

Generates 8–10 high-value queries based on document context (FAQ style).

## To Do

* Add PDF download for answer summaries
* Add multi-language **question** translation (not just answers)
* Improve NER accuracy for legal terms
* Add option to save FAISS index for reuse
* Provide offline model support
