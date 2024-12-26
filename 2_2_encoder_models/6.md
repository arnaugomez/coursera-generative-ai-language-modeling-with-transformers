1.
Question 1
Why does BERT use an encoder-only architecture, that is, only the encoder part of the transformer model?


Because encoder models possess a unidirectional training method.



It allows BERT to process entire sequences of text simultaneously.



Because in encoder models, causal attention is visually represented by an ‘X’ for the masked attention and ‘O’s’ for the active attention units.



It allows BERT to be used for text-generation tasks.


1 point
2.
Question 2
In the next sentence prediction (NSP) task, which of the following determines whether the second sentence logically follows the first for a given pair of sentences?


Segment embeddings 



Positional encoding



CLS token’s contextual embedding



Separate token


1 point
3.
Question 3
How many classes are there in the output layer of the neural network for mask language modeling (MLM)?


There will be two classes.



The number of classes will be equal to the size of NSP.



The number of classes will be equal to the number of special tokens.



The number of classes will be equal to the size of the vocabulary.


1 point
4.
Question 4
Identify one of the most common pretraining objectives useful for training the BERT model in PyTorch.


You can initialize the model's parameters randomly.



You can use unsupervised learning with masked language modeling (MLM).



You can supervise the learning with labeled data.



You can use semi-supervised learning with limited labeled data.


1 point
