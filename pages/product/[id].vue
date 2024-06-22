<script setup lang="ts">
import Product from '~/data/Product';
import { ref, onMounted } from "vue";
import { watchOnce } from '@vueuse/core';
import { Carousel, type CarouselApi, CarouselContent, CarouselItem, CarouselNext, CarouselPrevious } from '@/components/ui/carousel';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';


const route = useRoute()
const products = ref(Product);

function controlProduct() {
    if(products.value.filter(x => x.id == Number(route.params.id)).length === 0) {
        return navigateTo('/404');
    }
}
onMounted(() => { 
    controlProduct();
})
function getFillStarNumber(number: number) {
    return Math.floor(number);
}

function getEmptyStarNumber(number: number) {
    let num = Math.floor(5-number);
    if(num === 0) {
        num = 1;
    }
    return num;
}

function getProduct(value: number) {
    return products.value[value-1];
}

const emblaMainApi = ref<CarouselApi>()
const emblaThumbnailApi = ref<CarouselApi>()
const selectedIndex = ref(0)

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

</script>
<template>
    <Navbar />
    <div class="lg:w-[98%] 2xl:w-3/5 lg:ml-[1%] 2xl:ml-[20%] mt-10">
        <div class="flex flex-wrap">
            <div class="max-lg:basis-[98%] max-lg:ml-[1%] lg:basis-[30%]">
            <LazyProductCarousel :id="route.params.id" class="max-lg:max-w-full" itemclass="max-lg:max-w-full" />
            </div>
            <div class="max-lg:basis-[97%] max-lg:relative max-lg:left-[2%] max-lg:top-3 lg:basis-[50%]"> 
                <div>
                    <span><bold class="font-medium">{{ getProduct(Number(route.params.id)).title }}</bold> {{ getProduct(Number(route.params.id)).description }}</span>
                </div>
                <div class="flex items-center mt-4">
                    <span>{{ getProduct(Number(route.params.id)).star }} 
                        <Icon v-for="(_, index2) in getFillStarNumber(getProduct(Number(route.params.id)).star)" name="material-symbols:star" class="size-3 ml-1 mb-1 text-yellow-400"/>
                        <Icon v-for="(_, index3) in getEmptyStarNumber(getProduct(Number(route.params.id)).star)" name="material-symbols:star-outline" class="size-3 ml-1 mb-1 text-gray-400"/>
                    </span>
                    <span class="ml-2 text-xs">{{ getProduct(Number(route.params.id)).rating }} Değerlendirme</span>
                    <span class="ml-2 text-xs">{{ getProduct(Number(route.params.id)).questions }} Soru & Cevap</span>
                    <span class="ml-2 text-xs">{{ getProduct(Number(route.params.id)).favorite }} Favoriler</span>
                </div>
                <div class="mt-4">
                    <span class="text-xl font-medium" style="color: #f27a1a">{{getProduct(Number(route.params.id)).price}} TL</span>
                </div>
                <hr class="mt-6"/>
                <div class="mt-3">
                    <Button variant="secondary" class="bg-orange-400 text-white w-9/12">Sepete Ekle</Button>
                    <div class="bg-green-100 w-11/12 rounded text-xs text-center h-7 flex justify-center items-center mt-3">
                        <p>9 saat 18 dakika içinde sipariş verirsen <span class="font-medium">en geç yarın</span> kargoda!</p>
                    </div>
                    <div class="mt-3">
                        <p class="font-medium">Kuponlar</p>
                        <div class="flex">
                            <div class="w-[150px] h-[75px] bg-orange-100 flex justify-center items-center mt-3 rounded font-medium border border-orange-200">%10</div>
                            <div class="w-[150px] h-[75px] bg-orange-100 flex justify-center items-center mt-3 ml-2 rounded font-medium border border-orange-200">%15</div>
                        </div>
                    </div>
                    <div class="mt-7">
                        <p class="font-medium">Öne Çıkan Özellikler</p>
                        <ul class="list-disc list marker:text-orange-400 ml-8 text-sm mt-4">
                            <li><span>Bu ürün Trendyol Mağaza tarafından gönderilecektir.</span></li>
                            <li><span>Kampanya fiyatından satılmak üzere 100 adetten fazla stok sunulmuştur.</span></li>
                            <li><span>İncelemiş olduğunuz ürünün satış fiyatını satıcı belirlemektedir.</span></li>
                            <li><span>Bir ürün, birden fazla satıcı tarafından satılabilir. Birden fazla satıcı tarafından satışa sunulan ürünlerin satıcıları ürün için belirledikleri fiyata, satıcı puanlarına, teslimat statülerine, ürünlerdeki promosyonlara, kargonun bedava olup olmamasına ve ürünlerin hızlı teslimat ile teslim edilip edilememesine, ürünlerin stok ve kategorileri bilgilerine göre sıralanmaktadır.</span></li>
                        </ul>
                    </div>
                </div>
            </div>
            <div class="basis-1/5">

            </div>
        </div>
    </div>
</template>