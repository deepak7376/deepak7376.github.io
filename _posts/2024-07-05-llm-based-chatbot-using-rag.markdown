---
layout: post
comments: true
title: "LLM Based Chatbot using RAG"
date: 2024-07-05 00:04:58 +0530
categories: general
description: LLM based chatbot using RAG.
---

## Index
- Introduction
- Paradigms for Inserting Information
- RAG Stack
- End-to-End Application
- Conclusion

## Introduction
Large Language Models (LLMs) operate as powerful sequence-to-sequence models, trained on extensive datasets to understand and generate human-like text. However, their sheer size makes frequent fine-tuning challenging. What if we need information beyond the LLM’s knowledge cutoff date? To address this, we employ two techniques: Retrieval Augmentation and Fine-tuning.

## Paradigms for Inserting Information
1. **Retrieval Augmentation (RAG):** This involves fixing the LLM model and injecting context directly into the prompt.
2. **Fine-tuning:** Fine-tuning LLM weights with new information, but this method is comparatively complex.

In this discussion, we’ll focus on the first method due to its simplicity and efficiency.

## RAG Stack for Building QA System
The RAG architecture comprises two primary components:

### a. Data Ingestion (Indexing)
1. **Load:** Begin by loading your data using DocumentLoaders. This initial step is crucial for preparing the dataset for further processing.
2. **Split:** Break down large documents into smaller chunks using Text Splitters. This facilitates both data indexing and passing it into a model, ensuring compatibility with a model’s finite context window.
3. **Store:** Establish a system for storing and indexing splits. This is commonly achieved using a VectorStore and an Embeddings model, providing a searchable repository for future reference.

### b. Retrieval and Generation
1. **Retrieve:** When a user submits an input, relevant splits are retrieved from storage using a Retriever. This step is fundamental for pulling contextually significant information from the indexed dataset.
2. **Generate:** Utilize a ChatModel or LLM to produce an answer. This is accomplished by creating a prompt that includes the user’s question and the retrieved data. The seamless integration of retrieval and generation ensures that the system generates accurate and contextually relevant responses.

## End-to-End Application
Deploy the end-to-end application, which can be accessed by following [RAG Application](https://huggingface.co/spaces/Deepak7376/LLM-based-custom-pdf-chatbot).

## Conclusion
By adopting the RAG-based approach, we can build a robust Question-Answer System that efficiently handles information retrieval beyond the LLM’s original training data. This method empowers developers to create dynamic and up-to-date conversational AI systems.

## References:
- Building Production-Ready RAG Applications: Jerry Liu [https://www.youtube.com/watch?v=TRjq7t2Ms5I](https://www.youtube.com/watch?v=TRjq7t2Ms5I)
- [https://python.langchain.com/docs/use_cases/question_answering/](https://python.langchain.com/docs/use_cases/question_answering/)
