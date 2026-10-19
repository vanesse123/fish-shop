<script setup>
import { ref } from 'vue'
import Navbar from './components/Navbar.vue'
import CategoryNav from './components/CategoryNav.vue'
import Banner from './components/Banner.vue'
import ProductList from './components/ProductList.vue'
import SaleSection from './components/SaleSection.vue'

const selectedCategory = ref('全部商品')

const searchKeyword = ref('')

function searchProducts(keyword){
  searchKeyword.value = keyword.trim()
}

</script>

<template>
  <Navbar @search="searchProducts" />

  <Banner />

  <CategoryNav 
    :selected-category="selectedCategory"
    @change-category="selectedCategory = $event"
  />

  <ProductList 
    :selected-category="selectedCategory"
    :search-keyword="searchKeyword"
  />

  <SaleSection />
</template>
