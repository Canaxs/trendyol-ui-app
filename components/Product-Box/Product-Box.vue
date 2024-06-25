<script setup>
import ImageBox from '~/data/ImageBox';
import { reactive , ref , watch } from "vue";


const images = ref(ImageBox);

</script>
<template>
    <div class="lg:w-[98%] 2xl:w-[65%] lg:ml-[1%] 2xl:ml-[17%]">
        <div class="flex flex-wrap max-md:justify-center">
            <div v-for="image of images" class="md:w-[48%] lg:w-[31%] m-[1%]">
                <a :href="image.href"><img :src="image.image" style="border-radius: 6px 6px 0 0;"/></a>
            </div>
        </div>
    </div>
</template>