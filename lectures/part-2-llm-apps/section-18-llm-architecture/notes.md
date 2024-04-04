# Basic Architecture

1. Foundational LLM (level 1 app) 
2. Orchestration framework (level 1 app)
3. Vector database: store private data here (level 1 app)
4. UI (level 2 app)


# Advanced architecture 

Fullstack application.  

- external APIs
- LLM
- AWS S3 for cloud storage
- backend server (e.g. fastAPI)
- orchestration framework (?)
- database (vector + traditional)  
- frontend server (e.g. Next.js)  

For hosting the backend, we'll use `Render.com`.  
For hosting the frontend, we'll use `Vercel.com`  

Orchestration frameworks:
- langchain
- llama index  

# Preview of LLM adv. app (1)  

- SEC Insights
- built by LlamaIndex  
- uses the RAG technique  
- answers questions about SEC 10-k and 10-q documents 
- QA Chat grounded in source of truth SEC documents
- has a PDF viewer  



