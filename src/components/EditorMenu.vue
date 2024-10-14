<script setup lang="ts">
import { IconBold, IconH1, IconH2, IconH3, IconItalic } from '@tabler/icons-vue'
import { Editor } from '@tiptap/vue-3'

defineProps<{ editor: Editor | undefined }>()
</script>

<template>
  <div class="border-b flex gap-2">
    <div class="flex after:border-l">
      <div class="flex gap-2 p-1">
        <button
          @click="editor?.chain().focus().toggleBold().run()"
          class="p-1 rounded hover:bg-gray-200"
          :class="{ 'bg-gray-200': editor?.isActive('bold') }"
        >
          <IconBold />
        </button>
        <button
          @click="editor?.chain().focus().toggleItalic().run()"
          class="p-1 rounded hover:bg-gray-200"
          :class="{ 'bg-gray-200': editor?.isActive('italic') }"
        >
          <IconItalic />
        </button>
      </div>
    </div>

    <div class="flex">
      <div class="flex gap-2 p-1">
        <button
          @click="editor?.chain().focus().toggleHeading({ level: 1 }).run()"
          class="p-1 rounded hover:bg-gray-200"
          :class="{
            'bg-gray-200': editor?.isActive('heading', { level: 1 }),
          }"
        >
          <IconH1 />
        </button>
        <button
          @click="editor?.chain().focus().toggleHeading({ level: 2 }).run()"
          class="p-1 rounded hover:bg-gray-200"
          :class="{
            'bg-gray-200': editor?.isActive('heading', { level: 2 }),
          }"
        >
          <IconH2 />
        </button>
        <button
          @click="editor?.chain().focus().toggleHeading({ level: 3 }).run()"
          class="p-1 rounded hover:bg-gray-200"
          :class="{
            'bg-gray-200': editor?.isActive('heading', { level: 3 }),
          }"
        >
          <IconH3 />
        </button>
      </div>
    </div>
  </div>
</template>
