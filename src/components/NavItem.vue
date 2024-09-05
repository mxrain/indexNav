<template>
  <ul v-if="navItems.length">
    <li v-for="(item, index) in navItems" :key="index">
      <a :href="item.link" @mouseenter="showSubNav(index)" @mouseleave="hideSubNav">
        {{ item.title }}
      </a>
      <nav-item v-if="item.children && showSubNavIndex === index" :nav-items="item.children"></nav-item>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  navItems: {
    type: Array,
    required: true
  }
});

const showSubNavIndex = ref(null);

const showSubNav = (index) => {
  showSubNavIndex.value = index;
};

const hideSubNav = () => {
  showSubNavIndex.value = null;
};
</script>

<style scoped>
/* 这里可以添加NavItem组件的样式 */
</style>