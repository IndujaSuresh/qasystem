#  **Language-Aware PDF Question-Answering System**


### Overview

The script processes PDF files containing question-answer pairs, builds a question-answering (QA) system using these pairs, and interacts with the user to answer queries based on the processed content. It uses libraries like `LangChain`, `HuggingFace`, and `PyMuPDF`.

### Code Breakdown

1. **Imports:**
   - **PyTorch and HuggingFace Libraries:** For working with models and pipelines.
   - **LangChain:** For creating and managing the QA system.
   - **fitz (PyMuPDF):** For extracting text from PDF files.
   - **langdetect:** For language detection.
   - **pickle:** For serializing and deserializing the model.

2. **Functions:**
   - **`clean_output(output: str) -> str`:** Cleans the output text by removing extraneous parts and leading/trailing whitespace.
   - **`get_device()`:** Determines whether a GPU (`cuda:0`) or CPU should be used based on availability.
   - **`split_text_into_paragraphs(text_content)`:** Splits text into paragraphs based on a specified delimiter (in this case, `#`).
   - **`sanitize_filename(filename)`:** Sanitizes filenames by replacing non-alphanumeric characters with underscores.
   - **`extract_text_from_pdf(pdf_path)`:** Extracts text from each page of a given PDF file using `fitz`.
   - **`detect_language(text)`:** Detects the language of the provided text using `langdetect`.
   - **`generate_prompt(prompt: str, system_prompt: str) -> str`:** Creates a prompt for the QA system.
   - **`create_embeddings(language)`:** Creates embeddings for different languages using `HuggingFaceEmbeddings`.
   - **`create_database(documents, embeddings)`:** Creates a vector store (Chroma database) from the documents.
   - **`create_retriever(db)`:** Creates a retriever from the Chroma database for querying.
   - **`create_qa_chain(llm, retriever, prompt)`:** Sets up the QA chain using the retriever and language model.
   - **`create_llm_pipeline(model, tokenizer)`:** Creates a pipeline for text generation using a specified model and tokenizer.
   - **`process_pdf_file(filename, pdf_path, embeddings, llm, prompt)`:** Processes a PDF file, extracts question-answer pairs, detects language, creates embeddings, and sets up a QA chain.

3. **Main Function:**
   - **Model Loading:** Checks if the model is already saved as a pickle file. If not, it loads the model and tokenizer from the HuggingFace repository and saves them.
   - **LLM Pipeline Creation:** Sets up the text generation pipeline.
   - **PromptTemplate Creation:** Generates a prompt template for querying.
   - **Processing PDFs:** Iterates through the PDF files in the specified folder, extracts question-answer pairs, detects their language, and processes them to create QA chains for each language.
   - **User Interaction:** Provides a command-line interface for the user to ask questions. The script detects the language of the query and uses the corresponding QA chain to generate answers.

### Key Points

- **Handling Question-Answer Pairs:** The script extracts question-answer pairs from PDFs and uses them to build the QA system.
- **Language Detection:** Detects the language of the text and adapts the embeddings and QA chain accordingly.
- **Error Handling:** Includes error handling for various steps, including file processing and QA chain creation.
- **Interaction with User:** After processing the PDFs, the script enters a loop allowing users to input queries and get answers based on the processed question-answer pairs.

### Example Output

- For questions in Malayalam, the script uses the Malayalam QA chain and provides responses in Malayalam.
- For questions in English, it uses the English QA chain and provides responses in English.

The script sets up a robust QA system based on question-answer pairs in multiple languages, leveraging modern NLP tools and frameworks.
