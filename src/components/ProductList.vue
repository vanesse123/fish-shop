<script setup>
import { computed} from 'vue'
import { products } from '../data/products.js'
import ProductCard from './ProductCard.vue'

const props =defineProps(['selectedCategory'])

const filteredProducts = computed(() => {
    if(props.selectedCategory === '全部商品'){
        return products
    }

    return products.filter((product) => {
        return product.category === props.selectedCategory
    })
})

</script>

<template>
    <section class="max-w-7xl mx-auto px-4 py-8">

        <h2 class="text-2xl font-bold mb-6">
            商品推薦
        </h2>

        <!-- 商品列表 -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
            <ProductCard 
                v-for="product in filteredProducts"
                :key="product.id"
                :product="product"
            />
        </div>

        <!-- 沒有符合的商品 -->
        <p 
            v-if="filteredProducts.length === 0"
            class="text-center text-gray-500 py-10"
        >
            這個分類目前沒有商品
        </p>

    </section>
</template>
