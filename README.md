# Meta-LLaMA-3.1-8B-LLM-model-Fine-tune

## Project Documentation
Project Summary: Real Estate Sales Lead Qualification using Fine-Tuned LLaMA Language Model
This project is an end-to-end AI solution designed to automatically qualify real estate sales leads by categorizing incoming messages into one of three classes: <lead>, <ignore>, or <spam>. Built for a real estate company, the system leverages Large Language Models (LLMs)—specifically, Meta’s LLaMA-3.1–8B model—fine-tuned with domain-specific conversational data for accurate lead triage.

How It Was Developed:
1. Data Preparation:
    * Raw conversation data was stored in JSONL format and loaded into pandas DataFrames.
    * Preprocessing included transforming multi-turn dialogues into the LLaMA fine-tuning prompt structure using <s>[INST]<<SYS>> system instructions <</SYS>> user input [/INST] assistant reply </s> format.
    * Data was split into training and validation sets and uploaded to the Hugging Face Hub for scalable access and tracking.
2. Model Fine-Tuning:
    * The Meta-LLaMA-3.1–8B base model was loaded with 4-bit quantization using BitsAndBytesConfig, significantly reducing memory usage while preserving performance.
    * Fine-tuning was performed using Parameter-Efficient Fine-Tuning (PEFT) with LoRA (Low-Rank Adaptation), modifying only selected transformer modules (q_proj, k_proj, etc.) to minimize computational cost.
    * Training was managed via the TRL library's SFTTrainer, with hyperparameters such as 3 epochs, batch size of 4, learning rate of 1e-4, cosine learning rate scheduling, and gradient accumulation.
    * Weights & Biases (W&B) was used for experiment tracking, logging, and monitoring performance metrics.
3. Model Deployment & Prediction:
    * The fine-tuned model was pushed to the Hugging Face Hub as a private model for easy access and sharing.
    * A custom inference function was defined to process new sales messages using the trained model. It formats inputs, runs inference, and returns classifications (lead, ignore, or spam) with high consistency.
    * Example inputs such as "I am looking to buy a flat in Bangalore" return <lead>, while unrelated queries like "my bike got stolen" return <ignore> or <spam>, showing the model’s contextual accuracy.

Impact and Usefulness:
This AI-driven system significantly streamlines sales pipeline management for real estate businesses by:
* Automatically filtering high-quality leads, reducing manual triage time.
* Eliminating spam and irrelevant inquiries, improving team efficiency.
* Maintaining focus on genuine buyer intent, especially related to real estate market.

By combining state-of-the-art LLMs, LoRA fine-tuning, quantization, and cloud deployment, this solution provides a scalable, cost-effective, and production-ready lead qualification engine tailored for the real estate domain.
