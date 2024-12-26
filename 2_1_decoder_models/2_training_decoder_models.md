### Study Notes on Training Decoder Models

#### **Learning Objectives**

1. Explain the training process for decoder models.
2. Understand the application of causal attention masking in decoder model training.
3. Refresh concepts related to sequence models and explore new notations.

#### **Key Concepts**

**1. Notations in Language Modeling**

- **Omega (Ω̂_t):** Represents the token or word index at time \( t \), also used to denote token value when appropriate.
- Derived from the maximum output value of the decoder's final neural network layer.
- During prediction, it generates a word embedding vector, **\( x̂_t \)**, indicating the prediction.
- Hat notation signifies an estimate, although \( x̂_t \) is more of a hypothetical vector derived from decoder output.

**2. Prediction Process in Decoder Models**

- **Initial Step:** Start with the first word embedding \( x \) at \( t=0 \). The decoder generates a contextual embedding.
- **Contextual Embedding:**
  - Shaped through the neural network and used for subsequent encoding.
  - Predictions are reintroduced into the model to generate embeddings for subsequent tokens.
- **Cyclical Process:** Each contextual embedding (gray) is fed back into the model, forming a sequence of embeddings used to predict the next token.
- **Positional Encoding:** Added at every step to provide sequence information.

**3. Training Process for Decoder Models**

- **Training Dataset:**
  - Input tokens are paired with their targets, shifted one time step forward.
  - Start tokens and zero padding may be applied for uniform sequence lengths.
- **Operation During Training:**
  - The decoder processes the full sequence (e.g., indices 0-3) and uses a causal mask to ensure predictions depend only on prior elements.
  - Loss is calculated based on the predicted outputs and the actual token targets.

**Training Differences from Inference:**

- In training, actual word embeddings are used instead of approximations.
- Predictions are computed for all positions in the sequence, unlike inference which focuses on the final token.

**4. Teacher Forcing Technique**

- Instead of feeding the model's predictions back as input for subsequent steps, the actual previous token is used.
- Ensures that incorrect predictions do not disrupt the sequence alignment with actual data.
- Helps the model learn accurate input-output mappings to compute the loss.

**5. Causal Attention Masking**

- **Purpose:** Ensures that each token only attends to preceding tokens or itself, prohibiting influence from future tokens.
- **Implementation:**
  - Mask with negative infinity values in the upper triangle of the attention matrix is applied.
  - After masking, a softmax operation nullifies future tokens' impact on the attention scores.
- **Effect:**
  - Each token focuses only on current and prior tokens during training.
  - Essential for accurate intermediate token predictions in both training and inference.

**6. Sequence of Training Steps**

- Attention scores are computed for the full input sequence (e.g., \( x_0, x_1, \ldots, x_3 \)).
- Masking ensures that predictions for \( Ω_1 \), \( Ω_2 \), etc., only use appropriate past inputs (e.g., \( x_0, x_1 \)).
- Although the attention process appears sequential, it occurs in parallel in the decoder's attention mechanism.

**7. Limitations and Challenges**

- **Context Size:** Limited number of tokens the model can consider as input.
- **Loss Computation:** Derived by comparing the predicted tokens (\( Ω̂ \)) with actual tokens (\( Ω \)), and logits.

**8. Key Techniques and Applications**

- **Prediction Training Loop:**
  - Initial input (\( x_0 \)) generates \( Ω_1 \), which is used to produce the next token \( x̂_1 \). This process continues for the entire sequence.
- **Logarithmic Likelihood:** Used for combining loss across sequences during training.

#### **Summary**

1. The training process for decoder models uses actual embeddings instead of approximations and involves predicting the next token at every position.
2. Teacher forcing aligns predictions with actual tokens during training by using real prior tokens as input.
3. Causal attention masking is a critical technique to ensure that tokens attend only to prior inputs, enabling accurate sequence predictions.
4. The parallel nature of the attention mechanism accelerates computation despite the apparent sequential structure.
