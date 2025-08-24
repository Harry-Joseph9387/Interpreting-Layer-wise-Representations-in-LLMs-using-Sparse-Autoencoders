# 🧠 Interpreting Layer-wise Representations in LLMs using Sparse Autoencoders

## 🎯 Aim

- To identify the functionality of each transformer layer from its hidden representations by using **Sparse Autoencoders (SAEs)** and label-based interpretation.

---

## 🧩 Logic for Determining Layer Functionality

1. **Resolving Token–Label Ambiguity (Mutual Information Filtering)**  
   - Some tokens can appear with multiple labels (e.g., *bank* → *finance*, *river*).  
   - We group activation vectors by token and compute **mutual information (MI)** between activations and candidate labels.  
   - The label with the **highest MI score** is chosen, ensuring the most explainable label is retained for each token.

2. **Per Task Neuron Interpretation**  
   - For each neuron (feature index), strong activations are defined as those above the 90th percentile.  
   - Neurons with fewer than **5 strong activations** are ignored.  
   - The **dominant label** for a neuron is the most frequent label among its strong activations.  
   - **Consistency** = (# of activations for the dominant label) ÷ (total strong activations).  
   - Highly consistent neurons are treated as interpretable, revealing **task-specific layer functionality**.

3. **Across Task Layer Interpretation**  
   - Each neuron contributes a **dominant label per task**, based on per-task consistency.  
   - Across tasks, layers are summarized by the **most frequent dominant labels** across all tasks.  
   - This highlights whether layers encode **shared linguistic functions** (e.g., function words, syntax) or **task-specific roles**.

---

## ⚙️ Working Principle

- Sparse Autoencoder performs **dimensionality reduction**, transforming dense hidden states into minimal-overlapping, interpretable features.  
- The encoder activates sparse neurons, each tuned to specific linguistic patterns.  
- A decoder reconstructs the hidden representation, enforcing the encoder to use only the most relevant neurons.  
- Sparsity is enforced using **TopK**, which zeroes out all but the top-K activations, ensuring distinct neurons specialize in distinct patterns.  
- This leads to disentangled features, improving interpretability of the model’s internal representations.

---

## 🔧 Dataset Preparation & Feature Extraction

- Dataset: Universal Dependencies `.conllu` files (POS and dependency annotations).  
- Tokens are cleaned: remove short tokens, repeats, URLs, non-alphabetic characters, punctuation-only tokens, and hashtags.  
- POS tags are grouped into content categories (e.g., NOUN, VERB, ADJ) and a GRAMMAR category for function words.  
- Dependency relations are grouped into ARGUMENT, MODIFIER, FUNC, COORD, CLAUSE_LINK, etc.  
- Label balance is ensured by limiting max occurrences per label.  
- Hidden states from all transformer layers are extracted at the token level, excluding special tokens (`[CLS]`, `[SEP]`, padding).  
- Metadata (token, label, sentence index, token index) is aligned for interpretability and MI-based filtering.

---

## 🔍 SAE Layer-Wise Feature Interpretability Summary (DistilBERT)

- **6 layers analyzed** for POS and DEP tasks.  
- Extracted **top-10 interpretable neurons per layer** using SAE activations.

### POS Task Findings
- Early layers (0–1) were dominated by **ADV** (adverbs) and **PROPN** (proper nouns).  
- Mid layers (2–3) shifted toward stronger representation of **PROPN**, showing positional specialization.  
- Deeper layers (4–5) remained focused on **PROPN** with occasional **ADV** and **NOUN** signals.  
- **VERB** and **ADJ** were detected but not dominant.

### DEP Task Findings
- Across all 6 layers, **FUNC** (function words: case markers, auxiliaries) was consistently dominant.  
- Some layers also captured **CLAUSE_LINK**, **COORD**, and **ROOT** dependencies.  
- Deeper layers maintained strong focus on grammatical relations with minimal shift in dominance.

### Global Summary Across Tasks
- Layers 0–1 emphasized **ADV**, **FUNC**, and **CLAUSE_LINK** patterns.  
- Layers 2–5 increasingly emphasized **FUNC** and **PROPN** as dominant labels.  
- Suggests mid-to-deep SAE layers encode rich information about **function words** and **proper nouns**, key to structure and entity recognition.  
- Each SAE layer specializes in distinct linguistic patterns, with clearer specialization emerging in mid-to-deep layers (2–5).  

---

## 🔍 Use Cases

- **Model interpretability** in research  
- **Debugging** and optimizing deep transformer architectures  
- Understanding **layer specialization** in LLMs  
- Educational insight into **representation learning**  

---

## ✅ Pros and ❌ Cons

### ✅ Pros
1. **Improved Interpretability through Disentanglement**  
   - Encourages neurons to specialize in specific, meaningful patterns (e.g., syntax, punctuation), making them easier to interpret.

### ❌ Cons
1. **Limited Effectiveness in Deeper Layers**  
   - Struggles to interpret deep, abstract representations where polysemanticity and entanglement are high.

---

### 📄 Base Paper Reference 

**"Sparse Autoencoders Find Highly Interpretable Features in Language Models" — Hoagy Cunningham et al. (2023)**  

- This paper addresses *polysemanticity* in neural networks—where neurons respond to multiple unrelated features—by proposing sparse autoencoders to disentangle these features into more interpretable directions.  
- Uses *sparse dictionary learning* to identify directions in activation space that reconstruct model activations with highly interpretable, monosemantic features.  
- Improves interpretability over PCA/ICA, validated with *autointerpretability scores* and *causal interventions*.  
- Case studies show individual learned features correspond to linguistic patterns (e.g., apostrophes, legal terms), enabling tracing of model behaviour through internal circuits.  

📌 [arXiv:2309.08600v3](https://arxiv.org/abs/2309.08600)
