---
url: https://react.dev/reference/react-dom/unmountComponentAtNode
title: unmountComponentAtNode – React
source_domain: react.dev
---

# unmountComponentAtNode – React

[API Reference](https://react.dev/reference/react)

[APIs](https://react.dev/reference/react-dom)

# unmountComponentAtNode

### Deprecated

This API will be removed in a future major version of React.

In React 18, `unmountComponentAtNode` was replaced by [`root.unmount()`](https://react.dev/reference/react-dom/client/createRoot#root-unmount).

`unmountComponentAtNode` removes a mounted React component from the DOM.

```
unmountComponentAtNode(domNode)
```

* [Reference](https://react.dev/reference/react-dom/unmountComponentAtNode#reference) 
  + [`unmountComponentAtNode(domNode)`](https://react.dev/reference/react-dom/unmountComponentAtNode#unmountcomponentatnode)
* [Usage](https://react.dev/reference/react-dom/unmountComponentAtNode#usage) 
  + [Removing a React app from a DOM element](https://react.dev/reference/react-dom/unmountComponentAtNode#removing-a-react-app-from-a-dom-element)

---

## Reference

### `unmountComponentAtNode(domNode)`

Call `unmountComponentAtNode` to remove a mounted React component from the DOM and clean up its event handlers and state.

```
import { unmountComponentAtNode } from 'react-dom';

const domNode = document.getElementById('root');

render(<App />, domNode);

unmountComponentAtNode(domNode);
```

[See more examples below.](https://react.dev/reference/react-dom/unmountComponentAtNode#usage)

#### Parameters

* `domNode`: A [DOM element.](https://developer.mozilla.org/en-US/docs/Web/API/Element) React will remove a mounted React component from this element.

#### Returns

`unmountComponentAtNode` returns `true` if a component was unmounted and `false` otherwise.

---

## Usage

Call `unmountComponentAtNode` to remove a mounted React component from a browser DOM node and clean up its event handlers and state.

```
import { render, unmountComponentAtNode } from 'react-dom';

import App from './App.js';

const rootNode = document.getElementById('root');

render(<App />, rootNode);

// ...

unmountComponentAtNode(rootNode);
```

### Removing a React app from a DOM element

Occasionally, you may want to “sprinkle” React on an existing page, or a page that is not fully written in React. In those cases, you may need to “stop” the React app, by removing all of the UI, state, and listeners from the DOM node it was rendered to.

In this example, clicking “Render React App” will render a React app. Click “Unmount React App” to destroy it:

[Fork](https://codesandbox.io/api/v1/sandboxes/define?undefined&environment=create-react-app "Open in CodeSandbox")

```
import './styles.css';
import { render, unmountComponentAtNode } from 'react-dom';
import App from './App.js';

const domNode = document.getElementById('root');

document.getElementById('render').addEventListener('click', () => {
  render(<App />, domNode);
});

document.getElementById('unmount').addEventListener('click', () => {
  unmountComponentAtNode(domNode);
});
```

[Previousrender](https://react.dev/reference/react-dom/render)[NextClient APIs](https://react.dev/reference/react-dom/client)