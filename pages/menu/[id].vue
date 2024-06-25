<script setup lang="ts">
import { ref, onMounted } from "vue";
import Menu from "~/data/Menu";


const route = useRoute();
const menu = ref(Menu);

function controlRoute() {
    console.log(route.params.id);
    if(menu.value.filter(res => res.title == route.params.id).length === 0) {
       return navigateTo('/404');
    }
}

onMounted(() => {
    controlRoute();
})
</script>
<template>
    <div style="font-family: 'Poppins', sans-serif;">
        <Navbar />
        <LazyOwlCarousel />
        <ProductBox class="mt-10"/>
        <LazyCarouselTrend title="Çok Satan Ürünler" class="bg-gray-100"/>
        <LazyCarouselTrend title="Avantajlı Ürünler" class="bg-gray-100"/>
        <TrendFooter />
    </div>
</template>