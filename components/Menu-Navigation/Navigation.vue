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
import Menu from '~/data/Menu';
import { reactive , ref , watch } from "vue";
import ChildMenu from '~/data/ChildMenu';

const components = ref(Menu);
const childMenu = ref(ChildMenu);
const api = ref<CarouselApi>()
const totalCount = ref(0)
const current = ref(0)

function setApi(val: CarouselApi) {
  api.value = val
}

function getChildMenu(menuId: number) {
  return childMenu.value.filter(item => item.menuId === menuId);
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
          <CarouselItem v-for="item of components" :key="item.title" class="max-2xl:basis-[20%] 2xl:basis-[14%] max-sm:basis-[25%]">
          <NavigationMenuItem class="block">
            <NavigationMenuTrigger class="w-full text-[12px] font-normal">{{ item.title }}</NavigationMenuTrigger>
            <NavigationMenuContent class="w-full max-lg:hidden">
                <ul class="flex flex-wrap gap-3 p-7 w-full">
                <li v-for="child of getChildMenu(item.menuId)" class="row-span-3 lg:basis-[19%]">
                  <NavigationMenuLink as-child>
                    <a
                      class="flex h-full w-full select-none flex-col justify-end rounded-md bg-gradient-to-b from-muted/50 to-muted p-6 no-underline outline-none focus:shadow-md"
                      :href="child.href"
                    >
                      <img src="https://www.radix-vue.com/logo.svg" class="h-6 w-6">
                      <div class="mb-2 mt-4 text-lg font-medium">
                        {{ child.title }}
                      </div>
                      <p class="text-sm leading-tight text-muted-foreground">
                        {{child.description}}
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