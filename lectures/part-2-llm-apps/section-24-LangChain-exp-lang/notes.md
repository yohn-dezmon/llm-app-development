# LCEL Chains  

LangChain Expression Language

old way:
```python
llm = ChatOpenAI()
prompt = ChatPromptTemplate.from_template(
    "Who won the soccer world cup of {year}?"
)
chain = LLMChain(llm=llm, prompt=prompt)
chain.predict(year="2020")
```
new way (chain):
```python
new_chain = prompt | llm 
new_chain.invoke({"year": "2010"})
```

# LCEL Output Parsers 

old way:
```python
llm = ChatOpenAI()
prompt = ChatPromptTemplate.from_template(
    "Who won the soccer world cup of {year}?"
)
output_parser = StrOutputParser()
chain = LLMChain(llm=llm, prompt=prompt, output_parser=output_parser)
```

new way LCEL:
```python
new_chain = prompt | llm | StrOutputParser() 
new_chain.invoke({"year": "2010"})
```

# Arguments 

```
new_chain = prompt | lllm.bind(stop=["\n2"]) | StrOutputParser()
new_chain.invoke({"Year": "2010"})
```

^ This will stop a list that is supposed oto generate 3 bullet points
at the first bullet point.   
I'm not sure how `bind(stop=[])` works exactly...  


# LECL RAG APPS 

LCEL -> lang chain expression lang 
RAG -> ...

`RetrievalQA` chain.
- responds to questions about our private document

```python
# this is the vector db
stored_embeddings = FAISS.from_documents(document_chunks, embeddings)

QA_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=stored_embeddings.as_retriever()
)

from langchain.prompts import PromptTemplate

template = """Answer the question based only on the following context: {context}

Question: {question}
"""
prompt = PromptTemplate.from_template(template)

retriever = stored_embeddings.as_retriever()

from langchain.schema.output_parser import StrOutputParser
from langchain.schema.runnable import RunnablePassthrough

chain = (
    {"context": retriever, "question": RunnablePassthrough()}
    | prompt
    | llm
    | StrOutputParser()
)
```

- ok so you pass the entier vector db as the "context"
- what if the vector db doesn't fit in memory?
- RunnablePassthrough -- this is dynamic and becomes the response from the user passed in via `chain.invoke()`:

```python
chain.invoke("What is this article about?")
```



