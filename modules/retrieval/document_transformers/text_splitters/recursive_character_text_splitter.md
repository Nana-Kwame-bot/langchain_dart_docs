# Recursively split by character

This text splitter is the recommended one for generic text. It is parameterized by a list of 
characters. It tries to split on them in order until the chunks are small enough. The default list 
is `["\n\n", "\n", " ", ""]`. This has the effect of trying to keep all paragraphs (and then 
sentences, and then words) together as long as possible, as those would generically seem to be the 
strongest semantically related pieces of text.

1. How the text is split: by list of characters.
2. How the chunk size is measured: by number of characters.

If you have a list of documents, you can split them like this:
```dart
const filePath = 'state_of_the_union.txt';
const loader = TextLoader(filePath);
final documents = await loader.load();
const textSplitter = RecursiveCharacterTextSplitter(
  chunkSize: 1000,
  chunkOverlap: 200,
);
final docs = textSplitter.splitDocuments(documents);
```

If you have a text instead, you can split it like this:
```dart
const text = 'This is a long piece of text...';
final texts = textSplitter.splitText(text);
```

Here's an example of passing metadata along with the documents, notice that it is split along with 
the documents.

```dart
const text1 = 'This is a long piece of text...';
const text2 = 'This is a long piece of text...';
final metadatas = [
  {'document': 1},
  {'document': 2},
];
final docs = textSplitter.createDocuments(
  [text1, text2],
  metadatas: metadatas,
);
```
