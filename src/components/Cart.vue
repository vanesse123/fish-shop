<script setup>
import { computed } from 'vue'

const props = defineProps(['cart'])
const emit = defineEmits([
    'back',
    'update-quantity',
    'remove-item'
    ])

const totalPrice = computed(() => {
    return props.cart.reduce((total,item) => {
        return total + item.product.price * item.quantity
    }, 0)
})
</script>

<template>
    <section class="max-w-3xl mx-auto px-4 pt-8">
        <button
            @click="emit('back')"
            class="mb-6 text-blue-600 hover:text-blue-800"
        >
            ← 返回商品列表
        </button>
        <h1 class="text-3xl font-bold text-gray-800 mb-6">
            我的購物車
        </h1>

        <div class="bg-white rounded-xl shadow p-6">

            <p v-if="cart.length === 0" class ="text-gray-500">
                購物車目前沒有商品
            </p>

            <div v-else>
                <p class="text-gray-600 mb-6">
                    購物車目前有 {{ cart.length }} 種商品
                </p>

                <div
                    v-for="item in cart"
                    :key="item.product.id"
                    class="flex flex-col sm:flex-row gap-6 py-6 border-b"
                >
                    <!-- 商品圖片 -->
                    <img
                        :src="item.product.image"
                        :alt="item.product.name"
                        class="w-32 h-32 object-contain rounded-lg shrink-0"
                    >

                    <!-- 商品資訊 -->
                    <div class="flex-1 min-w-0 flex flex-col md:flex-row md:items-center justify-between gap-4">
                        <!-- 商品名稱價格 -->
                        <div>
                            <h2 class="text-xl font-semibold text-gray-800">
                                {{ item.product.name }}
                            </h2>

                            <p class="mt-2 text-red-500 font-bold">
                                NT$ {{ item.product.price.toLocaleString('en-US') }}
                            </p>

                            <p class="mt-3 font-semibold text-gray-800">
                                小計:NT$ {{ (item.product.price * item.quantity).toLocaleString('en-US') }}
                            </p>
                        </div>

                        <div class="flex flex-wrap items-center gap-4">
                            <!-- 商品數量控制 -->
                            <div class="flex items-center gap-3">
                                <!-- 減少數量 -->
                                <button
                                    @click="emit('update-quantity',item.product.id,-1)"
                                    :disabled="item.quantity <= 1"
                                    class="w-9 h-9 border rounded hover:bg-gray-100 transition disabled:opacity-40 disabled:cursor-not-allowed"
                                >
                                    -
                                </button>

                                <span class="w-8 text-center">
                                    {{ item.quantity }}
                                </span>

                                <!-- 增加數量 -->
                                <button
                                    @click="emit('update-quantity',item.product.id,1)"
                                    class="w-9 h-9 border rounded hover:bg-gray-100 transition"
                                >
                                    +
                                </button>
                            </div>

                            <button 
                                @click="emit('remove-item', item.product.id)"
                                class="border rounded-md px-3 py-2 text-red-500 hover:text-red-700 hover:bg-red-50 transition"
                            >
                                刪除商品
                            </button>
                        </div>
                    </div>
                </div>

                <!-- 購物車總金額 -->
                <div class="flex flex-col sm:flex-row sm:justify-between sm:items-center gap-3 mt-8 pt-6 border-t">

                    <h2 class="text-xl font-bold text-gray-800">
                        商品總金額
                    </h2>

                    <span class="text-2xl font-bold text-red-500">
                        NT$ {{ totalPrice.toLocaleString('en-US') }}
                    </span>
                </div>
            </div>

        </div>

    </section>
</template>