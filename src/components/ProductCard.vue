<script setup>
    defineProps(['product'])

    const emit = defineEmits(['select-product'])
</script>

<template>
    <div
        @click="emit('select-product',product)"
        class="bg-white rounded-lg overflow-hidden shadow hover:shadow-lg transition cursor-pointer"
    >
        <!-- 商品圖片 -->
        <img
            :src="product.image"
            :alt="product.name"
            class="w-full h-48 object-cover"
        >

        <!-- 商品資訊 -->
        <div class="p-4">

            <h3 class="text-lg font-medium truncate">
                {{ product.name }}
            </h3>

            <div class="mt-3">
                
                <span class="text-2xl font-bold text-red-500">
                    ${{ product.price }}
                </span>

                <span class="ml-2 text-sm text-gray-400 line-through">
                    ${{ product.originalPrice }}
                </span>

            </div>

            <div class="mt-2">
                <span class="text-sm text-red-500">
                    {{ product.discount }}% OFF
                </span>
            </div>

            <slot />
            
        </div>
    </div>
</template>