# PDF Question Answering System -- RAG with FAISS and Groq

## Overview

This notebook creates a Retrieval-Augmented Generation (RAG)
question-answering system for PDF documents. It extracts text from an
uploaded PDF, uses OCR when a page has no extractable text, splits the
content into overlapping chunks, converts chunks into embeddings, and
stores those vectors in a FAISS index. When a user asks a question, the
system retrieves relevant chunks and sends them as context to a
Groq-hosted language model.

## Features

-   Upload a PDF in Google Colab.
-   Extract text from normal, text-based PDF pages using PyMuPDF.
-   Apply Tesseract OCR to pages where normal text extraction returns no
    text.
-   Split extracted text into chunks of 500 characters with 100
    characters of overlap.
-   Generate embeddings with `all-MiniLM-L6-v2`.
-   Store and search embeddings using FAISS inner-product similarity
    with normalized embeddings.
-   Retrieve the top three matching chunks for a question.
-   Generate concise answers grounded in retrieved PDF context.
-   Continue asking questions until the user types `exit`.

## Technologies

-   Python
-   PyMuPDF (`fitz`)
-   Tesseract OCR and `pytesseract`
-   Pillow
-   Sentence Transformers
-   FAISS CPU
-   NumPy
-   Groq API (`openai/gpt-oss-20b`)
-   Google Colab file upload

## Notebook

Open and run `class5.ipynb` in Google Colab.

## Setup and Execution

1.  Upload `class5.ipynb` to Google Colab.

2.  Install the required packages:

    ``` python
    !pip -q install pymupdf sentence-transformers faiss-cpu groq numpy pytesseract pillow
    ```

3.  Install the Tesseract OCR executable in the Colab environment:

    ``` bash
    !apt-get -qq install -y tesseract-ocr
    ```

4.  Run the notebook cells in order.

5.  Upload the PDF when prompted.

6.  Enter your Groq API key when prompted. The notebook uses `getpass`,
    so the key is not echoed in the output.

7.  Wait for PDF extraction, chunking, embedding generation, and FAISS
    indexing to finish.

8.  Ask questions in the input loop. Type `exit` to stop.

## How It Works

1.  **PDF upload:** Google Colab's file picker uploads the document.
2.  **Text extraction:** PyMuPDF reads text from each page.
3.  **OCR fallback:** If a page has no extractable text, the page is
    rendered as an image and processed with Tesseract.
4.  **Chunking:** The extracted text is divided into 500-character
    chunks with 100-character overlap.
5.  **Embedding:** `all-MiniLM-L6-v2` converts each chunk into a vector.
    Embeddings are normalized.
6.  **Vector indexing:** FAISS `IndexFlatIP` stores the vectors and
    searches by inner product; with normalized vectors, this corresponds
    to cosine similarity.
7.  **Retrieval:** The three most relevant chunks are selected for each
    question.
8.  **Answer generation:** Groq receives the retrieved context and
    question. The system prompt instructs it to answer only from the
    supplied PDF context.

## Example Interaction

``` text
Ask a question (or 'exit'): What is the main topic of the document?

Best Matching PDF Content:
[Answer based on the retrieved PDF context]
```

## Important Notes and Limitations

-   The notebook is designed for Google Colab because it uses
    `google.colab.files.upload()` and Colab shell commands.
-   OCR is used only when `page.get_text("text")` returns no text for a
    page. A page with partial or poor-quality extracted text may not
    automatically trigger OCR.
-   Retrieval quality depends on the PDF text quality, chunk size,
    embedding model, and whether the relevant information appears in the
    retrieved top-three chunks.
-   The model is instructed not to answer beyond the retrieved context,
    but generated answers should still be checked against the source
    PDF.
-   The notebook downloads the embedding model the first time it is
    used.
-   Never commit API keys, private PDFs, or confidential extracted text
    to a public repository.

## Project Structure

``` text
project/
├── class5.ipynb
└── README_class5.md
```
