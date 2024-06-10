<script setup lang="ts">
import {
  NavigationMenu,
  NavigationMenuContent,
  NavigationMenuItem,
  NavigationMenuLink,
  NavigationMenuList,
  NavigationMenuTrigger,
  navigationMenuTriggerStyle,
} from '@/components/ui/navigation-menu';
import {
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselNext,
  CarouselPrevious,
} from '@/components/ui/carousel';
import { watchOnce } from '@vueuse/core';
import type { CarouselApi } from '@/components/ui/carousel';
const components: { title: string, href: string, description: string }[] = [
  {
    title: 'Kadın',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Erkek',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Anne & Çocuk',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Ev & Yaşam',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Süpermarket',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Kozmetik',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Moda',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Elektronik',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Çok Satanlar',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  },
  {
    title: 'Elektronik',
    href: '#',
    description:
      'Lorem İpsum Sit amet Dolor',
  }
]
const api = ref<CarouselApi>()
const totalCount = ref(0)
const current = ref(0)

function setApi(val: CarouselApi) {
  api.value = val
}

watchOnce(api, (api) => {
  if (!api)
    return

  totalCount.value = api.scrollSnapList().length
  current.value = api.selectedScrollSnap() + 1

  api.on('select', () => {
    current.value = api.selectedScrollSnap() + 1
  })
})
</script>
<template>
<NavigationMenu>
    <NavigationMenuList class="max-lg:mt-2">
      <Carousel :opts="{ align: 'start',}" @init-api="setApi" class="w-full">
        <CarouselContent>
          <CarouselItem v-for="item of components" :key="item.title" class="max-2xl:basis-[19%] 2xl:basis-[13%] max-sm:basis-[25%]">
          <NavigationMenuItem class="block">
            <NavigationMenuTrigger class="lg:w-full text-[12px]">{{ item.title }}</NavigationMenuTrigger>
            <NavigationMenuContent class="w-full">
                <ul class="grid gap-3 p-6 w-full lg:grid-cols-[minmax(0,.75fr)_minmax(0,1fr)]">
                <li class="row-span-3 w-full">
                  <NavigationMenuLink as-child>
                    <a
                      class="flex h-full w-full select-none flex-col justify-end rounded-md bg-gradient-to-b from-muted/50 to-muted p-6 no-underline outline-none focus:shadow-md"
                      :href="item.href"
                    >
                      <img src="https://www.radix-vue.com/logo.svg" class="h-6 w-6">
                      <div class="mb-2 mt-4 text-lg font-medium">
                        {{ item.title }}
                      </div>
                      <p class="text-sm leading-tight text-muted-foreground">
                        {{item.description}}
                      </p>
                    </a>
                  </NavigationMenuLink>
                </li>
            
                </ul>
            </NavigationMenuContent>
          </NavigationMenuItem>
        </CarouselItem>
      </CarouselContent>
    </Carousel>
    </NavigationMenuList>
  </NavigationMenu>
</template>