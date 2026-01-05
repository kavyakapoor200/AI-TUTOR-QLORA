# AI Tutor – Fine-Tuning Mistral-7B using QLoRA (PEFT)

## Overview

This project demonstrates **memory-efficient fine-tuning of a large language model (Mistral-7B)** using **QLoRA**, a Parameter-Efficient Fine-Tuning (PEFT) technique.
The goal is to adapt a powerful base model for an **AI Tutor use case**, improving clarity and structure of educational explanations while operating under **limited GPU resources**.

---

## Why Full Fine-Tuning Is Not Practical

Traditional fine-tuning updates **all parameters** of a model.
For modern LLMs (7B+ parameters), this approach has major drawbacks:

* Extremely high **GPU memory requirements**
* Long training time and high compute cost
* Large checkpoint sizes (GBs per model)
* Risk of **catastrophic forgetting**
* Not feasible for individuals or small teams

Fully fine-tuning a 7B model typically requires **multiple high-end GPUs**, making it impractical in constrained environments.

---

## Why PEFT (Parameter-Efficient Fine-Tuning) Was Introduced

**PEFT** addresses the inefficiencies of full fine-tuning by:

* Freezing the base model
* Training only a **small subset of parameters**
* Preserving the model’s general knowledge
* Reducing compute and memory usage drastically

PEFT enables fine-tuning large models **without modifying all weights**, making LLM adaptation feasible on limited hardware.

---

## LoRA (Low-Rank Adaptation)

**LoRA** is a PEFT technique that:

* Injects **low-rank adapter layers** into attention modules
* Keeps original model weights frozen
* Trains only these lightweight adapters

### Advantages of LoRA:

* Adapter weights are very small (MBs instead of GBs)
* Base model remains unchanged
* Multiple task-specific adapters can be used with the same base model
* Easy sharing and reuse of fine-tuned adapters

Conceptually:

> Base model = general knowledge
> LoRA adapters = task-specific learning

---

## QLoRA (Quantized LoRA)

**QLoRA** extends LoRA by combining it with **4-bit quantization**.

In QLoRA:

* The base model is loaded in **4-bit precision**
* LoRA adapters are trained in higher precision
* Memory usage is drastically reduced with minimal performance loss

### Benefits of QLoRA:

* Enables fine-tuning **7B+ models on a single GPU**
* Makes large-model fine-tuning possible on platforms like Google Colab
* Retains strong model performance despite low-precision loading

This project uses **QLoRA** to fine-tune Mistral-7B efficiently.

---

## Project Objective

The objective of this project is to:

* Adapt **Mistral-7B** for an **AI Tutor** use case
* Improve clarity, structure, and educational tone of responses
* Perform fine-tuning under **limited GPU memory**
* Preserve base model knowledge while improving domain-specific behavior

---

## Training Summary

* **Base Model:** Mistral-7B
* **Fine-Tuning Method:** QLoRA (PEFT)
* **Quantization:** 4-bit (NF4)
* **Training Environment:** Google Colab GPU
* **Trainable Parameters:** LoRA adapters only
* **Frozen Parameters:** Entire base model

Only the **LoRA adapter weights** were trained and saved.

---

## Inference

Inference is performed by:

1. Loading the base Mistral-7B model
2. Loading the trained LoRA adapters
3. Generating responses using the combined model

A demonstration of inference is provided in **`Inference.ipynb`**.

---

## Results

Qualitative inference results comparing the **fine-tuned model** with the **base Mistral-7B** are provided in **`results.txt`**.

The fine-tuned model shows:

* Clearer explanations
* Better step-by-step structure
* Improved educational tone

---

## Repository Structure

```
AI-TUTOR-QLORA/
├── adapters/          # Trained LoRA adapter weights
├── Inference.ipynb    # Inference demonstration
├── results.txt        # Qualitative output comparison
├── requirements.txt  # Dependencies
├── README.md
└── LICENSE
```

---

## Notes on Deployment

This project focuses on **model-level fine-tuning and evaluation**.
Deployment as a standalone application was **not included** due to GPU infrastructure constraints.

---

## Key Takeaway

This project demonstrates how **QLoRA (PEFT)** enables practical fine-tuning of large language models like Mistral-7B on limited hardware, making LLM adaptation accessible without full fine-tuning.

---
