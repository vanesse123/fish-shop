<script setup>
import { ref } from 'vue'

const banners = [
  '/images/banner/test_banner.jpg',
  '/images/banner/test_banner2.jpg',
  '/images/banner/test_banner3.png',
]

const currentIndex = ref(0)

function nextBanner() {
  currentIndex.value =
    (currentIndex.value + 1) % banners.length
}

function prevBanner() {
  currentIndex.value =
    (currentIndex.value - 1 + banners.length) % banners.length
}

</script>

<template>
    <section class="max-w-7xl mx-auto px-4 py-4">

        <img
        :src="banners[currentIndex]"
        alt="商品活動 Banner"
        class="w-full h-80 object-cover rounded-lg"
        >

        <!-- 上一張 -->
        <button
            @click="prevBanner"
            class="absolute left-3 top-1/2 -translate-y-1/2 bg-black/40 text-white w-10 h-10 rounded-full"
        >
            ‹
        </button>

        <!-- 下一張 -->
        <button
            @click="nextBanner"
            class="absolute right-3 top-1/2 -translate-y-1/2 bg-black/40 text-white w-10 h-10 rounded-full"
        >
            ›
        </button>

    </section>
</template>