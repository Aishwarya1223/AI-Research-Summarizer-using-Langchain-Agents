# AI Research Summarizer (LangChain Agents)

An intelligent research assistant that:
- Searches **arXiv** for recent papers on any topic  
- Summarizes them in plain English (even for non-experts)  
- Stores them in a persistent **vector database (Chroma)** for long-term retrieval  
- Lets you query your personal “research memory” conversationally

Built with **LangChain**, **OpenAI**, **Chroma**, and the **arxiv** Python client.

---

## ✨ Features

- **ArxivSearch Tool** – Find and summarize recent academic papers from arXiv  
- **Research Memory** – Store paper summaries in Chroma vectorstore for quick retrieval  
- **Conversational Memory** – Keep track of chat history and follow-ups with `ConversationBufferMemory`  
- **Extensible** – Add more sources, custom embeddings, or advanced summarization chains  

---

## 🏗️ Architecture

```
User ↔ LangChain Agent (ChatOpenAI)
         ├── Tool: ArxivSearch (arxiv API → titles + abstracts)
         ├── Tool: ResearchMemorySearch (Chroma retriever)
         └── Memory: ConversationBufferMemory
                   ↑
        Vectorstore: Chroma (./chroma_db) ← OpenAIEmbeddings
```

---

## 📦 Tech Stack

- Python 3.10+
- LangChain
- OpenAI API (Chat + Embeddings)
- ChromaDB
- arxiv Python client

---

## 🔑 Prerequisites

1. **Python Environment**  
   Create and activate a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate    # Windows: .venv\Scripts\activate
   ```

2. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **OpenAI API Key**
   ```bash
   export OPENAI_API_KEY="sk-..."
   ```
   *(For Windows PowerShell: `setx OPENAI_API_KEY "sk-..."`)*

---

## 📂 Project Structure

```
.
├── README.md
├── requirements.txt
├── main.py                # Your main script
├── chroma_db/              # Chroma persistent storage
```

---

## ⚙️ How It Works

1. **Search** – Use the `ArxivSearch` tool to query arXiv for recent papers  
2. **Summarize** – The LLM explains the papers in plain language  
3. **Store** – Save (title + abstract) into Chroma with embeddings for future queries  
4. **Retrieve** – Ask follow-up questions; the retriever finds relevant stored papers  
5. **Conversational Memory** – The agent remembers what you’ve already asked

---

## 🚀 Usage

### 1. Run the Agent with Arxiv Search
```python
agent.run("Find 3 recent papers on quantum computing and explain them to me like I'm 15.")
agent.run("What did I ask?")
```

### 2. Store Papers in Vector Memory
```python
store_arxiv_results("quantum computing superconducting qubits")
```

### 3. Query Stored Research
```python
agent.invoke({"input": "Give me a quick overview of stored research related to quantum entanglement."})
agent.invoke({"input": "What did I ask for?"})
```

---

## 📜 Example Output

**Prompt:**
```
Find 3 recent papers on quantum computing and explain them to me like I'm 15.
```

**Sample Response:**
> 1. *Paper A*: Talks about how qubits made from superconductors can store information longer.  
> 2. *Paper B*: Explains a way to reduce errors in quantum calculations.  
> 3. *Paper C*: Describes a method to connect multiple quantum computers.  
> *(All explained in simple terms.)*

---

## 🛠️ Extending the Project

- Swap **OpenAI** with **Groq** or other LLM providers  
- Add **PDF ingestion** for full-text summarization  
- Include **citations** in responses using stored metadata  
- Integrate with **Gradio** or **Streamlit** for a web UI  

---

## 🐛 Troubleshooting

- **Empty Results?** Try refining the arXiv query  
- **Chroma Not Saving?** Ensure `vectorstore.persist()` is called and `persist_directory` exists  
- **Token Limit Issues?** Reduce `k` in retriever or summarize chunks before passing to the LLM  

---

## 🔒 Responsible Use

This tool summarizes research papers. Always verify critical findings by reading the original sources.  
Respect **arXiv** usage policies and **OpenAI** terms of service.

---

## 📜 License

MIT License – you are free to use and modify this project.

---

## 🤝 Contributing

Pull requests welcome for:
- Additional research sources
- Improved summarization pipelines
- Better UI/UX
