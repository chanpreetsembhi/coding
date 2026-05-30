#### Change Navbar link style based on active route

```vue
<script setup>
import { useRoute } from 'vue-router';

const isActiveLink = (routePath) => {
 const route = useRoute()
 return route.path === routePath
}
</script>

<template>
  <nav>
      <RouterLink to="/" :class="[isActiveLink('/') ? 'bg-green-900': 'hover:bg-  gray-900 hover:text-white', 'text-white rounded-md px-3 py-2']">
        Home
       </RouterLink>

       <RouterLink to="/jobs" :class="[isActiveLink('/jobs') ? 'bg-green-900': 'hover:bg-gray-900 hover:text-white', 'text-white rounded-md px-3 py-2']">Jobs
       </RouterLink>
  </nav>
</template>
```

#### Another Method
- You can also use `activeClass` tag.

```vue
<template>
  <nav>
      <RouterLink to="/" class="text-white rounded-md px-3 py-2" 
         activeClass="bg-green-900 hover:bg-gray-900 hover:text-white">
        Home
       </RouterLink>

       <RouterLink to="/jobs" class="text-white rounded-md px-3 py-2"
         activeClass="bg-green-900 hover:bg-gray-900 hover:text-white">
       Jobs
       </RouterLink>
  </nav>
</template>
```