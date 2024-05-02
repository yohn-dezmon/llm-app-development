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


