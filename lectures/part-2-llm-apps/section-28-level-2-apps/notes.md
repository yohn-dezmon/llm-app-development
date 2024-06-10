# Intro

Level 2 Apps:
- similar to level 1, but includes a UI
- Streamlit is a "toy UI"
- 

PoC:
- build a graphical representation of app's structure  


# Streamlit

- https://docs.streamlit.io/library/get-started
- good for PoC UI
- we'll be using editors instead of jupyter notebook
- loading the app in the cloud
- VSCode:
    - has llm integrations (co-pilot)
- we'll have `requirements.txt` 
- has temporary cloud hosting
- streamlit will drop your app (sleeping)  
- streamlit community cloud, deploy, share for free  
- put your app in public gh, sign in to community cloud, then click deploy app


● st.title(“App title”)
● st.sidebar.title(“Sidebar title”)
● st.sidebar.text_input(“Enter text here”)
● button_click = st.sidebar.button(“Click Here”)
○ If button_click:
■ Do_whatever
● streamlit run main.py

Terminal
● pyenv virtualenv 3.11.14 envname
● pyenv activate envname
● pip install -r requirements.txt
● streamlit run main.py

1. Put your app in a public GitHub repo (and make sure it has a
requirements.txt!)
2. Sign into share.streamlit.io
3. Click 'Deploy an app' and then paste in your GitHub URL
