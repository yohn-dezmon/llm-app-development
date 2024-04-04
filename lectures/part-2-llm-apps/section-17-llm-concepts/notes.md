# Context Window
the information the user gives to the LLM when asking for something.  
The context window is the maximum size of the context.  
- maximum length of conversation history the model takes into account when generating its response.
- NOT the length of an individual message.  

# Token 
- minimum unit for a LLM
- typically a part of a word, sometimes an entire word 
- chatgpt trained with content equivalent to 10 million books


# Prompt 
- text supplied by user that asks about the context
- can also be used to set the tone of what kind of information is to be produced  
- i.e. each prompt is an individual message to the model  


# Prompt Engineering

- "science" to build better prompts  
- techniques 
- trial and error (iterative)  
- risk minimization
    - hallucinations 
    - prompt injection 
    - prompt leaking
        - get the model to give you sensitive information (private)
    - jailbreaking
- precision 


start at 5:54

# Hallucinations 

LLMs have high accuracy when asked about subjects on which they have been trained.  

How to reduce hallucinations?
- change the "temperature" of the LLM
    - regulates the level of creaitivity 
    - if you want precise responses, ask for low temperature
    - if you want creative responses, ask for high temperature
- improving the prompt 
