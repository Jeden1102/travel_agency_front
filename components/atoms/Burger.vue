<template>
  <button class="z-20 space-y-2 lg:hidden" @click="() => emits('onClick')">
    <span
      class="block h-0.5 w-6 bg-gray-600 transition-transform"
      :class="{ 'translate-y-[10px] rotate-45': isMenuToggled }"
    ></span>
    <span
      class="block h-0.5 w-6 bg-gray-600 transition-transform"
      :class="{ '-rotate-45': isMenuToggled }"
    ></span>
    <span
      class="block h-0.5 w-4 bg-gray-600 transition-all"
      :class="{ 'translate-x-full opacity-0': isMenuToggled }"
    ></span>
  </button>
</template>

<script setup lang="ts">
  import { defineEmits, defineProps } from 'vue'

  const emits = defineEmits(['onClick'])

  const props = defineProps<{
    isMenuToggled: boolean
  }>()
</script>
