---
url: https://react.dev/reference/react-dom/components/progress
title: <progress> – React
source_domain: react.dev
---

# <progress> – React

[API Reference](https://react.dev/reference/react)

[Components](https://react.dev/reference/react-dom/components)

# <progress>

The [built-in browser `<progress>` component](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress) lets you render a progress indicator.

```
<progress value={0.5} />
```

* [Reference](https://react.dev/reference/react-dom/components/progress#reference) 
  + [`<progress>`](https://react.dev/reference/react-dom/components/progress#progress)
* [Usage](https://react.dev/reference/react-dom/components/progress#usage) 
  + [Controlling a progress indicator](https://react.dev/reference/react-dom/components/progress#controlling-a-progress-indicator)

---

## Reference

### `<progress>`

To display a progress indicator, render the [built-in browser `<progress>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress) component.

```
<progress value={0.5} />
```

[See more examples below.](https://react.dev/reference/react-dom/components/progress#usage)

#### Props

`<progress>` supports all [common element props.](https://react.dev/reference/react-dom/components/common#common-props)

Additionally, `<progress>` supports these props:

* [`max`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress#max): A number. Specifies the maximum `value`. Defaults to `1`.
* [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress#value): A number between `0` and `max`, or `null` for indeterminate progress. Specifies how much was done.

---

## Usage

### Controlling a progress indicator

To display a progress indicator, render a `<progress>` component. You can pass a number `value` between `0` and the `max` value you specify. If you don’t pass a `max` value, it will assumed to be `1` by default.

If the operation is not ongoing, pass `value={null}` to put the progress indicator into an indeterminate state.

[Fork](https://codesandbox.io/api/v1/sandboxes/define?undefined&environment=create-react-app "Open in CodeSandbox")

```
export default function App() {
  return (
    <>
      <progress value={0} />
      <progress value={0.5} />
      <progress value={0.7} />
      <progress value={75} max={100} />
      <progress value={1} />
      <progress value={null} />
    </>
  );
}
```

[Previous<option>](https://react.dev/reference/react-dom/components/option)[Next<select>](https://react.dev/reference/react-dom/components/select)