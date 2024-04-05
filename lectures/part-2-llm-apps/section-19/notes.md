PostgreSQL can be used as a vector database. 
secinsights.ai  
Loads documents and answers questions about them  

Llama index is an alternative to LangChain  

SECTION 19

Selecting a foundational LLM:
Mistral
Anthropic
ChatGPT
Google’s PaLM 
Cohere
Falcon (open source)
Llama-2 (open source)
Considerations: accuracy, cost, latency, privacy 

By far, most used, foundational model was ChatGPT.  
ChatGPT is the most accurate.

Selecting tech stack:
Palm (alternative to ChatGPT)
LangChain is more popular than LLama index
LangSmith
Fine tuning … 

Vector databases:
Pinecone
Pg_embedding
PGvector (postgres)
Chroma
Supabase
Redis
Elastic
MongoDB Vector 
Databricks Lakehouse

Observability:
Langsmith 
Arthur 

Model Serving & Hosting:
OpenAI directly 

ORCHESTRATION FRAMEWORK 

Main ones:
LangChain 
LlamaIndex

Why do we need orchestration frameworks?
They eliminate the limitation of a context window with the RAG technique 
They provide connectors for databases and other sources
Pre-designed tools for common tasks

Alternative Orchestration Frameworks:
Prefect, Airflow, Luigi, Dagster


RAG TECHNIQUE:
Divide our data into small segments, allowing the LLM to use it within the limits of its window
Context window: maximum size that we can pass to the LLM (3,000 words 3.5 chatgpt, 6,000 words for chatgpt 4)
Retrieval augmentation generation 

RAG Technique workflow:
Divide data into small segments
Convert segments into numbers (vector embeddings)
Load embeddings into a vector database
Query the vector db (query gets converted into a vector as well) 
The vector database acts as the expert of your data that can be combined with the general knowledge of the LLM
If you ask a RAG model about a topic, it will first query the vector db, then use the results to generate a response with the LLM
LLM responsible for language generation 
Semantic similarity search

In-Context Learning Technique:
Adapting a pre-trained model to specific tasks by providing examples in the input context 

Components of RAG Technique:
Embeddings
Vector databases
Semantic similarity 
Query
Indexing 
Orchestration 

# Vector embeddings:
Each value within a given vector represents a component or dimension
For words, these might be syntactic relationships, semantic similarity, and so forth
The exact meaning of each dimension is not predefined or labeled…
These dimensions are learned automatically during the training process 

# RAG technique challenges

- splitters
    - split text into fragments
    - `CharacterTextSplitter`
    - `RecursiveCharacterTextSplitter`
- retrieval QA chain
    - `chain_type`:
        - `Stuff` -- aggregates all results of the semantic search and converts them into a prompt, with that prompt makes a call to the LLM. 
        - `MapReduce` -- makes a call to the LLM for each result of the semantic search. When it has all answers, it makes a new call to the LLM and asks it to design a single final answer considering all the previous responses.  
        - MapReduce is more expensive.

- vector database
- debugging

Rag Tecnique Phases:
- retrieval phase 
- response generation phase 

# LangChain

- highly dependent on ChatGPT
- mostly used for prototyping
- supports more features than LlamaIndex 
- many connectors

    # LangSmith
    - LLM Ops platform created by LangChain
    - 

# LlamaIndex

- generating possibilities for professional RAG applications
- also highly dependent on ChatGPT

# OpenAI

- many areas are opaque to the developer
- controls a closed app market
- favors microsoft...
- wants to take market share from LangChain and LlamaIndex  

