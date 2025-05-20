# openai-scrape-webiste
A Jupyter Notebook project demonstrating how to scrape a website, process its content into embeddings using OpenAI, store them in a Chroma vector database, and interact via a conversational retrieval interface.

## Features

- **Web Scraping**: Utilizes a custom `Website` loader to fetch page title, full text, and hyperlinks from any URL.
- **Text Processing**: Splits long content into chunks for efficient embedding with LangChain’s `CharacterTextSplitter`.
- **OpenAI Embeddings**: Generates embeddings using OpenAI’s Embeddings API (`text-embedding-ada-002` by default).
- **Vector Store**: Persists embeddings in a Chroma database for fast similarity search.
- **Conversational Retrieval**: Builds a `ConversationalRetrievalChain` combining `ChatOpenAI`, memory, and a retriever for context-aware Q&A.
- **Interactive UI**: (Optional) Demonstrates how to launch a Gradio app for URL input and chat over scraped content.

## Requirements

- Python 3.8+
- Jupyter Notebook
- An OpenAI API key (set `OPENAI_API_KEY` in a `.env` file)
- (Optional) Hugging Face API token for remote embeddings
- (Optional) Ollama local server for alternative model usage

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/openai-scrape-website.git
   cd openai-scrape-website
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the root directory with:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   ```

## Notebook Walkthrough

Open the notebook:
```bash
jupyter notebook RAG_scrap_openAI.ipynb
```

### Core Steps

1. **Load Environment**: Load API keys and necessary libraries (`os`, `dotenv`, `requests`, `BeautifulSoup`, `LangChain` modules).
2. **Scrape Website**: Instantiate `Website(url)` to fetch title, text, and links.
3. **Model Calls**: Configure `OpenAI` client (or Ollama via OpenAI config) to analyze URLs and generate resume-friendly content.
4. **Save & Split**: Write model responses to `output.txt`, wrap in a LangChain `Document`, and split using `CharacterTextSplitter`.
5. **Embeddings & Vector Store**: Create `OpenAIEmbeddings`, delete old Chroma collection if present, generate new embeddings, and persist.
6. **Conversational Chain**: Initialize `ChatOpenAI`, memory, retriever, and build `ConversationalRetrievalChain`.
7. **Querying**: Define helper functions (`chat`, `process_url`) and demonstrate querying the chain.
8. **Gradio UI**: (Optional) Set up a Gradio Blocks app for interactive URL input and chat interface.

## Configuration

- **`db_name`**: Directory for Chroma vector store (default: `scrape_website`).
- **`MODEL`**: AI model name (default: `o4-mini` or change to `gpt-4`).
- **Chunking**: Adjust `chunk_size` and `chunk_overlap` in the text splitter.
- **Memory & Temperature**: Tune `temperature` on `ChatOpenAI` for creativity control.

## Usage

After running the notebook cells, you can:
- Chat with the content directly in Jupyter outputs.
- Launch the Gradio app by running:
  ```bash
  python app.py
  ```

## Contributing

1. Fork the repository.
2. Create a branch: `git checkout -b feature/your-feature`.
3. Commit: `git commit -m "Add feature"`.
4. Push: `git push origin feature/your-feature`.
5. Open a Pull Request.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
