<script setup>

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
                    <div class="flex bg-white rounded-sm overflow-hidden">

                        <input
                            type="text"
                            placeholder="搜尋商品"
                            class="flex-1 px-4 pt-2 text-gray-700 outline-none"
                        />

                        <button
                            class="bg-blue-500 px-6 hover:bg-blue-600"
                        >
                            搜尋
                        </button>

                    </div>

                    <!-- 熱門搜尋 -->
                    <div class="flex gap-4 mt-2 text-sm">
                        <a href="#" class="hover:text-gray-300">滑鼠</a>
                        <a href="#" class="hover:text-gray-300">滑鼠墊</a>
                        <a href="#" class="hover:text-gray-300">鍵盤</a>
                        <a href="#" class="hover:text-gray-300">音響</a>
                        <a href="#" class="hover:text-gray-300">行動電源</a>
                        <a href="#" class="hover:text-gray-300">手機殼</a>
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