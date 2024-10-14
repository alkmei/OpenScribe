<template>
  <div :class="{ 'ml-4': depth > 0 }">
    <div
      @click="toggleExpand"
      class="flex items-center cursor-pointer hover:bg-gray-100 py-1"
    >
      <span v-if="item.type === 'folder'" class="mr-1">
        {{ isExpanded ? '📂' : '📁' }}
      </span>
      <span v-else class="mr-1">📄</span>
      {{ item.name }}
    </div>
    <div v-if="isExpanded && item.children">
      <FileItem
        v-for="(child, index) in item.children"
        :key="index"
        :item="child"
        :depth="depth + 1"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
  depth: {
    type: Number,
    default: 0,
  },
})

const isExpanded = ref(false)

const toggleExpand = () => {
  if (props.item.type === 'folder') {
    isExpanded.value = !isExpanded.value
  }
}
</script>
