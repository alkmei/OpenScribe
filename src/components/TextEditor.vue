<template>
  <div class="flex flex-col">
    <EditorMenu :editor="editor" class="" />
    <div class="flex-grow bg-gray-400 overflow-hidden" id="editor-content">
      <EditorContent :editor="editor" class="h-full bg-white overflow-auto" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
#editor-content {
  overflow-x: hidden;
}
</style>

<script setup lang="ts">
import { useEditor, EditorContent } from '@tiptap/vue-3'
import Document from '@tiptap/extension-document'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'
import Bold from '@tiptap/extension-bold'
import Italic from '@tiptap/extension-italic'
import Heading from '@tiptap/extension-heading'
import { watch } from 'vue'
import EditorMenu from './EditorMenu.vue'
import History from '@tiptap/extension-history'

const props = defineProps({
  modelValue: {
    type: String,
    default: '',
  },
})

const emit = defineEmits(['update:modelValue'])

const editor = useEditor({
  content: '<p>Welcome to OpenScribe!</p>',
  extensions: [
    Document,
    Paragraph,
    Text,
    Bold,
    Italic,
    Heading.configure({
      levels: [1, 2, 3],
    }),
    History,
  ],
  editorProps: {
    attributes: {
      class:
        'prose prose-sm sm:prose-base lg:prose-lg xl:prose-2xl m-5 focus:outline-none max-w-none h-full outline-none p-2',
    },
  },
  onUpdate: ({ editor }) => {
    emit('update:modelValue', editor.getHTML())
  },
})

watch(
  () => props.modelValue,
  newValue => {
    if (!editor.value) return
    const isSame = newValue === editor.value.getHTML()
    if (isSame) return

    editor.value.commands.setContent(newValue, false)
  },
)
</script>
