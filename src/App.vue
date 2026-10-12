<script setup>
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import CategoryNav from './components/CategoryNav.vue'
import Banner from './components/Banner.vue'
import ProductList from './components/ProductList.vue'
import SaleSection from './components/SaleSection.vue'

const selectedCategory = ref('全部商品')
</script>

<template>
  <Navbar />

  <CategoryNav 
    :selected-category="selectedCategory"
    @change-category="selectedCategory = $event"
  />

  <Banner />

  <ProductList 
    :selected-category="selectedCategory"
  />

  <SaleSection />
</template>
