# 🩺 Medical Chatbot (LangChain + Pinecone + OpenAI)

This project is a **Medical Question-Answering RAG Chatbot** built using LangChain, HuggingFace Embeddings, Pinecone and OpenAI GPT-4o.  
The system ingests medical PDFs, converts them into vector embeddings, stores them in Pinecone, and answers user questions using a Retrieval-Augmented Generation (RAG) pipeline.

---

## 📌 Features

- 📄 PDF ingestion from `/data` folder  
- ✂️ Text chunking using RecursiveCharacterTextSplitter  
- 🔍 Semantic Search using Pinecone  
- 🤖 GPT-4o as LLM backend  
- 🧠 Retrieval-Augmented Generation  
- 💬 Flask-based chat UI  
- 🔑 Environment variable-based secret management  

---

## 📂 Project Structure

```
GENAI/
│
├── data/                       # Medical PDFs
├── public/                     # UI images
├── research/                   # Jupyter experiments
│   └── trials.ipynb
│
├── src/
│   ├── helper.py               # PDF loader, splitter, embeddings
│   ├── prompt.py               # System prompt
│   └── __init__.py
│
├── static/                     # Static assets (optional)
├── templates/
│   └── chat.html               # Chat UI
│
├── app.py                      # Flask backend + RAG pipeline
├── store_index.py              # Index creation script
├── requirements.txt
├── .env
└── README.md
```

---

## 🧠 How the RAG Pipeline Works

### 1️⃣ Load PDFs  
Using `DirectoryLoader` to load all PDFs from `/data`.

### 2️⃣ Filter Metadata  
Keeps only clean metadata: `{ source: file_name.pdf }`.

### 3️⃣ Chunk Text  
Splits documents into overlapping chunks of 500 characters.

### 4️⃣ Create Embeddings  
Uses **MiniLM-L6-v2 (384D)** from HuggingFace.

### 5️⃣ Store/Load Pinecone Index  
Stores vector embeddings in Pinecone Serverless.

### 6️⃣ Create Retriever  
Top-k similarity search (k=3).

### 7️⃣ Build Chat Model  
Uses GPT-4o.

### 8️⃣ Build RAG Chain  
Retriever + system prompt + document stuffing + GPT output.

---

## 🚀 Setup & Installation

###  Clone the repository

```bash
git clone <https://github.com/vijaysarthak/AI-Medical-ChatBot.git>
```


###  Install dependencies

```bash
pip install -r requirements.txt
```

###  Add your `.env` file

```
OPENAI_API_KEY=your-openai-key
PINECONE_API_KEY=your-pinecone-key
```

###  (Optional) Build vector index

```bash
python store_index.py
```



## 🔧 Key Python Files

### **app.py**
- Loads embeddings  
- Loads Pinecone index  
- Creates GPT-4o RAG chain  
- Runs Flask app  
- Handles `/get` chat route  

### **src/helper.py**
Contains all helper utilities:
- `load_pdf_file()`
- `filter_to_minimal_docs()`
- `text_split()`
- `download_hugging_face_embeddings()`

### **src/prompt.py**
Defines behavior of the chatbot (system prompt).

---

## 🧪 Testing the Model

Run directly in Python:

```python
response = rag_chain.invoke({"input": "What is diabetes?"})
print(response["answer"])
```

---

## 🛡 Notes / Limitations

- Not a replacement for professional medical advice  
- PDFs must contain machine-readable text  
- Pinecone index dimension must be exactly **384**  
- GPT model cost applies  

---

## 🚀 Future Enhancements

- Add user authentication  
- Add PDF upload from UI  
- Add streaming responses (SSE/WebSocket)  
- Deploy on Render/AWS  
- Add chat history  

---

## 👨‍💻 Author

**Sarthak Vijay**  
Medical Chatbot – MCA Project

---