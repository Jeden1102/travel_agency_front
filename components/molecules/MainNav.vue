<template>
    <nav class="flex flex-col gap-2 px-4 lg:flex-row xl:gap-8 lg:py-4"
        @mouseleave="(event) => emits('menuChildChange', '')">
        <button v-if="menuChild !== ''" class="flex fixed top-6 left-4 z-50 text-primary font-semibold lg:hidden"
            @click="() => showChildMenu('')">
            <span>
                <Icon name="material-symbols:arrow-back-ios" />
            </span>
            <span>{{ $t('go_back') }}</span>
        </button>

        <AtomsInput placeholder="Search..." custom-class="block lg:hidden" />
        <NuxtLink class="text-xl transition-opacity hover:opacity-60 lg:text-sm lg:hidden xl:block" to="/">{{
            $t('home') }}
        </NuxtLink>
        <button @click="showChildMenu('explore')" @mouseenter="(event) => { hoverMenuItem(event, 'explore') }"
            @mouseleave="(event) => { handleMouseLeave(event) }" class="w-full flex items-center justify-between lg:w-fit">
            <div class="flex flex-col">
                <p class="text-xl w-fit transition-opacity hover:opacity-60 lg:text-sm">{{ $t('explore') }}
                </p>
                <p class="mobile-only text-gray-500 text-sm">{{ $t('menu.explore') }}</p>
            </div>
            <div class="mobile-only">
                <Icon name="material-symbols:arrow-forward-ios" />
            </div>
        </button>

        <button @click="showChildMenu('our_offer')" @mouseenter="(event) => { hoverMenuItem(event, 'our_offer') }"
            class="w-full flex items-center justify-between lg:w-fit">
            <div class="flex flex-col">
                <p class="text-xl w-fit transition-opacity hover:opacity-60 lg:text-sm">{{ $t('our_offer') }}
                </p>
                <p class="mobile-only text-gray-500 text-sm">{{ $t('menu.offer') }}</p>
            </div>
            <div class="mobile-only">
                <Icon name="material-symbols:arrow-forward-ios" />
            </div>
        </button>
        <NuxtLink class="text-xl transition-opacity hover:opacity-60 lg:text-sm" to="/">{{ $t('destination_map') }}
        </NuxtLink>

        <div :style="`${popoverLeft ? `left:${popoverLeft}px;` : ''} ${popoverHeight ? `height:${popoverHeight}px` : ''}`"
            class="fixed popover top-0 w-full h-full bg-white z-40 transition-all duration-300 px-4 pt-16 lg:absolute p-5 lg:rounded-xl lg:border lg:shadow-lg lg:w-[600px] lg:h-fit lg:left-0 lg:top-16"
            :class="{
                'right-0 opacity-100': menuChild !== '',
                '-right-full opacity-0': menuChild === '',
            }
                ">
            <div class="flex flex-col" v-for=" x  in  5 ">
                <p class="text-xl w-fit transition-opacity hover:opacity-60 lg:text-sm">Poland
                </p>
                <p class="mobile-only text-gray-500 text-sm">Europe</p>
            </div>
        </div>
    </nav>
</template>

<script setup lang="ts">
import { defineEmits, ref } from 'vue';

const emits = defineEmits(['menuChildChange'])

defineProps<{
    menuChild: string;
}>()

const showChildMenu = (menu: string) => {
    if (window.innerWidth > 991) return;
    emits('menuChildChange', menu)
}

const hoverMenuItem = (event: MouseEvent, menuName: string) => {
    if (!isDesktop()) return;
    const targetElement = event.target as HTMLElement;
    if (!targetElement) return;

    const popoverElement = document.querySelector(".popover") as HTMLElement | null;

    if (!popoverElement) return;

    popoverLeft.value = targetElement.getBoundingClientRect().left - (popoverElement.getBoundingClientRect().height / 2);
    popoverHeight.value = popoverElement.getBoundingClientRect().height;
    emits('menuChildChange', menuName);
};

const handleMouseLeave = (event) => {
    const element = event.currentTarget;
    const classes = element.classList;
    console.log(classes, element);
}
const isDesktop = () => {
    if (!window) return false
    return window.innerWidth > 991;
}

const popoverLeft = ref<number | null>(null)
const popoverHeight = ref<number | null>(null)
</script>