# Study Notes: Pretraining BERT Models with PyTorch

## Learning Objectives
- **Describe how to create data loaders in PyTorch** for BERT-specific training tasks.
- **Explain the steps to create a BERT model** using PyTorch.
- **Train the BERT model** with PyTorch.

---

## Step-by-Step Process to Pretrain a BERT Model

### 1. **Creating Custom Dataset for PyTorch**
   - Define a custom dataset class, **`BERTCSVDataset`**, to load data from a CSV file into a PyTorch dataset.
   - **`__getitem__` Method**:
     - Retrieves an individual item from the dataset using an index.
     - Accesses the corresponding row from the DataFrame and converts JSON-formatted strings back to tensors.
     - Includes:
       - BERT input
       - BERT label
       - Segment label
       - Is-next indicator
   - **Collate Function (`collate_batch`)**:
     - Handles batching and padding sequences for a PyTorch data loader.

### 2. **Creating Data Loaders**
   - Define the batch size and specify file paths for train and test datasets.
   - Create instances of the **`BERTCSVDataset`** class for the train and test datasets using the file paths.
   - Use PyTorch’s **`DataLoader`** class to create data loaders for both datasets.

---

### 3. **Defining the BERT Model**
   - **BERT Embedding Class**:
     - Implements embedding operations and positional encodings.
     - Includes **segment embeddings**, which are unique to BERT.

   - **BERT Model Class**:
     - Subclass of **`torch.nn.Module`**.
     - **`__init__` Method**:
       - Initializes the BERT model with:
         - Vocabulary size
         - Model dimension (`d_model`)
         - Number of layers (`n_layers`)
         - Number of attention heads
         - Dropout rate
       - Combines token embeddings and segment embeddings using the BERT embedding class.
       - Uses transformer encoder layers to encode input embeddings.
     - **Linear Layers**:
       - For **Next Sentence Prediction (NSP)**:
         - Predicts whether two consecutive sentences are related.
       - For **Masked Language Modeling (MLM)**:
         - Predicts masked tokens in the input sequence.
     - **Forward Method**:
       - Takes `bert_inputs` (input tokens) and `segment_labels` as inputs.
       - Returns predictions for NSP and MLM.

   - Example Parameters for a Mini BERT Model:
     - Embedding dimension: **10**
     - Vocabulary size: Determined by the length of the vocabulary.
     - Transformer layers: **2**
     - Attention heads: **2**
     - Dropout rate: **0.1**

---

### 4. **Training the BERT Model**
   - Define a loss function (**Cross-Entropy Loss**) to calculate the difference between predicted and actual values.
   - Define an optimizer (**Adam**) to update model parameters.
   - **Training Loop**:
     - Iterate through training data batches.
     - Perform forward pass, calculate loss, and update parameters using backpropagation and gradient clipping.
     - Print average training loss and evaluate performance on the test set after each epoch.
     - Optionally save the model after each epoch.

---

### 5. **Evaluating the BERT Model**
   - Define an **`evaluate`** function to assess model performance:
     - Disable dropout and training-specific behaviors using `model.eval()`.
     - Perform evaluation with gradients turned off using `torch.no_grad()` to save memory and computation.
     - Calculate losses for NSP and MLM tasks and compute averages across batches.
     - Print and return average losses.

---

### 6. **Prediction with Pretrained BERT**
#### a. **Next Sentence Prediction (NSP)**
   - Define a **`predict_nsp`** function to check whether a second sentence follows the first:
     - Input: Two sentences, BERT model, and tokenizer.
     - Steps:
       1. Tokenize input sentences using `tokenizer.encode_plus()`.
       2. Convert tokenized inputs into tensors and move to the appropriate device.
       3. Pass token and segment tensors to the BERT model.
       4. Use softmax on logits to obtain probabilities.
       5. Take the argmax to predict whether the second sentence follows the first.
     - Example output: "The second sentence follows the first."

#### b. **Masked Language Modeling (MLM)**
   - Define a **`predict_mlm`** function to predict masked tokens in a sentence:
     - Input: A sentence, BERT model, and tokenizer.
     - Steps:
       1. Tokenize the sentence into token IDs (including special tokens).
       2. Create dummy segment labels filled with zeros.
       3. Pass the token tensor and segment labels to the BERT model.
       4. Extract logits for MLM predictions.
       5. Identify the position of the mask token and use the logits to predict its value (argmax).
       6. Replace the mask token in the original sentence with the predicted token.

---

## Summary
- **Creating Data Loaders**:
  - Use a custom dataset class and collate function to create data loaders for train and test datasets.
- **BERT Model Design**:
  - Include embedding operations, positional encodings, transformer encoder layers, and linear layers for NSP and MLM.
- **Training and Evaluation**:
  - Train using Cross-Entropy Loss and the Adam optimizer.
  - Evaluate performance using an evaluation function to compute losses for NSP and MLM.
- **Predictions**:
  - Use pretrained BERT to perform Next Sentence Prediction and Masked Language Modeling.