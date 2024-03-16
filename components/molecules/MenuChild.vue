<template>
  <div class="flex flex-col" v-for="x in 5">
    {{ menuChild }}
    <p class="w-fit text-xl transition-opacity hover:opacity-60 lg:text-sm">
      Poland
    </p>
    <p class="mobile-only text-sm text-gray-500">Europe</p>
  </div>
</template>

<script setup lang="ts">
  import { onMounted } from 'vue'

  const props = defineProps<{
    menuChild: string
  }>()

  const queries = {
    offer: [{ title: '', query: 'query desitionation..' }],
    our_offer: [
      { title: 'Offers', query: 'query offer..' },
      { title: 'Vacation types', query: 'query vacation-types...' },
    ],
  }

  onMounted(() => {
    console.log('QUERY FOR', props.menuChild)
  })

  watch(
    () => props.menuChild,
    (first, second) => {
      console.log(
        'Watch props.selected function called with args:',
        first,
        second,
      )
    },
  )
</script>

<style scoped></style>
