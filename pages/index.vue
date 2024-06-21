<script setup>
</script>
<template>
    <div style="font-family: 'Poppins', sans-serif;">
        <Navbar />
        <LazyOwlCarousel />
        <LazyCarouselTrend class="bg-[#fffaf6]" title="Popüler Ürünler"/>
        <ProductBox2 />
        <LazyCarouselTrend class="bg-[url('https://cdn.dsmcdn.com/mobile/background/flashsales_widgetbacground_android.png')] bg-cover " title="Flaş Ürünler" tcolor="text-white"/>
        <ProductBox />
    </div>
</template>