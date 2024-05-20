# Retrieval

Many LLM applications require user-specific data that is not part of the model's
training set. LangChain gives you the building blocks to load, transform, store
and query your data via:

- [Document loaders](/modules/retrieval/document_loaders/document_loaders.md):
  load documents from many different sources.
- [Document transformers](/modules/retrieval/document_transformers/document_transformers.md):
  split documents, drop redundant documents, and more.
- [Text embedding models](/modules/retrieval/text_embedding/text_embedding.md):
  take unstructured text and turn it into a list of floating point numbers.
- [Vector stores](/modules/retrieval/vector_stores/vector_stores.md):
  Store and search over embedded data.
- [Retrievers](/modules/retrieval/retrievers/retrievers.md): Query your
  data.

![data connection diagram](img/retrieval.jpg)
*Image
source: [LangChain docs](https://python.langchain.com/docs/modules/retrieval/)*

