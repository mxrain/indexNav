<script setup>
import { ref,onMounted } from 'vue'
import BookmarkItem from '@/components/BookmarkItem.vue'; // 导入 BookmarkItem 组件
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
    <BookmarkItem :bookmarks="data" />
  </main>
</template>
