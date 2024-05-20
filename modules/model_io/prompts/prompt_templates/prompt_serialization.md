# Serialization

It is often preferable to store prompts not as Dart code but as files. This
can make it easy to share, store, and version prompts. This tutorial covers how
to do that in LangChain, walking through all the different types of prompts and
the different serialization options.

## PromptTemplate

This section covers examples for loading a `PromptTemplate`.

### Loading Template from a File

This shows an example of storing the template in a separate file and then
referencing it in the config.

`simple_template.txt`:
```txt
Tell me a {adjective} joke about {content}.
```

To load `simple_template.txt` as a `PromptTemplate`:

```dart
final prompt = await PromptTemplate.fromFile(templateFile);
print(prompt.format({'adjective': 'funny', 'content': 'chickens'}));
// -> 'Tell me a funny joke about chickens.'
```
