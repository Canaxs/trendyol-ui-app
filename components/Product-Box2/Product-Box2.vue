<script setup lang="ts">
import ImageBox from '~/data/ImageBox';
import { reactive , ref , watch } from "vue";


const images = ref(ImageBox);

function getImage(value: number) {
    return images.value[value];
}

</script>
<template>
    <div class="lg:w-[98%] 2xl:w-[65%] lg:ml-[1%] 2xl:ml-[17%]">
        <div class="flex flex-wrap max-md:justify-center">
            <div v-for="(_, index) in 3" class="md:w-[48%] lg:w-[31%] m-[1%]">
                <a :href="getImage(index).href"><img :src="getImage(index).image" style="border-radius: 6px 6px 0 0;"/></a>
            </div>
        </div>
    </div>
</template>