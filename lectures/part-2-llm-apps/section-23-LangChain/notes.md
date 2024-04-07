# LangChain

`v.0.1.0` version changes
- january 2024
- LangChain is divided into:
    - `langchain-core`: functionality  
    - `langchain-community`: integrations/extensions
    - `partner packages`:
        - `langchain-openai`
        - `from langchain_openai import OpenAI`

- pip install
    - `langchain-openai`
    - `langchain-community`


# Github Repo 

https://github.com/AI-LLM-Bootcamp/data

when you instantiate an OpenAI LLM, you can set its temperature (creativity)
(0.9 --> high creativity)  


pip install dotenv
pip install langchain_openai
pip install langchain 

`serpapi` tool == google search

agents can "reason" which tool to use out of those supplied when answering a question.  
agents have goals (?).   

You create a chain by giving it an (a) llm (b) prompt template
- each time you call chain.run() you pass in a different variable to be put into the prompt template.  

chain is a set of instructions.  

the LLM can be any model (OpenAI, Anthropic, etc.)  

`ConversationChain` --
- you assign it to a variable
- you then call `my_conversation("question or what evz?")`
- the AI responds
- both your questions and its responses are stored in the `my_conversation` variable/function :D  

we just went over `v1-052-langchain-in-15-mins` :D

# Models

Replicate API Token:
https://replicate.com/account/api-tokens


LLMs != Chat Models in langchain.

LLMs (langchain):
- receive text
- respond with text (no schema)

Chat Models:
- input a "chat message"
- output a "chat message"
- each chat message has a schema
- you get a response with "content" field 
- each response is of type `<class 'langchain_core.messages.ai.AIMessage'>`
- each question can have a SystemMessage (which has a content field)
and a HumanMessage (which has a content field)

???
`pip install replicate`

Multiple ways to do the same thing:
- `my_chat = ChatOpenAI()` --> `my_chat(chat_question)`
- `my_chat.predict_messages()` 
- `my_chat.invoke()`  

`invoke()`:
- the result of `my_chat.invoke()` has additional `response_metadata` field!   



