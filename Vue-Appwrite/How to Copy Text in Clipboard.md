
```vue
<script setup>
import { onMounted, ref } from "vue";

const notes = ref([])

const copyText = (toCopy) => {
  navigator.clipboard.writeText(toCopy)
    .then(() => console.log('Test Copy successfully!'))
    .catch(error => console.error('Error coping text:', error))
}
</script>
<template>
<div class="flex flex-col space-y-3">
    <div v-for="note in notes" :key="note.$id"
      class="bg-gray-50 border border-gray-300 rounded-lg shadow-sm flex items-center gap-3 p-4">
      <CopyIcon @click="copyText(note.body)" class="text-gray-500 size-6 cursor-pointer" />
      {{ note.body }}
    </div>
  </div>
</template>
```
==(note.body) note is ref value and body is in appwrite database strring name==