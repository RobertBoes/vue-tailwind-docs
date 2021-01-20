---
title: Button Component
description: VueJs reactive button component with customizable TailwindCSS or any CSS Framework classes.
---

# Button (TButton)

VueJs reactive `<button />` component with configurable classes, variants, and most common events. Friendly with utility-first frameworks like TailwindCSS..

<t-button-playground></t-button-playground>

<hr>

## Basic example

```html
<t-button>Example button</t-button>
```

<preview>
  <t-button>Example button</t-button>
</preview>


## Props

| Property          | Type                      | Default value | Description                                                                            |
| ----------------- | ------------------------- | ------------- | -------------------------------------------------------------------------------------- |
| value (`v-model`) | `[String, Number]`        | `null`        | HTML attribute                                                                         |
| id                | `String`                  | `undefined`   | HTML attribute                                                                         |
| name              | `String`                  | `undefined`   | HTML attribute                                                                         |
| disabled          | `Boolean`                 | `undefined`   | HTML attribute                                                                         |
| readonly          | `Boolean`                 | `undefined`   | HTML attribute                                                                         |
| autofocus         | `Boolean`                 | `undefined`   | HTML attribute                                                                         |
| required          | `Boolean`                 | `undefined`   | HTML attribute                                                                         |
| type              | `String`                  | `undefined`   | HTML attribute                                                                         |
| tabindex          | `[String, Number]`        | `undefined`   | HTML attribute                                                                         |
| text              | `String`                  | `undefined`   | Text of the button (when no slot used)                                                 |
| tagName           | `String`                  | `'button'`    | HTML Tag to use for the component `button` or `a`                                      |
| href              | `String`                  | `null`        | Href attribute for `a`                                                                 |
| native            | `Boolean`                 | `false`       | Set to force to render the default button instead for a router-link, inertia-link, etc |
| classes           | `[String, Array, Object]` | ...           | The default CSS classes                                                                |
| fixedClasses      | `[String, Array, Object]` | `undefined`   | Fixed CSS classes that will be merged with the active set of classes                   |
| variants          | `Object`                  | `undefined`   | The different variants of classes the component have                                   |
| variant           | `[String, Object]`        | `undefined`   | The variant that will be used                                                          |

*Note:* when the `href` prop is set it will change the tag name to `a`.

#### Default value of the *classes* prop:

```css
block px-4 py-2 text-white transition duration-100 ease-in-out bg-blue-500 border border-transparent rounded shadow-sm hover:bg-blue-600 focus:border-blue-500 focus:ring-2 focus:ring-blue-500 focus:outline-none focus:ring-opacity-50 disabled:opacity-50
```

## VueRouter compatibility

This button is compatible with `vue-router`, you just need to define the `to` prop, if the `router-link` or `nuxt-link` component is available it will render the component.

### RouterLink Props

When the component is rendered as RouterLink you can use the properties of that component:

| Property         | Type               | Default value                |
| ---------------- | ------------------ | ---------------------------- |
| to               | `[String, Object]` | `undefined`                  |
| replace          | `Boolean`          | `false`                      |
| append           | `Boolean`          | `false`                      |
| exact            | `Boolean`          | `false`                      |
| activeClass      | `String`           | `'router-link-active'`       |
| exactActiveClass | `String`           | `'router-link-exact-active'` |

## InertiaJs compatibility

This button is compatible with `inertia-link` and will be converted if the `href` prop is set, the `tagName` is `'a'` and the `InertiaLink` component is available.

<tip>
Pro tip: You can create a custom component, so you don't need to change the  `tagName` every time. <nuxt-link class="underline" to="/docs/settings#use-the-settings-to-create-different-components">(See override settings)</nuxt-link>
</tip>

```js
import Vue from 'vue'
import VueTailwind from 'vue-tailwind'

import TButton from 'vue-tailwind/dist/t-button'

const settings = {
  // Set the tagName as `a` so you can use easily use with Inertia
  't-inertia': {
    component: TButton,
    props: {
      tagName: 'a',
    }
  },
}

Vue.use(VueTailwind, settings)
```

### InertiaLink Props

When the component is rendered as RouterLink you can use the properties of that component:

| Property       | Type              | Default value |
| -------------- | ----------------- | ------------- |
| method         | `String`          | `'get'`       |
| data           | `Object`          | `{}`          |
| preserveState  | `Boolean`         | `false`       |
| preserveScroll | `Boolean`         | `false`       |
| event          | `[String, Array]` | `'click'`     |
| only           | `Array`           | `[]`          |

## Events

| Event | Arguments  | Description                        |
| ----- | ---------- | ---------------------------------- |
| focus | FocusEvent | Emitted when the button is focused |
| blur  | FocusEvent | Emitted when the button is blurred |
| click | MouseEvent | Emitted when the button is clicked |
