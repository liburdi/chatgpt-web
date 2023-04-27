<script setup lang='ts'>
import { ref } from 'vue'
interface Emit {
  (e: 'click'): void
}

const emit = defineEmits<Emit>()
const open = ref(false)

function handleClick() {
  emit('click')
}
</script>

<template>
  <button
    v-if="open"
    class="flex items-center justify-center w-10 h-10 transition rounded-full hover:bg-neutral-100 dark:hover:bg-[#414755]"
    @click="handleClick"
  >
    <slot />
  </button>
</template>
