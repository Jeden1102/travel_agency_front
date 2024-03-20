<template>
  <nav
    class="flex flex-col gap-2 px-4 lg:flex-row lg:py-4 xl:gap-8"
    @mouseleave="() => emits('menuChildChange', '')"
  >
    <button
      v-if="menuChild !== ''"
      class="fixed left-4 top-6 z-50 flex font-semibold text-primary lg:hidden"
      @click="() => showChildMenu('')"
    >
      <span>
        <Icon name="material-symbols:arrow-back-ios" />
      </span>
      <span>{{ $t('go_back') }}</span>
    </button>

    <AtomsInput placeholder="Search..." custom-class="block mb-6 lg:hidden" />
    <NuxtLink
      @mouseenter="() => emits('menuChildChange', '')"
      class="text-xl transition-opacity hover:opacity-60 lg:hidden lg:text-sm xl:block"
      to="/"
      >{{ $t('home') }}
    </NuxtLink>
    <button
      @click="showChildMenu('explore')"
      @mouseenter="
        (event) => {
          hoverMenuItem(event, 'explore')
        }
      "
      class="flex w-full items-center justify-between lg:w-fit"
    >
      <div class="flex flex-col">
        <p class="w-fit text-xl transition-opacity hover:opacity-60 lg:text-sm">
          {{ $t('explore') }}
        </p>
        <p class="mobile-only text-sm text-gray-500">
          {{ $t('menu.explore') }}
        </p>
      </div>
      <div class="mobile-only">
        <Icon name="material-symbols:arrow-forward-ios" />
      </div>
    </button>

    <button
      @click="showChildMenu('our_offer')"
      @mouseenter="
        (event) => {
          hoverMenuItem(event, 'our_offer')
        }
      "
      class="flex w-full items-center justify-between lg:w-fit"
    >
      <div class="flex flex-col">
        <p class="w-fit text-xl transition-opacity hover:opacity-60 lg:text-sm">
          {{ $t('our_offer') }}
        </p>
        <p class="mobile-only text-sm text-gray-500">{{ $t('menu.offer') }}</p>
      </div>
      <div class="mobile-only">
        <Icon name="material-symbols:arrow-forward-ios" />
      </div>
    </button>
    <NuxtLink
      @mouseenter="() => emits('menuChildChange', '')"
      class="text-xl transition-opacity hover:opacity-60 lg:text-sm"
      to="/"
      >{{ $t('destination_map') }}
    </NuxtLink>

    <div
      :style="`${popoverLeft ? `left:${popoverLeft}px;` : ''} ${popoverHeight ? `height:${popoverHeight}px` : ''}`"
      class="popover fixed top-0 z-40 h-full w-full gap-4 bg-white transition-all duration-300 md:flex-row lg:absolute lg:left-0 lg:top-16 lg:h-fit lg:w-[600px] lg:rounded-xl lg:border lg:shadow-lg"
      :class="{
        'right-0 opacity-100': menuChild !== '',
        '-right-full opacity-0': menuChild === '',
      }"
    >
      <MoleculesMenuChild :menu-child="menuChild" />
    </div>
  </nav>
</template>

<script setup lang="ts">
  import { defineEmits, ref } from 'vue'

  const emits = defineEmits(['menuChildChange'])

  defineProps<{
    menuChild: string
  }>()

  const popoverLeft = ref<number | null>(null)
  const popoverHeight = ref<number | null>(null)

  const showChildMenu = (menu: string) => {
    if (window.innerWidth > 991) return
    emits('menuChildChange', menu)
  }

  const hoverMenuItem = (event: MouseEvent, menuName: string) => {
    if (!isDesktop()) return
    const targetElement = event.target as HTMLElement
    if (!targetElement) return

    const popoverElement = document.querySelector(
      '.popover',
    ) as HTMLElement | null

    if (!popoverElement) return

    console.log(popoverElement)

    popoverLeft.value =
      targetElement.getBoundingClientRect().left -
      popoverElement.getBoundingClientRect().width / 3
    emits('menuChildChange', menuName)
  }

  const isDesktop = () => {
    if (!window) return false
    return window.innerWidth > 991
  }
</script>
