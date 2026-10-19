<script setup>
import { computed,ref } from 'vue'
import { products } from '../data/products.js'
import ProductCard from './ProductCard.vue'

const props = defineProps([
    'selectedCategory',
    'searchKeyword'
])

//default,price-asc,price-desc
const sortOrder = ref('default')

const filteredProducts = computed(() => {
    let result
    
    //分類
    if(props.selectedCategory === '全部商品'){
        result =  [...products]
    } else {
        result = products.filter((product) => {
            return product.category === props.selectedCategory
        })
    }

    //搜尋關鍵字
    if(props.searchKeyword) {
        result = result.filter((product) => {
            return product.name
                .toLowerCase()
                .includes(props.searchKeyword.toLowerCase())
        })
    }

    //價格排序
    if (sortOrder.value === 'price-asc') {
        result.sort((a,b) => a.price - b.price)
    } else if (sortOrder.value === 'price-desc') {
        result.sort((a,b) => b.price - a.price)
    }

    return result
})

</script>

<template>
    <section class="max-w-7xl mx-auto px-4 py-8">
        <div class="flex items-center justify-between mb-6">
            <h2 class="text-2xl font-bold">
                商品推薦
            </h2>

            <select
                v-model="sortOrder"
                class="border rounded-md px-3 py-2 text-sm"
            >
                <option value="default">預設排序</option>
                <option value="price-asc">價格由低到高</option>
                <option value="price-desc">價格由高到低</option>
            </select>
        </div>

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
