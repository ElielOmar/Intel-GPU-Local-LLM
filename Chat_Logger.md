# Chat Logger For Local LLM 
If you are using a GUI for ollama this does not apply since the GUI automatically saves chats. 
By default ollama does not save your chat logs if you decide to run directly on your terminal.
This is where we use a python script to run ollama, as well as save the transcript for your chat directly to your file system. 
1. Run: pip install llama 
2. Run: ollama pull ["MODELNAME"](https://ollama.com/library)
4. Open VS code. 
5. Create a folder to store VSCODE files 
6. Create a file e.g. Chat_logger.py paste the following script replacing ["Model_name_here"](https://ollama.com/library) with the name of model you are using 

```python
import os
import datetime
from ollama import Client

client = Client()

# Make sure "logs" folder exists
os.makedirs("logs", exist_ok=True)

# Ask the user to name the chat
custom_name = input("Enter a name for this chat (leave blank for timestamp): ").strip()

if custom_name:
    # Replace spaces with underscores to avoid filename issues
    filename = f"{custom_name.replace(' ', '_')}.txt"
else:
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d_%H-%M-%S")
    filename = f"chat_{timestamp}.txt"

logfile = os.path.join("logs", filename)

def log_message(role, content):
    with open(logfile, "a") as f:
        f.write(f"[{datetime.datetime.now()}] {role}: {content}\n")

def chat():
    messages = []
    print(f"Starting new chat log: {logfile}")
    while True:
        user_input = input("You: ")
        if user_input.lower() in ["exit", "quit"]:
            print("Chat ended. Saved to", logfile)
            break

        # Save user input
        messages.append({"role": "user", "content": user_input})
        log_message("User", user_input)

        # Get response from Llama3
        response = client.chat(model="model_name_here", messages=messages)
        reply = response["message"]["content"]
        print("Llama3:", reply)

        # Save response
        messages.append({"role": "assistant", "content": reply})
        log_message("Llama3", reply)

if __name__ == "__main__":
    chat()

```

1. Now go back to terminal and change directory to VSCODE folder and run the python file. 
2. If you are able to name the file but receive errors after typing prompt ensure that the model is installed and properly named in script
3. Use Ollama list to find the model name then replace with what is within quotation marks: response = client.chat(model="Model_name_here", messages=messages)
4. Once ollama is running do the following for easier access 
5. Go to power shell and input _'notepad $PROFILE'_
6. Paste the following to create a function (REPLACE PATH)
   ```powershell
   function chat_logger {
   python "C:\Users\eliel\Downloads\Visual_S\FILENAMEHERE"
   }
   ```
