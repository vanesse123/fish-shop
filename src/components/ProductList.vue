<script setup>
import { products } from '../data/products.js'
import ProductCard from './ProductCard.vue'
</script>

<template>
    <section class="max-w-7xl mx-auto px-4 py-8">

        <h2 class="text-2xl font-bold mb-6">
            商品推薦
        </h2>

        <div class="grid grid-cols-2 md:grid-cols-4 gap-6">

            <ProductCard 
                v-for="product in products"
                :key="product.id"
                :product="product"
            />
        
        </div>
    </section>
</template>
