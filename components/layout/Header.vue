<template>
    <header class="container-custom py-4 flex justify-between lg:items-center lg:gap-4">
        <img class="z-30 h-fit" src="@/assets/images/logo.png" alt="Page logo" width="167" height="32">

        <AtomsInput placeholder="Search..." custom-class="hidden lg:block lg:w-fit xl:ml-8" />
        <AtomsBurger :onClick="() => { isMenuToggled = !isMenuToggled }" :is-menu-toggled="isMenuToggled" />

        <div class="flex absolute top-0 flex-col transition-all w-full h-full z-10 bg-white pt-20 gap-4 lg:static lg:flex-row lg:pt-0 lg:items-center lg:justify-between"
            :class="{
                '-left-full': !isMenuToggled,
                'left-0': isMenuToggled,
            }">
            <nav class="flex flex-col gap-2 px-4 lg:flex-row xl:gap-8">
                <AtomsInput placeholder="Search..." custom-class="block lg:hidden" />
                <NuxtLink class="text-2xl transition-opacity hover:opacity-60 lg:text-sm lg:hidden xl:block" to="/">{{
                    $t('home') }}
                </NuxtLink>
                <div class="flex flex-col">
                    <NuxtLink class="text-2xl transition-opacity hover:opacity-60 lg:text-sm" to="/">{{ $t('explore') }}
                    </NuxtLink>
                    <p class="mobile-only text-gray-500">{{ $t('menu.explore') }}</p>
                </div>
                <div class="flex flex-col">
                    <NuxtLink class="text-2xl transition-opacity hover:opacity-60 lg:text-sm" to="/">{{ $t('our_offer') }}
                    </NuxtLink>
                    <p class="mobile-only text-gray-500">{{ $t('menu.offer') }}</p>
                </div>
                <NuxtLink class="text-2xl transition-opacity hover:opacity-60 lg:text-sm" to="/">{{ $t('destination_map') }}
                </NuxtLink>
            </nav>

            <div
                class="flex mt-8 flex-col px-4 border-t pt-4 lg:flex-row-reverse lg:mt-0 lg:pt-0 lg:border-0 lg:items-center lg:gap-2 xl:gap-6">
                <div class="flex w-full justify-between lg:gap-2 xl:gap-6">
                    <button>{{ $t('sign_up') }}</button>
                    <NuxtLink class="atoms-button w-fit " to="/">{{ $t('log_in') }}</NuxtLink>
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
</script>