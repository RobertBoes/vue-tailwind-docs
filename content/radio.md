---
title: Radio Input component
description: VueJs reactive radio button component with customizable TailwindCSS or any CSS Framework classes.
---

# Radio input (TRadio)

VueJs reactive `<input type="radio" />` component with configurable classes, variants, and most common events. Friendly with utility-first frameworks like TailwindCSS..

<t-radio-playground></t-radio-playground>

<hr>

## Basic example

```html
<div class="flex">
  <label class="flex items-center">
    <t-radio name="options" value="a" checked />
    <span class="ml-2 text-sm">Option A</span>
  </label>
  <label class="flex items-center ml-2">
    <t-radio name="options" value="b" />
    <span class="ml-2 text-sm">Option B</span>
  </label>
</div>
```

<radio-basic-example></radio-basic-example>

## Props

| Property          | Type                                       | Default value | Description                                                                                            |
| ----------------- | ------------------------------------------ | ------------- | ------------------------------------------------------------------------------------------------------ |
| value             | `[String, Object, Number, Boolean, Array]` | `'on'`        | The value for the radio element                                                                        |
| model (`v-model`) | `[String, Object, Number, Boolean, Array]` | `undefined`   | The element used for the `v-model`                                                                     |
| checked           | `[Boolean, String]`                        | `false`       | HTML attribute                                                                                         |
| id                | `String`                                   | `undefined`   | HTML attribute                                                                                         |
| autofocus         | `Boolean`                                  | `undefined`   | HTML attribute                                                                                         |
| disabled          | `Boolean`                                  | `undefined`   | HTML attribute                                                                                         |
| name              | `String`                                   | `undefined`   | HTML attribute                                                                                         |
| readonly          | `Boolean`                                  | `undefined`   | HTML attribute                                                                                         |
| required          | `Boolean`                                  | `undefined`   | HTML attribute                                                                                         |
| tabindex          | `[String, Number]`                         | `undefined`   | HTML attribute                                                                                         |
| wrapped           | `Boolean`                                  | `false`       | If set the input will be wrapped in a div within some extra HTML (see [wrapped radio](#wrapped-radio)) |
| wrapperTag        | `String`                                   | `'label'`     | The HTML tag used to wrap the input when `wrapped` is set to `true`                                    |
| label             | `String`                                   | `undefined`   | When the input is `wrapped` the label is added as sibling of the input                                 |
| labelTag          | `String`                                   | `'span'`      | The HTML tag to use for the label                                                                      |
| classes           | `[String, Array, Object]`                  | ...           | The default CSS classes                                                                                |
| fixedClasses      | `[String, Array, Object]`                  | `undefined`   | Fixed CSS classes that will be merged with the active set of classes                                   |
| variants          | `Object`                                   | `undefined`   | The different variants of classes the component have                                                   |
| variant           | `[String, Object]`                         | `undefined`   | The variant that will be used                                                                          |

#### Default value of the *classes* prop:

```css
text-blue-500 transition duration-100 ease-in-out border-gray-300 shadow-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 focus:ring-offset-0 disabled:opacity-50 disabled:cursor-not-allowed
```


## Events

| Event  | Arguments                                 | Description                                          |
| ------ | ----------------------------------------- | ---------------------------------------------------- |
| input  | `String` (The current value of the radio) | Emitted every time the value of the `v-model` change |
| change | `String` (The current value of the radio) | Emitted every time the value of the `v-model` change |
| focus  | `FocusEvent`                              | Emitted when the radio is focused                    |
| blur   | `FocusEvent`                              | Emitted when the radio is blurred                    |

## Wrapped radio

This component accepts the `wrapped` prop that, when set it will add some extra HTML tags that make the component even more flexible.

Remember that the component can set as "wrapped" when installed or by using the `wrapped` prop (see [wrapped inputs](/docs/theming#wrapped-inputs) for more info):

```js
// When installed
const settings = {
  't-radio': {
    component: TRadio,
    props: {
      wrapped: true,
      // classes, variants, etc...
    }
  }
  // ...
}

Vue.use(VueTailwind, settings)
```

```html
<!-- // Using the wrapped prop -->
<t-radio wrapped />
```

A wrapped radio input will be rendered like this:

```html
<label class="">
  <span class="">
    <input value="radio-value" type="radio" class="">
  </span>
  <span class="">label prop or default slot</span>
</label>
```

### Classes for wrapped input

When the input has the wrapped setting, the `classes`, `variants`, etc. need to be an object with the following properties:


| Property            | Description                                                                 |
| ------------------- | --------------------------------------------------------------------------- |
| wrapper             | Classes for the `label` HTML tag that wraps the whole component             |
| wrapperChecked      | Classes to apply to the wrapper when the radio input is checked             |
| inputWrapper        | Classes for the `span` that wraps the radio input                           |
| inputWrapperChecked | Classes to apply to the inputWrapper when the the input is checked          |
| input               | Classes for the radio input                                                 |
| label               | Classes for the `label` that wraps the label prop                           |
| labelChecked        | Classes for the `label` that wraps the label prop when the input is checked |

Note: The "checked" attributes are optional.

#### Example

```js
const settings = {
  't-radio': {
    component: TRadio,
    props: {
      wrapped: true,
      classes: {
        label: 'text-sm uppercase mx-2 text-gray-700',
        input: 'text-blue-500 transition duration-100 ease-in-out border-gray-300 shadow-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 focus:ring-offset-0  disabled:opacity-50 disabled:cursor-not-allowed transition duration-150 ease-in-out',
        inputWrapper: 'inline-flex',
        wrapper: 'flex items-center',
        // labelChecked: '',
        // inputWrapperChecked: '',
        // wrapperChecked: '',
      }
      // Variants and fixed classes in the same `object` format ...
    }
  },
  // ...
}

Vue.use(VueTailwind, settings)
```

If you use the settings in the example above the component will be rendered like this:

<preview>
  <t-radio name="example-b" :classes="{
    label: 'text-sm uppercase mx-2 text-gray-700',
    input: 'text-blue-500 transition duration-100 ease-in-out border-gray-300 shadow-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 focus:ring-offset-0  disabled:opacity-50 disabled:cursor-not-allowed transition duration-150 ease-in-out',
    inputWrapper: 'inline-flex',
    wrapper: 'flex items-center',
  }" label="Option A" wrapped ></t-radio>
  <t-radio name="example-b" :classes="{
    label: 'text-sm uppercase mx-2 text-gray-700',
    input: 'text-blue-500 transition duration-100 ease-in-out border-gray-300 shadow-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 focus:ring-offset-0  disabled:opacity-50 disabled:cursor-not-allowed transition duration-150 ease-in-out',
    inputWrapper: 'inline-flex',
    wrapper: 'flex items-center',
  }" label="Option B" wrapped></t-radio>
</preview>

### Use a label

When the TRadio component has the `wrapped` setting, it accepts a label prop that is added as a sibling of the `input`

```html
<t-radio wrapped label="my own option" name="example-2">
<t-radio wrapped label="my own option 2" name="example-2">
```

<preview>
<t-radio wrapped label="my own option" name="example-2"></t-radio>
<t-radio wrapped label="my own option 2" name="example-2"></t-radio>
</preview>

#### Label slot

The label can be also added by using the default slot.

```html
I am: 
<t-radio wrapped name="example-3">
😡
</t-radio>
<t-radio wrapped name="example-3">
😀
</t-radio>
```

<preview>
I am: 
<t-radio wrapped name="example-3">
😡
</t-radio>
<t-radio wrapped name="example-3">
😀
</t-radio>
</preview>
