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

