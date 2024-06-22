<script setup lang="ts">
import Product from '~/data/Product';
import { cn } from '@/lib/utils'
import { ref, onMounted } from "vue";
import { watchOnce } from '@vueuse/core';
import { Carousel, type CarouselApi, CarouselContent, CarouselItem, CarouselNext, CarouselPrevious } from '@/components/ui/carousel';
import { Card, CardContent } from '@/components/ui/card';

const emblaMainApi = ref<CarouselApi>()
const emblaThumbnailApi = ref<CarouselApi>()
const selectedIndex = ref(0)
const products = ref(Product);

function onSelect() {
  if (!emblaMainApi.value || !emblaThumbnailApi.value)
    return
  selectedIndex.value = emblaMainApi.value.selectedScrollSnap()
  emblaThumbnailApi.value.scrollTo(emblaMainApi.value.selectedScrollSnap())
}

function onThumbClick(index: number) {
  if (!emblaMainApi.value || !emblaThumbnailApi.value)
    return
  emblaMainApi.value.scrollTo(index)
}

watchOnce(emblaMainApi, (emblaMainApi) => {
  if (!emblaMainApi)
    return

  onSelect()
  emblaMainApi.on('select', onSelect)
  emblaMainApi.on('reInit', onSelect)
})
function getProduct(value: number) {
    return products.value[value-1];
}
const props = defineProps(['id','class','itemclass']);

</script>
<template>
<Carousel :class="cn('relative w-full max-w-xs',props.class)" @init-api="(val) => emblaMainApi = val">
                <CarouselContent>
                    <CarouselItem v-for="(_, index) in 3" :key="index">
                    <div class="p-1">
                        <Card>
                        <CardContent class="flex aspect-square items-center justify-center p-6">
                            <img :src="getProduct(Number(props.id)).image" />
                        </CardContent>
                        </Card>
                    </div>
                    </CarouselItem>
                </CarouselContent>
                <CarouselPrevious class="left-3"/>
                <CarouselNext  class="right-3"/>
            </Carousel>
            <Carousel :class="cn('relative w-full max-w-xs',props.itemclass)" @init-api="(val) => emblaThumbnailApi = val">
                <CarouselContent class="flex gap-1 ml-0">
                    <CarouselItem v-for="(_, index) in 3" :key="index" class="pl-0 basis-1/3 cursor-pointer" @click="onThumbClick(index)">
                    <div class="p-1" :class="index === selectedIndex ? '' : 'opacity-50'">
                        <Card>
                        <CardContent class="flex aspect-square items-center justify-center p-6">
                            <img :src="getProduct(Number(props.id)).image" />
                        </CardContent>
                        </Card>
                    </div>
                    </CarouselItem>
                </CarouselContent>
            </Carousel>
</template>