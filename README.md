##Task 6.1
I use fasttext to resprent words as embedding, the source sentence is tokenized and convert into vector  then i produce bidirectional LSTM with attention  I use BLEU which compare generating translation

## Task 6.2
                    IMAGE CAPTIONING PIPELINE

Images
  │
  ▼
Pre-trained ResNet-50
  │
  ▼
2048-D Image Feature Vector
  │
  ▼
Feature Caching
  │
  │  Avoid repeated feature extraction
  ▼
Cached Image Features
  │
  ├──────────────────────┐
  │                      │
  ▼                      ▼
Captions              Image Features
  │                      │
  ▼                      │
Tokenization              │
  │                      │
  ▼                      │
Word IDs                  │
  │                      │
  ▼                      │
Custom PyTorch Dataset ◄──┘
  │
  ▼
Word Embedding
  │
  ▼
LSTM
  │
  ▼
Linear Layer
  │
  ▼
Next Word Prediction
  │
  ▼
Cross Entropy Loss
  │
  ├── Ignore <pad> tokens
  │
  ▼
Model Training
  │
  ▼
Trained Model
  │
  ▼
New Image
  │
  ▼
ResNet-50 Feature
  │
  ▼
LSTM Generation
  │
  ▼
Word → Word → Word → ...
  │
  ▼
<end>
  │
  ▼
Generated Caption



Logic

The pipeline first uses ResNet-50 to extract a 2048-D feature vector from each image and caches these features to avoid repeated extraction. Captions are tokenized and converted into word IDs. A custom PyTorch Dataset loads the cached image features and captions. During training, the LSTM uses the image features and previous words to predict the next word through a Linear Layer, while <pad> tokens are ignored in the loss. Finally, the trained model generates captions word by word until <end>.
