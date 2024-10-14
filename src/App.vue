<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import MenuBar from './components/MenuBar.vue'
</script>

<template>
  <div class="flex flex-col h-screen">
    <MenuBar class="flex-shrink-0" />
    <RouterView class="flex-grow overflow-auto" />
  </div>
</template>
