<script setup lang="ts">
import Product from '~/data/Product';
import { ref, onMounted } from "vue";
import { watchOnce } from '@vueuse/core';
import { Carousel, type CarouselApi, CarouselContent, CarouselItem, CarouselNext, CarouselPrevious } from '@/components/ui/carousel';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';


const route = useRoute()
const products = ref(Product);
const productSeller = ref([
    { 
        title: "Trendyol1",
        point: "9.4",
        price: "254"
    },
    {
        title: "Trendyol2",
        point: "7.6",
        price: "150"
    }
]); 

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
    <div style="font-family: 'Poppins', sans-serif;">
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
                        <span class="text-sm">{{ getProduct(Number(route.params.id)).star }} 
                            <Icon v-for="(_, index2) in getFillStarNumber(getProduct(Number(route.params.id)).star)" name="material-symbols:star" class="size-3 ml-1 mb-1 text-yellow-400"/>
                            <Icon v-for="(_, index3) in getEmptyStarNumber(getProduct(Number(route.params.id)).star)" name="material-symbols:star-outline" class="size-3 ml-1 mb-1 text-gray-400"/>
                        </span>
                        <span class="ml-2 text-[10px]">{{ getProduct(Number(route.params.id)).rating }} Değerlendirme
                            <Icon name="streamline:image-camera-tripod-tripod-photos-picture-camera-photography-photo-pictures" class="size-4 ml-1 mb-1 text-blue-300" />
                        </span>
                        <span class="ml-2 text-[10px]">{{ getProduct(Number(route.params.id)).questions }} Soru & Cevap
                            <Icon name="mdi:frequently-asked-questions" class="size-4 ml-1 " />
                        </span>
                        <span class="ml-2 text-[10px]">{{ getProduct(Number(route.params.id)).favorite }} Favoriler
                            <Icon name="material-symbols:bookmark-heart-outline" class="size-5 ml-1 text-orange-400" />
                        </span>
                    </div>
                    <div class="mt-4">
                        <span class="text-xl font-medium" style="color: #f27a1a">{{getProduct(Number(route.params.id)).price}} TL</span>
                    </div>
                    <hr class="mt-6 w-11/12"/>
                    <div class="mt-3">
                        <div class="flex justify-around w-full h-[70px] border border-gray-200 fixed left-0 bottom-0 bg-white items-center lg:hidden z-20">
                            <span class="text-xl font-medium" style="color: #f27a1a">{{getProduct(Number(route.params.id)).price}} TL</span>
                            <Button variant="secondary" class="bg-orange-400 text-white w-9/12">Sepete Ekle</Button>
                        </div>
                        <Button variant="secondary" class="bg-orange-400 text-white w-9/12 max-lg:hidden">Sepete Ekle</Button>
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
                <div class="max-lg:basis-[97%]  max-lg:mt-10 max-lg:ml-[2%] lg:basis-1/5">
                    <div class="border border-gray-300 p-3 rounded">
                        <div class="flex flex-col bg-blue-100 p-3">
                            <span class="text-sm font-medium text-blue-500">Trendyol Mağaza<span class="text-xs ml-2 bg-green-400 px-2 py-1 text-white rounded">9.2</span></span>
                            <span class="text-xs">533,4B Takipçi</span>
                        </div>
                        <div class="flex flex-col text-xs font-medium mt-1">
                            <span class="flex items-center"><div class="border p-3 m-2 bg-gray-200 rounded"></div>Takip Et Kazan</span>
                            <span class="flex items-center"><div class="border p-3 m-2 bg-gray-200 rounded"></div>Satıcı Soruları</span>
                        </div>
                        <div class="w-full flex justify-center relative top-2 h-4">
                            <Button  variant="secondary" class="rounded-3xl tracking-wider text-[#333333]">Mağazaya Git</Button>
                        </div>
                    </div>
                    <div class="w-full bg-[#FEF4EB] mt-10 p-3 rounded cursor-pointer">
                        <Icon name="bxs:add-to-queue" class="size-6 mr-2 bg-orange-300 text-white" />
                        <span class="text-[#333333] text-xs font-medium">Koleksiyona Ekle</span>
                    </div>
                </div>
            </div>
        </div>
        <diV>
                <LazyCarouselTrend class="bg-[#ffffff]" title="Benzer Ürünler" />
        </diV>
        <diV>
                <LazyCarouselTrend class="bg-[#ffffff]" title="Bu Ürünü Alanlar Bunları da Aldı" />
        </diV>
        <div class="lg:w-[98%] 2xl:w-[65%] lg:ml-[1%] 2xl:ml-[17%] mt-10 pl-7">
            <p class="font-semibold text-base">Ürünün Diğer Satıcıları ( {{ productSeller.length }} )</p>
            <div class="flex flex-wrap mt-5">
                <div v-for="item of productSeller" class=" max-md:basis-[97%] basis-[47%] mr-[1%] border border-gray-300 rounded-md flex justify-between items-center mt-2">
                    <div class="flex flex-col p-3 w-1/2">
                            <span class="text-sm font-medium text-blue-500 m-1">{{ item.title }}<span class="text-xs ml-2 bg-green-400 px-2 py-1 text-white rounded">{{item.point}}</span></span>
                            <span class="text-xs m-1 font-medium">Tahmini Kargoya Teslim: 1 gün içinde</span>
                            <span class="text-xs text-gray-400 m-1 font-medium">Kargo Bedava</span>
                    </div>
                    <div>
                        <span class="mr-2 font-medium text-[#f27a1a]">{{ item.price }} TL</span>
                        <Button variant="secondary" class="bg-[#f27a1a] text-white mr-2">Ürüne Git</Button>
                    </div>
                </div>
            </div>
        </div>
        <div class="h-24"></div>
    </div>
    <TrendFooter />
</template>