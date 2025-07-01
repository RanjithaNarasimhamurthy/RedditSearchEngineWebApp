# RedditSearchEngineWebApp

A hybrid Reddit post search engine comparing traditional keyword search (PyLucene) and modern semantic search (BERT + FAISS). :contentReference[oaicite:0]{index=0}

## Objectives

- Develop a hybrid search system for Reddit posts.  
- Compare indexing time, query speed, and result quality between PyLucene inverted index and BERT-based dense vector search. :contentReference[oaicite:1]{index=1}

## Data Collection

- Uses PRAW to crawl Reddit posts and comments from targeted subreddits.  
- Manages data in 10 MB chunks for efficient processing. :contentReference[oaicite:2]{index=2}

## Indexing Approaches

### 1. PyLucene Inverted Index

- Builds an index with fields: title, body, comments, metadata.  
- Uses `StandardAnalyzer` for stop-word removal, tokenization, and stemming.  
- Supports Boolean, proximity, and wildcard queries.  
- Total indexing time: ~29–30 seconds for a large dataset. :contentReference[oaicite:3]{index=3}

### 2. BERT-Based Dense Embeddings

- Uses `sentence-transformers/all-distilroberta-v1` to generate contextual embeddings.  
- Indexes embeddings with FAISS for approximate nearest-neighbor search using cosine similarity.  
- Provides semantic relevance beyond exact keyword matches, at higher computational cost. :contentReference[oaicite:4]{index=4}

## Web Application

- Implemented with Flask, offering a clean, user-friendly interface.  
- Dual search options: PyLucene keyword search or BERT-based semantic search.  
- Real-time query execution via subprocess calls to Java-based Lucene and Python backend integration.  
- Displays search results with relevance scores for easy method comparison. :contentReference[oaicite:5]{index=5}

## System Architecture

[ PRAW Crawler ] → Python Scripts → { PyLucene Index ←→ Flask API ←→ FAISS Index } ← BERT Embeddings

## Usage

1. **Clone the repository**  
   ```bash
   git clone https://github.com/RanjithaNarasimhamurthy/RedditSearchEngineWebApp.git
   cd RedditSearchEngineWebApp

 
## Install dependencies

pip install -r requirements.txt

## Run data collection & indexing


python crawler.py           # Fetches Reddit posts/comments

python index_lucene.py      # Builds the PyLucene index

python index_faiss.py       # Builds the FAISS index with BERT embeddings

## Start the web app

flask run

Open http://localhost:5000 in your browser
