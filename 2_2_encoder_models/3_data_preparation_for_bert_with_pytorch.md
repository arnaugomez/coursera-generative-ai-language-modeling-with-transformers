### Study Notes: Data Preparation for BERT with PyTorch

#### **Overview**

- This lesson covers **data preparation for BERT** using PyTorch.
- By the end, you will be able to:
  - Preprocess data using **tokenization** and **masking**.
  - Create **training-ready inputs** for BERT’s tasks, such as **Masked Language Modeling (MLM)** and **Next Sentence Prediction (NSP)**.

#### **Key Concepts and Steps**

1. **Initial Steps in Data Preparation**

   - **Tokenization**: Break text into smaller units (tokens).
   - **Vocabulary Construction**: Build a vocabulary of all unique tokens.
   - Use the **standard PyTorch pipeline** for these tasks.

2. **Tokenization**

   - Initialize the tokenizer using the `get_tokenizer` function.
   - Example: Tokenizing text with a **basic English model**.
   - **Important Note**: Actual BERT uses **WordPiece tokenization**.

3. **Special Symbols and Indices**
   - Define the following **special symbols**:
     - **PAD**: Padding token.
     - **CLS**: Marks the start of a sequence.
     - **SEP**: Separates sequences.
     - **MASK**: Used for Masked Language Modeling (MLM).
     - **UNK**: Represents unknown tokens.
   - Assign **indices** to these symbols (e.g., `PAD_IDX`, `CLS_IDX`).

#### **Masked Language Modeling (MLM)**

1. **Masking Function**

   - Decides whether to mask a token:
     - If not masked, the function returns the original token with a **pad label**.
     - If masked, it randomly selects an operation with a **50% probability**:
       - Replace token with **[MASK]**.
       - Keep the token unchanged.
       - Replace with a **random token** from the vocabulary.
   - Returns the **modified token** and its **label**.

2. **Prepare for MLM Function**

   - Prepares tokenized text for BERT’s MLM training:
     - Takes a list of tokens as input.
     - Initializes lists for processed sentences, labels, and raw tokens.
     - Applies BERT’s **MLM masking strategy**.
   - Checks for valid sentences (more than 2 tokens) and stores them with their labels.

3. **MLM Sample Output**
   - Example:
     - If the token "the" is masked, BERT input is `[MASK]` and its label is "the".
     - Tokens unchanged have labels as **PAD**.
     - Tokens replaced are mapped to their corresponding **labels**.

#### **Next Sentence Prediction (NSP)**

1. **NSP Process**

   - Prepares data for BERT’s **Next Sentence Prediction** task:
     - Input: List of tokenized sentences and masked labels.
   - Verifies input consistency (e.g., equal lengths of sentences and labels).

2. **NSP Sentence Pair Creation**

   - Randomly creates:
     - **Next Sentence Scenario**: Select two consecutive sentences and assign label **1**.
     - **Not Next Sentence Scenario**: Select two random sentences and assign label **0**.
   - Appends **CLS** and **SEP** tokens to the input.

3. **NSP Final Outputs**

   - Returns prepared lists:
     - **Sentence pairs**.
     - **Masked labels**.
     - **Binary labels** for "is next" task.

4. **NSP Sample Output**
   - Example:
     - In a correct sentence pair, the **is next** label is **1**.
     - For a non-consecutive pair, the label is **0**.

#### **Final Input Preparation for BERT**

1. **Prepare BERT Final Inputs Function**

   - Prepares final input lists for BERT training:
     - Inputs include BERT inputs, labels, and "is next" labels.
     - Converts inputs into tensors for PyTorch.

2. **Padding and Consistency**

   - Applies **zero-padding** to ensure consistent input lengths.
   - Creates **segment labels**:
     - Sentence 1 tokens = label **1**.
     - Sentence 2 tokens = label **2**.
     - Padding = label **0**.

3. **Additional Transformations**

   - Uses lambda functions to:
     - Flatten nested lists.
     - Map tokens to their vocabulary indices.

4. **Final Tensor Conversion**

   - Converts inputs to PyTorch tensors if the `to_tensor` flag is set.
   - If not, appends flattened padded inputs and labels directly to the output.

5. **Sample Output**
   - Tokens like `CLS`, `SEP`, and `PAD` are mapped to vocab indices (e.g., `CLS` → `1`, `PAD` → `0`).
   - Mask labels are padded and mapped.
   - Outputs include token indices, segment labels, and "is next" labels.

#### **Example of Data Preparation Outputs**

1. **Steps for Data Preparation**

   - Corpus is processed into pairs of sentences.
   - Sentences are:
     - Tokenized.
     - Numericalized (converted to indices).
     - Appended with **CLS** and **SEP** tokens.
     - Zero-padded for consistent length.

2. **Output Details**
   - **BERT Labels**: Indicates which tokens are masked.
   - **Segment Labels**: Identifies sentence membership for each token.
   - **Is Next Labels**: Indicates whether the second sentence follows the first.

#### **Recap**

- Key steps in data preparation for BERT:
  1. **Tokenization** using `get_tokenizer`.
  2. Define **special symbols** and assign indices.
  3. Use the **masking function** for MLM.
  4. Process **NSP inputs** to create sentence pairs and labels.
  5. Prepare final inputs with **padding** and **segment labels**.
  6. Convert data into tensors for training.

This process ensures the input data is formatted and ready for effective BERT training tasks like MLM and NSP.
