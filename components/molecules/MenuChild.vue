<template>
  <div>
    <h4
      v-if="selectedMenu"
      class="mb-3 mt-16 flex items-center gap-4 bg-gray-100 px-4 py-2 text-2xl shadow-sm lg:mt-0 lg:rounded-t-lg"
    >
      <Icon :name="selectedMenu.icon" />
      {{ selectedMenu.title }}
    </h4>
    <div class="flex flex-col px-4 md:flex-row lg:gap-16 lg:pb-4">
      <div class="flex flex-col" v-for="(items, label) in menuItems">
        <p
          class="lg:text-md w-fit text-lg font-semibold transition-opacity hover:opacity-60"
        >
          {{ formatMenuItem(label) }}
        </p>
        <p v-for="menuItem in items">
          {{ menuItem.attributes.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import { onMounted, ref, computed } from 'vue'
  import type {
    DestinationsResponse,
    Destination,
  } from '../../types/destination'

  const props = defineProps<{
    menuChild: string
  }>()

  const menuItems = ref({})

  const menuConfig = {
    explore: {
      title: 'Explore',
      icon: 'material-symbols:explore-outline',
    },
    our_offer: {
      title: 'Our offer',
      icon: 'bx:trip',
      fields: [
        { title: 'Special offers', query: '...' },
        { title: 'Vacation type', query: '...' },
        { title: 'Object type', query: '...' },
      ],
    },
  }

  const selectedMenu = computed(() => {
    if (!props.menuChild) return null
    return menuConfig[props.menuChild]
  })

  const formatMenuItem = (menuItem: string) => {
    return menuItem.replaceAll('_', ' ')
  }

  const fetchMenuItems = () => {
    if (props.menuChild === 'our_offer') {
      fetchOfferMenu()
    } else {
      fetchExploreMenu()
    }
  }

  const fetchExploreMenu = async () => {
    const graphql = useStrapiGraphQL()

    const res = (await graphql(`
      query {
        destinations {
          data {
            attributes {
              name
              continent
            }
          }
        }
      }
    `)) as DestinationsResponse

    if (!res) return
    const groupedItems = groupExploreItems(
      res.data.destinations.data as Destination[],
    )
    menuItems.value = groupedItems
  }

  const groupExploreItems = (destinations: Destination[]) => {
    const groupedItems: Record<string, Destination[]> = {}

    destinations.forEach((destination) => {
      const continent = destination.attributes.continent

      if (!(continent in groupedItems)) {
        groupedItems[continent] = []
      }

      groupedItems[continent].push(destination)
    })

    return groupedItems
  }

  const fetchOfferMenu = () => {
    console.log('offer')
  }

  onMounted(() => {
    if (!props.menuChild) return
    console.log('QUERY FOR', props.menuChild)
    fetchMenuItems()
  })

  watch(
    () => props.menuChild,
    () => {
      fetchMenuItems()
    },
  )
</script>

<style scoped></style>
