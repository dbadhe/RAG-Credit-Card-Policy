# Advanced RAG Techniques Demonstration

This project demonstrates and compares several advanced Retrieval-Augmented Generation (RAG) techniques. The goal is to show how different strategies can improve the relevance and quality of answers generated by a Large Language Model (LLM) when querying information from a specific document (in this case, a PDF about a credit card policy).

## Description

The notebook implements a RAG pipeline that involves:

1.  Loading and processing a PDF document 
2.  Splitting the document text into manageable chunks.
3.  Generating vector embeddings for the text chunks using Sentence Transformers.
4.  Storing the text chunks and their embeddings in a ChromaDB vector database.
5.  Querying the vector database to retrieve relevant context based on a user question.
6.  Generating an answer using the OpenAI API, informed by the retrieved context.
7.  Comparing the results of different RAG enhancement strategies.

## Features / RAG Techniques Demonstrated

* **Baseline:** Querying the LLM without any retrieved context.
* **Basic RAG:** Retrieving relevant document chunks based on the original query and providing them as context to the LLM.
* **Query Expansion (Hypothetical Answer / HyDE):** Generating a hypothetical answer first, then using the original query + hypothetical answer to retrieve documents, potentially improving relevance.
* **Query Expansion (Multiple Subqueries):** Generating multiple related subqueries from the original query, retrieving documents for all queries, and using the combined, deduplicated context.
* **Re-ranking (Cross-Encoder):** Using a more computationally intensive Cross-Encoder model to re-rank the initially retrieved documents for better relevance before feeding them to the LLM.

## Requirements

* Python 3.x
* Jupyter Notebook or JupyterLab
* An OpenAI API Key (I've used Ollama too)

## Installation

1.  **Clone the repository (if applicable):**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Create a virtual environment :**
    ```bash
    python -m venv venv
    source venv/bin/activate  
    ```

3.  **Install required libraries:**
    ```bash
    pip install -r requirements.txt
    ```
    *(If a `requirements.txt` file is not provided, you can create one or install manually)*:
    ```bash
    pip install pandas numpy chromadb-client openai python-dotenv pypdf langchain sentence-transformers umap-learn matplotlib transformers
    ```
    *Note: `transformers` is needed for the `CrossEncoder`.*

4.  **Set up Environment Variables:**
    * Create a file named `.env` in the root directory.
    * Add your OpenAI API key to the file:
        ```
        OPENAI_API_KEY=sk-YourActualOpenAIKeyHere
        ```

5.  **Place Input Data:**
    * Ensure the input PDF file is present in the same folder.

## Usage

1.  Activate your virtual environment (if you created one).
2.  Launch Jupyter Notebook or JupyterLab:
    ```bash
    jupyter notebook
    # or
    jupyter lab
    ```
3.  Open the Rag Immplementation notebook.
4.  Run the cells sequentially from top to bottom.

## Workflow Overview

1.  **Load & Prepare:** Loads the API key, reads the PDF, and splits the text into chunks.
2.  **Embed & Store:** Initializes ChromaDB, creates embeddings for text chunks, and stores them in the vector database.
3.  **Define Helpers:** Sets up reusable functions for retrieving documents and generating LLM answers.
4.  **Execute Strategies:** Runs each RAG strategy:
    * No RAG (Baseline)
    * Basic RAG
    * Query Expansion (Hypothetical Answer)
    * Query Expansion (Subqueries)
    * Re-ranking (applied to initial retrieval and subquery retrieval results)


## Output

* **Notebook Output:** Prints the answers generated by each RAG strategy, status messages, and optionally displays the UMAP embedding plot.
* **`results_comparison.csv`:** A CSV file containing a table comparing the inputs and outputs of each demonstrated RAG technique.


