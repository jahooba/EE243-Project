
# EE243 Final Project: Limitations and Improvements of Vision-Language Models

This repository contains the code, experiments, results, and project report for my EE243 final project on vision-language models. The project studies the limitations of CLIP and compares it with newer vision-language models such as SigLIP, PaliGemma, ViLT, and Video-Language Models.


## Google Colab Notebook

The full implementation and experiments are available in Google Colab: 

[Open Google Colab Notebook](https://colab.research.google.com/drive/1fFjooLLGr-9ZvYuZBAKkZ51MTEmqxJrK?authuser=1#scrollTo=bX0yH5R91mKE)

## Youtube Link:
[Youtube link](https://youtu.be/ux6jaH9LsOQ?si=Hu1cqfGzbD0tTr6D)

## Project Interpretation Report:

The detailed report on the results and interpretation can be found at-

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

1. Can CLIP understand complex object relationships such as “a dog chasing a cat” versus “a cat chasing a dog”?
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

## Experiment Summary

| Experiment | Model(s) | Main Purpose | Main Result |
|---|---|---|---|
| Object relationship reasoning | CLIP | Test whether CLIP understands subject-object relationships | CLIP recognized objects but struggled with relationships such as dog chasing cat vs cat chasing dog |
| Prompt sensitivity | CLIP | Test whether wording changes predictions | CLIP predictions changed for some prompt templates |
| Grad-CAM localization | CLIP | Check whether CLIP focuses on correct visual regions | CLIP did not always show precise visual grounding |
| MNIST zero-shot | CLIP | Test out-of-distribution generalization | CLIP performed poorly on handwritten digits |
| Spatiotemporal reasoning | CLIP | Test motion and before-after reasoning | CLIP struggled with temporal order and motion direction |
| Long video context | VideoChat / Video-LLM | Test whether video models remember short events | The model missed a briefly appearing blue square |
| Object relationship with SigLIP | SigLIP | Test whether SigLIP improves CLIP’s relational reasoning | SigLIP improved some results but still had reasoning limitations |
| Multiple-choice VQA | SigLIP | Test image-text ranking for VQA | SigLIP worked only when answers were provided as choices |
| Generative VQA | PaliGemma | Study open-ended VQA | PaliGemma is better suited for generated answers |
| Counting | SigLIP and ViLT | Test object counting ability | ViLT performed better than SigLIP on explicit counting |
| MNIST comparison | CLIP and SigLIP | Compare zero-shot digit recognition | SigLIP achieved around 78.6%, while CLIP achieved around 25.3% |



## Summary of Findings

The experiments show that CLIP is a strong vision-language alignment model, but it is not a complete visual reasoning system. CLIP performs well when the task only requires matching an image with a broad text description, but it struggles when the task requires deeper reasoning about relationships, spatial grounding, temporal order, counting, or out-of-distribution data.

| Experiment / Task | Model(s) | Summary of Finding |
|---|---|---|
| Object relationship reasoning | CLIP | CLIP recognized that the image contained a dog and a cat, but it struggled to distinguish relationships such as “a dog chasing a cat” versus “a cat chasing a dog.” This suggests that CLIP is sensitive to object words but weaker at subject-object reasoning. |
| Prompt sensitivity | CLIP | CLIP’s predictions changed when the prompt template changed. This shows that CLIP’s output depends not only on the image, but also on the exact wording of the text prompt. |
| Visual localization | CLIP + Grad-CAM | Grad-CAM showed that CLIP does not always focus on the correct visual region. A correct or high-confidence prediction does not always mean that the model is visually grounded in the right object. |
| Out-of-distribution recognition | CLIP on MNIST | CLIP performed poorly on zero-shot MNIST digit classification. This shows that CLIP does not automatically generalize well to visual domains that are very different from its pretraining data. |
| Temporal reasoning | CLIP | CLIP struggled with before-and-after image reasoning, such as identifying whether an object moved from left to right or right to left. This is because CLIP does not naturally model time, sequence, or causality. |
| Long video context | VideoChat / Video-Language Model | Video-language models improve over CLIP by adding temporal information, but they can still miss short-lived events in longer videos. In the project experiment, the model missed a blue square that appeared only briefly at the beginning of the video. |
| Improved image-text alignment | SigLIP | SigLIP improved over CLIP in some tasks because it uses a sigmoid loss instead of CLIP’s softmax contrastive loss. However, SigLIP still inherits some CLIP-like limitations in compositional and relational reasoning. |
| Multiple-choice VQA | SigLIP | SigLIP can be adapted for multiple-choice VQA by ranking answer prompts, but it cannot naturally generate open-ended answers. Its performance depends heavily on the candidate answer choices. |
| Generative VQA | PaliGemma | PaliGemma is more suitable for open-ended visual question answering because it combines a SigLIP vision encoder with a Gemma language decoder. Unlike CLIP or SigLIP, it can generate natural-language answers. |
| Counting | SigLIP and ViLT | SigLIP was uncertain on counting questions, while ViLT performed better on explicit VQA-style counting tasks. This suggests that counting requires stronger object-level grounding and VQA-specific training. |
| MNIST comparison | CLIP vs SigLIP | SigLIP performed much better than CLIP on zero-shot MNIST classification. In the project results, SigLIP achieved around 78.6% accuracy, while CLIP achieved around 25.3% in a comparable setting. |



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

Sayantika Nag, Joshua Pena

## Acknowledgment

This project was completed as part of EE243. The experiments were designed to analyze the strengths and weaknesses of vision-language models and to better understand the difference between image-text alignment and true visual reasoning.

```
```
