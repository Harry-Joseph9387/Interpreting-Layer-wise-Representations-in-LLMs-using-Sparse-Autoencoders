# 🧠 Interpreting Layer-wise Representations in LLMs using Sparse Autoencoders

## 🎯 Aim

- 	To identify functionality of each layer from its hidden representation.

---

## 🧩 Logic for determining Layer functionality 
- Each layer processes the input to highlight some features.
- 	For that we use sparse auto encoder that extracts features from hidden representation and assigns a label on the basis of most commonly occuring.
- 	Then we conclude highly consistent features as the layer’s functionalities.
- 	This is done for all tasks (pos-tags,ner,dep) thus getting highly consistent features from each tasks
- 	To determine the layer functionality across the tasks, we compute the mutual information between the hidden representation and labels to determine the most related labels 

---

## ⚙️ Working Principle

- 	Sparse Autoencoder performs dimensionality reduction transforming dense representations into minimal-overlapping, interpretable features.
- 	The encoder represents interpretable features by activating distinct sparse neurons that each respond to specific, human-understandable patterns in the input.
- 	How the encoder is trained to do this is by using a decoder to reconstruct the hidden representation(input) so that loss can be calculated to evaluate the encoder’s ability to correctly map right neurons to the given pattern of input.
- 	This is possible because of applying sparsity, here I have used topK, which zeros out active neurons other than the topK.
- 	What sparsity does is that it limits the no. of neurons available for the decoder to reconstruct.
- 	On backpropagating the error, only those limited neuron’s related weights, that contribute to the error, is updated.
- 	This forces the encoder to activate different neurons for different pattern of input.


---

## 🔍 Use Cases

- **Model interpretability** in research
- **Debugging** and optimizing deep transformer architectures
- Understanding **layer specialization** in LLMs
- Educational insight into **representation learning**

---
✅ Pros and ❌ Cons
✅ Pros
Improved Interpretability through Disentanglement

-Encourages neurons to specialize in specific, meaningful patterns (e.g., syntax, punctuation), making them easier to interpret.

❌ Cons

Limited Effectiveness in Deeper Layers

-Struggles to interpret deep, abstract representations where polysemanticity and entanglement are high.

### Base Paper Reference 

**"Sparse Autoencoders Find Highly Interpretable Features in Language Models" — Hoagy Cunningham et al. (2023)**

- This paper addresses *polysemanticity* in neural networks—where neurons respond to multiple unrelated features—by proposing sparse autoencoders to disentangle these features into more interpretable directions.
- The authors use *sparse dictionary learning* to identify directions in activation space that reconstruct model activations using a small set of highly interpretable, monosemantic features.
- Their method improves interpretability over traditional methods like PCA and ICA, validated using *autointerpretability scores* and *causal interventions* (like activation patching).
- Case studies demonstrate that individual learned features correspond to specific linguistic patterns (e.g., apostrophes or legal terms), enabling detailed tracing of model behaviour through internal circuits.

*Paper Link*: [arXiv:2309.08600v3](https://arxiv.org/abs/2309.08600)
