<div align="center">

# 🧠 DocMind — RAG Document Q&A Chatbot

**Upload your documents → ask a question → get an answer with clickable source citations**

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-8A2BE2?style=for-the-badge)
![Offline Friendly](https://img.shields.io/badge/Works-Offline-brightgreen?style=for-the-badge)

</div>

---

## 📌 Overview

A **Retrieval-Augmented Generation (RAG)** application that answers questions **using only your own documents** and shows exactly which passages the answer came from.

Searching long PDFs and notes by hand is slow, and plain chatbots can make things up. DocMind first **retrieves the most relevant passages** from your files, then builds the answer from them with `[1]`, `[2]` citations you can click and verify.

It works **fully offline** out of the box. Add an Anthropic or OpenAI API key and it writes fluent, LLM-generated answers from the same retrieved passages.

## ✨ Features

- 📄 Reads **PDF, DOCX, TXT, MD and CSV** files
- ✦ Built-in **demo dataset** to try it instantly, plus **custom dataset** upload (drag & drop)
- 🔎 Sentence-aware chunking with overlap and heading metadata
- 🧮 **TF-IDF retrieval** (no downloads), with optional dense embeddings for hybrid search
- ⚡ **Streaming answers** with clickable `[n]` citations and highlighted source passages
- 🎯 Limit questions to a single file, and choose how many passages to retrieve
- 🤖 Optional **Claude / OpenAI** generation; clean offline fallback when no key is set
- 🎨 Smooth, animated glass UI with dark/light theme and mobile layout
- 🔒 Your files stay on your machine unless you add an API key

## 🛠️ Tech Stack

| Area | Tools |
|---|---|
| Language | Python |
| Backend | FastAPI, Uvicorn |
| Retrieval | scikit-learn (TF-IDF), NumPy, optional `sentence-transformers` |
| Document parsing | pypdf, python-docx, csv |
| Generation (optional) | Anthropic Claude or OpenAI API |
| Frontend | HTML, CSS, vanilla JavaScript (no build step) |

## 🔄 How It Works

```
Documents → Chunking → Index → Retrieve top-k → Answer + [n] citations
                                      │
                      ┌───────────────┴───────────────┐
                 No API key                       API key set
          (extract best sentences)        (LLM writes answer from passages)
```

1. **Load:** files are read and split into ~700-character passages on sentence boundaries.
2. **Index:** passages are indexed with TF-IDF (and embeddings, if installed).
3. **Retrieve:** your question is matched against all passages; the top results are kept and weak matches are dropped.
4. **Answer:** the reply streams in with numbered citations pointing to the source cards below it.

---

## 🚀 Getting Started

> **Requirements:** Python 3.9+ and `git`. No GPU needed.

**1. Clone the repository and open the project folder**

```bash
git clone https://github.com/Git-Markiv/DocMind.git
cd DocMind   # use your actual folder name
```

**2. Create and activate a virtual environment**

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# Mac / Linux
source .venv/bin/activate
```

**3. Install the dependencies**

```bash
pip install -r requirements.txt
```

**4. Run the server**

```bash
python run.py
```

Your browser opens at `http://127.0.0.1:8000`. (In VS Code you can also press **F5**.)

---

## 🤖 Optional: LLM Answers

```bash
pip install anthropic        # or: pip install openai
cp .env.example .env         # paste ONE key into .env
```

Restart the server. The pill in the sidebar turns green when an LLM is active.

## 🧲 Optional: Better Retrieval

```bash
pip install sentence-transformers
```

Adds dense embeddings (`all-MiniLM-L6-v2`, ~90 MB download on first run) fused with TF-IDF so paraphrased questions match better.

## 📁 Project Structure

```
DocMind/
├─ run.py                # start the server
├─ app/
│  ├─ main.py            # FastAPI routes: upload, ask, status
│  ├─ rag.py             # chunking, indexing, search, extractive answer
│  ├─ llm.py             # Claude / OpenAI streaming + offline fallback
│  ├─ loaders.py         # PDF / DOCX / TXT / MD / CSV readers
│  └─ static/            # index.html, style.css, app.js
└─ data/
   ├─ demo/              # demo dataset
   └─ uploads/           # your uploaded files
```

## 🗃️ Demo Dataset

Six short files bundled in `data/demo/`: computer vision basics, YOLOv8, machine learning essentials, RAG explained, AWS fundamentals, and a model-benchmark CSV. They were written for this project. Latency values for the classification models in the CSV are illustrative.

## ⚠️ Important Notes

- **Offline mode quotes, it doesn't write.** Without an API key, answers are the most relevant sentences from your documents, so requests like "summarize" or "explain simply" work best with an LLM key.
- **Keyword matching.** TF-IDF can miss synonyms (for example "car" vs "automobile"); install `sentence-transformers` to improve this.
- **No OCR.** Scanned PDFs without a text layer can't be read.
- **Privacy.** Nothing leaves your machine unless you add an API key; then only the retrieved passages and your question are sent to that provider.

## 🔮 Future Improvements

- [ ] Vector database support (FAISS / Chroma)
- [ ] Reranking of retrieved passages
- [ ] OCR for scanned PDFs
- [ ] Retrieval evaluation (recall@k, RAGAS)
- [ ] Docker image and cloud deployment

## 📄 License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.

## 👤 Author

**Vikram Mali**
[Portfolio](https://vikram-mali-portfolio.vercel.app/) • [LinkedIn](https://www.linkedin.com/in/vikram-mali-660a34438) • vikram2k04@gmail.com

<div align="center">

⭐ If you find this project useful, please give it a star!

</div>
