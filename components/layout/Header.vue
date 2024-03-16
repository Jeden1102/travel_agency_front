<template>
  <header
    class="container-custom flex justify-between py-4 lg:items-center lg:gap-4"
  >
    <img
      class="h-fit"
      src="@/assets/images/logo.png"
      alt="Page logo"
      width="167"
      height="32"
    />
    <AtomsInput
      placeholder="Search..."
      custom-class="hidden lg:block lg:w-fit xl:ml-8"
    />
    <AtomsBurger :onClick="toggleMenu" :is-menu-toggled="isMenuToggled" />

    <div
      class="absolute top-0 z-10 flex h-full w-full flex-col gap-4 bg-white pt-20 transition-all duration-300 lg:static lg:flex-row lg:items-center lg:justify-between lg:pt-0"
      :class="{
        '-left-full': !isMenuToggled || menuChild !== '',
        'left-0': isMenuToggled && menuChild === '',
      }"
    >
      <MoleculesMainNav
        @menu-child-change="(menu) => menuChildChange(menu)"
        :menu-child="menuChild"
      />
      <div
        class="mt-8 flex flex-col gap-4 border-t px-4 pt-4 lg:mt-0 lg:flex-row-reverse lg:items-center lg:gap-2 lg:border-0 lg:pt-0 xl:gap-6"
      >
        <div
          class="flex w-full flex-col items-center justify-between lg:flex-row lg:gap-2 xl:gap-6"
        >
          <button>{{ $t('sign_up') }}</button>
          <span class="mobile-only text-gray-400">-OR-</span>
          <NuxtLink
            class="atoms-button flex w-full justify-center lg:w-fit"
            to="/"
            >{{ $t('log_in') }}</NuxtLink
          >
        </div>
        <MoleculesLanguageSwitcher />
      </div>

      <MoleculesHeaderContact />
    </div>
  </header>
</template>

<script setup lang="ts">
  import { ref } from 'vue'

  const isMenuToggled = ref(false)
  const menuChild = ref('')

  const menuChildChange = (menu: string) => {
    menuChild.value = menu
  }

  const toggleMenu = () => {
    isMenuToggled.value = !isMenuToggled.value
    if (!isMenuToggled.value) {
      menuChild.value = ''
    }
  }
</script>
