<template>
  <div
    class="home-hero relative mx-auto flex min-h-[80vh] flex-col items-center justify-center px-8 py-20 text-white lg:gap-4 xl:w-11/12"
  >
    <img
      src="@/assets/images/home-hero.png"
      class="absolute left-0 top-0 -z-10 h-full w-full object-cover"
      alt="Beach image"
    />
    <h1 class="text-3xl font-bold lg:text-7xl">Your world of joy</h1>
    <p class="text-center xl:text-xl">
      From local escapes to far-flung adventures, find what makes you happy
      anytime, anywhere
    </p>
    <div>
      <VueDatePicker v-model="date" range />
    </div>
  </div>
</template>

<script setup lang="ts">
  import VueDatePicker from '@vuepic/vue-datepicker'
  import '@vuepic/vue-datepicker/dist/main.css'
  import { ref } from 'vue'

  const date = ref()
</script>

<style>
  .dp__theme_light {
    --dp-background-color: #fff;
    --dp-text-color: #212121;
    --dp-hover-color: #f3f3f3;
    --dp-hover-text-color: #212121;
    --dp-hover-icon-color: #959595;
    --dp-primary-color: #1976d2;
    --dp-primary-disabled-color: #6bacea;
    --dp-primary-text-color: #f8f5f5;
    --dp-secondary-color: #c0c4cc;
    --dp-border-color: #ddd;
    --dp-menu-border-color: #ddd;
    --dp-border-color-hover: #aaaeb7;
    --dp-disabled-color: #f6f6f6;
    --dp-scroll-bar-background: #f3f3f3;
    --dp-scroll-bar-color: #959595;
    --dp-success-color: #76d275;
    --dp-success-color-disabled: #a3d9b1;
    --dp-icon-color: #959595;
    --dp-danger-color: #ff6f60;
    --dp-marker-color: #ff6f60;
    --dp-tooltip-color: #fafafa;
    --dp-disabled-color-text: #8e8e8e;
    --dp-highlight-color: rgb(25 118 210 / 10%);
    --dp-range-between-dates-background-color: var(--dp-hover-color, #f3f3f3);
    --dp-range-between-dates-text-color: var(--dp-hover-text-color, #212121);
    --dp-range-between-border-color: var(--dp-hover-color, #f3f3f3);
  }
</style>
