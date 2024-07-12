## Build an AI Image Recognition app using Gemini on Vertex AI

### Working with Vertex AI Python SDK

Click File->New File to open a new file within the Code Editor.

Copy and paste the provided code snippet into your file.
```bash
import vertexai
from vertexai.generative_models import GenerativeModel, Part


def generate_text(project_id: str, location: str) -> str:
    # Initialize Vertex AI
    vertexai.init(project=project_id, location=location)
    # Load the model
    multimodal_model = GenerativeModel("gemini-1.0-pro-vision")
    # Query the model
    response = multimodal_model.generate_content(
        [
            # Add an example image
            Part.from_uri(
                "gs://generativeai-downloads/images/scones.jpg", mime_type="image/jpeg"
            ),
            # Add an example query
            "what is shown in this image?",
        ]
    )

    return response.text

# --------  Important: Variable declaration  --------

project_id = "qwiklabs-gcp-01-e6b151777875"
location = "europe-west1"

#  --------   Call the Function  --------

response = generate_text(project_id, location)
print(response)
```

Click File->Save, choose genai.py for the Name field and click Save.

Execute the Python file by clicking the triangle icon on the Code Editor or by invoking the below command inside the terminal within the Code Editor pane to view the output.

```bash
/usr/bin/python3 /home/student/genai.py
```

Check my progress 

## Congratulation!