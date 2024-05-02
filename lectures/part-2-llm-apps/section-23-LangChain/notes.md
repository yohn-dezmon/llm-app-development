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

# Chat Models:
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


prompt templates:
- the application developer creates a template and the user fills in specific variables
- user pases input via key value pairs 
- 
PromptTemplate:
- input_variables: list[str]
- template: str
The process for creating a prompt for a chat model vs a LLM model is similar but slightly different.
———————
Few Shot Prompt Template:
- not only instructions but also examples
- 
Chain of thought prompt:
- provide sample prompt, sample response, and then an explanation of why it’s correct 
FewShotPromptTemplate:
- examples
- example_prompt
- input_variables 
- suffix 
———————
# Output Parsers
- format output from model into a different format (e.g. JSON dictionary)
PydanticOutputParser !
- 
In our template we include a `{format_instructions}` variable.  
You create a class (Pydantic)
```
class ReviewsDesiredOutputStructure(BaseModel):
	sentiment: List[str] = Field(
	)
	positive: List[str] = Field(
	)
	negative: List[str] = Field(
	)
output_parser = PydnaticOutputParser( pydantic_object=ReviewsDesiredOutputStructure )
```
PromptTemplate:
- template
- input_variables
- partial_variables= { “format_instructions”: output_parser.get_format_instructions() } 


———————

# Document Loaders
From PDF
From youtube video (to text)
From websites (various loaders for this)


# Splitters:
First step of the RAG technique!
Create chunks of text from your data source
Paragraphs are much more useful for chatgpt than words or chunks of sentences
Paragraphs provide much more context per token
Adding metadata to text chunks if possible is useful
Markdown is useful if you want to provide metadata (MarkdownHeaderTextSplitter)

RecursiveCharacterSplitter:
Most commonly used splitter

- what is the `chunk_overlap` of `RecursiveCharacterTextSplitter`
- I guess it just allows there to be a window of x characters where it can try to find a newline or whitespace to separate on?



# Callbacks:
StdOutCallbackHandler() 
Outputs chat text to stdout if you use chain.run(input=”bear”, callbacks=[handler])
Equivalent to using verbose=true 
Can be used to debug the internals of a Chat response 
Get_openai_callback -- this allows you to see the cost of a given chat response 

# OpenAI Functions:
- You can pass in info about a function and the functions parameters to ChatGPT
- You can make an agent that will select the proper function based on the users question
- Problem: With langchain, this might break if they ask a question that doesn’t relate to any of the functions provided (!!)
    - solution: Use chat model from OpenAI directly...

- `from langchain.chains.openai_functions import create_openai_fn_chain`

`create_openai_fn_chain`:
- `functions` argument:
    - functions with metadata that you pass in via JSON explaining what each function does.
    - the fn chain can choose which function to use for each prompt  


pass in prompts via `chain.run()`  

# Connect with FastAPI

- yeah.

# Agents

- not mature functionality
- expensive with OpenAI
- get stuck in loops if asked questions they aren't trained for  

load embeddings into a vector database...

you provide "tools" to the LLM agent, and it decides which tool to use.

```python
from langchain.agents import load_tools

tool_names = ["llm-math"]
```

max iterations necessary to limit the agent.  

You can define a custom tool, which provides access to a vector database created with the RAG technique.  

# Indexing API  


```python
from langchain.indexes import SQLRecordManager, index
```

allows you to iteratively update your vector database with new documents/modified documents.  





