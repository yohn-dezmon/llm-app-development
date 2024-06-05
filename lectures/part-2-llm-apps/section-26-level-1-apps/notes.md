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

# v1-055 extracting structured data

this can be accomplished via the `ResponseSchema` object.
- you put the kind of info (fields) you want to extract  

```python
ResponseSchema(
    name="singer",
    description="name of the singer"
)
```

`StructuredOutputParser`:
- archives the extracted data into a JSON dictionary
- `StructuredOutputParser.from_response_schemas(__)`

**The format instructions created from the ResponseSchema + StructuredOutputParser are passed in to each prompt!**  
- in the prompt template we insert it as `{format_instructions}`   

# v1-056 Evaluate a QA app  

you can provide a set of questions and their correct answers.  
Then you can generate the predictions from a given model (e.g. conversational model).  
Then you can pass the correct answers + questions, and predictions into the `evaluation chain`.  
this will return a list of dictionaries determining if each prediction matches the desired correct response!  


Evaluation chain:
- `from langchain.evaluation.qa import QAEvalChain`
```python
evaluation_chain = QAEvalChain.from_llm(llm)
evaluate_responses = evaluation_chain.evaluate(
    questions_and_answers,
    predictions,
    question_key="question",
    answer_key="answer"
)
```

output:
```python
[{'results': ' CORRECT'}, {'results': ' CORRECT'}]
```

# v1-057 Ask a database  

question:
- what if the db is not in memory?
```python
db_chain = SQLDatabaseChain(
    llm=llm,
    database=db,
    verbose=True
)
```

answer:
- I think this can just be a SQLAlchemy wrapper around a db engine!  
- https://api.python.langchain.com/en/latest/utilities/langchain_community.utilities.sql_database.SQLDatabase.html#langchain_community.utilities.sql_database.SQLDatabase  
- https://api.python.langchain.com/en/latest/sql/langchain_experimental.sql.base.SQLDatabaseChain.html  


- `SQLDatabaseChain`
- ask questions in natural language
- db_chain.run(' ')
- it produces SQL
- queries db
- returns results   

It has to be SQLAlchemy/ORM such that the python code has access to the data model.  


# v1-058 Using a github repo as the source material

- `os.walk(repo)` 
    - allows you to iterate over a directory tree
    - each step produces a three tuple
    - (directory_path, sub_directories, filenames)
- in this context you load each dirpath into the `TextLoader`
- convert text chunks into embeddings and store them in vector db
- pass vector db into chat RetrievalQA Chain as a retriever
- ask questions about the github repo with `.run()`
- .run() output is the answer.

# v1-059 Ask an API

- there's a specific chain for API docs
    - `APIChain` 
- you pass in API docs to the APIChain
- ask questions with .run(question)
- output is answer!

# v1-060 Chatbot with memory + personality 

- specify the chatbot's role in plain text
- in the template, put a section for `{chat_history}`
- in the template put input for human: `Human: {human_input}`
- also put section for `Chatbot: `
- Make a `PromptTemplate`
    - specify `input_variables` of `chat_history` and `human_input`
- Use `ConversationBufferMemory`
- make an `LLMChain` with `OpenAI()` as the `llm`
- ask it questions with `chatbot.predict(human_input=question)`


# v1-061 RAG with DeepLake

`pip install "deeplake[enterprise]"`

- **DeepLake** is a more sophisticated vector database.
- created DeepLake api key via activeloop.ai 
- load credentials 
- create db name
- provide private documents to the vector db
- provide private doc to the RecursiveCharacterTextSplitter
- use .create_documents(data)
- create DeepLake db like so:
```python
embeddings = OpenAIEmbeddings()
dataset_path = f"hub://{my_activeloop_org_id}/{my_activeloop_dataset_name}"
DeepLake(
    dataset_path=dataset_path,
    embedding=embeddings
)
```
- load chunks and transform them into embeddings with `db.add_documents(doc_chunks)`
- create llm obj
- create RetreivalQA chain 
- pass in vector db as retriever `retriever=db.as_retriever()`
- ask questions via `.run()`


# v1-062 Simple Agent 

- the agent will decide which external plugin to use
- `pip install google-api-python-client`
- you need to generate GOOGLE_API_KEY and GOOGLE_CSE_ID
- `GoogleSearchAPIWrapper()` -- allows you to search google via an agent!
- `TextRequestsWrapper()` -- allows you to make requests to a URL...
- You pass those in as `Tool` objects to a tools array
- `Tool` is an agent
- you initialize an `agent` with `tools=tools`
- if you ask a question about a specific URL, then the TextRequestsWrapper() tool will be chosen by the agent 
- ask questions with `response = my_agent(question)` 
- output: `response['output']`

