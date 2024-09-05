<script setup>
import { ref, onMounted } from 'vue';
import NavItem from '@/components/NavItem.vue'; // 假设你创建了一个名为NavItem的组件

const navItems = ref([]);
const showSubNavIndex = ref(null);

onMounted(async () => {
  const response = await fetch('https://raw.githubusercontent.com/mxrain/indexNav/main/src/assets/data/data.json'); // 获取JSON数据
  navItems.value = await response.json();
});

const showSubNav = (index) => {
  showSubNavIndex.value = index;
};

const hideSubNav = () => {
  showSubNavIndex.value = null;
};
</script>

<template>
   <nav class="nav">
    <ul v-if="navItems.length">
      <li v-for="(item, index) in navItems" :key="index">
        <a :href="item.link" @mouseenter="showSubNav(index)" @mouseleave="hideSubNav">
          {{ item.title }}
        </a>
        <nav-item v-if="item.children && showSubNavIndex === index" :nav-items="item.children"></nav-item>
      </li>
    </ul>
  </nav>
</template>


<style scoped>
.nav {
  position: relative;
}

.nav li {
  list-style: none;
  display: inline-block;
  margin-right: 20px;
}

.nav li a {
  text-decoration: none;
  color: #333;
}

.nav li a:hover {
  color: #007bff;
}

.nav li nav-item {
  position: absolute;
  top: 100%;
  left: 0;
  background-color: #fff;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 10px;
  z-index: 1;
  display: none; /* 默认隐藏 */
}

.nav li nav-item.show {
  display: block;
}
</style>