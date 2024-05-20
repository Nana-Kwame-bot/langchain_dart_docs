# Vector stores

One of the most common ways to store and search over unstructured data is to
embed it and store the resulting embedding vectors, and then at query time to
embed the unstructured query and retrieve the embedding vectors that are 'most
similar' to the embedded query. A vector store takes care of storing embedded
data and performing vector search for you.

## Get started

This walkthrough showcases basic functionality related to VectorStores. A key
part of working with vector stores is creating the vector to put in them, which
is usually created via embeddings. Therefore, it is recommended that you
familiarize yourself with the text embedding model interfaces before diving into
this.

```dart
const filePath = './test/chains/assets/state_of_the_union.txt';
const loader = TextLoader(filePath);
final documents = await loader.load();
const textSplitter = CharacterTextSplitter(
  chunkSize: 800,
  chunkOverlap: 0,
);
final texts = textSplitter.splitDocuments(documents);
final textsWithSources = texts
    .mapIndexed(
      (final i, final d) => d.copyWith(
        metadata: {
          ...d.metadata,
          'source': '$i-pl',
        },
      ),
    )
    .toList(growable: false);
final embeddings = OpenAIEmbeddings(apiKey: openaiApiKey);
final docSearch = await MemoryVectorStore.fromDocuments(
  documents: textsWithSources,
  embeddings: embeddings,
);
```

### Similarity search

```dart
const query = 'What did the president say about Ketanji Brown Jackson';
final docs = await docSearch.similaritySearch(query: query);
```

### Similarity search by vector

```dart
final embeddingVector = await embeddings.embedQuery(query);
final docs = await docSearch.similaritySearchByVector(
    embedding: embeddingVector,
);
```
