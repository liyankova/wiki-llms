---
url: https://react.dev/reference/react/addTransitionType
title: addTransitionType – React
source_domain: react.dev
---

# addTransitionType – React

[API Reference](https://react.dev/reference/react)

[APIs](https://react.dev/reference/react/apis)

# addTransitionType

### Canary

**The `addTransitionType` API is currently only available in React’s Canary and Experimental channels.**

[Learn more about React’s release channels here.](https://react.dev/community/versioning-policy#all-release-channels)

`addTransitionType` lets you specify the cause of a transition.

```
startTransition(() => {

addTransitionType('my-transition-type');

setState(newState);

});
```

* [Reference](https://react.dev/reference/react/addTransitionType#reference) 
  + [`addTransitionType`](https://react.dev/reference/react/addTransitionType#addtransitiontype)
* [Usage](https://react.dev/reference/react/addTransitionType#usage) 
  + [Adding the cause of a transition](https://react.dev/reference/react/addTransitionType#adding-the-cause-of-a-transition)
  + [Customize animations using browser view transition types](https://react.dev/reference/react/addTransitionType#customize-animations-using-browser-view-transition-types)
  + [Customize animations using `View Transition` Class](https://react.dev/reference/react/addTransitionType#customize-animations-using-view-transition-class)
  + [Customize animations using `ViewTransition` events](https://react.dev/reference/react/addTransitionType#customize-animations-using-viewtransition-events)

---

## Reference

### `addTransitionType`

#### Parameters

* `type`: The type of transition to add. This can be any string.

#### Returns

`startTransition` does not return anything.

#### Caveats

* If multiple transitions are combined, all Transition Types are collected. You can also add more than one type to a Transition.
* Transition Types are reset after each commit. This means a `<Suspense>` fallback will associate the types after a `startTransition`, but revealing the content does not.

---

## Usage

### Adding the cause of a transition

Call `addTransitionType` inside of `startTransition` to indicate the cause of a transition:

```
import { startTransition, addTransitionType } from 'react';

function Submit({action) {

function handleClick() {

startTransition(() => {

addTransitionType('submit-click');

action();

});

}

return <button onClick={handleClick}>Click me</button>;

}
```

When you call addTransitionType inside the scope of startTransition, React will associate submit-click as one of the causes for the Transition.

Currently, Transition Types can be used to customize different animations based on what caused the Transition. You have three different ways to choose from for how to use them:

* [Customize animations using browser view transition types](https://react.dev/reference/react/addTransitionType#customize-animations-using-browser-view-transition-types)
* [Customize animations using `View Transition` Class](https://react.dev/reference/react/addTransitionType#customize-animations-using-view-transition-class)
* [Customize animations using `ViewTransition` events](https://react.dev/reference/react/addTransitionType#customize-animations-using-viewtransition-events)

In the future, we plan to support more use cases for using the cause of a transition.

---

### Customize animations using browser view transition types

When a [`ViewTransition`](https://react.dev/reference/react/ViewTransition) activates from a transition, React adds all the Transition Types as browser [view transition types](https://www.w3.org/TR/css-view-transitions-2/#active-view-transition-pseudo-examples) to the element.

This allows you to customize different animations based on CSS scopes:

```
function Component() {

return (

<ViewTransition>

<div>Hello</div>

</ViewTransition>

);

}

startTransition(() => {

addTransitionType('my-transition-type');

setShow(true);

});
```

```
:root:active-view-transition-type(my-transition-type) {

&::view-transition-...(...) {

...

}

}
```

---

### Customize animations using `View Transition` Class

You can customize animations for an activated `ViewTransition` based on type by passing an object to the View Transition Class:

```
function Component() {

return (

<ViewTransition enter={{

'my-transition-type': 'my-transition-class',

}}>

<div>Hello</div>

</ViewTransition>

);

}

// ...

startTransition(() => {

addTransitionType('my-transition-type');

setState(newState);

});
```

If multiple types match, then they’re joined together. If no types match then the special “default” entry is used instead. If any type has the value “none” then that wins and the ViewTransition is disabled (not assigned a name).

These can be combined with enter/exit/update/layout/share props to match based on kind of trigger and Transition Type.

```
<ViewTransition enter={{

'navigation-back': 'enter-right',

'navigation-forward': 'enter-left',

}}

exit={{

'navigation-back': 'exit-right',

'navigation-forward': 'exit-left',

}}>
```

---

### Customize animations using `ViewTransition` events

You can imperatively customize animations for an activated `ViewTransition` based on type using View Transition events:

```
<ViewTransition onUpdate={(inst, types) => {

if (types.includes('navigation-back')) {

...

} else if (types.includes('navigation-forward')) {

...

} else {

...

}

}}>
```

This allows you to pick different imperative Animations based on the cause.

[Previousact](https://react.dev/reference/react/act)[Nextcache](https://react.dev/reference/react/cache)