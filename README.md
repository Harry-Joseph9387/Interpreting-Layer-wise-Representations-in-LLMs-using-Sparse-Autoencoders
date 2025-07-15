# 🧠 Interpreting Layer-wise Representations in LLMs using Sparse Autoencoders

## 🎯 Aim

This project aims to **identify the functionality of each layer** in a large language model (LLM) by analyzing its hidden representations. By doing so, we explore the *interpretability* of LLMs and understand *what each layer learns*.

---

## 🧩 Core Idea

Each layer in an LLM processes the input to emphasize certain features. This project uses **Sparse Autoencoders (SAEs)** to extract and interpret those features. The basic flow:

1. **Extract features** from each layer’s hidden representations using a sparse autoencoder.
2. **Assign labels** to each extracted feature based on the most common label it aligns with.
3. **Compute consistency** for the assigned labels.
4. **Accept a feature as part of a layer's functionality** only if its consistency exceeds a certain threshold.
5. **Repeat for all layers and tasks** to derive layer-wise functional mappings.

---

## ⚙️ Working Principle

- A **Sparse Autoencoder** reduces the dimensionality of dense LLM representations, transforming them into minimal-overlapping, interpretable features.
- The **encoder** maps input (hidden representation) to a sparse latent vector, while the **decoder** reconstructs the input from it.
- **Sparsity** is enforced using a **Top-K** mechanism that restricts the number of active neurons.
- This encourages the encoder to:
  - Use different neurons for different input patterns.
  - Update only the relevant weights during backpropagation.
- As a result, the encoder learns **distinct and interpretable neuron activations** that represent meaningful features from the LLM layer.

---

## 📌 Method Summary

- Train a separate sparse autoencoder for each LLM layer.
- Evaluate and select features based on **label consistency**.
- Use these features to interpret **what functionality a layer focuses on** (e.g., POS tagging, dependency parsing).
- Generalize across multiple tasks to find **prime features per layer**.

---

## 🔍 Use Cases

- **Model interpretability** in research
- **Debugging** and optimizing deep transformer architectures
- Understanding **layer specialization** in LLMs
- Educational insight into **representation learning**

---


## 🛠 Requirements

- Python 3.8+
- PyTorch
- NumPy
- scikit-learn
- Matplotlib

Install dependencies using:

```bash
pip install -r requirements.txt
