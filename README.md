# **LLM Input Tokens Importance Visualization**

## **Overview**
This repository implements a method for calculating token importance in generative language models using the **ReAGent** approach. ReAGent is a model-agnostic feature attribution technique that computes token importance recursively, enabling robust insights without requiring access to model weights.

---

## **Files**
- **`requirements.txt`**: Lists necessary libraries.
- **`Input_Tokens_Importance.ipynb`**: Main code file.
- **`iterations_data.json`**: Example data for a given input.

---

## **Features**
-**Token Importance Calculation**:
Implements a method for analyzing the contribution of individual tokens to the output of a language model. To do so it applies the Reagent Methodology.

-**Iterative Process**:
Tracks the evolution of token contributions over multiple iterations, thus allowing the user to identify patterns or stability in token importance.

-**Visualization**:
Provides a visualization of token inportance for the given input and of how token scores evolve across iterations to identify if the convergence has been properly reached.

---

## **ReAgent Methodology**
The **ReAGent methodology** computes the input importance distribution for each predicted token in a way that is:

1. **Model-agnostic**: It does not rely on an attention mechanism, making it applicable to a wide range of models.
2. **Black-box compatible**: It requires no access to model weights or architecture details, relying solely on forward passes without gradients.

Inspired by occlusion-based feature attribution (FA) methods, ReAGent assumes that replacing more important tokens in the input context $x_1, \dots, x_{t-1}$ results in larger reductions in the predictive likelihood of the target token $x_t$. The method iteratively replaces context tokens to compute their importance scores.

### Algorithm Overview

The process consists of the following steps:

1. **Initialization**:
   - Randomly initialize importance scores $S_{t+1} = \{s_1, \dots, s_{t}\}$ for all context tokens.

2. **Iterative Update**:
   - The algorithm updates the scores through the following steps:
     - **Step 3**: Randomly select a subset of tokens $R \subset x_1, \dots, x_{t}$ for replacement. Typically, $r = 30$ % of the sequence is replaced.
     - **Step 4**: Replace the selected tokens $R$ with predictions from a secondary language model (e.g., RoBERTa). This creates a new sequence $C(x+1) =$ $\hat{x}_1$, ..., $\hat{x}_t$.
     - **Steps 5 & 6**: Compute the change in predictive probability $\Delta p$ of the target token $x_t$, and update the importance scores $S_t$ accordingly:
       $$\Delta p_{t+1} = p_{t+1}^{(o)} - p_{t+1}^{(r)}$$
       where $p_t^{(o)}$ is the predictive probability of $x_t$ for the original sequence, and $p_t^{(r)}$ is the probability for the replaced sequence. Scores are updated using:
       $$S_{t+1}^{(l)} = \text{softmax}\left(S_{t}^{(l)} + \log\left(\frac{\Delta S_{t+1} + 1}{2}\right)\right)$$

3. **Stopping Condition**:
   - The process stops when the following condition is met: if the top 70% least important tokens are replaced, and the model's top-3 predictions include the target token $x_t$.

---

## **Acknowledgments**
- **Zhixue Zhao & Boxuan Shan, University of Sheffield** for the Reagent Methodology creation.
Zhao, Z., & Shan, B. (2024). ReAGent: A Model-agnostic Feature Attribution Method for Generative Language Models.

