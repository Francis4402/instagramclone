<script setup>
import { onMounted, ref, toRef } from 'vue';
import { Head, Link } from '@inertiajs/vue3';
import MainLayout from '@/Layouts/MainLayout.vue';

import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Navigation } from 'vue3-carousel';
import DotsHorizontal from 'vue-material-design-icons/DotsHorizontal.vue';


let wWidth = ref(window.innerWidth)
let currentSlide = ref(0)
let currentPost = ref(null)
let openOverlay = ref(false)

const props = defineProps({ posts: Object, allUsers: Object })
const { posts, allUsers } = toRef(props)

onMounted(() => {
    window.addEventListener('resize', () => {
        wWidth.value = window.innerWidth
    })
})

</script>

<template>
    <Head title="Home" />

    <MainLayout>
        <div class="mx-auto lg:pl-0 md:pl-[80px] pl-0">
            <Carousel v-model="currentSlide" class="max-w-[700px] mx-auto" :items-to-show="wWidth >= 768 ? 8 : 6" :items-to-scroll="4" :wrap-around="true" :transition="500" snapAlign="start">
                <Slide v-for="slide in 10" :key="slide" class="h-60">
                    <Link href="/" class="relative mx-auto text-center mt-4 px-2 cursor-pointer">
                        <div class="absolute z-[-1] -top-[5px] left-[4px] rounded-full rotate-45 w-[64px] h-[64px] contrast-[1.3] bg-gradient-to-t from-yellow-300 to-purple-500 via-red-500">
                            <div class="rounded-full ml-[3px] mt-[3px] w-[58px] h-[58px] bg-white" />
                        </div>
                        <img src="https://picsum.photos/id/50/300/320" class="rounded-full w-[56px] h-[56px] -mt-[1px]" alt="i">
                        <div class="text-xs mt-2 w-[60px] truncate text-ellipsis overflow-hidden">Name Here</div>
                    </Link>
                </Slide>

                <template #addons>
                    <Navigation />
                </template>
            </Carousel>

            <div id="Posts" class="px-4 max-w-[600px] mx-auto mt-10">
                <div class="flex items-center justify-between py-2">
                    <div class="flex items-center">
                        <Link href="/" class="flex items-center">
                            <img src="https://picsum.photos/id/50/300/320" class="rounded-full w-[38px] h-[38px]" alt="i">
                            <div class="ml-4 font-extrabold text-[15px]">Name Here</div>
                        </Link>
                    </div>
                </div>
            </div>
        </div>
    </MainLayout>
</template>

<style>
    .carousel__prev,
    .carousel__next,
    .carousel__prev:hover,
    .carousel__next:hover {
        color: rgb(49, 49, 49);
        background-color: rgb(255, 255, 255);
        border-radius: 100%;
        margin: 0 20px;
    }
</style>
