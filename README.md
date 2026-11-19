
# Automobile Insurance Claim Intake Assistant: LLM Fine-Tuning

**Generative AI | Python | Hugging Face | Large Language Models | Model Evaluation**

## Project Overview

For my DSC 670 Generative AI coursework at Bellevue University, I developed an experimental automobile insurance claim intake assistant using a fine-tuned language model.

The goal was to determine whether full-parameter fine-tuning could improve a language model's ability to convert accident narratives into structured JSON records.

I compared the original model against the fine-tuned version to evaluate formatting reliability and information extraction accuracy.

## Project Objectives

- Select and prepare a language model for full-parameter fine-tuning.
- Create synthetic automobile accident narratives.
- Prepare structured training and validation datasets.
- Fine-tune the model to extract information into JSON.
- Evaluate the model using independent test cases.
- Compare performance against the original model.
- Investigate incorrect predictions and model limitations.

## Tools and Technologies

- Python
- Google Colab
- PyTorch
- Hugging Face Transformers
- Hugging Face Datasets
- Scikit-learn
- Pandas
- SmolLM2-135M-Instruct
- JSON
- GPU-based model training

## Model

**Base model:** `HuggingFaceTB/SmolLM2-135M-Instruct`

I selected this model because its relatively small size made full-parameter fine-tuning more practical within my available computing environment.

Unlike parameter-efficient approaches, this experiment updated all 134,515,008 model parameters.

## Dataset

I developed a synthetic dataset containing 75 automobile accident narratives.

Each example included a written accident description and corresponding structured information about the collision, reported vehicle damage, and drivability.

I used synthetic data to avoid exposing actual insurance claim information.

### Dataset Preparation

- Created an initial set of five examples.
- Expanded the dataset to 75 synthetic narratives.
- Checked for missing values and duplicate records.
- Prepared structured JSON target responses.
- Divided the data into 60 training examples and 15 validation examples.

The synthetic training data is generated directly in the notebook, so a separate dataset download is not required.

## Methodology

### Baseline Testing

I first tested the original SmolLM2 model on an automobile accident narrative to observe its behavior before fine-tuning.

The original model produced a conversational response rather than the structured JSON output needed for the intake task.

### Full-Parameter Fine-Tuning

I formatted the training examples as instruction-and-response conversations and tokenized them for model training.

I then trained the model for three epochs using Hugging Face Trainer.

All model parameters remained trainable during the experiment.

### Prompt Refinement

After training, my initial test did not produce the JSON response I expected.

I investigated the problem and adjusted the inference prompt to match the system instructions used during training.

This improved the model's ability to produce structured responses.

### Independent Evaluation

I evaluated the fine-tuned model using ten accident narratives and compared its predictions against expected values.

I measured valid JSON output and exact-match accuracy for collision type, damage, and vehicle drivability.

I then evaluated the original model using the same ten narratives.

## Results

| Evaluation Metric | Original Model | Fine-Tuned Model |
|---|---:|---:|
| Valid JSON responses | 0% | **100%** |
| Collision type accuracy | 0% | 30% |
| Damage accuracy | 0% | 10% |
| Drivability accuracy | 0% | 70% |

The fine-tuned model generated valid JSON for all ten evaluation cases.

However, its ability to extract accurate information remained inconsistent.

The original model's zero accuracy scores were influenced by its failure to produce valid JSON, rather than demonstrating that it understood none of the accident descriptions.

### Training Results

Training loss decreased from approximately 0.893 during the first epoch to 0.041 during the third epoch.

Despite this improvement, the independent evaluation demonstrated that low training loss did not guarantee accurate extraction on new examples.

## Error Analysis

Some predictions were incorrect because the model extracted the wrong information or introduced details that were not explicitly stated.

Other predictions were marked incorrect because the model used wording that differed from the expected response, even when the descriptions were similar.

This showed that exact-match evaluation can be too restrictive for some text extraction tasks.

A stronger evaluation would distinguish between formatting errors, factual extraction errors, and semantically equivalent responses.

## Challenges and Limitations

- The training dataset contained only 75 synthetic examples.
- The independent evaluation used ten test narratives.
- The model sometimes generated unsupported information.
- Valid JSON did not guarantee accurate extraction.
- Exact-match scoring did not recognize all equivalent descriptions.
- The experiment did not use real insurance claim data.
- The model has not been validated for production insurance workflows.
- Reproducing the full training process requires additional computing resources.

## What I Learned

This project helped me understand the difference between teaching a model to follow an output format and teaching it to extract information accurately.

Fine-tuning substantially improved JSON formatting, but the model still struggled with some factual details.

I also learned the importance of matching training and inference prompts, examining individual predictions, and evaluating model behavior beyond training loss.

## Future Improvements

- Expand and diversify the training dataset.
- Evaluate using a larger independent test set.
- Add semantic evaluation alongside exact-match scoring.
- Improve validation of extracted fields.
- Compare full fine-tuning with parameter-efficient methods.
- Add safeguards against unsupported information.
- Test additional models and prompt configurations.

## How to Run the Project

1. Download the Jupyter notebook from this repository.
2. Open it in Google Colab.
3. Enable a GPU runtime if one is available.
4. Run the notebook's installation and setup cells.
5. Execute the data preparation and fine-tuning cells in order.
6. Review the independent evaluation and baseline comparison.
7. Optionally save the fine-tuned model using the final notebook cells.

The notebook installs its primary Hugging Face dependencies and generates the synthetic training examples directly in Python.

The final cells save and download the trained model. They are optional if you only want to review the experiment.

**Note:** Re-running the notebook may produce different results because of differences in hardware, dependency versions, and model training behavior.

## Model Attribution

Base model: [HuggingFaceTB/SmolLM2-135M-Instruct](https://huggingface.co/HuggingFaceTB/SmolLM2-135M-Instruct)

The base model was developed by Hugging Face. This repository documents an educational fine-tuning experiment and does not claim ownership of the original model.

## Author

**Kevin Feracho**

Master of Science in Data Science  
Bellevue University

[GitHub Profile](https://github.com/kevinf529-cool) | [Data Science Portfolio](https://kevinf529-cool.github.io/)
