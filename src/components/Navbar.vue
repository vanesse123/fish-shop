<script setup>
import { ref } from 'vue'

const searchKeyword = ref('')

const emit = defineEmits(['search'])

const hotKeywords = [
    '滑鼠',
    '滑鼠墊',
    '鍵盤',
    '音響',
    '行動電源',
    '手機殼',
]

function searchByKeyword(keyword) {
    searchKeyword.value = keyword
    emit('search',searchKeyword.value)
}

function clearSearch() {
    searchKeyword.value = ''
    emit('search','')
}
</script>

<template>
    <!-- 第一層 -->
    <div class="bg-blue-800 text-white">
        <div class="max-w-7xl mx-auto flex justify-between items-center px-4 py-2">
            <!-- 左邊 -->
            <div class="flex items-center">
                <a href="#" class="px-3 hover:text-gray-300">
                    賣家中心
                </a>
                <a href="#" class="px-3 hover:text-gray-300">
                    買家中心
                </a>
                <div class="px-3 border-1 border-white">
                    追蹤我們
                </div>
            </div>
            <!-- 右邊 -->
            <div class="flex itens-center">
                <a href class="px-3 hover:text-gray-300">
                    通知總覽
                </a>
                <a href class="px-3 hover:text-gray-300">
                    幫助中心
                </a>
                <a href class="px-3 hover:text-gray-300">
                    繁體中文
                </a>
                <a href class="px-3 hover:text-gray-300">
                    註冊
                </a>
                <a href class="px-3 border-l border-white hover:text-gray-300">
                    登入
                </a>
            </div>
        </div>
    </div>
    <!-- 第二層 -->
    <div class="bg-blue-700 text-white">
        <div class="max-w-7xl mx-auto px-4 py-4">
            <!-- Logo + 搜尋框 + 購物車 -->
            <div class="flex items-center gap-6">
                <!-- Logo -->
                <div class="shrink-0">
                    <a href="#" class="text-2xl font-bold">
                        🐟 魚皮購物
                    </a>
                </div>

                <!-- 搜尋 -->
                <div class="flex-1">
                    <form 
                        @submit.prevent="emit('search',searchKeyword)"
                        class="flex bg-white rounded-sm overflow-hidden"
                    >

                        <input
                            v-model="searchKeyword"
                            type="text"
                            placeholder="搜尋商品"
                            class="flex-1 px-4 pt-2 text-gray-700 outline-none"
                        />

                        <button
                            v-if="searchKeyword"
                            type="button"
                            @click="clearSearch"
                            class="px-3 text-gray-500 hover:text-gray-800"
                        >
                           ✖
                        </button>

                        <button
                            type="submit"
                            class="bg-blue-500 px-6 hover:bg-blue-600"
                        >
                            搜尋
                        </button>

                    </form>

                    <!-- 熱門搜尋 -->
                    <div class="flex gap-4 mt-2 text-sm">
                        <button
                            v-for="keyword in hotKeywords"
                            :key="keyword"
                            type="button"
                            @click="searchByKeyword(keyword)"
                            class="hover:text-gray-300"
                        >
                            {{ keyword }}
                        </button>
                    </div>

                </div>

                <!-- 購物車 -->
                <div class="shrink-0">
                    <button class="text-2xl hover:text-gray-300">
                    🛒
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<style>

</style>