<script setup lang="ts">
import { cn } from '@/lib/utils'
import Product from '~/data/Product';

import { reactive , ref } from "vue";

const products = ref(Product);

function getProduct(number: number) {
    return products.value[number];
}

function getFillStarNumber(number: number) {
    return Math.floor(products.value[number].star);
}
function getEmptyStarNumber(number: number) {
    let num = Math.floor(5-products.value[number].star);
    if(num === 0) {
        num = 1;
    }
    return num;
}

function navigateProduct(value: number) {
    return navigateTo('/product/'+value);
}

const props = defineProps(['class','title','tcolor']);

</script>
<template>
    <div :class="cn('lg:w-[98%] 2xl:w-[65%] lg:ml-[1%] 2xl:ml-[17%] p-7 mt-10 rounded-lg',props.class)">
        <h4 :class="cn('mb-5 font-semibold text-lg',props.tcolor)">{{ props.title }}</h4>
        <Carousel class="relative w-full" :opts="{align: 'start'}">
            <CarouselContent>
            <CarouselItem v-for="(_, index) in 10" class="max-md:basis-1/2 md:basis-1/3 lg:basis-1/5 cursor-pointer" @click="navigateProduct(getProduct(index).id)">
                <div class="p-1 bg-white" style="border: 1px solid #e6e6e6;box-shadow: 0 2px 10px 1px rgba(0, 0, 0, 0.05) !important;border-radius: 6px;">
                <div>
                    <div class="flex justify-center w-full h-[225px]">
                        <img :src="getProduct(index).image" :alt="getProduct(index).title" class="w-[150px] h-[220px]">
                    </div>
                    <div class="flex flex-col p-1">
                    <span class="text-sm font-semibold max-lg:line-clamp-1 lg:line-clamp-2">{{ getProduct(index).title }}<span class="text-xs ml-1" style="font-weight: 400 !important;">{{ getProduct(index).description }}</span></span>
                    <div class="mt-1">
                        <span>{{ getProduct(index).star }}</span>
                        <Icon v-for="(_, index2) in getFillStarNumber(index)" name="material-symbols:star" class="size-3 ml-1"/>
                        <Icon v-for="(_, index3) in getEmptyStarNumber(index)" name="material-symbols:star-outline" class="size-3 ml-1"/>
                    </div>
                    <div class="mt-1">
                        <span class="font-medium text-sm" style="color:#f27a1a">{{ getProduct(index).price }} TL</span>
                    </div>
                    </div>
                </div>
                </div>
            </CarouselItem>
            </CarouselContent>
            <CarouselPrevious />
            <CarouselNext />
        </Carousel>
    </div>
</template>