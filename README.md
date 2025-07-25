
<img width="1200" height="480" alt="Deberta_Kaggle" src="https://github.com/user-attachments/assets/58560767-6cb5-49f8-9f58-23c79256c100" />

# deberta-v3-small-kaggle-preference

This project is an ongoing trial & error for the LLM Preference Prediction Kaggle competition, where the goal is to predict which of two large language model responses a human would prefer, given a prompt. This is framed as a 3-way classification problem: choose between model_a, model_b, or tie.
My first attemot is using a fine-tuned deberta-v3-small model using Hugging Face Transformers and PyTorch. 
The model was trained for 4 epochs and achieved a peak validation accuracy of 43.38% 
(*clearly* needs more training & tweaking), outperforming random and naive baselines.

# UPDATE (notebook 2):
Used a DeBERTaV3 model using the **Shared Weight strategy**, typically used in multiple-choice QA and it allows the model to jointly process both responses with shared context, capturing comparative nuances effectively.The model was trained for 7 epochs and achieved a peak validation accuracy of 48.13% 


<img width="964" height="546" alt="Screenshot 2025-07-24 at 9 40 26 PM" src="https://github.com/user-attachments/assets/8a65ddbb-c9e0-44a3-a46d-705419527539" />


This architecture was chosen and iteratively refined to capture the nuanced relative preference between two semantically rich LLM responses.


# Challenges i'm currently facing:
While DeBERTa-v3-small performed well relative to its size, capturing subtle nuances in human preference remains a significant challenge (this is borderline irritating). 
The prompt-response pairs in this competition often involve fine-grained differences in tone, reasoning, factual correctness, or stylistic fluency.
Some specific limitations include:
- Semantic Subtlety: Phrases can differ only slightly in structure but drastically in clarity or helpfulness. Small models can often miss these distinctions without explicit training on human preference signals.
- Contextual Ambiguity: Certain prompts are underspecified, requiring implicit reasoning or real-world knowledge.
- Tie Detection: Identifying when both responses are equally acceptable ("tie" class) poses issues. The model tends to favor one over the other, even when both are equally valid.
- Lack of Reinforcement Feedback: Unlike models fine-tuned with Reinforcement Learning from Human Feedback (RLHF), this classifier doesn't receive gradient signals based on ranked preferences, it only categorical labels, limiting its sensitivity to preference gradients.
These challenges highlight the inherent subjectivity and complexity of modeling human preferences, especially with compact models.
