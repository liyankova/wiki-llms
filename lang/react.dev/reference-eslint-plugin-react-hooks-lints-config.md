---
url: https://react.dev/reference/eslint-plugin-react-hooks/lints/config
title: config – React
source_domain: react.dev
---

# config – React

[API Reference](https://react.dev/reference/react)

[Lints](https://react.dev/reference/eslint-plugin-react-hooks)

# config

Validates the compiler [configuration options](https://react.dev/reference/react-compiler/configuration).

## Rule Details

React Compiler accepts various [configuration options](https://react.dev/reference/react-compiler/configuration) to control its behavior. This rule validates that your configuration uses correct option names and value types, preventing silent failures from typos or incorrect settings.

### Invalid

Examples of incorrect code for this rule:

```
// ❌ Unknown option name

module.exports = {

plugins: [

['babel-plugin-react-compiler', {

compileMode: 'all' // Typo: should be compilationMode

}]

]

};

// ❌ Invalid option value

module.exports = {

plugins: [

['babel-plugin-react-compiler', {

compilationMode: 'everything' // Invalid: use 'all' or 'infer'

}]

]

};
```

### Valid

Examples of correct code for this rule:

```
// ✅ Valid compiler configuration

module.exports = {

plugins: [

['babel-plugin-react-compiler', {

compilationMode: 'infer',

panicThreshold: 'critical_errors'

}]

]

};
```

## Troubleshooting

### Configuration not working as expected

Your compiler configuration might have typos or incorrect values:

```
// ❌ Wrong: Common configuration mistakes

module.exports = {

plugins: [

['babel-plugin-react-compiler', {

// Typo in option name

compilationMod: 'all',

// Wrong value type

panicThreshold: true,

// Unknown option

optimizationLevel: 'max'

}]

]

};
```

Check the [configuration documentation](https://react.dev/reference/react-compiler/configuration) for valid options:

```
// ✅ Better: Valid configuration

module.exports = {

plugins: [

['babel-plugin-react-compiler', {

compilationMode: 'all', // or 'infer'

panicThreshold: 'none', // or 'critical_errors', 'all_errors'

// Only use documented options

}]

]

};
```

[Previouscomponent-hook-factories](https://react.dev/reference/eslint-plugin-react-hooks/lints/component-hook-factories)[Nexterror-boundaries](https://react.dev/reference/eslint-plugin-react-hooks/lints/error-boundaries)