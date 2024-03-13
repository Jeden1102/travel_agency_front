<template>
    <button class="space-y-2 z-20 lg:hidden" @click="() => emits('onClick')">
        <span class="block w-6 h-0.5 bg-gray-600 transition-transform"
            :class="{ 'rotate-45 translate-y-[10px]': isMenuToggled }"></span>
        <span class="block w-6 h-0.5 bg-gray-600 transition-transform" :class="{ '-rotate-45': isMenuToggled }"></span>
        <span class="block w-4 h-0.5 bg-gray-600 transition-all"
            :class="{ 'translate-x-full opacity-0': isMenuToggled }"></span>
    </button>
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from 'vue';

const emits = defineEmits(['onClick'])

const props = defineProps<{
    isMenuToggled: boolean;
}>()
</script>
