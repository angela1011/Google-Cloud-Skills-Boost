## Advanced: Generative AI for Developers Learning 
## 04 Transformer Models and BERT Model

1. BERT is a transformer model that was developed by Google in 2018. What is BERT used for?
```bash
It is used to solve many natural language processing tasks, such as question answering, text classification, and natural language inference.
```

2. What are the three different embeddings that are generated from an input sentence in a Transformer model?
```bash
Token, segment, and position embeddings
```

3. What does fine-tuning a BERT model mean?
```bash
Training the model and updating the pre-trained weights on a specific task by using labeled data
```

4. What are the encoder and decoder components of a transformer model?
```bash
The encoder ingests an input sequence and produces a sequence of hidden states. The decoder takes in the hidden states from the encoder and produces an output sequence.
```

5. What are the two sublayers of each encoder in a Transformer model?
```bash
Self-attention and feedforward
```

6. What is the name of the language modeling technique that is used in Bidirectional Encoder Representations from Transformers (BERT)?
```bash
Transformer
```

7. What is the attention mechanism?
```bash
A way of determining the importance of each word in a sentence for the translation of another sentence
```

8. What is a transformer model?
```bash
A deep learning model that uses self-attention to learn relationships between different parts of a sequence.
```

9. What kind of transformer model is BERT?
```bash
Encoder-only model
```

## 05 Create Image Captioning Models

1. What is the goal of the image captioning task?
```bash
To generate text captions for images
```

2. What is the name of the model that is used to generate text captions for images?
```bash
Encoder-decoder model
```

3. What is the purpose of the attention mechanism in an encoder-decoder model?
```bash
To allow the decoder to focus on specific parts of the image when generating text captions
```

4. What is the purpose of the decoder in an encoder-decoder model?
```bash
To generate output data from the information extracted by the encoder
```

5. What is the name of the dataset the video uses to train the encoder-decoder model?
```bash
COCO dataset
```

6. What is the purpose of the encoder in an encoder-decoder model?
```bash
To extract information from the image.
```

## 06 Introduction to Vertex AI Studio

1. What is a prompt?
```bash
A prompt is the natural language request or instruction to guide a model to generate a desired output.
```

2. What is Vertex AI Studio?
```bash
A tool that lets you quickly test and customize generative AI models.
```

3. Which of the following is a type of prompt that allows a generative AI model to perform a task with only a few examples?
```bash
Few-shot prompt
```

4. What does Gemini multimodal do with Vertex AI Studio?
```bash
Gemini multimodal processes text, image, and video data, and generates text as output.
```

5. Which of the following is the best way to generate more creative or unexpected content by adjusting the model parameters in Vertex AI Studio?
```bash
Setting the temperature to a high value.
```

## 07 Vector Search and Embeddings 

1. Which of the following is correct to compare between vector search and traditional keyword search?
```bash
Vector search addresses semantic similarity and is good at solving ambiguous queries, whereas traditional keyword search is good at solving precise queries.
```

2. What is the process of encoding text data into vectors called?
```bash
Generating text embeddings.
```

3. What is the general process to build a search application by using Vertex AI Vector Search?
```bash
Encode data to embeddings, build an index, and search results.
```

4. What are the two main techniques used by ScaNN (Scalable Approximate Nearest Neighbor) to improve search performance in vector search?
```bash
Space pruning and data quantization
```

5. What are the two main technical challenges that need to be addressed in order to implement vector search effectively?
```bash
Encoding and indexing
```

6. What is the main purpose of using distance metrics like dot product distance in vector search?
```bash
Measure the distance between vectors in terms of semantic similarity.
```

7. What is the main benefit of using vector search in RAG (retrieval-augmented generation) to address LLM (Large Language Models) hallucination?
```bash
It allows the LLM to access real-time information for fact-checking.
```

## 09 Responsible AI for Developers: Fairness & Bias
# Introduction to Responsible AI
1. Which statement accurately describes a Google AI principle?
```bash
Be accountable to people.
```

