Question 1
    Why does the decoder use a cross-attention layer for translation?

To maintain the words’ order

To complete the decoder’s operation

To attend to the encoder’s hidden representations

To convert a token into a D-dimensional embedding vector

1 point 2.
Question 2
Which of the following functions is designed to construct masks for the source and target sequences?

“generate_square_subsequent_mask”

“Masking(token)”

“src_padding_mask”

“create_mask”

1 point 3.
Question 3
What is the following code used for?

```python
def generate_square_subsequent_mask(sz,device=DEVICE):
    mask = (torch.triu(torch.ones((sz, sz),
    device=device)) == 1).transpose(0, 1)
    mask = mask.float().masked_fill(mask == 0, float('-inf')).masked_fill(mask == 1, float(0.0))
    return mask
```

To generate a causal mask

To initiate the token embeddings and positional encodings

To create a mask

To construct the memory tensor

1 point
