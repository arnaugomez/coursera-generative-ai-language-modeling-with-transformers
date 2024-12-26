1.
Question 1
In a transformer model’s self-attention mechanism, consider a token at position ‘t’ is ‘apple’ in a sentence ‘I love to eat apples every day.’ You’ve applied a self-attention mechanism to predict the token ‘apple’ representation based on the context provided in the sentence. Which of the following is the most influential factor for the token ‘apple’ prediction in the self-attention mechanism? 


Position of the token ‘apple’ in the sequence



The word ‘love’



The word ‘apple’



The presence of the word ‘eat’


1 point
2.
Question 2
In the following embedding, what is the dimensionality of the embedding for the word Transformers?




4



0.2



3



1 


1 point
3.
Question 3
What purpose does the following formula serve in the context of using the attention mechanism in language translation?




Applies attention mechanism to word embeddings



Provides the word vector for the translated word



Finds the index of the embedding that is more similar to H.



Retrieves the translated word from the translated vector


1 point
4.
Question 4
Which statement is true about the scaled dot-product attention mechanism with multiple heads?


It follows the setting batch_first = True for PyTorch implementations.



There is a constraint that the input dimension must be a prime number.



It is implemented using the nn.Attention module of PyTorch.



Each head can attend to distinct segments of the input sequence in parallel.


1 point
5.
Question 5
When using transformer-based models for text classification, creating the text pipeline is a key activity. Identify the missing step (step number 5) from the following list of steps for creating the text pipeline.

Steps for creating the text pipeline:

Create iterators and allocate a training set

Generate tokens and construct a vocabulary

Design a custom collate function

Apply padding

?


Create a data loader



Record cumulative losses and epoch accuracies



Apply the transformer encoder layers



Add positional encoding


1 point
