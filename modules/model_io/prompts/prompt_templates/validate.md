# Validate template

The default constructor of `PromptTemplate` will not validate the template 
string. If you want to validate you can call `validateTemplate()`. It will 
check whether the `inputVariables` match the variables defined in `template`. 

```dart
const template = 'I am learning langchain because {reason}.';

final promptTemplate = PromptTemplate(
  inputVariables: const {'reason', 'foo'},
  template: template,
  validateTemplate: false,
);
// -> No exception

final promptTemplate1 = PromptTemplate(
  inputVariables: const {'reason', 'foo'},
  template: template,
);
promptTemplate1.validateTemplate();
// -> 'Exception: Invalid template: 1 variables found, but 2 expected.}'


```

The factory constructors `fromTemplate()` and `fromExamples()` will validate the
template string by default (you don't need to explicitly call 
`validateTemplate()`). You can disable this behavior by setting 
`validateTemplate` to `false`.

```dart
const template = 'I am learning langchain because {reason}.';

final promptTemplate = PromptTemplate.fromTemplate(template);
// -> 'Exception: Invalid template: 1 variables found, but 2 expected.}'

final promptTemplate1 = PromptTemplate.fromTemplate(
  template,
  validateTemplate: false,
);
// -> No exception
```

_Note: the reason why the default constructor does not validate the template by
default is because that allows to define it as `const` constructor._ 