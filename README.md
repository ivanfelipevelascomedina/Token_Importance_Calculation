# **LLM Input Tokens Importance Visualization**

## **Overview**
This repository implements a method for calculating token importance in generative language models using the **ReAGent** approach. ReAGent is a model-agnostic feature attribution technique that computes token importance recursively, enabling robust insights without requiring access to model weights.

---

## **Files**
- **`Requirements.txt`**: Lists necessary libraries.
- **`Input_Tokens_Importance.ipynb`**: Main code file.

---

## **Features**
- Fetches contextual data (e.g., news or academic papers) to enrich video prompts.
- Generates videos scene-by-scene using **Luma AI**.
- Combines video segments and narrations into a single output.
- Handles errors with retry mechanisms.
- Session persistence ensures iterative processes retain prior results.
- Displays the results with a **Streamlit-based GUI**.

---

## **Troubleshooting**
### **Error: "Generation failed"**
- Ensure the prompt adheres to **Luma AI's input guidelines** and is not overly complex.  
- Check API quotas and retry if necessary.

### **Error: "No files to concatenate"**
- Verify that video generation steps completed successfully.  
- Retry or simplify the prompts.

### **"Dreaming" message in logs**
- Indicates the tool is waiting for the **Luma AI** generation to complete.  
- If this persists, check network stability or retry later.

### **Missing API keys**
- Ensure all required API keys are entered in the sidebar.

---

## **Acknowledgments**
- **Luma AI** for advanced video generation.
- **OpenAI** for contextual script creation.
- **Resemble AI** for voice narration.

