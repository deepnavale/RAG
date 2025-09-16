### README.md for the RAG Conversational Chatbot

This is a comprehensive README for a Python-based conversational chatbot built with **Streamlit** that utilizes **Retrieval-Augmented Generation (RAG)** to answer questions based on uploaded PDF documents. The application also incorporates chat history to maintain conversational context.

-----

### Key Features :zap:

  * **Conversational AI:** Engage in a natural, back-and-forth conversation with the chatbot.
  * **PDF Integration:** Upload PDF files, and the chatbot will use their content as a knowledge base.
  * **Chat History:** The application remembers previous interactions in the conversation for a more coherent experience.
  * **Groq API Integration:** Uses the Groq API for fast and efficient inference with the **Gemma2-9b model**.
  * **LangChain Framework:** Built using various LangChain components for a robust RAG pipeline, including `Chroma` for vector storage and `HuggingFaceEmbeddings` for text embedding.
  * **Streamlit UI:** A simple, intuitive web interface built with Streamlit for easy user interaction.

-----

### Prerequisites :gear:

To run this application, you need to have **Python** installed and a **Groq API key**.

You will also need to install the following Python libraries:

```bash
pip install streamlit langchain-chroma langchain-community langchain-core langchain-groq langchain-huggingface python-dotenv
```

Additionally, the `PyPDFLoader` from `langchain_community` will require a PDF-parsing library. You can install a common one like `pypdf`:

```bash
pip install pypdf
```

-----

### How to Run :rocket:

1.  **Clone the repository** (if applicable) or ensure you have the `app.py` file and the necessary PDF documents in your project directory.

2.  **Set up your environment variables:** Create a `.env` file in the same directory and add your Hugging Face token. This is used by `HuggingFaceEmbeddings` to download the embedding model.

    ```env
    HF_TOKEN=YOUR_HUGGINGFACE_TOKEN
    ```

3.  **Run the Streamlit application** from your terminal:

    ```bash
    streamlit run app.py
    ```

4.  **Enter your Groq API key:** When the application launches in your browser, a text input field will prompt you to enter your Groq API key.

5.  **Upload a PDF:** Use the file uploader widget in the sidebar to upload one or more PDF documents. The application will process these files and create a vector store.

6.  **Start chatting:** Ask questions related to the content of the uploaded PDF, and the chatbot will respond.

-----

### Technical Breakdown :brain:

The `app.py` script orchestrates the entire RAG pipeline.

  * **Initialization:** Imports all necessary libraries and sets up Streamlit for the user interface. It also loads the Hugging Face token from a `.env` file.
  * **Embedding and Vector Store:** Uses `HuggingFaceEmbeddings` with the `all-MiniLM-L6-v2` model to create vector embeddings from the PDF text. The embeddings are stored in a `Chroma` vector store.
  * **Chat History Management:** A `ChatMessageHistory` object is used to store and retrieve past messages, which are then integrated into the prompt to maintain conversational context.
  * **LLM Integration:** The `ChatGroq` model is used with your provided API key to power the language model.
  * **Chains:** The script constructs several LangChain chains:
      * `create_history_aware_retriever`: This chain modifies the user's question based on chat history to make it a better query for the retriever.
      * `create_stuff_documents_chain`: This chain takes the retrieved documents and the user's question and formats them into a single prompt for the LLM.
      * `create_retrieval_chain`: This combines the retriever and the document chain.
  * **Streamlit Interface:** The front end handles user input for the Groq API key and the chat box. It also displays the chatbot's responses and the underlying chat history.

-----
