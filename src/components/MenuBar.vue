<template>
  <div class="bg-gray-200 border-b border-gray-300">
    <div class="container px-4">
      <ul class="flex">
        <li v-for="(menu, index) in menus" :key="index" class="relative group">
          <button
            @click.stop="toggleMenu(index)"
            class="px-4 py-2 text-sm text-gray-700 hover:bg-gray-300 focus:outline-none focus:bg-gray-300"
          >
            {{ menu.label }}
          </button>
          <ul
            v-if="menu.isOpen"
            @click.stop
            class="absolute left-0 mt-1 w-48 bg-white border border-gray-300 rounded shadow-lg z-10"
          >
            <li v-for="(item, itemIndex) in menu.items" :key="itemIndex">
              <a
                href="#"
                @click.prevent="handleMenuItemClick(item)"
                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
              >
                {{ item.label }}
              </a>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const menus = ref([
  {
    label: 'File',
    isOpen: false,
    items: [
      { label: 'New', action: () => console.log('New file') },
      { label: 'Open', action: () => console.log('Open file') },
      { label: 'Save', action: () => console.log('Save file') },
    ],
  },
  {
    label: 'Edit',
    isOpen: false,
    items: [
      { label: 'Undo', action: () => console.log('Undo') },
      { label: 'Redo', action: () => console.log('Redo') },
      { label: 'Cut', action: () => console.log('Cut') },
      { label: 'Copy', action: () => console.log('Copy') },
      { label: 'Paste', action: () => console.log('Paste') },
    ],
  },
  {
    label: 'Help',
    isOpen: false,
    items: [
      { label: 'About', action: () => console.log('About') },
      { label: 'Documentation', action: () => console.log('Documentation') },
    ],
  },
])

const toggleMenu = index => {
  menus.value = menus.value.map((menu, i) => ({
    ...menu,
    isOpen: i === index ? !menu.isOpen : false,
  }))
}

const handleMenuItemClick = item => {
  item.action()
  closeAllMenus()
}

const closeAllMenus = () => {
  menus.value = menus.value.map(menu => ({ ...menu, isOpen: false }))
}

const handleOutsideClick = event => {
  if (!event.target.closest('.relative')) {
    closeAllMenus()
  }
}

onMounted(() => {
  window.addEventListener('click', handleOutsideClick)
})

onUnmounted(() => {
  window.removeEventListener('click', handleOutsideClick)
})
</script>
