<script setup lang="ts">
import { Search } from 'lucide-vue-next';
import { Input } from "@/components/ui/input";
import Navigation from '../Menu-Navigation/Navigation.vue';
import ToggleMenu from '../Toggle-Menu/ToggleMenu.vue';


onMounted(() => {
    window.addEventListener("scroll",function () {
        let header = document.getElementById('stickyHeader');
        header?.classList.toggle("stickyHeader",window.scrollY > 0);
        header?.classList.toggle("lg:w-[98%]",window.scrollY > 0);
        header?.classList.toggle("2xl:w-3/5",window.scrollY > 0);
        header?.classList.toggle("lg:ml-[1%]",window.scrollY > 0);
        header?.classList.toggle("2xl:ml-[20%]",window.scrollY > 0);
    })
})

</script>
<template>
    <div class="navbar-container lg:w-[98%] 2xl:w-3/5 pt-1 lg:ml-[1%] 2xl:ml-[20%]">
        <div>
           <ul class="flex float-end text-[11px] text-stone-400 cursor-pointer">
            <li>İndirim Kuponlarım</li>
            <li class="ml-5">Trendyol'da Satış Yap</li>
            <li class="ml-5">Hakkımızda</li>
            <li class="ml-5">Yardım & Destek</li>
           </ul> 
        </div>
        <div id="stickyHeader" class="flex mt-6 items-center max-lg:hidden transition-all">
            <div class="w-1/5">
                <a href="/"><img src="https://cdn.dsmcdn.com/web/logo/ty-web.svg" alt="Trendyol Logo" width="150px" height="150px"/></a>
            </div>
            <div class="w-3/6">
                <div class="relative w-100 items-center">
                    <Input id="search" type="text" placeholder="Aradığınız ürün, kategori veya markayı yazınız" class="pl-4 text-xs bg-gray-100" />
                    <span class="absolute inset-y-0 flex items-center justify-center px-2" style="inset-inline-end: 0 !important;">
                    <Search class="size-5 text-muted-foreground float-right text-cyan-600" />
                    </span>
                </div>
            </div>
            <div class="flex justify-end text-[13px] text-right w-[30%]">
                <div class="m-2 cursor-pointer transition hover:text-cyan-600">
                    <Icon name="la:user" class="size-5 mr-1 mb-1" />
                    <span>Hesabım</span>
                </div>
                <div class="m-2 cursor-pointer transition hover:text-cyan-600"> 
                    <Icon name="la:heart" class="size-5 mr-1 mb-1" />
                    <span>Favorilerim</span>
                </div>
                <div class="m-2 cursor-pointer transition hover:text-cyan-600">
                    <Icon name="ph:basket-light" class="size-5 mr-1 mb-1" />
                    <span>Sepetim</span>
                </div>
            </div>
        </div>
        <div class="mt-6 lg:hidden max-lg:flex justify-between">
            <div class="ml-2">
                <ToggleMenu />
            </div>
            <div class="flex mt-2">
                <a href="#"><Icon name="la:user" class="size-8 mr-3 cursor-pointer hover:text-cyan-600" /></a>
                <a href="#"><Icon name="la:heart" class="size-8 mr-3 cursor-pointer hover:text-cyan-600" /></a>
                <a href="#"><Icon name="ph:basket-light" class="size-8 mr-3 cursor-pointer hover:text-cyan-600" /></a>
            </div>
        </div>
        <div>
            <Navigation />
        </div>
    </div>
</template>