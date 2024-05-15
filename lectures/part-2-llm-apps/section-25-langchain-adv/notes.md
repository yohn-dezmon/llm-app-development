# LangSmith

- created by LangChain
- beta
- good for evaluation phase
- you have to ask for invitation code

https://smith.langchain.com/o/4efe5901-501c-53d7-a202-0bae57c3873e/

You need to create a langchain API key. 

LANGCHAIN_TRACING_V2=true
LANGCHAIN_ENDPOINT=https://api.smith.langchain.com
LANGCHAIN_API_KEY=<your-api-key>
LANGCHAIN_PROJET=<project>

`pip install langsmith`  

You can create "groups" in LangSmith.
There are LangSmith "projects".  
Within the project it shows you what operations you're doing in that script.  

You can create "tags" and set them on your LLMChain object:
```python
chain = LLMChain(
    llm=llm,
    prompt=prompt,
    tags=["Cyrus", "Persia"]
)
```

You can "auto evaluate" your LLM applications.  
- you provide LangSmith with an evaluation dataset
    - i.e. questions and answers that are correct
- you can use these to compare the output of your application
- it can be expensive to run! (be careful with the size of your evaluation datasets)  

# LangServe  

- helps us build an API for our application 
- integration with FastAPI


# LangChain Templates  

- CLI based
- install the client in your terminal
- 

`langchain app new my_app --package rag-conversation`
- this creates a `my_app` folder
- has an app folder with `server.py` 
- packages folder
    - rag-conversation
        - rag-conversation
        - test
- pyproject.toml
- readme.md

`langchain serve`

... 
very beta
... 

# LangChain Chatbot  

https://chat.langchain.com/  