2. You have been asked to do a presentation to a stakeholder in your organization on the importance of responsible AI. As you are thinking through your key opening statement, what is the most appropriate statement you can make that describes the importance of having responsible AI?
```bash
Responsible AI is important for our organization because it reduces overall harm that our products may inflict on underrepresented groups.
```
3. As you think through the development of your AI product, your organization is looking to you to lead and guide the development team around responsible AI best practices. What is a key best practice the team should think through as they develop the AI product?
```bash
When possible, the team should hold the capability to access raw data to investigate issues or unintended behaviors.
```

4. The data scientist team in your company is working to implement an AI model to assist processing credit card applications. During testing, you notice that the model has inconsistent performance among different sub-group of applicants. What responsible AI best practice should the team apply to the model?
```bash
Ensure the recommendation data the product is pulling from is fairly representative of the entire dataset.
```
# AI Fairness & Bias
1. As a data scientist, you are tasked with identifying bias in training data in an effective way. Which of the tools below can be used to identify bias in data?
```bash
TensorFlow Data Validation, What-if Tool.
```

2. 

You have been asked to do a presentation in your organization on the importance of AI fairness and bias. As you are thinking through your key opening statement, what is the most appropriate statement you can make that explains why AI fairness is difficult?
```bash
Fairness is difficult because there are pre-existing biases, a variety of scenarios, no standard definition of fairness, and incompatibility of fairness metrics.
```

3. A researcher did an anonymous survey with students in a mixed-gender middle school to learn the health and diet patterns of middle school students in the entire country. What type of bias could it introduce?
```bash
Selection bias
```

## 10 Responsible AI for Developers: Interpretability & Transparency

1. Your manager is a strong advocate for responsible AI development. During a project review, they emphasize the importance of transparency and documentation around the dataset you're using and the resulting AI model. They want to know what steps you're taking to ensure this. Which of the following tools or techniques are you using to provide a clear understanding of your dataset and model?
```bash
Data card, Model card
```

2. You're working on an image classification model for identifying different types of clouds. During testing, you notice some strange results. The model seems to be focusing on irrelevant areas of the images (like background objects) instead of the actual cloud features. To understand why your model is behaving this way, which of the following tools or techniques would be the most helpful?
```bash
XRAI (eXplainable Region-based Artificial Intelligence)
```

3. As an AI engineering team manager, you're giving a presentation to explain why interpretability and transparency in AI development is important for engineers. Which of the following statements would be best to include in your slides?
```bash
Understand model behaviors
```

## 11 Responsible AI for Developers: Privacy & Safety
# Module 1: Quiz
1. A customer is working with a large dataset of healthcare records to develop a diagnostic AI model. They want to ensure privacy of sensitive data, by restricting the contribution of specific data on the model during training. Which privacy-focused technique would be best for the customer?
```bash
DP-SGD (Differentially Private - Stochastic Gradient Descent)
```

2. In machine learning, privacy measures often introduce trade-offs with other important factors. Which of the following does NOT represent a typical trade-off?
```bash

Privacy and Transparency
```

3. You've applied various de-identification techniques to a customer dataset containing sensitive information before using it to train an AI model. Which of the following concepts should you use to evaluate the suitability of your de-identification techniques?
```bash
Reversibility and referential integrity.
```

# Module 2: Quiz
1. Your manager asked you to lead a project to research the key considerations in AI safety and develop a failure mode catalog to assist evaluate safety in Generative AI products. Which of the following should not be included as a failure mode?
```bash
Citation
```

2. You want to embed the concept of safety into a pre-trained LLM by fine-tuning it. You have a dataset of prompts and pairs of possible answers, along with labels created by human safety evaluators indicating their preference for one answer over the other. Which technique is the most suitable for fine-tuning the LLM in this scenario?
```bash
Reinforcement Learning from Human Feedback (RLHF)
```

3. You're pitching an AI-powered customer support solution to a potential client. Their company handles highly sensitive user information, and they have reservations about potential risks associated with AI systems. To address their concerns and win their trust, which key message about AI safety would be most effective to emphasize?
```bash
"Adherence to AI safety principles helps us build reliable systems that minimize unexpected errors, safeguarding your customer data."
```

