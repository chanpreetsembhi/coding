#### How to Toggle Between dark and light theme using `VueUse` Library

```vue
<script setup lang="ts">
import { RiMoonFill, RiSunFill } from "@remixicon/vue";
import { useDark, useToggle } from "@vueuse/core"

const isDark = useDark()
const toggleDark = useToggle(isDark)
</script>

<template>
    <div @click="toggleDark()" class="p-1">
        <RiMoonFill v-if="isDark" />
        <RiSunFill v-else />
    </div>
</template>
```
