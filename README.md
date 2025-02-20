# Homework 4

## Prerequisites

you'll need to get API keys from OpenAI and Cohere. Once you do, open a Terminal and add the API keys as environment values:

```
export OPENAI_API_KEY="<your key>"
export COHERE_API_KEY="<your key>"
```

You’re also expected to have Python installed.

## Project Summary

This project demonstrates how to build a sophisticated Retrieval-Augmented Generation (RAG) pipeline using LangChain. The Jupyter Notebook walks you through the entire process, from retrieving a long Wikipedia article on the Department of Government Efficiency (DOGE) to generating concise, context-aware answers using multiple enhancement techniques.

## Key Components

### Retrieval
  •  Pre-processing:
The notebook loads and splits the DOGE Wikipedia page into manageable chunks. These chunks are then embedded using OpenAI embeddings and stored in a Chroma vector database.
  •  Ensemble Retrieval:
It combines a dense retriever (from the vector database) with a BM25 retriever for keyword-based matching using an EnsembleRetriever. This dual approach helps improve the quality of the initial document retrieval.
  •  Post-processing with Cohere:
After retrieving candidate documents, the pipeline uses Cohere’s re-ranking capabilities via a ContextualCompressionRetriever that employs the CohereRerank model. This step reorders and compresses the documents to prioritize the most semantically relevant content.

### Augmentation
  •  Vector Database Storage:
The split and embedded documents are stored in the Chroma vector database, which serves as the backbone for efficient retrieval.

### Generation
  •  Conversational QA Chain:
The final step integrates a history-aware conversational retrieval chain that uses the compressed (re-ranked) documents as context. This chain leverages OpenAI’s ChatGPT (or similar models) to generate clear, concise answers. It also maintains session history to handle follow-up questions effectively.
