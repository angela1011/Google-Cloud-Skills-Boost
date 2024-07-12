## Build an application to send Chat Prompts using the Gemini model

### Working with Generative AI
### Chat responses without using stream:

Click File->New File to open a new file within the Code Editor.

Copy and paste the provided code snippet into your file.
```bash
import vertexai
from vertexai.generative_models import GenerativeModel, ChatSession

project_id = ""your-project-id""
location = ""REGION""

vertexai.init(project=project_id, location=location)
model = GenerativeModel("gemini-1.0-pro")
chat = model.start_chat()

def get_chat_response(chat: ChatSession, prompt: str) -> str:
    response = chat.send_message(prompt)
    return response.text

prompt = "Hello."
print(get_chat_response(chat, prompt))

prompt = "What are all the colors in a rainbow?"
print(get_chat_response(chat, prompt))

prompt = "Why does it appear when it rains?"
print(get_chat_response(chat, prompt))
```

Click File->Save, enter SendChatwithoutStream.py for the Name field and click Save.

Execute the Python file by clicking the triangle icon on the top-right corner of Code Editor or by running the below command inside the terminal within the Code Editor pane to view the output.

```bash
/usr/bin/python3 /home/student/SendChatwithoutStream.py
```

### Chat responses with using stream:
Click File->New File to open a new file within the Code Editor.
Copy and paste the provided code snippet into your file.

```bash
import vertexai
from vertexai.generative_models import GenerativeModel, ChatSession

project_id = ""your-project-id""
location = ""REGION""

vertexai.init(project=project_id, location=location)
model = GenerativeModel("gemini-1.0-pro")
chat = model.start_chat()

def get_chat_response(chat: ChatSession, prompt: str) -> str:
    text_response = []
    responses = chat.send_message(prompt, stream=True)
    for chunk in responses:
        text_response.append(chunk.text)
    return "".join(text_response)

prompt = "Hello."
print(get_chat_response(chat, prompt))

prompt = "What are all the colors in a rainbow?"
print(get_chat_response(chat, prompt))

prompt = "Why does it appear when it rains?"
print(get_chat_response(chat, prompt))
```

Click File->Save, enter SendChatwithStream.py for the Name field and click Save.

Execute the Python file by clicking the triangle icon on the top-right corner of Code Editor or by running the below command inside the terminal within the Code Editor pane to view the output.

```bash
/usr/bin/python3 /home/student/SendChatwithStream.py
```
Check my progress 

## Congratulation!