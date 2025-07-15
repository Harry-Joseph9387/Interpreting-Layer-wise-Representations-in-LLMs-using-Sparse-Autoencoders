# 🧠 Interpreting Layer-wise Representations in LLMs using Sparse Autoencoders

## 🎯 Aim

- 	To identify functionality of each layer from its hidden representation.

---

## 🧩 Logic for determining Layer functionality 
- Each layer processes the input to highlight some features.
- 	For that we use sparse auto encoder that extracts each feature and assigns a label on the basis of most common label.
- 	Then we conclude features as the layer’s functionalities if the computed consistency of those features label passes the threshold.
- 	This is done for all tasks thus getting prime features in relation with layers,
- 	To determine the layer functionality we compute the mutual information

---

## ⚙️ Working Principle

- 	Sparse Autoencoder performs dimensionality reduction transforming dense representations into minimal-overlapping, interpretable features.
- 	How the encoder is trained to do this is by using a decoder to reconstruct the hidden representation(input) so that loss can be calculated to evaluate the encoder’s ability to correctly map right neurons to the given pattern of input.
- 	This is possible because of applying sparsity, here I have used topK.
- 	What this does is that it limits the no. of neurons available for the decoder to reconstruct.
- 	On backpropagating the error, only that limited neuron’s related weights that contribute to the error is updated.
- 	This forces the encoder to activate different neurons for different pattern of input.


---

## 🔍 Use Cases

- **Model interpretability** in research
- **Debugging** and optimizing deep transformer architectures
- Understanding **layer specialization** in LLMs
- Educational insight into **representation learning**

---

