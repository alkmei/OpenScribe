<script setup lang="ts">
import TextEditor from '../components/TextEditor.vue'
import {
  ResizableHandle,
  ResizablePanel,
  ResizablePanelGroup,
} from '@/components/ui/resizable'
import { ref } from 'vue'

const content = ref('')
</script>

<template>
  <div class="h-screen flex flex-col">
    <ResizablePanelGroup direction="horizontal">
      <ResizablePanel>
        <div class="p-2 font-bold bg-gray-100">File Explorer</div>
        <div class="flex-grow overflow-auto">
          File explorer content goes here
        </div>
      </ResizablePanel>
      <ResizableHandle class="hover:bg-blue-300" />
      <ResizablePanel>
        <ResizablePanelGroup direction="vertical">
          <ResizablePanel class="flex flex-col">
            <div class="p-2 font-bold bg-gray-100">Editor</div>
            <div class="flex-grow overflow-auto">
              <TextEditor v-model="content" class="h-full" />
            </div>
          </ResizablePanel>
          <ResizableHandle class="hover:bg-blue-300" />
          <ResizablePanel>
            <div class="p-2 font-bold bg-gray-100">Metadata</div>
            <div class="flex-grow overflow-auto p-2">{{ content }}</div>
          </ResizablePanel>
        </ResizablePanelGroup>
      </ResizablePanel>
    </ResizablePanelGroup>
  </div>
</template>
