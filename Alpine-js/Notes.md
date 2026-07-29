# Alpine.js Complete Notes — Beginner to Advanced

## Table of Contents

1. [[#Introduction]]
2. [[#Setup]]
3. [[#Core Concept x-data]]
4. [[#Displaying Data]]
5. [[#Event Handling]]
6. [[#Binding Attributes]]
7. [[#Conditionals]]
8. [[#Loops]]
9. [[#Two-Way Binding x-model]]
10. [[#Magic Properties]]
11. [[#Other Directives]]
12. [[#Components & Reusability]]
13. [[#Global State Alpine.store]]
14. [[#Lifecycle & Reactivity]]
15. [[#Transitions & Animations]]
16. [[#Plugins]]
17. [[#Custom Directives & Magics]]
18. [[#Advanced Patterns]]
19. [[#Best Practices]]
20. [[#Practice Project Ideas]]

---

## Introduction

Alpine.js is a lightweight JavaScript framework (~15kb) for adding interactivity directly in your HTML. Think of it as "jQuery for the modern web" or "Tailwind for JavaScript" — you sprinkle behavior into markup using directives, without needing a build step, virtual DOM, or complex tooling.

**Why Alpine?**

- No build step required
- Small footprint
- Works great with server-rendered apps (Laravel, Django, Rails, PHP, static HTML)
- Declarative syntax similar to Vue.js
- Perfect for adding interactivity to mostly-static sites

---

## Setup

### Option 1: CDN (fastest way to start)

```html
<!DOCTYPE html>
<html>
<head>
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
</head>
<body>
  <div x-data="{ message: 'Hello Alpine!' }">
    <span x-text="message"></span>
  </div>
</body>
</html>
```

> `defer` is important — it ensures the DOM is parsed before Alpine initializes.

### Option 2: NPM (for build-tool projects)

```bash
npm install alpinejs
```

```js
import Alpine from 'alpinejs'
window.Alpine = Alpine
Alpine.start()
```

---

## Core Concept: x-data

`x-data` declares a new **Alpine component** and its reactive state (a plain JS object).

```html
<div x-data="{ open: false, count: 0, name: 'Sam' }">
  <!-- everything inside can access open, count, name -->
</div>
```

- State is scoped to the element and its children.
- Components can be nested; child scopes inherit and can override parent data.
- You can extract data into a function for reuse:

```html
<div x-data="dropdown()">
  ...
</div>

<script>
  function dropdown() {
    return {
      open: false,
      toggle() { this.open = !this.open }
    }
  }
</script>
```

---

## Displaying Data

### x-text

Sets the text content of an element.

```html
<div x-data="{ name: 'Alpine' }">
  <p x-text="name"></p>
</div>
```

### x-html

Sets innerHTML (be careful — same XSS risks as innerHTML in vanilla JS).

```html
<div x-data="{ content: '<b>Bold</b>' }">
  <div x-html="content"></div>
</div>
```

---

## Event Handling

### x-on (shorthand: @)

```html
<button x-on:click="count++">Increment</button>
<!-- shorthand -->
<button @click="count++">Increment</button>
```

### Common modifiers

|Modifier|Purpose|
|---|---|
|`.prevent`|calls `preventDefault()`|
|`.stop`|calls `stopPropagation()`|
|`.self`|only trigger if event target is the element itself|
|`.window`|listen on the `window` object|
|`.document`|listen on the `document` object|
|`.once`|only trigger once|
|`.debounce.500ms`|debounce the handler|
|`.throttle.500ms`|throttle the handler|
|`.outside`|trigger when click happens outside the element|

```html
<form @submit.prevent="submitForm()">...</form>

<div @click.outside="open = false">...</div>

<input @keydown.enter="addItem()" @keydown.escape="cancel()">

<button @click.debounce.300ms="search()">Search</button>
```

### Passing the event object

```html
<input @input="query = $event.target.value">
```

---

## Binding Attributes

### x-bind (shorthand: `:`)

Binds any HTML attribute to a JS expression.

```html
<div x-data="{ isRed: true }">
  <span :class="isRed ? 'text-red-500' : 'text-blue-500'">Text</span>
  <button :disabled="loading">Submit</button>
  <img :src="imageUrl" :alt="imageAlt">
</div>
```

### Class object syntax (very handy)

```html
<div :class="{ 'active': isActive, 'hidden': !visible }"></div>
```

### Binding styles

```html
<div :style="{ color: activeColor, fontSize: size + 'px' }"></div>
```

---

## Conditionals

### x-show

Toggles `display: none` — element stays in the DOM.

```html
<div x-data="{ open: false }">
  <button @click="open = !open">Toggle</button>
  <div x-show="open">I'm visible when open is true</div>
</div>
```

### x-if

Actually adds/removes the element from the DOM. **Must be used on a `<template>` tag.**

```html
<template x-if="loggedIn">
  <div>Welcome back!</div>
</template>
```

**x-show vs x-if:**

- `x-show`: cheap toggle, good for frequent show/hide, animatable.
- `x-if`: full mount/unmount, good when you want the element (and any component state inside) fully destroyed and recreated.

---

## Loops

### x-for

Must be on a `<template>` tag with a single root element inside.

```html
<ul x-data="{ items: ['Apple', 'Banana', 'Cherry'] }">
  <template x-for="item in items" :key="item">
    <li x-text="item"></li>
  </template>
</ul>
```

With index:

```html
<template x-for="(item, index) in items" :key="index">
  <li x-text="index + ': ' + item"></li>
</template>
```

Looping over objects/arrays of objects:

```html
<template x-for="user in users" :key="user.id">
  <li x-text="user.name"></li>
</template>
```

> Always provide `:key` for correct DOM diffing, especially when the list can reorder.

---

## Two-Way Binding: x-model

Syncs form inputs with data automatically.

```html
<div x-data="{ search: '' }">
  <input type="text" x-model="search">
  <p x-text="search"></p>
</div>
```

Works with checkboxes, radios, selects, and textareas too:

```html
<input type="checkbox" x-model="agreed">
<select x-model="selected">
  <option value="a">A</option>
  <option value="b">B</option>
</select>
```

### Modifiers

- `.lazy` — update on `change` instead of `input`
- `.number` — cast value to a number
- `.debounce` — debounce updates

```html
<input x-model.lazy.debounce.500ms="query">
<input type="number" x-model.number="age">
```

---

## Magic Properties

Alpine provides special `$`-prefixed helpers available inside any expression.

|Magic|Purpose|
|---|---|
|`$el`|reference to the current DOM node|
|`$refs`|access elements marked with `x-ref`|
|`$store`|access global Alpine stores|
|`$watch`|watch a property for changes|
|`$dispatch`|dispatch a custom DOM event|
|`$nextTick`|run code after Alpine's next DOM update|
|`$root`|the root element of the closest x-data scope|
|`$data`|the raw data object of current scope|
|`$id`|generate unique ids scoped to component|

### x-ref + $refs

```html
<div x-data>
  <input x-ref="emailInput">
  <button @click="$refs.emailInput.focus()">Focus input</button>
</div>
```

### $watch

```html
<div x-data="{ count: 0 }" x-init="$watch('count', value => console.log('count is now', value))">
  <button @click="count++">+</button>
</div>
```

### $dispatch (component communication)

```html
<div @notify="alert($event.detail.message)">
  <button @click="$dispatch('notify', { message: 'Hi there!' })">Notify</button>
</div>
```

### $nextTick

```html
<button @click="showText = true; $nextTick(() => { $refs.text.focus() })">
  Show and focus
</button>
```

---

## Other Directives

### x-init

Runs an expression when a component initializes.

```html
<div x-data="{ count: 0 }" x-init="console.log('Component loaded')"></div>
```

Or fetch data on init:

```html
<div x-data="{ users: [] }" x-init="fetch('/api/users').then(r => r.json()).then(data => users = data)">
```

### x-effect

Re-runs whenever any referenced reactive property changes (similar to Vue's watchEffect).

```html
<div x-data="{ count: 0 }" x-effect="console.log('Count changed to', count)"></div>
```

### x-cloak

Hides an element until Alpine has finished initializing (prevents flash of unstyled content).

```html
<div x-cloak x-show="open">...</div>
```

```css
[x-cloak] { display: none !important; }
```

### x-ignore

Tells Alpine to skip initializing this element and its children.

### x-teleport

Moves an element (and its Alpine context) elsewhere in the DOM — useful for modals.

```html
<template x-teleport="body">
  <div class="modal">I'm rendered at the end of body!</div>
</template>
```

### x-transition

Add smooth enter/leave animations (see Transitions section).

---

## Components & Reusability

### Extracting logic into functions

```html
<div x-data="counter(10)">
  <button @click="decrement()">-</button>
  <span x-text="count"></span>
  <button @click="increment()">+</button>
</div>

<script>
function counter(start = 0) {
  return {
    count: start,
    increment() { this.count++ },
    decrement() { this.count-- }
  }
}
</script>
```

### Alpine.data() — registering reusable components globally

```js
document.addEventListener('alpinejs:init', () => {
  Alpine.data('dropdown', () => ({
    open: false,
    toggle() { this.open = !this.open }
  }))
})
```

```html
<div x-data="dropdown">
  <button @click="toggle()">Menu</button>
  <div x-show="open">...</div>
</div>
```

### Getters (computed properties)

```js
Alpine.data('cart', () => ({
  items: [{ price: 10 }, { price: 20 }],
  get total() {
    return this.items.reduce((sum, i) => sum + i.price, 0)
  }
}))
```

```html
<div x-data="cart">
  <p x-text="total"></p>
</div>
```

---

## Global State: Alpine.store

For sharing state across multiple, unrelated components.

```js
document.addEventListener('alpine:init', () => {
  Alpine.store('darkMode', {
    on: false,
    toggle() { this.on = !this.on }
  })
})
```

```html
<button @click="$store.darkMode.toggle()">Toggle theme</button>
<body :class="$store.darkMode.on ? 'dark' : ''">
```

Simple primitive stores also work:

```js
Alpine.store('count', 0)
```

```html
<button @click="$store.count++">Count: <span x-text="$store.count"></span></button>
```

---

## Lifecycle & Reactivity

### Order of events

1. `alpine:init` — fired on `document` right before Alpine initializes. Register stores/components/directives here.
2. `x-init` — runs per-component, after data is initialized but before DOM is rendered.
3. Alpine walks the DOM tree and initializes each `x-data` block it finds.
4. `alpine:initialized` — fired after Alpine has fully initialized the page.

### Reactivity

Alpine's reactivity is powered by JS Proxies (like Vue 3). Just mutate the data — no `setState` needed:

```js
this.count++
this.items.push(newItem)
this.user.name = 'New name'
```

---

## Transitions & Animations

### x-transition (built-in, CSS-based)

```html
<div x-show="open" x-transition>...</div>
```

### Fine-grained control

```html
<div x-show="open"
     x-transition:enter="transition ease-out duration-300"
     x-transition:enter-start="opacity-0 scale-90"
     x-transition:enter-end="opacity-100 scale-100"
     x-transition:leave="transition ease-in duration-200"
     x-transition:leave-start="opacity-100 scale-100"
     x-transition:leave-end="opacity-0 scale-90">
  Content
</div>
```

### Shorthand helpers

```html
<div x-show="open" x-transition.duration.500ms>...</div>
<div x-show="open" x-transition.opacity.scale.80>...</div>
```

---

## Plugins

Official first-party plugins extend Alpine's core. Add via CDN or npm.

|Plugin|Purpose|
|---|---|
|**Persist**|persist state to localStorage|
|**Intersect**|trigger behavior with Intersection Observer|
|**Focus**|trap and manage focus (great for modals)|
|**Collapse**|smooth expand/collapse (accordion-friendly)|
|**Mask**|input masking (phone numbers, dates, etc.)|
|**Anchor**|anchor positioning for dropdowns/tooltips|

### Example: Persist

```html
<script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/persist@3.x.x/dist/cdn.min.js"></script>

<div x-data="{ count: $persist(0) }">
  <button @click="count++" x-text="count"></button>
</div>
```

### Example: Intersect

```html
<div x-intersect="visible = true" x-data="{ visible: false }">
  <div x-show="visible" x-transition>I fade in when scrolled into view</div>
</div>
```

### Example: Collapse (accordion)

```html
<div x-data="{ open: false }">
  <button @click="open = !open">Toggle</button>
  <div x-show="open" x-collapse>
    Long content that collapses smoothly...
  </div>
</div>
```

### Example: Focus (modal trap)

```html
<div x-show="open" x-trap.inert.noscroll="open">
  <!-- focus stays trapped inside while open -->
</div>
```

---

## Custom Directives & Magics

### Custom directive

```js
document.addEventListener('alpine:init', () => {
  Alpine.directive('tooltip', (el, { expression }) => {
    el.setAttribute('title', expression)
  })
})
```

```html
<button x-tooltip="'Click to save'">Save</button>
```

### Custom magic property

```js
document.addEventListener('alpine:init', () => {
  Alpine.magic('clipboard', () => {
    return subject => navigator.clipboard.writeText(subject)
  })
})
```

```html
<button @click="$clipboard('Copied text!')">Copy</button>
```

---

## Advanced Patterns

### Fetching data & handling async

```html
<div x-data="{ posts: [], loading: true }" x-init="
  fetch('/api/posts')
    .then(res => res.json())
    .then(data => { posts = data; loading = false })
">
  <template x-if="loading"><p>Loading...</p></template>
  <template x-for="post in posts" :key="post.id">
    <p x-text="post.title"></p>
  </template>
</div>
```

### Building a modal with x-teleport + x-trap + x-transition

```html
<div x-data="{ open: false }">
  <button @click="open = true">Open Modal</button>

  <template x-teleport="body">
    <div x-show="open"
         x-trap.inert.noscroll="open"
         @keydown.escape.window="open = false"
         @click.self="open = false"
         x-transition.opacity
         class="fixed inset-0 flex items-center justify-center bg-black/50">
      <div class="bg-white p-6 rounded" @click.stop>
        <h2>Modal title</h2>
        <button @click="open = false">Close</button>
      </div>
    </div>
  </template>
</div>
```

### Nested components communicating via events

```html
<div @add-to-cart.window="cartCount++" x-data="{ cartCount: 0 }">
  <span x-text="cartCount"></span>

  <div x-data>
    <button @click="$dispatch('add-to-cart')">Add item</button>
  </div>
</div>
```

### Debounced live search

```html
<div x-data="{ query: '', results: [] }">
  <input x-model.debounce.400ms="query"
         @input="results = query ? items.filter(i => i.includes(query)) : []">
</div>
```

### Multi-step form (wizard)

```html
<div x-data="{ step: 1 }">
  <template x-if="step === 1"><div>Step 1 content <button @click="step++">Next</button></div></template>
  <template x-if="step === 2"><div>Step 2 content <button @click="step++">Next</button></div></template>
  <template x-if="step === 3"><div>Done!</div></template>
</div>
```

### Combining Alpine with Alpine.store for a theme switcher app-wide

```js
Alpine.store('theme', {
  mode: Alpine.$persist('light').as('theme_mode'),
  toggle() { this.mode = this.mode === 'light' ? 'dark' : 'light' }
})
```

---

## Best Practices

1. **Keep components small.** Extract logic into `Alpine.data()` functions once markup gets complex.
2. **Use `x-cloak`** to avoid flash-of-unstyled-content on page load.
3. **Prefer `x-show` for frequent toggles**, `x-if` when you truly need mount/unmount.
4. **Always use `:key`** in `x-for` loops.
5. **Avoid deeply nested `x-data`** — use `Alpine.store` for cross-component state instead.
6. **Sanitize any HTML** passed to `x-html` to avoid XSS.
7. **Use `$dispatch`/custom events** instead of tightly coupling sibling components.
8. **Debounce expensive operations** (search, API calls) with `.debounce`.
9. Combine Alpine with **Tailwind CSS** — they're designed to complement each other well.
10. For larger apps, consider whether you actually need a heavier framework (Vue/React) — Alpine shines for sprinkles of interactivity, not full SPAs.

---

## Practice Project Ideas

**Beginner**

- Counter app
- Toggle show/hide panel
- Simple to-do list (add/remove items)
- Tabs component

**Intermediate**

- Accordion/FAQ list (with x-collapse)
- Dropdown menu with click-outside-to-close
- Live search filter over a list
- Form validation with error messages
- Dark mode toggle with persistence

**Advanced**

- Modal system using x-teleport + x-trap
- Multi-step form wizard with validation per step
- Shopping cart with Alpine.store shared across components
- Infinite scroll / lazy-loaded content using x-intersect
- Custom directive library (e.g., tooltip, click-outside, copy-to-clipboard)
- Toast/notification system using global store + custom events

---

## Quick Reference Cheat Sheet

```
x-data       declare component state
x-init       run code on init
x-show       toggle display:none
x-if         add/remove from DOM (needs <template>)
x-for        loop (needs <template>, use :key)
x-text       set text content
x-html       set innerHTML
x-model      two-way bind form inputs
x-bind / :   bind any attribute
x-on / @     listen for events
x-transition animate show/hide
x-effect     re-run on dependency change
x-ignore     skip initializing element
x-cloak      hide until Alpine ready
x-ref        mark element for $refs
x-teleport   move element elsewhere in DOM
x-trap       trap focus within element (plugin)
x-collapse   smooth collapse animation (plugin)
x-intersect  run when element enters viewport (plugin)

$el          current DOM element
$refs        access x-ref elements
$store       access global store
$watch       watch a property
$dispatch    fire custom event
$nextTick    run after DOM updates
$root        root element of scope
$persist     persist value to localStorage (plugin)
```