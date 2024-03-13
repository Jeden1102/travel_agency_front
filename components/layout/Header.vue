<template>
    <header class="container py-4 flex justify-between">
        <img src="@/assets/images/logo.png" alt="Page logo" width="167" height="32">
        <input type="text" placeholder="Search..." class="hidden md:block">
        <AtomsBurger :onClick="() => { isMenuToggled = !isMenuToggled }" :is-menu-toggled="isMenuToggled" />
        <div class="flex absolute top-0 flex-col transition-all w-full h-full z-10 bg-white justify-center gap-4" :class="{
            '-left-full': !isMenuToggled,
            'left-0': isMenuToggled,
        }">
            <nav class="flex flex-col gap-2 px-4">
                <input type="text" id="first_name"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary focus:border-primary block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary dark:focus:border-primary"
                    placeholder="Search..." required />
                <NuxtLink class="text-2xl transition-opacity hover:opacity-60" to="/">Home</NuxtLink>
                <div class="flex flex-col">
                    <NuxtLink class="text-2xl transition-opacity hover:opacity-60" to="/">Explore</NuxtLink>
                    <p class="mobile-only text-gray-500">Explore best destinations we offer.</p>
                </div>
                <div class="flex flex-col">
                    <NuxtLink class="text-2xl transition-opacity hover:opacity-60" to="/">Our offer</NuxtLink>
                    <p class="mobile-only text-gray-500">Checkout our offer.</p>
                </div>
                <NuxtLink class="text-2xl transition-opacity hover:opacity-60" to="/">Destination map</NuxtLink>

            </nav>
            <div class="flex mt-8 flex-col px-4 border-t pt-4">
                <div class="flex w-full justify-between">
                    <button>Sign up</button>
                    <NuxtLink class="atoms-button w-fit " to="/">Log in</NuxtLink>
                </div>
                <button>EN</button>
            </div>
            <div class="bg-primary bg-opacity-80 text-white absolute bottom-0 w-full p-2 flex flex-col">
                <a>
                    <Icon name="material-symbols:alternate-email-rounded" />
                    contact@viatours.com
                </a>
                <a>
                    <Icon name="material-symbols:call-outline" />
                    (80) 123 123 123
                </a>
            </div>
        </div>
    </header>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const isMenuToggled = ref(false);
</script>