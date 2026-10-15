<script setup>
import { ref,onMounted, onBeforeUnmount } from 'vue'
import { categories } from '../data/categories.js'

defineProps(['selectedCategory'])
const emit = defineEmits(['change-category'])

//取得分類列的HTML元素
const categoryContainer = ref(null)

const canScrollLeft = ref(false)
const canScrollRight = ref(false)

//向左捲動
function scrollLeft(){
    categoryContainer.value.scrollBy({
        left:-300,
        behavior:'smooth',
    })
}

//向右捲動
function scrollRight(){
    categoryContainer.value.scrollBy({
        left:300,
        behavior:'smooth',
    })
}

function checkScroll(){
    const el =categoryContainer.value

    if(!el) return
    canScrollLeft.value = el.scrollLeft > 0
    canScrollRight.value = el.scrollLeft + el.clientWidth < el.scrollWidth - 1
}

onMounted(() => {
    checkScroll()
    window.addEventListener('resize', checkScroll)
})

onBeforeUnmount(() =>{
    window.removeEventListener('resize', checkScroll)
})
</script>

<template>
    <div class="bg-white border-b">

        <div class="max-w-7xl mx-auto px-4 flex items-center gap-3">
            <!-- 向左按鈕 -->
            <button
                @click="scrollLeft"
                :disabled="!canScrollLeft"
                class="shrink-0 text-gray-500 hover:text-blue-600 disabled:opacity-30 disabled:cursor-not-allowed"
                aria-label="向左捲動分類"
            >
                &#10094;
            </button>
            <!-- 分類項 -->
            <div 
                ref="categoryContainer"
                @scroll="checkScroll"
                class="flex items-center gap-8 h-12 overflow-x-auto whitespace-nowrap flex-1 hide-scrollbar"
            >
                <button 
                    v-for="category in categories"
                    :key="category"
                    @click="emit('change-category',category)"
                    class="whitespace-nowrap transition shrink-0"
                    :class="
                        selectedCategory === category
                        ? 'text-blue-600 font-bold'
                        : 'text-gray-700 hover:text-blue-600'
                    "
                >
                    {{ category }}
                </button>
            </div>
            <!-- 向右按鈕 -->
            <button
                @click="scrollRight"
                :disabled="!canScrollRight"
                class="shrink-0 text-gray-500 hover:text-blue-600 disabled:opacity-30 disabled:cursor-not-allowed"
                aria-label="向右捲動分類"
            >
                &#10095;
            </button>
        
        </div>
    </div>
</template>

<style>
.hide-scrollbar{
    scrollbar-width: none;
    -ms-overflow-style: none;
}
.hide-scrollbar::-webkit-scrollbar {
    display: none;
}
</style>
