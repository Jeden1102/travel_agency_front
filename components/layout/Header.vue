<template>
    <header class="container-custom py-4 flex justify-between lg:items-center lg:gap-4">
        <img class="h-fit" src="@/assets/images/logo.png" alt="Page logo" width="167" height="32">
        <AtomsInput placeholder="Search..." custom-class="hidden lg:block lg:w-fit xl:ml-8" />
        <AtomsBurger :onClick="toggleMenu" :is-menu-toggled="isMenuToggled" />

        <div class="flex absolute top-0 flex-col transition-all duration-300 w-full h-full z-10 bg-white pt-20 gap-4 lg:static lg:flex-row lg:pt-0 lg:items-center lg:justify-between"
            :class="{
                '-left-full': !isMenuToggled || menuChild !== '',
                'left-0': isMenuToggled && menuChild === '',
            }">
            <MoleculesMainNav @menu-child-change="(menu) => menuChildChange(menu)" :menu-child="menuChild" />
            <div
                class="flex mt-8 flex-col gap-4 px-4 border-t pt-4 lg:flex-row-reverse lg:mt-0 lg:pt-0 lg:border-0 lg:items-center lg:gap-2 xl:gap-6">
                <div class="flex flex-col lg:flex-row w-full justify-between items-center lg:gap-2 xl:gap-6">
                    <button>{{ $t('sign_up') }}</button>
                    <span class="text-gray-400 mobile-only">-OR-</span>
                    <NuxtLink class="atoms-button w-full flex justify-center lg:w-fit" to="/">{{
                        $t('log_in') }}</NuxtLink>
                </div>
                <MoleculesLanguageSwitcher />
            </div>

            <MoleculesHeaderContact />
        </div>
    </header>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const isMenuToggled = ref(false);
const menuChild = ref("");

const menuChildChange = (menu: string) => {
    menuChild.value = menu;
}

const toggleMenu = () => {
    isMenuToggled.value = !isMenuToggled.value
    if (!isMenuToggled.value) {
        menuChild.value = "";
    }
}
</script>