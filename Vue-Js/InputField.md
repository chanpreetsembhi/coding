#### Create Reusable Input in Vue-JS.

Create a `InputField` component.
```vue
<script setup>
defineProps({
    id: String,
    label: String,
    type: String,
    placeholder: String,
    value: String,
    modelValue: String
})

const emit = defineEmits(['update:modelValue'])

/* if you want to pass in function */
// const handleInput = ($event) => {
//     emit('update:modelValue', $event.target.value)
// }

</script>

<template>
<div class="flex flex-col space-y-1">
        <label :for="id">{{ label }}</label>
        <input :type="type" :id="id" :placeholder="placeholder" :value="modelValue"
            @input="emit('update:modelValue', $event.target.value)" v-bind="$attrs"
            class="border border-gray-300 rounded-md p-2" />
    </div>
</template>
```

How to use `App.js` or any other components or pages.

```vue
<script setup>
import {ref} from 'vue';
import InputField from '@/components/InputField.vue';

const newName = ref("")
</script>

<template>
<InputField type="text" label="Name" id="name" placeholder="Enter Your Name" 
 v-model="newName" class="text-class" />
</template>
```
==If you pass any extra class in only input you can use class with the help of v-bind="$attrs" label not effected with that class==
#### Create a Reusable Input with Vue-Ts

Create a `InputField` component.

```vue
<script setup lang="ts">
defineProps<{
    id: string
    label: string
    type: string,
    placeholder?: string
    modelValue: string
}>();

const emit = defineEmits<{
    (e: 'update:modelValue', modelValue: string): void
}>();
</script>

<template>
    <div class="flex flex-col space-y-1">
        <label :for="id" class="block text-sm/6 font-semibold text-gray-900">
        {{ label }}
        </label>
        <input :id="id" :type="type" :name="id" :placeholder="placeholder" :value="modelValue"
            @input="emit('update:modelValue', ($event.target as any)?.value)"
            class="block w-full rounded-md bg-white px-3.5 py-2 text-sm text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-sky-600" />
    </div>
</template>
```

How to use `App.js` or any other components or pages.

```vue
```