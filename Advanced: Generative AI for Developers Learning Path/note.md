## Advanced: Generative AI for Developers Learning 
## 02 Attention Mechanism
1. What is the advantage of using the attention mechanism over a traditional recurrent neural network (RNN) encoder-decoder?
```bash
The attention mechanism lets the decoder focus on specific parts of the input sequence, which can improve the accuracy of the translation.
```

2. What is the name of the machine learning architecture that can be used to translate text from one language to another?
```bash
Encoder-decoder
```

3. What is the name of the machine learning technique that allows a neural network to focus on specific parts of an input sequence?
```bash
Attention mechanism
```

4.How does an attention model differ from a traditional model?
```bash
Attention models pass a lot more information to the decoder.
```

5. What is the advantage of using the attention mechanism over a traditional sequence-to-sequence model?
```bash
The attention mechanism lets the model focus on specific parts of the input sequence.
```

6. What is the purpose of the attention weights?
```bash
To assign weights to different parts of the input sequence, with the most important parts receiving the highest weights.
```

7. What are the two main steps of the attention mechanism?
```bash
Calculating the attention weights and generating the context vector
```

## 03 Encoder-Decoder Architecture
1. What is the purpose of the decoder in an encoder-decoder architecture?
```bash
To generate the output sequence from the vector representation
To predict the next word in the output sequence
```

2. What are two ways to generate text from a trained encoder-decoder model at serving time?
```bash
Greedy search and beam search
```

3. What is the name of the machine learning architecture that takes a sequence of words as input and outputs a sequence of words?
```bash
Encoder-decoder
```

4. What is the purpose of the encoder in an encoder-decoder architecture?
```bash
To convert the input sequence into a vector representation
```

5. What is the difference between greedy search and beam search?
```bash
Greedy search always selects the word with the highest probability, whereas beam search considers multiple possible words and selects the one with the highest combined probability.
```

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

## 09 Responsible AI for Developers: Fairness & Bias

1. Which statement accurately describes a Google AI principle?
```bash

```

2. You have been asked to do a presentation to a stakeholder in your organization on the importance of responsible AI. As you are thinking through your key opening statement, what is the most appropriate statement you can make that describes the importance of having responsible AI?
```bash

```
3. As you think through the development of your AI product, your organization is looking to you to lead and guide the development team around responsible AI best practices. What is a key best practice the team should think through as they develop the AI product?
```bash

```

4. The data scientist team in your company is working to implement an AI model to assist processing credit card applications. During testing, you notice that the model has inconsistent performance among different sub-group of applicants. What responsible AI best practice should the team apply to the model?
```bash

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

1. A customer is working with a large dataset of healthcare records to develop a diagnostic AI model. They want to ensure privacy of sensitive data, by restricting the contribution of specific data on the model during training. Which privacy-focused technique would be best for the customer?
```bash

```


2. In machine learning, privacy measures often introduce trade-offs with other important factors. Which of the following does NOT represent a typical trade-off?
```bash

```


3. You've applied various de-identification techniques to a customer dataset containing sensitive information before using it to train an AI model. Which of the following concepts should you use to evaluate the suitability of your de-identification techniques?
```bash

```



















