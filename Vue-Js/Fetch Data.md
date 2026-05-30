#### How to Fetch JSON Data.

```vue
<script setup>
import { onMunted, ref } from "vue";

const jobs = ref([]);

onMounted( async() => {
    try {
        const response = await fetch('http://localhost:8000/jobs');
        jobs.value = await response.data;
    } catch (error) {
        console.error('Error fetching jobs', error);
    }
})
</script>

<template>
<JobListing v-for="job in jobs" :key="job.id" :job="job" />
</template>
```

#### How to Fetch JSON data with help of `axios` library.

```vue
<script setup>
import { onMounted, ref } from "vue";
import axios from 'axios';

const jobs = ref([])

onMounted( async() => {
    try {
        const response = await axios.get('http://localhost:8000/jobs');
        jobs.value = response.data
    } catch (error) {
        console.error('Error fetching jobs', error);
    }
})
</script>

<template>
<JobListing v-for="job in jobs" :key="job.id" :job="job" />
</template>
```
