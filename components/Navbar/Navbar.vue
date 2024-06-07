<script setup lang="ts">
import { Search } from 'lucide-vue-next';
import { Input } from "@/components/ui/input";

</script>
<template>
    <div class="navbar-container w-3/5 pt-1 ml-[20%]">
        <div>
           <ul class="flex float-end text-[11px] text-stone-400 cursor-pointer">
            <li>İndirim Kuponlarım</li>
            <li class="ml-5">Trendyol'da Satış Yap</li>
            <li class="ml-5">Hakkımızda</li>
            <li class="ml-5">Yardım & Destek</li>
           </ul> 
        </div>
        <div class="flex mt-6 items-center">
            <div class="w-1/5">
                <img src="https://cdn.dsmcdn.com/web/logo/ty-web.svg" alt="Trendyol Logo" width="150px" height="150px"/>
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
                    <Icon name="la:user" class="size-5 mr-1" />
                    <span>Hesabım</span>
                </div>
                <div class="m-2 cursor-pointer transition hover:text-cyan-600"> 
                    <Icon name="la:heart" class="size-5 mr-1" />
                    <span>Favorilerim</span>
                </div>
                <div class="m-2 cursor-pointer transition hover:text-cyan-600">
                    <Icon name="ph:basket-light" class="size-5 mr-1" />
                    <span>Sepetim</span>
                </div>
            </div>
        </div>
        <div>

        </div>
    </div>
</template>