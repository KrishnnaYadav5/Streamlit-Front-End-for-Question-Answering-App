# LLM Question-Answering Application 🤖

A powerful Streamlit-based web application that enables you to upload documents and ask questions about their content using OpenAI's GPT models and LangChain.

## Features

✨ **Multi-Format Document Support**
- Upload and process PDF documents
- Support for DOCX (Word) files
- Support for TXT text files

🧠 **Intelligent Document Processing**
- Automatic document chunking with configurable chunk sizes
- Vector embeddings using OpenAI's text-embedding-3-small model
- Semantic search capabilities with Chroma vector store

💬 **Interactive Q&A Interface**
- Ask questions about your uploaded documents
- Get precise answers powered by GPT-3.5-turbo
- Maintain conversation history for context

📊 **Cost Tracking**
- Real-time embedding cost calculation
- Token count estimation using tiktoken
- Transparent pricing information

## Tech Stack

- **Streamlit** - Interactive web application framework
- **LangChain** - LLM orchestration and chain management
- **OpenAI** - GPT models and embedding services
- **Chroma** - Vector database for semantic search
- **Python 3.8+** - Core programming language

## Installation

### Prerequisites
- Python 3.8 or higher
- OpenAI API key (get it from [OpenAI Platform](https://platform.openai.com/))

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/KrishnnaYadav5/Streamlit-Front-End-for-Question-Answering-App.git
   cd Streamlit-Front-End-for-Question-Answering-App
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up your OpenAI API key**
   
   Option A: Using environment file (recommended)
   ```bash
   # Create a .env file in the project root
   echo "OPENAI_API_KEY=your_api_key_here" > .env
   ```
   
   Option B: Input via application UI
   - Run the app and enter your API key in the sidebar text input

## Usage

### Running the Application

```bash
streamlit run chat_with_documents.py
```

The application will open in your browser at `http://localhost:8501`

### How to Use

1. **Upload a Document**
   - Click on "Upload a file" in the sidebar
   - Select a PDF, DOCX, or TXT file from your computer

2. **Configure Settings (Optional)**
   - **Chunk size**: Adjust the size of text chunks (default: 512)
     - Smaller chunks = more precise but slower
     - Larger chunks = faster but less precise
   - **k value**: Number of similar documents to retrieve (default: 3)
     - Higher k = more context but potentially less focused

3. **Click "Add Data"**
   - The application will process and embed your document
   - You'll see the embedding cost in USD

4. **Ask Questions**
   - Enter your question in the text input
   - The AI will search relevant document sections and provide an answer
   - View the answer and chat history in real-time

## Project Structure

```
.
├── chat_with_documents.py                 # Main application file
├── requirements.txt                        # Python dependencies
├── img.png                                 # Application logo/image
├── code_for_old_library_version/          # Legacy code for older LangChain versions
│   ├── chat_with_documents.py
│   └── requirements.txt
└── README.md
```

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| openai | 2.26.0 | OpenAI API client |
| langchain | 1.2.12 | LLM framework |
| langchain-classic | 1.0.2 | Legacy chain compatibility |
| langchain-openai | 1.1.11 | OpenAI integration |
| langchain-community | 0.4.1 | Community tools |
| langchain-core | 1.2.18 | Core abstractions |
| langchain-text-splitters | 1.1.1 | Text chunking utilities |
| chromadb | 1.5.5 | Vector database |
| streamlit | 1.55.0 | Web framework |
| tiktoken | 0.12.0 | Token counting |
| pypdf | 6.8.0 | PDF processing |
| docx2txt | 0.9 | DOCX processing |
| python-dotenv | 1.2.2 | Environment management |

## How It Works

### Document Processing Pipeline

1. **Loading**: Documents are loaded using appropriate loaders (PyPDFLoader, Docx2txtLoader, or TextLoader)
2. **Chunking**: Text is split into overlapping chunks using RecursiveCharacterTextSplitter
3. **Embedding**: Each chunk is converted to a vector embedding using OpenAI's embedding model
4. **Storage**: Embeddings are stored in Chroma vector database

### Question-Answering Flow

1. **Retrieval**: When you ask a question, similar document chunks are retrieved from the vector store
2. **Context Assembly**: Retrieved chunks are combined into the LLM prompt
3. **Generation**: GPT-3.5-turbo generates an answer based on the document context
4. **Conversation**: Answers are added to chat history for context

## Configuration Options

### Chunk Size
- **Range**: 100 - 2048 characters
- **Default**: 512
- **Recommendation**: 256-512 for most documents

### k (Number of Retrieved Documents)
- **Range**: 1 - 20
- **Default**: 3
- **Recommendation**: 3-5 for balanced results

## Pricing

OpenAI API costs depend on:
- **Embeddings**: $0.00002 per 1K tokens (text-embedding-3-small)
- **Chat Completions**: Variable based on model and token usage
- **Tokens Calculated**: The app shows estimated costs before processing

Check [OpenAI Pricing](https://openai.com/pricing) for current rates.

## Legacy Support

For users with older versions of LangChain (pre-v0.2), the `code_for_old_library_version/` directory contains compatible code using deprecated APIs.

### Key Differences in Old Version:
- Uses `RetrievalQA.from_chain_type()` instead of modern chain factories
- Different import paths for embeddings and vector stores
- Older tiktoken pricing

## Troubleshooting

### Common Issues

**"Document format is not supported"**
- Ensure file is one of: .pdf, .docx, .txt
- Check file isn't corrupted

**"OPENAI_API_KEY not found"**
- Add API key to .env file or input via sidebar
- Verify .env file is in the project root

**"Chroma vector store error"**
- Clear chromadb cache: `rm -rf .chroma_db`
- Reinstall chromadb: `pip install --upgrade chromadb`

**"Memory/Performance issues"**
- Reduce chunk size
- Process smaller documents
- Restart the application

## Environment Setup

Create a `.env` file in the project root:

```
OPENAI_API_KEY=sk-your-actual-key-here
```

Never commit this file to version control!

## Performance Tips

1. **For Large Documents**: Increase chunk overlap to maintain context
2. **For Better Accuracy**: Lower the k value to focus on most relevant chunks
3. **For Faster Processing**: Reduce chunk size, but this may hurt accuracy
4. **For Cost Savings**: Use larger chunks to reduce embedding costs

## Security Notes

- 🔒 Never hardcode API keys in code
- 🔐 Use environment variables or secure vaults
- 🛡️ Limit API key permissions to necessary endpoints only
- 📝 Store API keys in .env (add to .gitignore)

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest improvements
- Submit pull requests

## License

This project is open source and available for use and modification.

## Support

For issues and questions:
1. Check the Troubleshooting section above
2. Review OpenAI's API documentation
3. Open an issue on GitHub

## Changelog

### Current Version (v1.0)
- ✅ Multi-format document support (PDF, DOCX, TXT)
- ✅ LangChain v1.x compatibility
- ✅ Modern chain API implementation
- ✅ Real-time cost tracking
- ✅ Chat history persistence
- ✅ Configurable parameters

### Legacy
- Old library versions supported in `code_for_old_library_version/`

## Resources

- [Streamlit Documentation](https://docs.streamlit.io/)
- [LangChain Documentation](https://python.langchain.com/)
- [OpenAI API Reference](https://platform.openai.com/docs/)
- [Chroma Vector Database](https://www.trychroma.com/)

---

**Created by**: KrishnnaYadav5  
**Last Updated**: 2024  
**Language**: Python 🐍
