<script setup lang="ts">
import { IconBold, IconH1, IconH2, IconH3, IconItalic } from '@tabler/icons-vue'
import { Editor } from '@tiptap/vue-3'
import { ToggleGroup, ToggleGroupItem } from '@/components/ui/toggle-group'

defineProps<{ editor: Editor | undefined }>()
</script>

<template>
  <div class="border-b flex divide-x">
    <ToggleGroup type="multiple" class="p-1">
      <ToggleGroupItem
        value="bold"
        :data-state="editor?.isActive('bold') ? 'on' : 'off'"
        @click="editor?.chain().focus().toggleBold().run()"
      >
        <IconBold />
      </ToggleGroupItem>
      <ToggleGroupItem
        value="italic"
        :data-state="editor?.isActive('italic') ? 'on' : 'off'"
        @click="editor?.chain().focus().toggleItalic().run()"
      >
        <IconItalic />
      </ToggleGroupItem>
    </ToggleGroup>

    <ToggleGroup type="single" class="p-1">
      <ToggleGroupItem
        value="h1"
        :data-state="editor?.isActive('heading', { level: 1 }) ? 'on' : 'off'"
        @click="editor?.chain().focus().toggleHeading({ level: 1 }).run()"
      >
        <IconH1 />
      </ToggleGroupItem>
      <ToggleGroupItem
        value="h2"
        :data-state="editor?.isActive('heading', { level: 2 }) ? 'on' : 'off'"
        @click="editor?.chain().focus().toggleHeading({ level: 2 }).run()"
      >
        <IconH2 />
      </ToggleGroupItem>
      <ToggleGroupItem
        value="h3"
        :data-state="editor?.isActive('heading', { level: 3 }) ? 'on' : 'off'"
        @click="editor?.chain().focus().toggleHeading({ level: 3 }).run()"
      >
        <IconH3 />
      </ToggleGroupItem>
    </ToggleGroup>
  </div>
</template>
