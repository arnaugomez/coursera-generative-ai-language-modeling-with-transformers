### Study Notes: From Attention to Transformers

#### Learning Objectives
After completing this lesson, you will be able to:
1. **Describe the functionality and implementation** of the scaled dot-product attention mechanism with multiple heads.
2. **Explain how the transformer architecture** enhances the efficiency of attention mechanisms.
3. **Implement a series of encoder layer instances** in PyTorch.

---

#### Scaled Dot-Product Attention with Multiple Heads
- The **scaled dot-product attention mechanism** operates within transformer models and involves:
  - **Matrix multiplications** using queries (Q), keys (K), and values (V).
  - A **scaling factor** to prevent large dot-product values.
  - **Optional masking** for specific task requirements.
  - Final multiplication with values (V) to generate the output.

- **Self-Attention**:
  - Queries (Q), keys (K), and values (V) are derived from the same input vector \( X \).
  - These are multiplied by respective **learnable parameter matrices**.

- **Cross-Attention**:
  - For tasks like language translation:
    - Keys and values are taken from a different input source (e.g., the source language) represented as \( Z \).

---

#### Multihead Attention
- **Multihead attention** performs several scaled dot-product attention processes in parallel:
  - The output is referred to as **heads**.
  - Each head focuses on **different parts of the input sequence**.
  - Inputs are embeddings, represented as vectors.

- Example Process:
  - Inputs (e.g., embeddings of size 4) are split into smaller vectors (e.g., two 2-dimensional vectors per input).
  - These smaller vectors are processed independently by attention mechanisms.
  - Outputs from individual heads are concatenated and passed through a **final linear layer**.

- **Hyperparameter**:
  - The **number of heads** is a hyperparameter.
  - Constraint: The input dimension must be divisible by the number of heads.

---

#### Multihead Attention in PyTorch
- Use the `nn.MultiheadAttention` module in PyTorch:
  - Specify parameters like **embedding dimension** and **number of heads**.
  - Ensure the embedding dimension is divisible by the number of heads using a **modulus check**.

- Steps:
  1. Initialize a **multihead attention object** with specified parameters.
  2. Generate random **query, key, and value tensors** with a sequence length and batch size.
  3. Invoke the `forward` method to compute the multihead attention output.
  4. The output size matches the input size, maintaining dimensional consistency.

---

#### Transformer Architecture
- Transformers improve efficiency by **stacking additional layers** of attention and feed-forward networks.
- The architecture is composed of:
  1. **Encoders**
  2. **Decoders**

---

#### Transformer Encoder
- **Encoder Process**:
  - Input embeddings are combined with **positional encodings**.
  - **Multihead attention** handles the inputs without applying masking.
  - Residual connections and **add and norm** steps merge attention output with input embeddings, followed by normalization.
  - A **feed-forward network** applies a fully connected layer to each position, followed by an additional add and norm phase.
  
- **Stacking Layers**:
  - Multiple encoder layers can be stacked to model complex relationships.
  - Layer depth is a key **hyperparameter** to optimize model performance.

---

#### Transformer Decoder
- **Decoder Features**:
  - Multihead attention is **masked** to prevent access to future positions in the sequence.
  - Cross-attention layers enable the decoder to attend to encoder outputs.
  - Decoders primarily drive language generation.

- The output embeddings are passed through a **final linear layer**, mapping embeddings to word predictions.

---

#### Implementing Encoders in PyTorch
- **Steps to Create Encoder Layers**:
  1. Specify the **number of heads** and **embedding dimensions**.
  2. Determine the **number of layers** required.
  3. Create a **transformer encoder layer object** with these parameters.
  4. Add positional encodings to the input tensor.

- **Input Processing**:
  - The input tensor \( X \) is defined with dimensions for sequence length, batch size, and embedding dimension.
  - Tensor \( X \) is passed sequentially through all encoder layers.
  - Each encoder layer applies:
    - Multihead self-attention.
    - Feed-forward networks with **residual connections** and **layer normalization**.

- **Output**:
  - The final output embeddings retain the same size as the input.

---

#### Recap
1. **Scaled dot-product attention** involves:
   - Queries, keys, and values, combined with a scaling factor and optional masking.
2. **Multihead attention** enables parallel processing of attention with multiple heads.
3. Transformers **enhance efficiency** by stacking attention and feed-forward layers.
4. Encoders and decoders are key components:
   - Encoders focus on input embeddings.
   - Decoders include masked attention for sequence generation.
5. PyTorch provides modules like `nn.MultiheadAttention` to implement attention mechanisms.