<script setup>
    import { products } from '../data/products.js'
</script>

<template>
  <section class="max-w-7xl mx-auto px-4 py-8">

    <!-- 標題 -->
    <div class="flex items-center justify-between mb-6">
        <h2 class="text-2xl font-bold">
            限時特賣
        </h2>

        <span class="text-red-500 font-medium">
            限時優惠
        </span>
    </div>

    <!-- 商品 -->
    <div class="grid grid-cols-2 md:grid-cols-4 gap-6">

        <div
            v-for="product in products"
            :key="product.id"
            class="bg-white rounded-lg overflow-hidden shadow hover:shadow-lg transition"
        >
            <!-- 商品圖片 -->
            <div class="relative">
                <img
                    :src="product.image"
                    :alt="product.name"
                    class="w-full h-48 object-cover"
                >

                <!-- 折扣 -->
                <span
                    class="absolute top-2 left-2 bg-red-500 text-white text-sm px-2 py-1 rounded"
                >
                    -{{ product.discount }}%
                </span>
            </div>

            <!-- 商品資訊 -->
            <div class="p-4">

            <h3 class="font-medium truncate">
                {{ product.name }}
            </h3>

            <div class="mt-3">
                <span class="text-2xl font-bold text-red-500">
                ${{ product.price }}
                </span>
            </div>

            <!-- 熱銷進度 -->
            <div class="mt-4">

                <div class="flex justify-between text-sm mb-1">
                <span class="text-gray-500">
                    熱銷中
                </span>

                <span class="text-gray-400">
                    75%
                </span>
                </div>

                <div class="w-full bg-gray-200 rounded-full h-2">
                <div
                    class="bg-red-500 h-2 rounded-full w-3/4"
                ></div>
                </div>

            </div>

        </div>

      </div>

    </div>

  </section>
</template>