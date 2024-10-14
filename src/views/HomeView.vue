<script setup lang="ts">
import TextEditor from '../components/TextEditor.vue'
import { Splitpanes, Pane } from 'splitpanes'
import 'splitpanes/dist/splitpanes.css'

import { ref } from 'vue'

const content = ref('')
</script>

<template>
  <div class="h-screen flex flex-col">
    <Splitpanes class="flex-grow overflow-hidden">
      <Pane class="flex flex-col" size="20">
        <div class="p-2 font-bold bg-gray-100">File Explorer</div>
        <div class="flex-grow overflow-auto">
          <!-- File explorer content goes here -->
        </div>
      </Pane>
      <Pane class="flex flex-col">
        <Splitpanes horizontal class="flex-grow">
          <Pane class="flex flex-col">
            <div class="p-2 font-bold bg-gray-100">Editor</div>
            <div class="flex-grow overflow-auto">
              <TextEditor v-model="content" class="h-full" />
            </div>
          </Pane>
          <Pane class="flex flex-col" size="30">
            <div class="p-2 font-bold bg-gray-100">Metadata</div>
            <div class="flex-grow overflow-auto p-2">{{ content }}</div>
          </Pane>
        </Splitpanes>
      </Pane>
    </Splitpanes>
  </div>
</template>

<style lang="scss">
.splitpanes {
  &__splitter {
    position: relative;
    background-color: #ccc;
    &:hover {
      background-color: #00f;
      transition: background-color 0.5s ease;
    }
  }

  &__splitter:before {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    transition: 0.4s;
  }
  &--vertical > &__splitter:before {
    left: -10px;
    right: -10px;
  }
  &--horizontal > &__splitter:before {
    top: -10px;
    bottom: -10px;
  }
}
</style>
