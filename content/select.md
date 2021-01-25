---
title: Select component
description: VueJs reactive select component with customizable TailwindCSS or any CSS Framework classes.
---

# Select (TSelect)

VueJs reactive `<select></select>` component with configurable classes, variants, and most common events. Friendly with utility-first frameworks like TailwindCSS..

<t-select-playground></t-select-playground>

<hr>

## Basic example

```html
<t-select
  placeholder="Select an option"
  :options="['Option A', 'Option B', 'Option C']"
  variant="demo"
></t-select>
```

<preview>
  <t-select placeholder="Select an option" :options="['Option A', 'Option B', 'Option C']" variant="demo" />
</preview>

## Props

| Property          | Type                      | Default value | Description                                                                                                                                      |
| ----------------- | ------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| value (`v-model`) | `[Array, String, Number, Object, Boolean]` | `undefined`   | The value for the element                                                                                                                        |
| id                | `String`                  | `undefined`   | HTML attribute                                                                                                                                   |
| autofocus         | `Boolean`                 | `undefined`   | HTML attribute                                                                                                                                   |
| disabled          | `Boolean`                 | `undefined`   | HTML attribute                                                                                                                                   |
| name              | `String`                  | `undefined`   | HTML attribute                                                                                                                                   |
| readonly          | `Boolean`                 | `undefined`   | HTML attribute                                                                                                                                   |
| required          | `Boolean`                 | `undefined`   | HTML attribute                                                                                                                                   |
| tabindex          | `[String, Number]`        | `undefined`   | HTML attribute                                                                                                                                   |
| multiple          | `Boolean`                 | `undefined`   | HTML attribute                                                                                                                                   |
| placeholder       | `String`                  | `undefined`   | When set it will prepend an empty `option` tag with the text the value of `null`                                                                 |
| options           | `[Array, Object]`         | `undefined`   | The options of the select (see [options format](#options-format))                                                                                |
| textAttribute     | `String`                  | `undefined`   | Used to extract the text of the `option` from the options list. <br />(see [define the value/text attributes](#define-the-valuetext-attributes)) |
| valueAttribute    | `String`                  | `undefined`   | Used to extract the value of the `option` from the options list <br />(see [define the value/text attributes](#define-the-valuetext-attributes)) |
| wrapped           | `Boolean`                 | `false`       | If set, the select will be wrapped in a div within an SVG icon (see [wrap select](#wrap-select))                                                 |
| classes           | `[String, Object, Array]` | ...           | The default CSS classes                                                                                                                          |
| fixedClasses      | `[String, Object, Array]` | `undefined`   | Fixed CSS classes that will be merged with the active set of classes                                                                             |
| variants          | `Object`                  | `undefined`   | The different variants of classes the component have                                                                                             |
| variant           | `[String, Object]`        | `undefined`   | The variant that will be used                                                                                                                    |

#### Default value of the *classes* prop:

```css
block w-full pl-3 pr-10 py-2 text-black placeholder-gray-400 transition duration-100 ease-in-out bg-white border border-gray-300 rounded shadow-sm focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:outline-none focus:ring-opacity-50 disabled:opacity-50 disabled:cursor-not-allowed
```
## Options format

This component accepts the `options` in different formats:

### Array of objects

```html
<!-- `value`, `text` attributes (Preferred) -->
<t-select :options="[
  { value: 1, text: 'Option 1' },
  { value: 2, text: 'Option 2' },
  { value: 3, text: 'Option 3', disabled: true }
]" />
<!-- `id` instead of `value` as attribute -->
<t-select :options="[
  { id: 1, text: 'Option 1' },
  { id: 2, text: 'Option 2' },
  { id: 3, text: 'Option 3', disabled: true }
]" />
<!-- `label` instead of `text` as attribute -->
<t-select :options="[
  { value: 1, label: 'Option 1' },
  { value: 2, label: 'Option 2' },
  { value: 3, label: 'Option 3', disabled: true }
]" />

<!-- All the examples above will render: -->
<select>
  <option value="1">Option 1</option>
  <option value="2">Option 2</option>
  <option disabled value="3">Option 3</option>
</select>
```

<tip>
  Notice that you can optionally add a `disabled` attribute.
</tip>

### Object with value => text pairs
```html
<t-select :options="{
  A: 'Option A',
  B: 'Option B',
  C: 'Option C'
}" />

<!-- Will Render: -->
<select>
  <option value="A">Option A</option>
  <option value="B">Option B</option>
  <option value="C">Option C</option>
</select>
```

### Array of strings
```html
<t-select :options="['Red', 'Blue', 'Yellow']" />

<!-- Will Render: -->
<select>
  <option value="Red">Red</option>
  <option value="Blue">Blue</option>
  <option value="Yellow">Yellow</option>
</select>
```
### Array of numbers
```html
<t-select :options="[18, 19, 20]" />

<!-- Will Render: -->
<select>
  <option value="18">18</option>
  <option value="19">19</option>
  <option value="20">20</option>
</select>
```

## Define the value/text attributes

When your options come in a format not handled by the component, you can define which attributes you want to use as the `value` and the `text` of every option tag.

Example:

Consider the following example where the options are an array of roles where the `role` should be the value of the option and the nested `name` inside the `details` attribute should be the text:

<meh-tip>
One alternative is to `map` the options to match one of the accepted formats:
</meh-tip>

```html
<t-select
  :options="[
    { role: 'root', details: { name: 'Root', expires: '2020-20-12' }, active: true },
    { role: 'admin', details: { name: 'Root', expires: '2020-20-12' }, active: true },
    { role: 'user', details: { name: 'Root', expires: '2020-20-12' }, active: true },
  ].map((option) => ({ value: option.role, text: option.details.name }))"
/>
```

<ok-tip>
A better approach is to use the <strong>valueAttribute</strong> and <strong>textAttribute</strong> props.
</ok-tip>

```html
<t-select
  :options="[
    { role: 'root', details: { name: 'Root', expires: '2020-20-12' }, active: true },
    { role: 'admin', details: { name: 'Root', expires: '2020-20-12' }, active: true },
    { role: 'user', details: { name: 'Root', expires: '2020-20-12' }, active: true },
  ]"
  value-attribute="role"
  text-attribute="details.name"  
/>
```

<tip>
Notice that in the example above we are using dot notation to get a nested attribute in the option for the `textAttribute`. That notation also works for the `valueAttribute`.
</tip>

## Wrapped select

This component accepts the `wrapped` prop that, when set it will wrap the `select` tag in a `DIV` and will add a sibling `SPAN` with an a `SVG` icon. This can give you more flexibility to customize your component.

Remember that the component can set as "wrapped" when installed or by using the `wrapped` prop (see [wrapped inputs](/docs/theming#wrapped-inputs) for more info):

```js
// When installed
const settings = {
  't-select': {
    component: TSelect,
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
<t-select wrapped />
```


A wrapped select will be rendered like this:

```html
<div>
  <select><!-- --></select>
  <span>
    <svg fill="currentColor" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
      <path clip-rule="evenodd" fill-rule="evenodd" d="M10 3a1 1 0 01.707.293l3 3a1 1 0 01-1.414 1.414L10 5.414 7.707 7.707a1 1 0 01-1.414-1.414l3-3A1 1 0 0110 3zm-3.707 9.293a1 1 0 011.414 0L10 14.586l2.293-2.293a1 1 0 011.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z"></path>
    </svg>
  </span>
</div>
```

### Classes for wrapped select

When the select is wrapped the `classes`, `variants`, etc need to be an object with the following properties:

| Property     | Description                                                                |
| ------------ | -------------------------------------------------------------------------- |
| wrapper      | `div` that wraps the whole component                                       |
| input        | `select` tag                                                               |
| arrowWrapper | `span` that is a sibling of the `select` tag that is used to wrap the icon |
| arrow        | `svg` icon                                                                 |

#### Example

```js
const settings = {
  't-select': {
    component: TSelect,
    props: {
      wrapped: true,
      classes: {
        wrapper: 'relative',
        input: 'block w-full py-2 pl-3 pr-10 text-black placeholder-gray-400 transition duration-100 ease-in-out bg-white border border-gray-300 rounded shadow-sm bg-none focus:ring-2 focus:ring-blue-500 focus:outline-none focus:ring-opacity-50 disabled:opacity-50 disabled:cursor-not-allowed focus:border-blue-500',
        arrowWrapper: 'pointer-events-none absolute inset-y-0 right-0 flex items-center px-2',
        arrow: 'fill-current h-4 w-4'
      }
    },
    // Variants and fixed classes in the same `object` format ...
  },
  // ...
}

Vue.use(VueTailwind, settings)
```

If you use the settings above the component will be rendered like this:

<preview>
  <t-select :classes="{
    wrapper: 'relative',
    input: 'block w-full py-2 pl-3 pr-10 text-black placeholder-gray-400 transition duration-100 ease-in-out bg-white border border-gray-300 rounded shadow-sm bg-none focus:ring-2 focus:ring-blue-500 focus:outline-none focus:ring-opacity-50 disabled:opacity-50 disabled:cursor-not-allowed focus:border-blue-500',
    arrowWrapper: 'pointer-events-none absolute inset-y-0 right-0 flex items-center px-2',
    arrow: 'fill-current h-4 w-4'
  }" :options="['Option 1', 'Option 2', 'Option 3']" wrapped />
</preview>

### Customize the select icon

If you want to use your own HTML instead of the default SVG icon you can use the `arrow` or `arrowWrapper` slots. Use the first one if you only want to override the SVG icon and the second one if you want to override the whole icon wrapper.

On the `scope` of both slot you have access to the currrent `variant`, the original classes the element has (`className`), and the current `value` of the component in case you want to use those values inside the slot.

##### Example:

Let's say that for some reason you want to:

- Use an ASCII down arrow (▼) instead of the default SVG icon,
- An angry emoji when the input has the `error` variant,
- And, just because you can, show a potato emoji when the current value is `>=2`

You know, a typical real-world use case:

```html
<t-select wrapped :options="[1,2,3]" variant="wrappedDemo">
  <template slot="arrow" slot-scope="{ className, variant, value }">
    <span v-if="variant==='error'" class="pr-2">😡</span>
    <span v-else-if="value>=2" class="pr-2">🥔</span>
    <span
      v-else
      :class="className"
    >▼</span>
  </template>
</t-select>
```

The example above will look like this:

<select-arrow-slot-example />

## Events

| Event  | Arguments                                  | Description                                          |
| ------ | ------------------------------------------ | ---------------------------------------------------- |
| input  | `String` (The current value of the select) | Emitted every time the value of the `v-model` change |
| change | `String` (The current value of the select) | Emitted when the select value change                 |
| focus  | `FocusEvent`                               | Emitted when the select is focused                   |
| blur   | `FocusEvent`                               | Emitted when the select is blurred                   |
