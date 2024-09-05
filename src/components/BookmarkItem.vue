<template>
    <ul>
      <li v-for="(item, index) in bookmarks" :key="index">
        <a :href="item.url" target="_blank">
          <img :src="item.icon" alt="图标">
          {{ item.name }}
        </a>
        <span v-if="item.description">{{ item.description }}</span>
        <ul v-if="item.children" class="nested">
          <BookmarkItem :bookmarks="item.children" />
        </ul>
      </li>
    </ul>
  </template>
  
  <script setup>
  import { ref, computed,defineComponent } from 'vue';
  
  // 这里假设 bookmarks 是从你的 JSON 文件中读取的
  const bookmarks = ref([
    // 你的 JSON 数据
  ]);
  
  // 递归组件
  const BookmarkItem = defineComponent({
    props: {
      bookmarks: {
        type: Array,
        required: true
      }
    },
    template: `
      <ul v-if="bookmarks.length > 0" class="nested">
        <li v-for="(item, index) in bookmarks" :key="index">
          <a :href="item.url" target="_blank">
            <img :src="item.icon" alt="图标">
            {{ item.name }}
          </a>
          <span v-if="item.description">{{ item.description }}</span>
          <BookmarkItem :bookmarks="item.children" />
        </li>
      </ul>
    `
  });
  </script>
  
  <style scoped>
  .nested {
    margin-left: 20px;
  }
  </style>