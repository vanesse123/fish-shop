<script setup>
import { categories } from '../data/categories.js'

defineProps(['selectedCategory'])
const emit = defineEmits(['change-category'])
</script>

<template>
    <div class="bg-white border-b">

        <div class="max-w-7xl mx-auto px-4">

            <div class="flex items-center gap-8 h-12">
                <button 
                    v-for="category in categories"
                    :key="category"
                    @click="emit('change-category',category)"
                    class="whitespace-nowrap transition"
                    :class="
                        selectedCategory === category
                        ? 'text-blue-600 font-bold'
                        : 'text-gray-700 hover:text-blue-600'
                    "
                >
                    {{ category }}
                </button>
            </div>
        
        </div>
    </div>
</template>
