<script setup>
import { ref,onMounted } from 'vue'

const data = ref([])
onMounted(async ()=>{
  const res = await fetch(
    'https://raw.githubusercontent.com/mxrain/indexNav/main/src/assets/data/data.json'
  );
  data.value = await res.json()
})
</script>

<template>
  <main>
    {{data}}
  </main>
</template>
