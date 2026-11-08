# ☀️ RAG Solar Feasibility Assistant

An AI-powered **Retrieval-Augmented Generation (RAG)** system that helps rural and semi-urban users in India assess the feasibility of adopting solar energy through personalized, source-backed recommendations.

## 📌 Overview

The RAG Solar Feasibility Assistant helps users understand whether installing a solar energy system is suitable for their homes or properties.

Users can describe their location, rooftop area, monthly electricity bill, and energy requirements in natural language. The assistant retrieves relevant information from a curated knowledge base of Indian government solar policies and energy guidelines, including **MNRE, PM-KUSUM, and BEE**.

Using IBM Granite, the system generates a feasibility report covering:

- Recommended solar system capacity.
- Estimated installation cost.
- Approximate payback period.
- Applicable government subsidy schemes.
- Relevant policy references and source citations.

## 🌍 Sustainable Development Goals (SDG Alignment)

This project supports the following United Nations Sustainable Development Goals:

| SDG | Goal | Contribution |
|---|---|---|
| **SDG 7** | Affordable and Clean Energy | Promotes awareness and accessibility of solar energy. |
| **SDG 1** | No Poverty | Helps users understand potential long-term electricity cost savings. |
| **SDG 9** | Industry, Innovation and Infrastructure | Applies AI and RAG technology to renewable energy assessment. |
| **SDG 13** | Climate Action | Encourages the adoption of cleaner energy alternatives. |

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| LLM | IBM Granite (`granite4:1b`) via Ollama |
| RAG Framework | LangChain |
| Embedding Model | Sentence Transformers (`all-MiniLM-L6-v2`) |
| Vector Database | ChromaDB |
| PDF Processing | PyMuPDF |
| Frontend | Streamlit |
| Programming Language | Python |

## 📁 Project Structure

```text
solar-assistant/
│
├── docs/                  # Government solar policy PDFs
│                          # MNRE, PM-KUSUM, BEE guidelines
│
├── vectorstore/           # Persisted ChromaDB embeddings
│                          # Automatically generated
│
├── ingest.py              # PDF ingestion, chunking and embedding
├── rag.py                 # RAG pipeline and Granite LLM integration
├── app.py                 # Streamlit application interface
├── .env                   # Environment variables (not committed)
├── .gitignore             # Git ignored files
└── README.md              # Project documentation
```

## ⚙️ Installation and Setup

Follow these steps to set up and run the project locally.

### 1. Clone the Repository

```bash
git clone https://github.com/25a35a0512/RAG-SolarFeasibility.git
```

Navigate into the project directory:

```bash
cd RAG-SolarFeasibility
```

### 2. Install Dependencies

Install the required Python packages:

```bash
pip install streamlit langchain langchain-community langchain-huggingface langchain-chroma langchain-text-splitters langchain-ollama sentence-transformers chromadb pymupdf python-dotenv huggingface_hub
```

### 3. Install Ollama and Download Granite

Download and install Ollama from:

https://ollama.com/

Pull the IBM Granite model:

```bash
ollama pull granite4:1b
```

Verify the installation:

```bash
ollama run granite4:1b
```

### 4. Add the Knowledge Base

Create a `docs/` directory if it does not already exist.

Add relevant government policy documents and guidelines, such as:

- MNRE solar energy guidelines.
- PM-KUSUM scheme documentation.
- Bureau of Energy Efficiency (BEE) standards.
- Other relevant government renewable energy publications.

### 5. Configure Environment Variables

Create a `.env` file in the project root:

```env
HUGGINGFACEHUB_API_TOKEN=your_huggingface_token_here
```

Replace the placeholder with your Hugging Face API token.

**Important:** Never commit your `.env` file or expose API credentials publicly.

### 6. Build the Knowledge Base

Run the ingestion script:

```bash
python ingest.py
```

This process:

1. Loads PDF documents from the `docs/` directory.
2. Extracts text from the documents.
3. Splits the extracted content into smaller chunks.
4. Generates embeddings using Sentence Transformers.
5. Stores the embeddings in ChromaDB.

The vector database is persisted locally in the `vectorstore/` directory.

### 7. Run the Application

Start the Streamlit application:

```bash
streamlit run app.py
```

Open the application in your browser:

http://localhost:8501

## 🔄 How It Works

The system follows a Retrieval-Augmented Generation workflow:

1. **User Input:** Users provide their location, rooftop area, monthly electricity bill, and energy requirements through the Streamlit interface.
2. **Query Embedding:** The user's query is converted into vector embeddings using `all-MiniLM-L6-v2`.
3. **Information Retrieval:** ChromaDB retrieves the five most relevant document chunks using similarity search.
4. **Context Assembly:** The retrieved information is passed to the language model as contextual information.
5. **AI Generation:** IBM Granite (`granite4:1b`), running locally through Ollama, generates a response grounded in the retrieved information.
6. **Feasibility Report:** The application presents solar capacity recommendations, estimated costs, payback periods, applicable government schemes, and supporting references.

## 🛡️ Responsible AI Considerations

- **Fairness:** The knowledge base includes relevant rural and urban policies without assuming users' income levels.
- **Transparency:** Recommendations include references to retrieved source documents and their relevant chunks.
- **Privacy:** The application is designed not to persist personal user information; session handling depends on the implementation.
- **Safety:** The system prompt instructs the model to identify uncertainty and avoid unsupported figures. Users are advised to consult certified solar installers before making investment decisions.

## ⚠️ Limitations

- **Knowledge Base Dependency:** Recommendation accuracy depends on the quality and freshness of the PDFs provided. Government policies and subsidy guidelines should be updated periodically.
- **Model Limitations:** `granite4:1b` is a small language model intended for resource-constrained environments. Its responses should be treated as preliminary guidance.
- **Language Support:** The current implementation supports English only. Regional language support is a planned enhancement.
- **Financial Estimates:** Installation costs, savings, and payback periods are estimates and may vary depending on location, equipment, installation costs, tariffs, and applicable subsidies.

## 🚀 Future Enhancements

- Telugu and other regional language support.
- Real-time government subsidy and policy updates.
- Interactive solar savings calculator.
- Location-based solar potential assessment.
- More detailed financial analysis and system comparisons.

## 👨‍💻 Author

**Bobbili Madhava**

- **Email:** [madhavabobbili@gmail.com](mailto:madhavabobbili@gmail.com)
- **GitHub:** [25a35a0512](https://github.com/25a35a0512)
- **LinkedIn:** [Madhava Bobbili](https://www.linkedin.com/in/madhava-bobbili/)
- **LeetCode:** [25a35a0512](https://leetcode.com/u/25a35a0512/)

---

⭐ If you find this project useful, consider giving the repository a star!

**Built with Python, LangChain, ChromaDB, IBM Granite, and Streamlit.**
