<script setup>
import { categories } from '../data/categories.js'
</script>

<template>
    <div class="bg-white border-b">

        <div class="max-w-7xl mx-auto px-4">

            <div class="flex items-center gap-8 h-12">
                <a  
                    v-for="category in categories"
                    :key="category"
                    href="#"
                    class="hover:text-blue-600"
                >
                    {{ category}}
                </a>
            </div>
        
        </div>
    </div>
</template>
