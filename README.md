# RAG Sustav - Istraživanje i Implementacija

Ovaj projekt dokumentira proces učenja i implementacije **RAG (Retrieval-Augmented Generation)** sustava korištenjem ChromaDB i LangChain biblioteka.

## Kronologija Razvoja

### 1. **ChromaDB Istraživanje** (`/chromadb`)

Prvi korak bio je razumijevanje kako funkcionira **vektorska baza podataka**.

**Ključni koncepti:**
- Što su embeddings (vektorski prikazi teksta)
- Kako ChromaDB pohranjuje i pretražuje vektore
- Similarity search (pretraživanje po semantičkoj sličnosti)
- Collection management (organizacija podataka)

**Notebook:** [chromadb/test.ipynb](chromadb/test.ipynb)

---

### 2. **LangChain Pipeline** (`/langchain`)

Nakon razumijevanja ChromaDB-a, prešlo se na izgradnju kompletnog **Data Ingestion** i **Retrieval** pipeline-a korištenjem LangChain-a.

**Implementirano:**

#### **A) Data Ingestion Pipeline**
1. **Učitavanje dokumenata:**
   - `TextLoader` za `.txt` datoteke s UTF-8 encodingom (hrvatski znakovi)
   - `PyMuPDFLoader` za `.pdf` datoteke
   - `DirectoryLoader` za grupno učitavanje svih datoteka

2. **Document Chunking:**
   - `RecursiveCharacterTextSplitter`
   - `chunk_size=1000`, `chunk_overlap=200`
   - Dijeljenje po separatorima: `["\n\n", "\n", " ", ""]`

3. **Embeddings:**
   - OpenAI `text-embedding-3-small` model
   - Pretvaranje teksta u numeričke vektore (1536 dimenzija)

4. **Vektorska baza:**
   - ChromaDB `PersistentClient` (podatci se spremaju na disk)
   - Collection s metadata-om za svaki dokument

#### **B) Retrieval Pipeline**
1. **RAGRetriever klasa:**
   - Query embedding (pretvaranje upita u vektor)
   - Similarity search (pronalaženje najsličnijih dokumenata)
   - Top-k retrieval (vraćanje najboljih N rezultata)

**Notebook:** [langchain/test.ipynb](langchain/test.ipynb)

---

## Instalacija i Pokretanje

### 1. **Kreiranje virtualnog okruženja**

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### 2. **Instalacija zavisnosti**

```bash
pip install -r requirements.txt
```

### 3. **Konfiguracija API ključeva**

Kreirajte `.env` datoteku u root direktoriju:

```env
API_KEY=your_openai_api_key_here
```

### 4. **Pokretanje**

#### **Jupyter Notebooks (istraživanje):**
```bash
jupyter notebook
```

Otvorite:
- `chromadb/test.ipynb` - ChromaDB osnove
- `langchain/test.ipynb` - LangChain RAG pipeline


