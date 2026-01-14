# GraphRag_basic_implementation
Explainable RAG pipeline for the DataForge Challenge, transforming unstructured data into structured Knowledge Graphs. This system solves traditional RAG transparency issues by providing grounded evidence via entity-relationship extraction. 
The implementation of a basic **GraphRAG system** for preliminary testing focuses on creating an explainable and transparent pipeline that transforms unstructured text into a structured knowledge base of entities and relationships.

### 1. Environment and Technical Baseline
For a successful preliminary implementation, the following environment and models are required:
*   **Programming Environment:** A dedicated directory using **Python 3.10** is recommended, as later versions may cause errors with libraries like Gensim. The setup involves creating a conda virtual environment, upgrading `pip` and `setuptools`, and installing the `graphrag` library.
*   **Model Selection:** The system utilizes **GPT-4o** for the LLM and **text-embedding-small** for the embedding model. These are typically deployed via **Microsoft Azure OpenAI** to manage keys and endpoints in a single location.

### 2. Implementation Workflow
The implementation follows a structured sequence of configuration and indexing:
*   **Initialization:** Running the command `python -m graphrag.index --init --root .` creates the necessary folder structure, including configuration files like `settings.yaml` and `.env`.
*   **Configuration:** The `settings.yaml` file must be updated to change the model type to `azure_openai_chat` and `azure_openai_embeddings`, while the `.env` file is used to store the **OpenAI API Key**.
*   **Data Preparation:** Raw information is provided as `.txt` files within an `input` folder.

### 3. Core Processing Pipeline
The system processes data through four key stages to ensure grounding and interpretability:
*   **Entity and Relationship Extraction:** The system identifies nodes (people, places, concepts) and their connections based on co-occurrence within the text.
*   **Indexing and Graph Generation:** By running `python -m graphrag.index --root .`, the system converts text units into a **Knowledge Graph** saved as **parquet artifacts**.
*   **Community Detection:** The graph is organized into a hierarchical structure, grouping related entities into "communities" to enable high-level summarization.
*   **Querying (Local vs. Global):** 
    *   **Local Search:** Used for specific entity-based queries to provide a high-level overview.
    *   **Global Search:** Traverses multiple communities for a more detailed, multi-faceted answer.

### 4. Output and Verification
The system generates a final response grounded in the retrieved graph. To ensure **transparency**, the system can output structured evidence (entities and connections) that helps users verify the answer against the original source text. In preliminary tests, this was verified by cross-referencing specific words from the model's output with their locations in the input text file.
