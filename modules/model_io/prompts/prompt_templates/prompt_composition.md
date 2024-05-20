# Composition

This tutorial goes over how to compose multiple prompts together. This can be
useful when you want to reuse parts of prompts. This can be done with a
PipelinePrompt. A PipelinePrompt consists of two main parts:

- Final prompt: This is the final prompt that is returned.
- Pipeline prompts: This is a list of tuples, consisting of a string name and a
  prompt template. Each prompt template will be formatted and then passed to
  future prompt templates as a variable with the same name.

```dart
const fullTemplate = '''
{introduction}

{example}

{start}
''';

final fullPrompt = PromptTemplate.fromTemplate(fullTemplate);

const introductionTemplate = 'You are impersonating {person}.';
final introductionPrompt = PromptTemplate.fromTemplate(introductionTemplate);

const exampleTemplate = '''
Here's an example of an interaction: 

Q: {example_q}
A: {example_a}''';
final examplePrompt = PromptTemplate.fromTemplate(exampleTemplate);

const startTemplate = '''
Now, do this for real!

Q: {input}
A:''';
final startPrompt = PromptTemplate.fromTemplate(startTemplate);

final inputPrompts = [
  ('introduction', introductionPrompt),
  ('example', examplePrompt),
  ('start', startPrompt)
];
final pipelinePrompt = PipelinePromptTemplate(
  finalPrompt: fullPrompt,
  pipelinePrompts: inputPrompts,
);

print(pipelinePrompt.inputVariables);
// -> {person, example_q, example_a, input}

final formatted = pipelinePrompt.format({
  'person': 'Elon Musk',
  'example_q': "What's your favorite car?",
  'example_a': 'Telsa',
  'input': "What's your favorite social media site?",
});
print(formatted);
// '''You are impersonating Elon Musk.
// 
// Here's an example of an interaction: 
// 
// Q: What's your favorite car?
// A: Telsa
// 
// Now, do this for real!
// 
// Q: What's your favorite social media site?
// A:'''
```
