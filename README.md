
# EE243 Final Project: Limitations and Improvements of Vision-Language Models

This repository contains the code, experiments, results, and project report for my EE243 final project on vision-language models. The project studies the limitations of CLIP and compares it with newer vision-language models such as SigLIP, PaliGemma, ViLT, and Video-Language Models.


## Google Colab Notebook

The full implementation and experiments are available in Google Colab: 

[Open Google Colab Notebook](https://colab.research.google.com/drive/1fFjooLLGr-9ZvYuZBAKkZ51MTEmqxJrK?authuser=1#scrollTo=bX0yH5R91mKE)

## Youtube Link:
[Youtube link](https://youtu.be/ux6jaH9LsOQ?si=Hu1cqfGzbD0tTr6D)

## Project Interpretation Report:
[Project Report](https://github.com/jahooba/EE243-Project/blob/8a95c1d8743c927c24733b5abaa5af740f171efc/InterpretationReport.pdf)

## Project Website 

The GitHub Pages website for this project is available here:

[Project Website](https://jahooba.github.io/EE243-Project/)



## Project Overview

Vision-language models are designed to connect visual information with natural language. CLIP is one of the most widely used models for this task because it learns a shared embedding space between images and text. This allows CLIP to perform zero-shot image classification by comparing an image with different text prompts.

However, image-text alignment is not the same as complete visual understanding. A model may recognize that an image contains a dog and a cat, but still fail to understand which animal is chasing the other, how many objects are present, where objects are located, or what happened earlier in a video.

This project investigates these limitations through a series of experiments.

## Main Research Questions

This project focuses on the following questions:

1. Can CLIP understand object relationships such as “a dog chasing a cat” versus “a cat chasing a dog”?
2. How sensitive is CLIP to different prompt templates?
3. Does CLIP focus on the correct image regions when making predictions?
4. How well does CLIP generalize to out-of-distribution datasets such as MNIST?
5. Can CLIP understand temporal or causal changes in an image sequence?
6. Can video-language models remember short events in longer videos?
7. Do newer models such as SigLIP, PaliGemma, and ViLT improve on CLIP’s limitations?
8. Which models are better suited for visual question answering and counting?

## Models Used

The project studies and compares the following models:

| Model | Description |
|---|---|
| CLIP | A contrastive image-text model used for zero-shot classification and image-text matching. |
| SigLIP | A CLIP-like model that uses a sigmoid loss instead of the standard softmax contrastive loss. |
| PaliGemma | A generative vision-language model that combines a SigLIP vision encoder with a Gemma language decoder. |
| ViLT | A Vision-and-Language Transformer designed for vision-language tasks such as VQA. |
| Video-Language Model | A model used to test temporal reasoning and long video context understanding. |

## Experiments

### 1. Object Relationship Failure in CLIP

This experiment tests whether CLIP can distinguish between prompts such as:

- `a dog chasing a cat`
- `a cat chasing a dog`
- `a dog next to a cat`
- `a cat next to a dog`

The results show that CLIP can identify the objects in the image, but it often struggles with the relationship between them. This suggests that CLIP may rely heavily on object words such as “dog” and “cat” instead of fully understanding subject-object structure.

### 2. Prompt Sensitivity

This experiment tests whether changing the prompt wording affects CLIP’s output. Different templates were used, such as:

- `Question: {} Answer: {}`
- `Q: {} A: {}`
- `The answer to '{}' is '{}'`
- `This image shows '{}'`

The results show that CLIP can be sensitive to prompt phrasing. In some examples, the prediction changed even though the image and answer choices stayed the same.

### 3. Localization with Grad-CAM

Grad-CAM was used to examine whether CLIP focuses on the correct visual regions when making predictions. This experiment helps determine whether the model is actually looking at the object or region described by the text prompt.

The results suggest that CLIP’s visual grounding is not always precise. A model can produce a plausible label while focusing on incomplete or incorrect image regions.

### 4. Zero-Shot MNIST Classification

CLIP was tested on MNIST handwritten digits using zero-shot prompts. MNIST is very different from the natural image-text data used to train CLIP.

The results show that CLIP performs poorly on this out-of-distribution task. This demonstrates that CLIP’s zero-shot ability depends strongly on the pretraining distribution.

### 5. Temporal Reasoning

This experiment tested whether CLIP can understand a before-and-after image sequence, such as a blue circle moving from left to right.

CLIP struggles with this task because it is not designed to model temporal order. It processes the image globally and does not naturally understand sequence, motion, or causality.

### 6. Video-Language Model Long-Context Failure

A video-language model was tested on a video where a blue square appeared briefly at the beginning and was later replaced by a red square.

The model incorrectly stated that there was no blue square. This shows that even video-language models can miss short-lived events when the majority of frames show something else.

### 7. SigLIP Comparison

SigLIP was tested as an improvement over CLIP. SigLIP performed better than CLIP on some tasks, especially MNIST zero-shot classification.

However, SigLIP still struggled with fine-grained relationship reasoning. This shows that improving the image-text training objective does not fully solve compositional reasoning.

### 8. PaliGemma and ViLT for VQA

PaliGemma and ViLT were studied as models more suitable for visual question answering.

PaliGemma is not the same as ViLT. PaliGemma combines a SigLIP vision encoder with a Gemma language decoder, which allows it to generate text answers. ViLT is a Vision-and-Language Transformer often used for classification-style VQA tasks.

These models are better suited for VQA than CLIP because they are designed to process both images and questions more directly.

### 9. Counting Experiment

The counting experiment tested questions such as:

- How many dogs are in the image?
- How many cats are in the image?
- How many animals are in the image?

CLIP and SigLIP showed uncertainty in counting tasks, while ViLT performed better on explicit visual question answering. This suggests that counting requires stronger object-level grounding than simple image-text similarity.

## Summary of Findings

| Task | Main Finding |
|---|---|
| Object relationship reasoning | CLIP recognizes objects but struggles with subject-object relationships. |
| Prompt sensitivity | CLIP predictions can change depending on wording. |
| Localization | CLIP does not always focus on the correct visual regions. |
| MNIST zero-shot classification | CLIP performs poorly on out-of-distribution handwritten digits. |
| Temporal reasoning | CLIP struggles with sequence and motion direction. |
| Long video context | Video-language models can miss short events. |
| SigLIP comparison | SigLIP improves some tasks but still has reasoning limitations. |
| VQA and counting | ViLT and PaliGemma-style models are better suited for VQA than CLIP. |

## Main Conclusion

The main conclusion of this project is that vision-language alignment is not the same as visual understanding.

CLIP is useful for broad image-text matching and zero-shot classification, but it has important limitations. It often recognizes objects correctly, but struggles when the task requires:

- Fine-grained object relationships
- Prompt robustness
- Spatial grounding
- Out-of-distribution recognition
- Temporal reasoning
- Long-context memory
- Counting
- Visual question answering

Newer models such as SigLIP, PaliGemma, and ViLT improve some of these weaknesses, but they do not completely solve visual reasoning. Future vision-language models need stronger object-level grounding, better compositional reasoning, improved temporal memory, and more robust prompt handling.



## How to Run

1. Open the Google Colab notebook.
2. Run the setup cells to install required libraries.
3. Run each experiment section one by one.
4. Update the GitHub Pages website with the final figures and results.

## Tools and Libraries

This project uses:

* Python
* PyTorch
* Hugging Face Transformers
* CLIP
* SigLIP
* PaliGemma
* ViLT
* Matplotlib
* PIL
* Google Colab

## Author

Joshua Pena, Sayantika Nag

## Acknowledgment

This project was completed as part of EE243. The experiments were designed to analyze the strengths and weaknesses of vision-language models and to better understand the difference between image-text alignment and true visual reasoning.

```
```
