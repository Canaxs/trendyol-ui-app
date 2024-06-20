<script setup lang="ts">
import Menu from '~/data/Menu';
import ChildMenu from '~/data/ChildMenu';

import { reactive , ref , watch } from "vue";

let current = ref(true);
const menuItems = ref(Menu);
const subItems = ref(ChildMenu);

let onClickLi = (value,item) => {
    current.value = value;
    subItems.value = subItems.value.filter(subItem => subItem.menuId === item.menuId);
}
let onClickBack = (value) => {
    current.value = value;
    subItems.value = ChildMenu;
}

</script>
<template>
    <div>
        <div class="absolute left-3 top-3 cursor-pointer" @click="onClickBack(true)" v-if="!current"><Icon name="material-symbols:arrow-back-rounded" class="size-5 text-gray-400" /></div>
        <div class="mt-8" id="sideToggle">
            <ul v-for="item of menuItems" v-if="current">
                <li @click='onClickLi(false,item)' class="p-5 mt-3 border border-gray-300 rounded shadow hover:bg-gray-100 transition-all cursor-pointer">
                    <Icon :name="item.icon" class="size-4 text-gray-400 float-start mt-1 mr-2" />
                    {{ item.title }}
                    <Icon name="material-symbols-light:arrow-forward-ios" class="size-4 text-gray-400 float-end mt-1"/>
                </li>
            </ul>
            <ul v-if="!current" v-for="item of subItems">
                <a :href="item.href"><li class="p-5 mt-3 border border-gray-300 rounded shadow hover:bg-gray-100 transition-all">
                    {{item.title }}
                </li>
                </a>
            </ul>
                
        </div>
    </div>
</template>