<script setup>
import { ref,onBeforeUnmount} from 'vue'
import { products } from '../data/products.js'
import ProductCard from './ProductCard.vue'

const hours =ref(0)
const minutes = ref(0)
const seconds = ref(5)

const timer = setInterval(()=>{
    if(
        hours.value === 0 &&
        minutes.value === 0 &&
        seconds.value === 0  
    ){
        clearInterval(timer)
        return
    }



    if(seconds.value > 0){
        seconds.value--
    } else {
        seconds.value = 59

        if(minutes.value > 0){
            minutes.value--
        } else {
            minutes.value = 59

            if(hours.value > 0){
                hours.value--
            }
        }
    }
},1000)

onBeforeUnmount(()=>{
    clearInterval(timer)
})
</script>

<template>
  <section class="max-w-7xl mx-auto px-4 py-8">
    <div class="flex items-center justify-between mb-6">
        <!-- 標題 -->
        <div class="flex items-center mb-6">
            <h2 class="text-2xl font-bold">
                限時特賣
            </h2>

            <div 
                v-if="hours > 0 || minutes > 0 || seconds > 0"
                class="flex items-center gap-1 font-mono"
            >
                <span class="text-red-500 font-medium">
                    剩餘
                </span>

                <span class="bg-black text-white px-2 py-1 rounded">
                    {{ String(hours).padStart(2,'0') }}
                </span>

                <span>:</span>

                <span class="bg-black text-white px-2 py-1 rounded">
                    {{ String(minutes).padStart(2,'0') }}
                </span>

                <span>:</span>

                <span class="bg-black text-white px-2 py-1 rounded">
                    {{ String(seconds).padStart(2,'0') }}
                </span>
            </div>

            <span
                v-else
                class="text-gray-500 font-medium"
            >
                活動已結束
            </span>

        </div>

        <span class="text-red-500 font-medium">
                限時優惠
        </span>
    </div>

    <!-- 商品列表 -->
    <div class="grid grid-cols-2 md:grid-cols-4 gap-6">

        <ProductCard
            v-for="product in products"
            :key="product.id"
            :product="product"
        >

            <!-- 熱銷進度 -->
            <div class="mt-4">

                <div class="flex justify-between text-sm mb-1">
                    <span class="text-gray-500">
                        熱銷中
                    </span>

                    <span class="text-gray-400">
                        {{ product.soldPercent }}%
                    </span>
                </div>

                <div class="w-full bg-gray-200 rounded-full h-2">
                    <div
                        class="bg-red-500 h-2 rounded-full"
                        :style="{ width:product.soldPercent + '%' }"
                    ></div>
                </div>

            </div>

        </ProductCard>

      </div>

  </section>
</template>