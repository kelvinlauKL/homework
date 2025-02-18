# Homework 4

## Prerequisites

You'll need to get API keys from OpenAI and Cohere. Once you do, open a Terminal and add the API keys as environment variables:

```
export OPENAI_API_KEY="<your key>"
export COHERE_API_KEY="<your key>"
```

You're also expected to have Python installed.

## Project Summary

This project retrieves the DOGE wikipedia page and applies several enhancement techniques:

### Retrieval

We'll do some pre-processing and post-processing on the retrieval step to achieve a more efficient retrieval. In the pre-processing step, we'll use **BM25** to score documents based on exact word matches, term frequency, and inverse document frequency. This helps with keyword matching.

The setup for this is as follows:

```
# Imports
import os
from langchain_openai import ChatOpenAI
from langchain_chroma import Chroma
from langchain_community.document_loaders import WikipediaLoader
from langchain_openai import OpenAIEmbeddings
from langchain_text_splitters import RecursiveCharacterTextSplitter

# Environment Setup
os.environ['USER_AGENT'] = 'doge_information'

# LLM 
llm = ChatOpenAI(model="gpt-4o-mini")

# Loading Wikipedia
loader = WikipediaLoader("Department_of_Government_Efficiency",)
docs = loader.load()

# Splitting Document into Chunks
text_splitter = RecursiveCharacterTextSplitter(
  chunk_size=1000,
  chunk_overlap=0
)
splits = text_splitter.split_documents(docs)

# Storing Chunks in Vector Database
database = Chroma.from_documents(
  documents=splits,
  embedding=OpenAIEmbeddings()
)
retriever = database.as_retriever()
```

For the post-processing step, we'll use **Cohere** which uses neural nets to re-rank documents based on semantic relevance. This helps with the retrieval process by helping it understand synonyms, intent, and meaning.

```
# Imports
pip install cohere
pip install langchain-cohere

import getpass
os.environ["COHERE_API_KEY"] = getpass.getpass("Cohere API Key:")

from langchain.retrievers.contextual_compression import ContextualCompressionRetriever
from langchain_cohere import CohereRerank
from langchain_community.llms import Cohere

llm = Cohere(


