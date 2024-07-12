## Build a Multi-Modal GenAI Application: Challenge Lab

### Task 1:

Click `File` -> `New File` to open a new file within the Code Editor.

Copy and paste the provided code snippet into your file.

```bash
import argparse

import vertexai
from vertexai.preview.vision_models import ImageGenerationModel

def generate_bouquet_image(
    project_id: str, location: str, output_file: str, prompt: str
) -> vertexai.preview.vision_models.ImageGenerationResponse:
    """Generate an image using a text prompt.
    Args:
      project_id: Google Cloud project ID, used to initialize Vertex AI.
      location: Google Cloud region, used to initialize Vertex AI.
      output_file: Local path to the output image file.
      prompt: The text prompt describing what you want to see."""

    vertexai.init(project=project_id, location=location)

    model = ImageGenerationModel.from_pretrained("imagegeneration@002")

    images = model.generate_images(
        prompt=prompt,
        # Optional parameters
        number_of_images=1,
        seed=1,
        add_watermark=False,
    )

    images[0].save(location=output_file)

    return images

generate_bouquet_image(
    project_id='qwiklabs-gcp-04-999d9d9c06fc',
    location='europe-west1',
    output_file='image.jpeg',
    prompt='Create an image containing a bouquet of 2 sunflowers and 3 roses',
    )
```

Click `File` -> `Save`, choose `GenerateImage.py` for the Name field and click `Save`.

Execute the Python file by clicking the triangle icon on the Code Editor or by invoking the below command inside the terminal within the Code Editor pane to view the output.

```bash
/usr/bin/python3 /home/student/GenerateImage.py
```

Check my progress 

### Task 2:

Click `File` -> `New File` to open a new file within the Code Editor.

Copy and paste the provided code snippet into your file.

```bash
import vertexai
from vertexai.generative_models import GenerativeModel, Part


def analyze_bouquet_image(project_id: str, location: str) -> str:
    # Initialize Vertex AI
    vertexai.init(project=project_id, location=location)
    # Load the model
    multimodal_model = GenerativeModel("gemini-pro-vision")
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

project_id = "qwiklabs-gcp-04-999d9d9c06fc"
location = "europe-west1"

#  --------   Call the Function  --------

response = analyze_bouquet_image(project_id, location)
print(response)
```

Click `File` -> `Save`, choose `genai.py` for the Name field and click `Save`.

Execute the Python file by clicking the triangle icon on the Code Editor or by invoking the below command inside the terminal within the Code Editor pane to view the output.

```bash
/usr/bin/python3 /home/student/genai.py
```

Check my progress 

## Congratulation!