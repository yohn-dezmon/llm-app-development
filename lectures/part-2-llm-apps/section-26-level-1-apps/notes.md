# Level 1 Apps  

- the environment is changing
- get used to change
- LangChain is evolving  

v0.1.0
- langchain expression language 
- facilitate langchain updates
- will affect demos  
- main LangChain package divited into:
    - langchain-core: functionality (pip install)
    - langchain-community: integrations (pip install)
    - partner packages:
        - langchain-openai


v0.1.0
```python
from langchain_openai import OpenAI
# prev: from langchain.llms import OpenAI
```

things will be deprecated in v0.2.0  

# .env and /data folder 

- provided in github repo

# Code

I have it in `code/section-26-level-1-app`
- I added a `.env` file there
- I added a `/data` folder there too


# turning off deprecation warnings

```python 
import warnings

from langchain._api import LangChainDeprecationWarning

warnings.simplefilter("ignore", category=LangChainDeprecationWarning)
```


# v1-053 Summarization App

- if you have an article that has more tokens than the context window (3500 for ChatGPT 3.5), then you cannot pass the doc in at once
- you instead:
    - load document
    - check token count
    - split it into smaller parts
        - `RecursiveTextSplitter`
        - `create_documents`
    - use predefined LangChain chain to send parts to ChatGPT to get a summary of the document
        - run(article_chunks)
        - chain is a summary chain

# v1-054 Document QA

- ask questions about a large document

- load document via `langchain.document_loaders.TextLoader`
    - this is a list with metadata
    - `document[0].metadata`
    - `document[0].page_content`
- split text with a text splitter
    - this produces chunks
- convert text chunks into vector embeddings
- store embeddings in a vector database
    - FAISS
    - `FAISS.from_documents(document_chunks, embeddings)`
- use RetrieveQA chain for asking questions
    - set vector db as `retriever` in chain
    - ask questions with `QA_chain.run(question)`


