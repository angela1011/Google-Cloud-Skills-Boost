## Build an AI Image Generator app using Imagen on Vertex AI

### Working with Generative AI

Click File->New File to open a new file within the Code Editor.

Copy and paste the provided code snippet into your file.

```bash
import argparse

import vertexai
from vertexai.preview.vision_models import ImageGenerationModel

def generate_image(
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

generate_image(
    project_id='"project-id"',
    location='"REGION"',
    output_file='image.jpeg',
    prompt='Create an image of a cricket ground in the heart of Los Angeles',
    )
```

Click File->Save, choose GenerateImage.py for the Name field and click Save.

Execute the Python file by clicking the triangle icon on the Code Editor or by invoking the below command inside the terminal within the Code Editor pane. This will generate a image file with name image.jpeg.

```bash
/usr/bin/python3 /home/student/GenerateImage.py
```

Now to view the generated image, Click EXPLORER > image.jpeg

Check my progress 

## Congratulation!