---
url: https://react.dev/reference/react-dom/components/option
title: <option> – React
source_domain: react.dev
---

# <option> – React

[API Reference](https://react.dev/reference/react)

[Components](https://react.dev/reference/react-dom/components)

# <option>

The [built-in browser `<option>` component](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) lets you render an option inside a [`<select>`](https://react.dev/reference/react-dom/components/select) box.

```
<select>

<option value="someOption">Some option</option>

<option value="otherOption">Other option</option>

</select>
```

* [Reference](https://react.dev/reference/react-dom/components/option#reference) 
  + [`<option>`](https://react.dev/reference/react-dom/components/option#option)
* [Usage](https://react.dev/reference/react-dom/components/option#usage) 
  + [Displaying a select box with options](https://react.dev/reference/react-dom/components/option#displaying-a-select-box-with-options)

---

## Reference

### `<option>`

The [built-in browser `<option>` component](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) lets you render an option inside a [`<select>`](https://react.dev/reference/react-dom/components/select) box.

```
<select>

<option value="someOption">Some option</option>

<option value="otherOption">Other option</option>

</select>
```

[See more examples below.](https://react.dev/reference/react-dom/components/option#usage)

#### Props

`<option>` supports all [common element props.](https://react.dev/reference/react-dom/components/common#common-props)

Additionally, `<option>` supports these props:

* [`disabled`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#disabled): A boolean. If `true`, the option will not be selectable and will appear dimmed.
* [`label`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#label): A string. Specifies the meaning of the option. If not specified, the text inside the option is used.
* [`value`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option#value): The value to be used [when submitting the parent `<select>` in a form](https://react.dev/reference/react-dom/components/select#reading-the-select-box-value-when-submitting-a-form) if this option is selected.

#### Caveats

* React does not support the `selected` attribute on `<option>`. Instead, pass this option’s `value` to the parent [`<select defaultValue>`](https://react.dev/reference/react-dom/components/select#providing-an-initially-selected-option) for an uncontrolled select box, or [`<select value>`](https://react.dev/reference/react-dom/components/select#controlling-a-select-box-with-a-state-variable) for a controlled select.

---

## Usage

### Displaying a select box with options

Render a `<select>` with a list of `<option>` components inside to display a select box. Give each `<option>` a `value` representing the data to be submitted with the form.

[Read more about displaying a `<select>` with a list of `<option>` components.](https://react.dev/reference/react-dom/components/select)

[Fork](https://codesandbox.io/api/v1/sandboxes/define?undefined&environment=create-react-app "Open in CodeSandbox")

```
export default function FruitPicker() {
  return (
    <label>
      Pick a fruit:
      <select name="selectedFruit">
        <option value="apple">Apple</option>
        <option value="banana">Banana</option>
        <option value="orange">Orange</option>
      </select>
    </label>
  );
}
```

[Previous<input>](https://react.dev/reference/react-dom/components/input)[Next<progress>](https://react.dev/reference/react-dom/components/progress)