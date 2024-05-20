# Split by character

This is the simplest method. This splits based on characters (by default `\n\n`) and measure chunk 
length by number of characters.

1. How the text is split: by single character.
2. How the chunk size is measured: by number of characters.

If you have a list of documents, you can split them like this:
```dart
const filePath = 'state_of_the_union.txt';
const loader = TextLoader(filePath);
final documents = await loader.load();
const textSplitter = CharacterTextSplitter(
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
