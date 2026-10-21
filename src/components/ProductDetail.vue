<script setup>
defineProps(['product'])

const emit = defineEmits(['back'])
</script>

<template>
    <section class="max-w-7xl mx-auto px-4 py-8">
        <!-- 返回按鈕 -->
        <button
            @click="emit('back')"
            class="mb-6 text-blue-600 hover:text-blue-800"
        >
            ← 返回商品列表
        </button>

        <!--  商品詳情 -->
        <div class="bg-white rounded-xl shadow p-6 grid grid-cols-1 md:grid-cols-2 gap-8">
            <!-- 商品圖片 -->
            <div>
                <img
                    :src="product.image"
                    :alt="product.name"
                    class="w-full h-80 object-contain rounded-lg"
                >
            </div>

            <!-- 商品資訊 -->
            <div class="flex flex-col">
                <h1 class="text-3xl font-bold text-gray-800">
                    {{ product.name }}
                </h1>

                <div class="mt-6">
                    <span class="text-3xl font-bold text-red-500">
                        ${{ product.price }}
                    </span>

                    <span class="ml-3 text-lg text-gray-400 line-through">
                        ${{ product.originalPrice }}
                    </span>
                </div>
            </div>

            <div class="mt-3">
                <span class="bg-red-100 text-red-600 px-3 py-1 rounded">
                    {{ product.discount }}% OFF
                </span>
            </div>

            <div class="mt-6 text-gray-600">
                <p>商品分類：{{ product.category }}</p>
            </div>

            <div class="mt-8">
                <button
                    class="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition"
                >
                    加入購物車
                </button>
            </div>

        </div>
    
    </section>

</template>