<template>
    <div class="relative">
        <div class="flex items-center space-x-2">
            <label v-for="lang in languages" :key="lang.value" class="cursor-pointer">
                <input type="radio" :value="lang.value" v-model="locale" class="hidden">
                <div
                    :class="{ 'bg-white bg-opacity-20 hover:bg-opacity-30 text-primary font-semibold px-3 py-1 rounded lg:px-0': locale === lang.value, 'text-gray-400 bg-opacity-10 hover:bg-opacity-20': locale !== lang.value }">
                    {{ lang.label }}
                </div>
            </label>
        </div>
    </div>
</template>

<script setup lang="ts">
const { locale } = useI18n()

const languages = ref([
    { label: 'EN', value: 'en' },
    { label: 'PL', value: 'pl' }
]);
</script>