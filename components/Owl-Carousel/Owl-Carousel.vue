<script setup lang="ts">
import OwlMenu from '~/data/OwlData';

const owlMenu = ref(OwlMenu);


</script>
<template>
    <div class="lg:w-[98%] 2xl:w-[65%] lg:ml-[1%] 2xl:ml-[17%] mt-10">
        <Carousel class="w-full" :opts="{align: 'start',}">
            <CarouselContent class="-ml-1">
                <CarouselItem v-for="item in owlMenu" class="pl-1 max-md:basis-1/4 md:basis-1/6 lg:basis-[10%]">
                    <div class="">
                    <div>
                        <div class="flex items-center justify-center flex-col">
                        <div class="rounded-full"  style="border: 1px solid #e6e6e6">
                            <img :src="item.image" class="w-[50px] h-[50px] rounded m-2"/>
                        </div>
                        <p class="text-xs mt-1">{{ item.title }}</p>
                        </div>
                    </div>
                    </div>
                </CarouselItem>
            </CarouselContent>
            <CarouselNext class="max-md:right-1" />
            <CarouselPrevious class="max-md:left-1" />
        </Carousel>
    </div>
</template>
